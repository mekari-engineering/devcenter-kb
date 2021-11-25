---
layout: page
title: HMAC Authentication in Ruby
permalink: /examples/hmac-authentication-in-ruby
nav_order: 0
parent: Guides
---

# HMAC Authentication in Ruby

We will be using [Ruby](https://www.ruby-lang.org) version 2.7 (v2.7.4) and [Bundler](https://bundler.io) version 2.1.4. We assume you are already familiar with Ruby and have Bundler installed on your system. Let's get started.

## Install Dependencies
{: .fw-300 }

Because we'll be using Bundle, make sure you have the `Gemfile` file in your working directory.
If you don't have the file, make one with the following content: 

```
source "https://rubygems.org"

git_source(:github) { |repo_name| "https://github.com/#{repo_name}" }
```

We will need to add faraday to Gemfile [Faraday](https://lostisland.github.io/faraday) for  HTTP requests to the Mekari API.
```
# Gemfile
gem 'faraday'
```

And we will put all credentials on .env since  we don't want to Mekari API client ID and client secret exposed directly on the code. To load the .env, we will need [Doetenv](https://github.com/bkeepers/dotenv) .

```
# Gemfile
gem 'dotenv'
```

## Making API Request
{: .fw-300 }

Using Faraday and Dotenv that we have installed earlier, we are going to setup Ruby script that will perform API request to one of Klikpajak API endpoint which is [create sales invoice](https://documenter.getpostman.com/view/17365057/U16hrR5d#63ba32aa-0f91-44a5-ab40-a0da6a8bf608) (`https://api.mekari.com/v2/klikpajak/v1/efaktur/out`). 

We create the script called `main.rb` then use Faraday to perform the HTTP POST request. This is how the script will looks like:

```
path = '/v2/klikpajak/v1/efaktur/out/'
headers = { 'X-Idempotency-Key' => '1234' }
response = Faraday.post("#{ENV['MEKARI_API_BASE_URL']}/#{path}", nil, headers)

puts "Got response with status: #{response.status}, body: #{response.body}"
```

We can run the script on the console by typing `ruby main.rb`. Because we just created a plain HTTP POST request, it will has an error response similar to this: 

```
$ ruby main.rb
Got response with status: 401, body: {"message":"Unauthorized"}
```

## Creating HMAC Signature
{: .fw-300 }

[The signature](/docs/kb/authentication/hmac#generating-signature) is one of the requirements for forming an API request with HMAC Authentication. The signature is an HMAC256 representation of the request line (a combination of the request method, the request path, and `HTTP/1`.1) and the `Date` header in [RFC 7231](https://www.ietf.org/rfc/rfc7231.txt) format. Carbon will be used to generate the date string for us. The signature must then be converted into a Base64 string so that it can be attached to the `Authorization` header.

The code will look like this: 

```
// ... the rest of the code

datetime = Time.now.httpdate
request_line = "POST /v2/klikpajak/v1/efaktur/out HTTP/1.1"
payload = [datetime, request_line].join("\n")
digest = OpenSSL::HMAC.digest(OpenSSL::Digest.new('sha256'), 'YOUR_MEKARI_API_CLIENT_SECRET', payload)
signature = Base64.strict_encode64(digest)

puts "hmac username=\"YOUR_MEKARI_API_CLIENT_ID", algorithm=\"hmac-sha256\", headers=\"date request-line\", signature=\"#{signature}\""
```

If you replace `datetime` with `Wed, 10 Nov 2021 07:24:29 GMT` and run the code, you will get the following result.

```
$ ruby main.rb
hmac username="YOUR_MEKARI_API_CLIENT_ID", algorithm="hmac-sha256", headers="date request-line", signature="RDHVOBEGBcr86Eyv2Dg42PcwDlTDY4QoJOdkd9w5L0M="
```

It is important to note that we should not include any credentials in our codebase. This means that we must save the Mekari API client id and client secret that you obtained from the Mekari Developer dashboard to an environment variable. Modern full-stack frameworks, such as Laravel, usually include an `.env` file to make managing environment variables easier. This is also why Dotenv was installed. We can use this library to move the client id and client secret to the `.env` file. 

```
# .env file
MEKARI_API_CLIENT_ID=YOUR_MEKARI_API_CLIENT_ID
MEKARI_API_CLIENT_SECRET=YOUR_MEKARI_CLIENT_SECRET
```

Then we use `ENV` to replace the credentials in the code.

```
// main.rb

require 'time'
require 'base64'
require 'openssl'
require 'faraday'

// ... the rest of the code

datetime = Time.now.httpdate
request_line = "POST /v2/klikpajak/v1/efaktur/out HTTP/1.1"
payload = [datetime, request_line].join("\n")
digest = OpenSSL::HMAC.digest(OpenSSL::Digest.new('sha256'), ENV['MEKARI_API_CLIENT_SECRET'], payload)
signature = Base64.strict_encode64(digest)

puts "hmac username=\"#{ENV['MEKARI_API_CLIENT_ID']}", algorithm=\"hmac-sha256\", headers=\"date request-line\", signature=\"#{signature}\""
```

## Wrap It Out
{: .fw-300 }

It's now time to combine everything we've learned into a single Ruby script.

```
require 'time'
require 'base64'
require 'openssl'
require 'faraday'
require 'dotenv'

Dotenv.load

# Generate headers to be used on API call.
#
# @return [Hash<String, Object>]
def generate_headers(method, path)
  datetime = Time.now.httpdate
  request_line = "#{method} #{path} HTTP/1.1"
  payload = ["date: #{datetime}", request_line].join("\n")
  digest = OpenSSL::HMAC.digest(OpenSSL::Digest.new('sha256'), ENV['MEKARI_API_CLIENT_SECRET'], payload)

  signature = Base64.strict_encode64(digest)

  {
    'Content-Type' => 'application/json',
    'Date' => datetime,
    'Authorization' => "hmac username=\"#{ENV['MEKARI_API_CLIENT_ID']}\", algorithm=\"hmac-sha256\", headers=\"date request-line\", signature=\"#{signature}\""
  }
end

# Set method and path for the request
method = 'POST'
path = '/v2/klikpajak/v1/efaktur/out'
default_headers = { 'X-Idempotency-Key' => '1234' }
request_headers = default_headers.merge(generate_headers(method, path))

puts "Start request with url: #{ENV['MEKARI_API_BASE_URL']}#{path}, headers: #{request_headers}"

conn = Faraday.new(url: ENV['MEKARI_API_BASE_URL']) do |faraday|
  faraday.response :logger # log requests and responses to $stdout
end

response = conn.post(path, nil, request_headers)

puts "Got response with status: #{response.status}, body: #{response.body}"
```

If you want to integrate this script with your existing code, you may need to modify it. Additionally, each Mekari API has its own requirements regarding request headers, query, or body, and you may need to change the script based on your needs. We hope that this guide makes integrating Mekari API into your code easier for you.

You can also look at the final code on [this repository](https://github.com/mekari-engineering/mekari-api-hmac-example-ruby).








