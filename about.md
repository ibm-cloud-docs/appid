---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-10"

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

{{site.data.keyword.appid_short_notm}} helps developers to easily add authentication to their web and mobile apps with few lines of code, and secure their Cloud-native applications and services on {{site.data.keyword.Bluemix_notm}}. By requiring users to sign in to your app, you can store user data such as app preferences, or information from public social profiles, and then leverage that data to customize each user's experience within the app. {{site.data.keyword.appid_short_notm}} provides a log-in framework for you, but you can also bring your own branded sign in screens to use with cloud directory.
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
    <dd>Do you develop apps for Apple? Try out the <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS programming guide <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to learn, experiment, and enhance your existing iOS apps with {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>You can monitor administrative activity that is made in {{site.data.keyword.appid_short_notm}} such as changes to the dashboard configuration, by using the [{{site.data.keyword.cloudaccesstrailshort}} service](/docs/services/cloud-activity-tracker/index.html).</dd>
  <dt>Node.js programming guide</dt>
    <dd>Do you develop apps in Node.js? Try out the <a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Node.js programming guide <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to learn, experiment, and enhance your existing Node.js apps with {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>


## Architecture
{: #architecture}

With {{site.data.keyword.appid_short_notm}}, you can add a level of security to your apps by requiring users to sign in. You can also use the server SDK or APIs to protect your back-end resources.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} architecture diagram](/images/appid_architecture1.png)

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

While your request flow might vary depending on your application configuration, there are three main flows that you might encounter while working with {{site.data.keyword.appid_short_notm}}. You might create a mobile app flow, a web app flow, or protect your resources with a different flow. Check out some of the example flows to see if you might be able to start there when configuring your app.
{: shortdesc}

### Web app request flow
{: #web-flow}

![{{site.data.keyword.appid_short_notm}} request flow](/images/web_flow1.png)

1. By using a browser, a user performs an action that triggers a request to the {{site.data.keyword.appid_short_notm}} SDK.
2. If the user is unauthorized, a redirect to {{site.data.keyword.appid_short_notm}} is started.
3. {{site.data.keyword.appid_short_notm}} launches the login widget and sends it to the browser.
4. The user chooses an identity provider to authenticate with and completes the sign in process.
5. The identity provider redirects back to the {{site.data.keyword.appid_short_notm}} SDK with an identity token.
6. The {{site.data.keyword.appid_short_notm}} SDK gets access tokens from the {{site.data.keyword.appid_short_notm}} service.
7. The tokens are saved by the {{site.data.keyword.appid_short_notm}} SDK and a redirect occurs.
8. The user is granted access to the application.

### Mobile request flow
{: #mobile-flow}

![{{site.data.keyword.appid_short_notm}} request flow](/images/mobile_flow.png)

1. A user performs an action the triggers a request by the client application to the {{site.data.keyword.appid_short_notm}} SDK.
2. If the user does not have valid access tokens, the {{site.data.keyword.appid_short_notm}} SDK starts the authorization process.
3. The login widget is displayed to the user.
4. By using one of the configured identity providers, the user authenticates.
5. Once the user has an identity token, then the SDK gets an access token from the {{site.data.keyword.appid_short_notm}} service.
6. With both tokens, the SDK performs the request again.
7. If the tokens are valid, the user is granted access to the application.

### Protected resource request flow
{: #pr-flow}

![{{site.data.keyword.appid_short_notm}} request flow](/images/pr_flow.png)

1. Before a request to the resource can be made, a client application must have a set of public keys.
2. With the public keys, a request is made by a client application.
3. If there is not a valid access token, the application receives an error.
4. After obtaining a valid token, the client app can make the request again. But this time, include the token.
5. When the application can validate the permissions that are granted by the access token, then the application is granted access to the protected resource.


