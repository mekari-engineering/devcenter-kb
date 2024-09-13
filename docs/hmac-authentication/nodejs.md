---
layout: page
title: Node.js
permalink: /hmac-authentication/node
nav_order: 1
parent: HMAC Authentication
---

# Setup HMAC Authentication in Node.js

We will be using [Node.js](https://nodejs.org/en/download/) version 16 (v16.13.0) and [npm](https://getcomposer.org/) version 8 (v8.1.0). We assume you are already familiar with Node.js and have npm installed on your system. Let's get started.

## Install Dependencies
{: .fw-300 }

Because we'll be using npm, make sure you have the `package.json` file in your working directory.
If you don't have the file, make one by running this command `npm init`. Then you will be asked couple question regarding your npm project and once it done the content of the file will look like this:

```
{
  "name": "your-node-project",
  "version": "0.1.0",
  "description": "Your project description",
  "main": "main.js",
  "author": "Your Name <your-email@example.com>",
  "dependencies": {}
}
```

There will be two dependency: [Axios](https://axios-http.com/) to make HTTP requests to the Mekari API and [dotenv](https://github.com/motdotla/dotenv) for environment variable loader, because we don't want to put the Mekari API client ID and client secret directly on the code. 

```
$ npm add axios dotenv --save
```

Once installed, your `dependencies` attribute on the `package.json` will look something like this.

```
{
  "dependencies": {
    "axios": "^0.24.0",
    "dotenv": "^10.0.0"
  }
}
```

## Making API Request
{: .fw-300 }

Using Axios that we have installed earlier, we are going to setup a script that will perform API request to one of Klikpajak API endpoint which is [create sales invoice](https://documenter.getpostman.com/view/17365057/U16hrR5d#63ba32aa-0f91-44a5-ab40-a0da6a8bf608) (`https://api.mekari.com/v2/klikpajak/v1/efaktur/out`) with query param `?auto_approval=false`. 

We create the script called `main.js` then use Axios to perform the HTTP POST request. This is how the script will looks like:

```
const axios = require('axios');

axios({
  method: 'POST',
  url: 'https://api.mekari.com/v2/klikpajak/v1/efaktur/out?auto_approval=false'
}).then(function (response) {
    console.log(response.data);
  })
  .catch(function (error) {
    console.log(error);
  });
```

We can run the script on the console by typing `node main.js`. Because we just created a plain HTTP POST request, it will throw an error similar to this: 

```
$ node main.js
{
  {
    // ...a lot of data
    data: { message: 'Unauthorized' }
  },
  isAxiosError: true,
  toJSON: [Function: toJSON]
}
```

Before we add authentication to the request, let's catch the error and display it nicely on the console.

```
const axios = require('axios');

axios({
  method: 'POST',
  url: 'https://api.mekari.com/v2/klikpajak/v1/efaktur/out?auto_approval=false'
}).then(function (response) {
    console.log(response.data);
  })
  .catch(function (error) {
    if (error.response) {
      // The request was made and the server responded with a status code
      // that falls out of the range of 2xx
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // The request was made but no response was received
      // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
      // http.ClientRequest in node.js
      console.log(error.request);
    } else {
      // Something happened in setting up the request that triggered an Error
      console.log('Error', error.message);
    }
  });
```

When we run the script again, the error message will be as follows: 

```
$ node main.js
{ message: 'Unauthorized' }
401
{
  date: 'Thu, 25 Nov 2021 02:21:08 GMT',
  'content-type': 'application/json; charset=utf-8',
  'content-length': '26',
  'x-envoy-upstream-service-time': '2',
  server: 'Mekari',
  connection: 'close'
}
```

## Creating HMAC Signature
{: .fw-300 }

[The signature](/docs/kb/authentication/hmac#generating-signature) is one of the requirements for forming an API request with HMAC Authentication. The signature is an HMAC256 representation of the request line (a combination of the request method, the request path, the query param and `HTTP/1`.1) and the `Date` header in [RFC 7231](https://www.ietf.org/rfc/rfc7231.txt) format. The signature must then be converted into a Base64 string so that it can be attached to the `Authorization` header.

The code will look like this: 

```
// ... the rest of the code

const datetime = new Date().toUTCString();
const requestLine = "POST /v2/klikpajak/v1/efaktur/out?auto_approval=false  HTTP/1.1";
const payload = [`date: ${datetime}`, requestLine].join('\n');
const signature = crypto.createHmac('SHA256', 'YOUR_MEKARI_CLIENT_SECRET').update(payload).digest('base64');

console.log(`hmac username="YOUR_MEKARI_CLIENT_ID", algorithm="hmac-sha256", headers="date request-line", signature="${signature}"`)
```

If you replace `datetime` with `Wed, 10 Nov 2021 07:24:29 GMT` and run the code, you will get the following result.

```
$ node main.js
hmac username="YOUR_MEKARI_CLIENT_SECRET", algorithm="hmac-sha256", headers="date request-line", signature="6+Ah/UTmbqd+DDqlh6zYZ0HuCwVhtElYDOoucRPCaFg="
```

It is important to note that we should not include any credentials in our codebase. This means that we must save the Mekari API client id and client secret that you obtained from the Mekari Developer dashboard to an environment variable. Modern full-stack frameworks, such as Laravel, usually include an `.env` file to make managing environment variables easier. This is also why phpdotenv was installed. We can use this library to move the client id and client secret to the `.env` file. 

```
# .env file
MEKARI_API_BASE_URL=https://api.mekari.com
MEKARI_API_CLIENT_ID=YOUR_MEKARI_API_CLIENT_ID
MEKARI_API_CLIENT_SECRET=YOUR_MEKARI_CLIENT_SECRET
```

Then we use `process.env.*` to replace the credentials in the code.

```
const axios = require('axios');
const crypto = require('crypto');

require('dotenv').config();

// ... the rest of the code

const datetime = new Date().toUTCString();
const requestLine = "POST /v2/klikpajak/v1/efaktur/out?auto_approval=false  HTTP/1.1";
const payload = [`date: ${datetime}`, requestLine].join('\n');
const signature = crypto.createHmac('SHA256', process.env.MEKARI_API_CLIENT_SECRET).update(payload).digest('base64');

console.log(`hmac username="${process.env.MEKARI_API_CLIENT_ID}", algorithm="hmac-sha256", headers="date request-line", signature="${signature}"`)
```

## Wrap It Out
{: .fw-300 }

It's now time to combine everything we've learned into a single Node.js script.

```
const axios = require('axios');
const crypto = require('crypto');

require('dotenv').config();

/**
 * Generate authentication headers based on method and path
 */
function generate_headers(method, pathWithQueryParam) {
  let datetime = new Date().toUTCString();
  let requestLine = `${method} ${pathWithQueryParam} HTTP/1.1`;
  let payload = [`date: ${datetime}`, requestLine].join("\n");
  let signature = crypto.createHmac('SHA256', process.env.MEKARI_API_CLIENT_SECRET).update(payload).digest('base64');

  return {
    'Accept': 'application/json',
    'Content-Type': 'application/json',
    'Date': datetime,
    'Authorization': `hmac username="${process.env.MEKARI_API_CLIENT_ID}", algorithm="hmac-sha256", headers="date request-line", signature="${signature}"`
  };
}

// Set method and path for the request
let method = 'POST';
let path = '/v2/klikpajak/v1/efaktur/out';
let queryParam = '?auto_approval=false';
let headers = {
  'X-Idempotency-Key': '1234'
};
let body = {/* request body */};

const options = {
  method: method,
  url: `${process.env.MEKARI_API_BASE_URL}${path}${queryParam}`,
  headers: {...generate_headers(method, path + queryParam), ...headers}
}

// Initiate request
axios(options)
  .then(function (response) {
    console.log(response.data);
  })
  .catch(function (error) {
    if (error.response) {
      // The request was made and the server responded with a status code
      // that falls out of the range of 2xx
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // The request was made but no response was received
      // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
      // http.ClientRequest in node.js
      console.log(error.request);
    } else {
      // Something happened in setting up the request that triggered an Error
      console.log('Error', error.message);
    }
  });
```

If you want to integrate this script with your existing code, you may need to modify it. Additionally, each Mekari API has its own requirements regarding request headers, query, or body, and you may need to change the script based on your needs. We hope that this guide makes integrating Mekari API into your code easier for you.

You can also look at the final code on [this repository](https://github.com/mekari-engineering/mekari-api-hmac-example-node).
