---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# About
{: #about}

Application security can be incredibly complicated. For most developers, it's one of the hardest parts of creating an app. How can you be sure that you are protecting your user's information? By integrating {{site.data.keyword.appid_full}} into your apps, you can secure resources and add authentication, even when you don't have much security experience.
{:shortdesc}


## Reasons to use the service
{: #reasons}

{{site.data.keyword.appid_short_notm}} helps developers to easily add authentication to their web and mobile apps with few lines of code, and secure their Cloud-native applications and services on {{site.data.keyword.Bluemix_notm}}. By requiring users to sign in to your app, you can store user data such as app preferences, or information from public social profiles, and then leverage that data to customize each user's experience within the app. {{site.data.keyword.appid_short_notm}} provides a log-in framework for you, but you can also bring your own branded sign-in screens to use with cloud directory.
{: shortdesc}

Why would you want to use {{site.data.keyword.appid_short_notm}}? Check out the following scenarios to see whether any of them apply to you.

<table>
  <tr>
    <th>Scenario</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td>You need to add [authorization and authentication](/docs/services/appid/authorization.html) to your mobile and web apps but don't have a background in security.</td>
    <td>{{site.data.keyword.appid_short_notm}} makes it easy to add an authentication step to your apps. You can add email or username sign in, social sign in, or enterprise sign in to your apps with APIs, SDKs, prebuilt UIs, or your own branded UIs.</td>
  </tr>
  <tr>
    <td>You want to limit access to your apps and back-end resources.</td>
    <td>You can secure your apps, back-end resources, and APIs easily by using the standards based authentication provided by {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td>You want to build personalized app experiences for your users.</td>
    <td>With {{site.data.keyword.appid_short_notm}}, you can [store user data](/docs/services/appid/user-profile.html) such as app preferences or information from their public social profiles, and then use that data to customize each experience of your app.</td>
  </tr>
  <tr>
    <td>You want to manage users in a scalable way.</td>
    <td> {{site.data.keyword.appid_short_notm}} allows you to create a [Cloud Directory](/docs/services/appid/cloud-directory.html), which makes it possible for you to add user sign-up and sign-in to your apps. Cloud Directory provides you with the framework to maintain a user registry that can scale with your user base. With the pre-built functionality for self service, such as email verification and password resets, you can be sure that your app is authenticating users securely.</td>
  </tr>
</table>


## Integrations
{: #integrations}

You can use {{site.data.keyword.appid_short_notm}} with other {{site.data.keyword.Bluemix_notm}} offerings.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>By configuring ingress in a standard cluster, you can secure your apps at the cluster level. Check out the <a href="/docs/containers/cs_annotations.html#appid-auth">{{site.data.keyword.appid_short_notm}} authentication Ingress annotation</a> or the <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Announcing App ID integration to IBM Cloud Kubernetes Service <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> blog post to get started.</dd>
  <dt>{{site.data.keyword.openwhisk}} and API Connect</dt>
    <dd>When you create your APIs with [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) and [API Connect](/docs/apis/management/manage_apis.html), you can secure your applications at the gateway rather than in your app code. To see the integration in action, watch <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Try out one of the provided sample Cloud Foundry apps to see how you can integrate {{site.data.keyword.appid_short_notm}} into your apps.</dd>
  <dt>iOS Programming Guide</dt>
    <dd>Do you develop apps for Apple? Try out the <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS Programming Guide <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to learn, experiment, and enhance your existing iOS apps with {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>You can monitor administrative activity that is made in {{site.data.keyword.appid_short_notm}} such as changes to the dashboard configuration, by using the [{{site.data.keyword.cloudaccesstrailshort}} service](/docs/services/cloud-activity-tracker/index.html).</dd>
</dl>


## Architecture
{: #architecture}

With {{site.data.keyword.appid_short_notm}}, you can add a level of security to your apps by requiring users to sign in. You can also use the server SDK to protect your back-end resources.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} architecture diagram](/images/appid_architecture.png)

<dl>
  <dt>Application</dt>
    <dd><strong>Server SDK</strong>: You can protect your back-end resources that are hosted on {{site.data.keyword.Bluemix_notm}} and your web apps by using the server SDK. It extracts the access token from a request and validates it with {{site.data.keyword.appid_short_notm}}. </br>
    <strong>Client SDK</strong>: You can protect your mobile apps with the Android or iOS client SDK. The client SDK communicates with your cloud resources to start the authentication process when it detects an authorization challenge.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: After successful authentication, {{site.data.keyword.appid_short_notm}} returns access and identity tokens to your app.</br>
    <strong>Cloud directory</strong>: Users can sign up for your service with their email and a password. You can then manage your users in a list view through the UI. With cloud directory, {{site.data.keyword.appid_short_notm}} functions as your identity provider.</dd>
  <dt>External (third party)</dt>
    <dd><strong>Social and enterprise identity providers</strong>: {{site.data.keyword.appid_short_notm}} supports Facebook, Google+,and  SAML 2.0 Federation as identity provider options. The service arranges a redirect to the identity provider and verifies the returned authentication tokens. If the tokens are valid, the service grants access to your app without ever having access to the actual passphrase.</dd>
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



