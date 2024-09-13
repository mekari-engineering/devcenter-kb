---
layout: page
title: PHP
permalink: /hmac-authentication/php
nav_order: 0
parent: HMAC Authentication
---

# Setup HMAC Authentication in PHP

We will be using [PHP](https://www.php.net/manual/en/install.php) version 8 (v8.0.12) and [Composer](https://getcomposer.org/) version 2 (v2.1.11). We assume you are already familiar with PHP and have Composer installed on your system. Let's get started.

## Install Dependencies
{: .fw-300 }

Because we'll be using Composer, make sure you have the `composer.json` file in your working directory.
If you don't have the file, make one with the following content: 

```
{
    "require": {}
}
```

There will be three dependency: [GuzzleHTTP](https://docs.guzzlephp.org/en/stable/index.html) to make HTTP requests to the Mekari API, [Carbon](https://carbon.nesbot.com/) to handle datetime formatting for generating HMAC signatures, and [phpdotenv](https://github.com/vlucas/phpdotenv) for environment variable loader, because we don't want to put the Mekari API client ID and client secret directly on the code. 

```
$ php composer.phar require guzzlehttp/guzzle:^7.0 nesbot/carbon vlucas/phpdotenv
```

Once installed, your `require` attribute on the `composer.json` will look something like this.

```
{
    "require": {
        "guzzlehttp/guzzle": "^7.0",
        "nesbot/carbon": "^2.54",
        "vlucas/phpdotenv": "^5.3"
    }
}
```

## Making API Request
{: .fw-300 }

Using GuzzleHTTP that we have installed earlier, we are going to setup PHP script that will perform API request to one of Klikpajak API endpoint which is [create sales invoice](https://documenter.getpostman.com/view/17365057/U16hrR5d#63ba32aa-0f91-44a5-ab40-a0da6a8bf608) (`https://api.mekari.com/v2/klikpajak/v1/efaktur/out`). 

We create the script called `main.php` then use GuzzleHTTP to perform the HTTP POST request. Since we are using Composer, we need to make sure we put the autoload file on the top of the script. This is how the script will looks like:

```
<?php // main.php

require 'vendor/autoload.php';

$client = new GuzzleHttp\Client([
    'base_uri' => 'https://api.mekari.com/v2/klikpajak/v1'
]);

$response = $client->request('POST', 'efaktur/out?auto_approval=false');
```

We can run the script on the console by typing `php main.php`. Because we just created a plain HTTP POST request, it will throw an error similar to this: 

```
$ php main.php
PHP Fatal error:  Uncaught GuzzleHttp\Exception\ClientException: Client error: `POST https://api.mekari.com/v2/klikpajak/efaktur/out?auto_approval=false` resulted in a `401 Unauthorized` response:
{"message":"Unauthorized"}
 in /working/directory/vendor/guzzlehttp/guzzle/src/Exception/RequestException.php:113
Stack trace: ...
```

Before we add authentication to the request, let's catch the error and display it nicely on the console.

```
<?php // main.php

require 'vendor/autoload.php';

use GuzzleHttp\Psr7;
use GuzzleHttp\Exception\ClientException;

$client = new GuzzleHttp\Client([
    'base_uri' => 'https://api.mekari.com/v2/klikpajak/v1'
]);

try {
    $response = $client->request('POST', 'efaktur/out?auto_approval=false');
} catch (ClientException $e) {
    echo Psr7\Message::toString($e->getRequest());
    echo Psr7\Message::toString($e->getResponse());
    echo PHP_EOL;
}
```

When we run the script again, the error message will be as follows: 

```
$ php main.php
POST /v2/klikpajak/efaktur/out?auto_approval=false HTTP/1.1
User-Agent: GuzzleHttp/7
Host: api.mekari.com

HTTP/1.1 401 Unauthorized
date: Tue, 09 Nov 2021 02:37:41 GMT
content-type: application/json; charset=utf-8
content-length: 26
x-envoy-upstream-service-time: 0
server: Mekari

{"message":"Unauthorized"}
```

## Creating HMAC Signature
{: .fw-300 }

[The signature](/docs/kb/authentication/hmac#generating-signature) is one of the requirements for forming an API request with HMAC Authentication. The signature is an HMAC256 representation of the request line (a combination of the request method, the request path, the query param, and `HTTP/1.1`) and the `Date` header in [RFC 7231](https://www.ietf.org/rfc/rfc7231.txt) format. Carbon will be used to generate the date string for us. The signature must then be converted into a Base64 string so that it can be attached to the `Authorization` header.

The code will look like this: 

```
<?php // main.php

use Carbon\Carbon;

// ... the rest of the code

$datetime       = Carbon::now()->toRfc7231String();
$request_line   = "POST /v2/klikpajak/v1/efaktur/out?auto_approval=false HTTP/1.1";
$payload        = implode("\n", ["date: {$datetime}", $request_line]);
$digest         = hash_hmac('sha256', $payload, 'YOUR_MEKARI_CLIENT_SECRET', true);
$signature      = base64_encode($digest);

echo "hmac username=\"YOUR_MEKARI_API_CLIENT_ID\", algorithm=\"hmac-sha256\", headers=\"date request-line\", signature=\"{$signature}\"";
```

If you replace `$datetime` with `Wed, 10 Nov 2021 07:24:29 GMT` and run the code, you will get the following result.

```
$ php main.php
hmac username="YOUR_MEKARI_API_CLIENT_ID", algorithm="hmac-sha256", headers="date request-line", signature="6+Ah/UTmbqd+DDqlh6zYZ0HuCwVhtElYDOoucRPCaFg="
```

It is important to note that we should not include any credentials in our codebase. This means that we must save the Mekari API client id and client secret that you obtained from the Mekari Developer dashboard to an environment variable. Modern full-stack frameworks, such as Laravel, usually include an `.env` file to make managing environment variables easier. This is also why phpdotenv was installed. We can use this library to move the client id and client secret to the `.env` file. 

```
# .env file
MEKARI_API_CLIENT_ID=YOUR_MEKARI_API_CLIENT_ID
MEKARI_API_CLIENT_SECRET=YOUR_MEKARI_CLIENT_SECRET
MEKARI_API_BASE_URL=https://api.mekari.com/v2/klikpajak/v1
```

Then we use `$_ENV[]` to replace the credentials in the code.

```
<?php // main.php

use Carbon\Carbon;
use Dotenv\Dotenv;

$dotenv = Dotenv::createImmutable(__DIR__);
$dotenv->load();

// ... the rest of the code

$datetime       = Carbon::now()->toRfc7231String();
$request_line   = "POST /v2/klikpajak/v1/efaktur/out?auto_approval=false  HTTP/1.1";
$payload        = implode("\n", ["date: {$datetime}", $request_line]);
$digest         = hash_hmac('sha256', $payload, $_ENV['MEKARI_API_CLIENT_SECRET'], true);
$signature      = base64_encode($digest);

echo "hmac username=\"{$_ENV['MEKARI_API_CLIENT_ID']}\", algorithm=\"hmac-sha256\", headers=\"date request-line\", signature=\"{$signature}\"";
```

## Wrap It Out
{: .fw-300 }

It's now time to combine everything we've learned into a single PHP script.

```
<?php

require 'vendor/autoload.php';

use Carbon\Carbon;
use Dotenv\Dotenv;
use GuzzleHttp\Psr7\Request;
use GuzzleHttp\Psr7;
use GuzzleHttp\Exception\ClientException;

// Load .env file
$dotenv = Dotenv::createImmutable(__DIR__);
$dotenv->load();

/**
 * Generate authentication headers based on method and path
 */
function generate_headers($method, $pathWithQueryParam) {
    $datetime       = Carbon::now()->toRfc7231String();
    $request_line   = "{$method} {$pathWithQueryParam} HTTP/1.1";
    $payload        = implode("\n", ["date: {$datetime}", $request_line]);
    $digest         = hash_hmac('sha256', $payload, $_ENV['MEKARI_API_CLIENT_SECRET'], true);
    $signature      = base64_encode($digest);
    
    return [
        'Accept'        => 'application/json',
        'Content-Type'  => 'application/json',
        'Date'          => $datetime,
        'Authorization' => "hmac username=\"{$_ENV['MEKARI_API_CLIENT_ID']}\", algorithm=\"hmac-sha256\", headers=\"date request-line\", signature=\"{$signature}\""
    ];
}

// Set http client
$client = new GuzzleHttp\Client([
    'base_uri' => $_ENV['MEKARI_API_BASE_URL']
]);

$method     = 'POST';
$path       = '/v2/klikpajak/v1/efaktur/out';
$queryParam = '?auto_approval=false';
$headers    = [
    'X-Idempotency-Key' => '1234'
];
$body       = [/* request body */];

// Initiate request
try {
    $response = $client->request($method, $path . $queryParam, [
        'headers'   => array_merge(generate_headers($method, $path . $queryParam), $headers),
        'body'      => json_encode($body)
    ]);

    echo $response->getBody();
} catch (ClientException $e) {
    echo Psr7\Message::toString($e->getRequest());
    echo Psr7\Message::toString($e->getResponse());
    echo PHP_EOL;
}
```

If you want to integrate this script with your existing code, you may need to modify it. Additionally, each Mekari API has its own requirements regarding request headers, query, or body, and you may need to change the script based on your needs. We hope that this guide makes integrating Mekari API into your code easier for you.

You can also look at the final code on [this repository](https://github.com/mekari-engineering/mekari-api-hmac-example-php).








