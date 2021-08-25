---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: Home
permalink: /
nav_order: 1
---

# Mekari Developers Documentation
{: .fs-9 }

Explore our guides and examples to integrate Mekari products.
{: .fs-6 .fw-300 } 

## Getting Started

Mekari Developers Center allows you to incorporate powerful Mekari APIs into your own applications. All you have to do is configure the authentication and make an API call to the Mekari product you want to integrate. We provide a variety of APIs to help you automate your business within Mekari's product. 

### Authentication

You can choose between two types of authentication: OAuth2 authentication and HMAC-based authentication. Each of them has its own set of advantages depending on the type of application you want to integrate with Mekari APIs. 

#### OAuth2
{: .fs-3 }

OAuth2 provides more stringent security and authorization, allowing you to call the Mekari API on behalf of existing Mekari users. This is appropriate if you are a Software as a Service (SaaS) developer looking to expand your features by integrating with one of Mekari's products. 

<span class="fs-2">
[Learn More about OAuth2]({{ site.baseurl }}/authentication/oauth2){: .btn }
</span>

#### HMAC
{: .fs-3 }

HMAC authentication is the simplest key-based authentication method, allowing for faster integration with your business. However, the API resource you can access with this authentication is limited to specific company data that already exists on one of Mekari's products. As a result, if you are a company that is already using Mekari products and want to integrate your internal company application with the Mekari API, this is ideal. 

<span class="fs-2">
[Learn More about HMAC]({{ site.baseurl }}/authentication/hmac){: .btn }
</span>

You must set the authentication token for each API call you make, regardless of the type of authentication you use.
Client credentials, consisting of client id and client secret, are used to generate the authentication token.
Please do not hesitate to contact our customer support if you require these credentials. 

<!-- ### Application Scopes

Following the selection of the authentication type for your application, you must specify the integration scope for your application. This scope functions similarly to a permission, determining which API endpoints your application is permitted to call. During the application registration process, our support team will ask you which scope you want to allow for your application. 

<span class="fs-2">
[Learn More about Scopes]({{ site.baseurl }}/scopes){: .btn }
</span> -->

### Calling the API

Once your application's authentication credentials and scopes have been established, you can begin developing your integration with Mekari API. We offer an HTTP-based API that you can integrate with your existing application. The implementation varies depending on the programming language used. Other than that, we also provider Postman collection that you can use to test the API.

<!-- We also provide some examples for you to look at to help you develop the integration. 

<span class="fs-2">
[Code Examples](http://example.com/){: .btn }
</span> -->

<span class="fs-2">
[Postman Collections]({{ site.baseurl }}/product-api){: .btn }
</span>

