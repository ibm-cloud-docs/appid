---

copyright:
  years: 2017
lastupdated: "2017-12-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# About
{: #about}

You can use {{site.data.keyword.appid_full}} to add authentication to your apps and protect your back-end resources.
{:shortdesc}

## Reasons to use the service
{: #reasons}

Why would you want to use {{site.data.keyword.appid_short_notm}}? Check out the following scenarios to see if any of them apply to you.
{: shortdesc}

<table>
  <tr>
    <th> Scenario </th>
    <th> Reason </th>
  </tr>
  <tr>
    <td> You need to add [authorization and authentication](/docs/services/appid/authorization.html) to your mobile and web apps but don't have a background in security. </td>
    <td> {{site.data.keyword.appid_short_notm}} makes it easy to add an authentication step to your apps. You can use the service to communicate with [identity providers](/docs/services/appid/identity-providers.html) to manage access to your apps. </td>
  </tr>
  <tr>
    <td> You want to limit access to your apps and back-end resources. </td>
    <td> The service gives you the ability to [protect your resources](/docs/services/appid/protecting-resources.html) for both authenticated and anonymous users. </td>
  </tr>
  <tr>
    <td> You want to build personalized app experiences for your users. </td>
    <td> {{site.data.keyword.appid_short_notm}} allows you to [store user data](/docs/services/appid/user-profile.html) such as app preferences or information from their public social profiles. You can use that data to ensure that your users have an experience that is customized for them. </td>
  </tr>
</table>


## Architecture
{: #architecture}

With {{site.data.keyword.appid_short_notm}} you can add a level of security to your apps by requiring users to sign in. You can also use the server SDK to protect your back-end resources.

The following diagram shows an overview of how the {{site.data.keyword.appid_short_notm}} service works.

![{{site.data.keyword.appid_short_notm}} architecture diagram](/images/appid_architecture.png)

Figure 1. {{site.data.keyword.appid_short_notm}} architecture diagram


<dl>
  <dt> Application </dt>
    <dd> Server SDK: You can protect your back-end resources that are hosted on {{site.data.keyword.Bluemix_notm}} and your web apps by using the server SDK. It extracts the access token from a request and validates it with {{site.data.keyword.appid_short_notm}}. </br>
    Client SDK: You can protect your mobile apps with the Android or iOS client SDK. The client SDK communicates with your cloud resources to start the authentication process when it detects an authorization challenge.</dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd> App ID: After successful authentication, {{site.data.keyword.appid_short_notm}} returns access and identity tokens to your app.</br>
    Cloud Directory: Users can sign up for your service with their email and a password. You can then manage your users in a list view through the UI. </dd>
  <dt> External (3rd party) </dt>
    <dd>  {{site.data.keyword.appid_short_notm}} supports two social identity providers: Facebook and Google+. The service arranges a redirect to the identity provider and provides access to your app after verifying authentication. {{site.data.keyword.appid_short_notm}} verifies the credentials without having access to the actual passphrase. </dd>
</dl>


## Request flow
{: #request}

The following diagram describes how a request flows from the client SDK to your back-end resources and identity providers.

![{{site.data.keyword.appid_short_notm}} request flow](/images/appidrequestflow.png)

Figure 2. {{site.data.keyword.appid_short_notm}} request flow


* The {{site.data.keyword.appid_short_notm}} client SDK to makes a request to your back-end resources that are protected with the {{site.data.keyword.appid_short_notm}} server SDK.
* The {{site.data.keyword.appid_short_notm}} server SDK detects an unauthorized request and returns an HTTP 401 and authorization scope.
* The client SDK automatically detects the HTTP 401 and starts the authentication process.
* When the client SDK contacts the service, the server SDK returns the login widget if more than one identity provider is configured. {{site.data.keyword.appid_short_notm}} calls the identity provider and presents the login form for that provider, or returns a grant code that allows them to authenticate if no identity providers are configured.
* {{site.data.keyword.appid_short_notm}} asks the client app to authenticate by supplying an authentication challenge.
* If an identity provider is configured when the user logs in, the authentication is handled by the respective OAuth flow.
* If the authentication ends with the same grant code, the code is sent to the token endpoint. The endpoint returns two tokens: an access token and an identity token. From this point on, all requests that are made with the client SDK have a newly obtained authorization header.
* The client SDK automatically resends the original request that triggered the authorization flow.
* The server SDK extracts the authorization header from the request, validates the header with the service, and grants access to a back-end resource.

**Note**: The implemented protocols are fully compliant with OpenID Connect (OIDC).
