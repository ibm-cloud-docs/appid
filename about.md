---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# About
{: #about}

You can use {{site.data.keyword.appid_full}} to add authentication to your apps and protect your back-end resources.
{:shortdesc}

## Reasons to use the service
{: #reasons}

Why would you want to use {{site.data.keyword.appid_short_notm}}? Check out the following scenarios to see whether any of them apply to you.
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
    <td> With {{site.data.keyword.appid_short_notm}}, you can [store user data](/docs/services/appid/user-profile.html) such as app preferences or information from their public social profiles, and then use that data to customize each experience of your app. </td>
  </tr>
  <tr>
    <td> You want to give users the ability to gain access to your app with their email and a password. </td>
    <td> {{site.data.keyword.appid_short_notm}} allows you to create a [cloud directory](/docs/services/appid/cloud-directory.html), which makes it possible for you to add user sign-up and sign-in to your apps. Cloud directory provides you with the framework to maintain a user registry that can scale with your user base. With the pre-built functionality for self service, such as email verification and password resets, you can be sure that your app is authenticating users securely. </td>
  </tr>
</table>


## Integrations
{: #integrations}

You can use {{site.data.keyword.appid_short_notm}} with other {{site.data.keyword.Bluemix_notm}} offerings.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>By configuring ingress in a standard cluster, you can secure your apps at the cluster level. Check out the {{site.data.keyword.appid_short_notm}} authentication ingress annotation to get started.</dd>
  <dt>{{site.data.keyword.openwhisk}} and API Connect</dt>
    <dd>When you create your APIs with [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) and [API Connect](/docs/apis/management/manage_apis.html), you can secure your applications at the gateway rather than in your app code. To see the integration in action, watch <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Try out one of our sample Cloud Foundry apps to see how you can integrate app id into your apps.</dd>
  <dt>iOS Programming Guide</dt>
    <dd>Do you develop apps for Apple? Try out the <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS Programming Guide <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to learn, experiment, and enhance your existing iOS apps with {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>


## Architecture
{: #architecture}

With {{site.data.keyword.appid_short_notm}}, you can add a level of security to your apps by requiring users to sign in. You can also use the server SDK to protect your back-end resources.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} architecture diagram](/images/appid_architecture.png)

<dl>
  <dt> Application </dt>
    <dd><strong>Server SDK</strong>: You can protect your back-end resources that are hosted on {{site.data.keyword.Bluemix_notm}} and your web apps by using the server SDK. It extracts the access token from a request and validates it with {{site.data.keyword.appid_short_notm}}. </br>
    <strong>Client SDK</strong>: You can protect your mobile apps with the Android or iOS client SDK. The client SDK communicates with your cloud resources to start the authentication process when it detects an authorization challenge.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: After successful authentication, {{site.data.keyword.appid_short_notm}} returns access and identity tokens to your app.</br>
    <strong>Cloud directory</strong>: Users can sign up for your service with their email and a password. You can then manage your users in a list view through the UI. With cloud directory, {{site.data.keyword.appid_short_notm}} functions as your identity provider.</dd>
  <dt>External (third party)</dt>
    <dd><strong>Social and enterprise identity providers</strong>:{{site.data.keyword.appid_short_notm}} supports two social identity providers: Facebook and Google+, and one enterprise identity provider: SAML 2.0 Federation. The service arranges a redirect to the identity provider and verifies the returned authentication tokens. If the tokens are valid, the service grants access to your app without ever having access to the actual passphrase.</dd>
</dl>


## Request flow
{: #request}

The following diagram describes how a request flows from the client SDK to your back-end resources and identity providers.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} request flow](/images/appidrequestflow.png)


* The {{site.data.keyword.appid_short_notm}} client SDK makes a request to your back-end resources that are protected with the {{site.data.keyword.appid_short_notm}} server SDK.
* The {{site.data.keyword.appid_short_notm}} server SDK detects an unauthorized request and returns an HTTP 401 and authorization scope.
* The client SDK automatically detects the HTTP 401 and starts the authentication process.
* When the client SDK contacts the service, the server SDK returns the login widget if more than one identity provider is configured. {{site.data.keyword.appid_short_notm}} calls the identity provider and presents the login form for that provider, or returns a grant code that allows them to authenticate if no identity providers are configured.
* {{site.data.keyword.appid_short_notm}} asks the client app to authenticate by supplying an authentication challenge.
* If an identity provider is configured when the user logs in, the authentication is handled by the respective OAuth flow.
* If the authentication ends with the same grant code, the code is sent to the token endpoint. The endpoint returns two tokens: an access token and an identity token. From this point on, all requests that are made with the client SDK have a newly obtained authorization header.
* The client SDK automatically resends the original request that triggered the authorization flow.
* The server SDK extracts the authorization header from the request, validates the header with the service, and grants access to a back-end resource.

**Note**: The implemented protocols are fully compliant with OpenID Connect (OIDC).
