---
layout: page
title: Java 8
permalink: /hmac-authentication/java
nav_order: 3
parent: HMAC Authentication
---

# Setup HMAC Authentication in Java 8

We will be using [Java 8](https://www.java.com/en/download/) and use [maven](https://maven.apache.org/download.cgi) to manage dependency. We assume you are already familiar with Java and have it installed on your system. Let's get started.

## Install Dependencies
{: .fw-300 }

Because we'll be using maven, make sure you have the `pom.xml` file in the root of your working directory.
The content of the file should look like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>HMAC Signature</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        ...
    </dependencies>

</project>
```

There will be only one dependency: [OkHttp](https://square.github.io/okhttp/4.x/okhttp/okhttp3/) to make HTTP requests to the Mekari API. There are many Http Client Library out there and you can also choose any other clients.

To install the dependency simply add it under `dependencies` attribute on the `pom.xml`. The file will look something like this.

```xml
<dependencies>
    <dependency>
        <groupId>com.squareup.okhttp3</groupId>
        <artifactId>okhttp</artifactId>
        <version>4.9.1</version>
    </dependency>
</dependencies>
```

## Making API Request
{: .fw-300 }

Using OkHttp Client that we have installed earlier, we are going to setup a script that will perform API request to one of Klikpajak API endpoint which is [create sales invoice](https://documenter.getpostman.com/view/17365057/U16hrR5d#63ba32aa-0f91-44a5-ab40-a0da6a8bf608) (`https://api.mekari.com/v2/klikpajak/v1/efaktur/out`). 

We create the script inside the main function:

```java
public static final MediaType JSON = MediaType.parse("application/json; charset=utf-8");

public static void main(String[] args) {

    OkHttpClient client = new OkHttpClient();

    //      Request Base URL
    String base = "https://api.mekari.com";

    //      HMAC User client id
    String clientId = System.getenv("MEKARI_API_CLIENT_ID");

    //      HMAC User client secret
    String clientSecret = System.getenv("MEKARI_API_CLIENT_SECRET");

    //      Request method GET/POST/PUT/DELETE
    String method = "POST";

    //      Request endpoint
    String path = "/v2/klikpajak/v1/efaktur/out";

    String queryParam = "?auto_approval=false";

    //      Request Body
    String json = "requestBody";

    RequestBody body = RequestBody.create(json, JSON); 

    Request request = new Request.Builder()
        .url(base + path + queryParam)
        .post(body)
        .build();

    Call call = client.newCall(request);
    try {
        Response response = call.execute();
        System.out.println(response.body().string());
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

We can try run the script now but will immediately get Unauthorized response due to no authentication attached in the request.
```json
{"message":"Unauthorized"}
```

## Creating HMAC Signature
{: .fw-300 }

[The signature](/docs/kb/authentication/hmac#generating-signature) is one of the requirements for forming an API request with HMAC Authentication. The signature is an HMAC256 representation of the request line (a combination of the request method, the request path, the query param and `HTTP/1.1`) and the `Date` header in [RFC 7231](https://www.ietf.org/rfc/rfc7231.txt) format. The signature must then be converted into a Base64 string so that it can be attached to the `Authorization` header.

The full request will look like this: 

```java
// ... the rest of the code

//      Request Date
String dateFormatted = getDateTimeNowUtcString();
        
Request request = new Request.Builder()
    .url(base + path + queryParam)
    .post(body)
    .addHeader("Date", dateFormatted)
    .addHeader("Authorization",
        generateAuthSignature(clientId, clientSecret, method, path + queryParam, dateFormatted)
    )
    .build();

Call call = client.newCall(request);
```

To get Date following RFC 7231 format we use this function

```java
private static String getDateTimeNowUtcString() {
    Instant instant = Instant.now();
    return DateTimeFormatter.ofPattern("EEE, dd MMM yyyy HH:mm:ss O")
        .withZone(ZoneOffset.UTC)
        .withLocale(Locale.US)
        .format(instant);
}
```

To generate the Authorization Header we use these functions

```java
import java.nio.charset.StandardCharsets;

private static String generateAuthSignature(
    String clientId, String clientSecret, String method,
    String pathWithQueryParam, String dateString
) {
    String payload = generatePayload(pathWithQueryParam, method, dateString);
    String signature = hmacSha256(clientSecret, payload);

    return "hmac username=\"" + clientId
        + "\", algorithm=\"hmac-sha256\", headers=\"date request-line\", signature=\""
        + signature + "\"";
}

private static String generatePayload(String pathWithQueryParam, String method, String dateString) {
    String requestLine = method + ' ' + pathWithQueryParam + " HTTP/1.1";
    return String.join("\n", Arrays.asList("date: " + dateString, requestLine));
}

private static String hmacSha256(String clientSecret, String payload) {
    try {
        SecretKeySpec signingKey = new SecretKeySpec(clientSecret.getBytes(StandardCharsets.UTF_8), "HmacSHA256");
        Mac mac = Mac.getInstance("HmacSHA256");
        mac.init(signingKey);

        return Base64.getEncoder().encodeToString(mac.doFinal(payload.getBytes(StandardCharsets.UTF_8)));
    } catch (NoSuchAlgorithmException | UnsupportedEncodingException | InvalidKeyException exception) {
        exception.printStackTrace();
        return null;
    }
}
```


It is important to note that we should not include any credentials in our codebase. This means that we must save the Mekari API client id and client secret that you obtained from the Mekari Developer dashboard to an environment variable. Modern full-stack frameworks, such as Spring, usually include an application properties file to make managing environment variables easier.

```
MEKARI_API_CLIENT_ID=YOUR_MEKARI_API_CLIENT_ID
MEKARI_API_CLIENT_SECRET=YOUR_MEKARI_CLIENT_SECRET
```

## Wrap It Out
{: .fw-300 }

It's now time to combine everything we've learned.

```java
import java.nio.charset.StandardCharsets;

public class HmacGeneratorApplication {
    public static final MediaType JSON = MediaType.parse("application/json; charset=utf-8");

    public static void main(String[] args) {

        OkHttpClient client = new OkHttpClient();

        //      Request Base URL
        String base = "https://api.mekari.com";

        //      HMAC User client id
        String clientId = System.getenv("MEKARI_API_CLIENT_ID");

        //      HMAC User client secret
        String clientSecret = System.getenv("MEKARI_API_CLIENT_SECRET");

        //      Request method GET/POST/PUT/DELETE
        String method = "POST";

        //      Request endpoint
        String path = "/v2/klikpajak/v1/efaktur/out";
        String queryParam = "?auto_approval=false";

        //      Request Body
        String json = "requestBody";

        RequestBody body = RequestBody.create(json, JSON);

        //      Request Date
        String dateFormatted = getDateTimeNowUtcString();

        Request request = new Request.Builder()
            .url(base + path + queryParam)
            .post(body)
            .addHeader("Date", dateFormatted)
            .addHeader("Authorization",
                generateAuthSignature(clientId, clientSecret, method, path + queryParam, dateFormatted)
            )
            .addHeader("Content-Type", "application/json")
            .addHeader("Accept", "application/json")
            .addHeader("x-idempotency-key", UUID.randomUUID().toString())
            .build();

        Call call = client.newCall(request);
        try {
            Response response = call.execute();
            System.out.println(response.body().string());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static String generateAuthSignature(
        String clientId, String clientSecret, String method,
        String pathWithQueryParam, String dateString
    ) {
        String payload = generatePayload(pathWithQueryParam, method, dateString);
        String signature = hmacSha256(clientSecret, payload);

        return "hmac username=\"" + clientId
            + "\", algorithm=\"hmac-sha256\", headers=\"date request-line\", signature=\""
            + signature + "\"";
    }

    private static String generatePayload(String pathWithQueryParam, String method, String dateString) {
        String requestLine = method + ' ' + pathWithQueryParam + " HTTP/1.1";
        return String.join("\n", Arrays.asList("date: " + dateString, requestLine));
    }

    private static String hmacSha256(String clientSecret, String payload) {
        try {
            SecretKeySpec signingKey = new SecretKeySpec(
                clientSecret.getBytes(StandardCharsets.UTF_8), 
                "HmacSHA256"
            );
            Mac mac = Mac.getInstance("HmacSHA256");
            mac.init(signingKey);

            return Base64.getEncoder()
                .encodeToString(mac.doFinal(payload.getBytes(StandardCharsets.UTF_8)));
        } catch (NoSuchAlgorithmException 
            | UnsupportedEncodingException 
            | InvalidKeyException exception
        ) {
            exception.printStackTrace();
            return null;
        }
    }

    private static String getDateTimeNowUtcString() {
        Instant instant = Instant.now();
        return DateTimeFormatter.ofPattern("EEE, dd MMM yyyy HH:mm:ss O")
            .withZone(ZoneOffset.UTC)
            .withLocale(Locale.US)
            .format(instant);
    }
}
```

If you want to integrate this script with your existing code, you may need to modify it. Additionally, each Mekari API has its own requirements regarding request headers, query, or body, and you may need to change the script based on your needs. We hope that this guide makes integrating Mekari API into your code easier for you.

You can also look at the final code on [this repository](https://github.com/mekari-engineering/mekari-api-hmac-example-java8).
