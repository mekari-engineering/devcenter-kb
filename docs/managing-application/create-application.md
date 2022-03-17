---
layout: page
title: Create Application
permalink: /managing-applications/create-application
nav_order: 0
parent: Managing Applications
---

# Create Your First Application

## Request Access
{: .fs-5 }

Before continue on this guide, you need to make sure that your account has been authorized to Mekari Developer. To check it you can login login then if your dashboard show an empty page, this means you account has not been authorized. Please contact your specialist or support if you want to access to Mekari Developer.

### For Talenta Company
{: .fs-4 }

To start the integration, please contact our team, by providing your email, company_name & company_id to talenta-integration[at]mekari.com. The email must be registered and can access the company_name or company_id on [https://hr.talenta.co/](https://hr.talenta.co/)

Next, we will notice if your email has been successfully registered to [Mekari Developer](https://developers.mekari.com/) and once registered, you can generate HMAC and connect to Talenta API by following the instruction below.

## Create Application
{: .fs-5 }

![](/docs/kb/assets/images/create-application-1.png)

On Mekari Developer dashboard, you will see "Create Application" button on the top near header. Click the button and you will be redirected to a page where you can create an application.

![](/docs/kb/assets/images/create-application-2.png)

On the page, you will see 3 fields:

- Application Name
- Company
- Authorized Scopes

**Application Name** is a field where you need to enter the name of your application. You can set the name into anything you want, but make sure that it reflect your application. Most of the time, people fill it with the name of their internal company application.

**Company** is a field where you need to select the company you want to develop integration into. You are only allowed to select one company on this field. If you happen to have more than one company and you want to setup integration to all of it, you need to create application for each company and get separated client credentials.

**Authorized Scopes** is a field where you need to tick the scopes you need for the integration. Each scope represent specific API endpoint. Please only choose only scope that you need for your company internal application. To learn more about application scopes, please visit [this page](#).

Once you fill all the fields, click submit to create client credentials for your application.

## Client Credentials
{: .fs-5 }

![](/docs/kb/assets/images/create-application-3.png)

After you create the application, Client ID and Client Secret your application will appear on the page. Make sure you copy the credentials especially Client Secret, because you only able to see the value of client secret on this page.

From here you can use the credentials to integrate your application with Mekari API. You can see examples on how to setup HMAC authentication on [this section]({{ site.baseurl }}/hmac-authentication).

