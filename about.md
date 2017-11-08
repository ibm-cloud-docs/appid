---

copyright:
  years: 2017
lastupdated: "2017-11-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# About
{: #about}

{{site.data.keyword.appid_full}} provides you with the ability to manage access to your applications in a user friendly way.
{:shortdesc}





* To add authentication to your mobile and web applications
* To grant access to protected back-end resources and web apps
* To protect apps that are hosted on {{site.data.keyword.Bluemix_notm}}
* To store user data, such as app preferences or information from their public social profiles
* To use stored data to build personalized app experiences
* To protect resources for both authenticated and anonymous users

**Note**: The implemented protocols are fully compliant with OpenID Connect (OIDC).



## Components
{: #components}

The service is comprised of the following components.

<dl>
  <dt> Dashboard </dt>
    <dd> In the service dashboard you can download on-boarding samples, see activity logs, and configure authentication and identity providers. </dd>
  <dt> Client SDK </dt>
    <dd> You can use the client SDK with your mobile and web apps to implement user authentication. </br></br>
    Prerequisites for Android:
    <ul><ul><li> API 25 or higher </li>
    <li> Java 8.x </li>
    <li> Android SDK tools 25.2.5 or higher </li>
    <li> Android SDK platform tools 25.0.3 or higher </li>
    <li> Android Build Tools version 25.0.2 or higher </li></ul></ul></br>
    Prerequisites for iOS:
    </br>
    <ul><ul><li> iOS9 or higher </li>
    <li> MacOS 10.11.5 </li>
    <li>Xcode 8.2 </li></ul></ul></dd>
  <dt> Server SDK </dt>
    <dd> You can protect your back-end resources that are hosted on {{site.data.keyword.Bluemix_notm}} </br>
    Supported runtimes:
    <ul><ul><li> Node.js </li>
    <li> Liberty for Java </li>
    <li> Swift </li></ul></ul></dd>
</dl>


## Architecture
{: #architecture}

With {{site.data.keyword.appid_short_notm}} you can add a level of security to your applications by requiring users to sign in. You can also use the server SDK to protect your back end resources.

The following diagram shows an overview of how the {{site.data.keyword.appid_short_notm}} service works.


![{{site.data.keyword.appid_short_notm}} architecture diagram](/images/appid_architecture2.png)

Figure 1. {{site.data.keyword.appid_short_notm}} architecture diagram



<dl>
  <dt> Application </dt>
    <dd> The client SDK provides a request class to communicate with your cloud resources. The client SDK automatically starts the authentication process when it detects an authorization challenge. </dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd>  The server SDK extracts the access token from the request and validates it with {{site.data.keyword.appid_short_notm}}. After successful authentication, {{site.data.keyword.appid_short_notm}} returns access and identity tokens to your application. </dd>
  <dt> Identity providers </dt>
    <dd> The service arranges a redirect to the identity provider and verifies the authentication to provide access to your application. {{site.data.keyword.appid_short_notm}} verifies the credentials without having access to the actual passphrase. </dd>
</dl>


## Request flow
{: #request}

The following diagram describes how a request flows from the client SDK to your back-end application and identity providers.

![{{site.data.keyword.appid_short_notm}} request flow](/images/appidrequestflow.png)

Figure 2. {{site.data.keyword.appid_short_notm}} request flow


* Use the {{site.data.keyword.appid_short_notm}} client SDK to make a request to your back-end resources that are protected with the {{site.data.keyword.appid_short_notm}} server SDK.
* The {{site.data.keyword.appid_short_notm}} server SDK detects an unauthorized request and returns an HTTP 401 and authorization scope.
* The client SDK automatically detects the HTTP 401 and starts the authentication process.
* When the client SDK contacts the service, the server SDK returns the login widget if more than one identity provider is configured. {{site.data.keyword.appid_short_notm}} calls the identity provider and presents the login form for that provider, or returns a grant code that allows them to authenticate if no identity providers are configured.
* {{site.data.keyword.appid_short_notm}} asks the client app to authenticate by supplying an authentication challenge.
* If an identity provider is configured when the user logs in, the authentication is handled by the respective OAuth flow.
* If the authentication ends with the same grant code, the code is sent to the token endpoint. The endpoint returns two tokens: an access token and an identity token. From this point on, all requests that are made with the client SDK have a newly obtained authorization header.
* The client SDK automatically resends the original request that triggered the authorization flow.
* The server SDK extracts the authorization header from the request, validates the header with the service, and grants access to a back-end resource.
