---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}

# About {{site.data.keyword.appid_short_notm}}
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

</br>

## Advanced security features
{: #advanced-security}

If you have an instance of App ID that was created after March 15, 2018, you can take advantage of advanced security features.

These features are available only to those instances that are on the graduated tier pricing plan.
{: note}

By default, advanced security features are disabled. Enabling any of these features incurs an extra charge. If you disable all of the advanced features, your account will revert to the lower-cost policy. For the most accurate pricing information, check out the [pricing calculator](https://console.bluemix.net/pricing/configure/service/AdvancedMobileAccess-d6aece47-d840-45b0-8ab9-ad15354deeea).

Check out the following table to learn about the available features and what they can do for you.

<table>
  <tr>
    <th>Feature</th>
    <th>Benefit</th>
  </tr>
  <tr>
    <td>Multi-Factor Authentication</td>
    <td>MFA confirms a user’s identity by requiring multiple types of credentials. For example, having a user input a one-time code that is sent to a their email account or phone in addition to entering their username and password. For more information about using MFA, see the [Multi-Factor Authentication](mfa.html).</td>
  </tr>
  <tr>
    <td>Password policy management</td>
    <td>As an account owner, you can specify rules that all passwords must adhere to. Examples include, the number of attempted sign-ins before lockout, expiration times, minimum time span between password updates, or the number of times that a password can't be repeated. For a complete list of the options and set up information, see [Advanced password management](cloud-directory.html#advanced-password)</td>
  </tr>
</table>

Keep checking back, new features are being added all the time. Do you have a specific feature request? Reach out to our team and <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">let us know <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>!
{: tip}

</br>


## Integrations
{: #integrations}

You can use {{site.data.keyword.appid_short_notm}} with other {{site.data.keyword.Bluemix_notm}} offerings.
{:shortdesc}

<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>By configuring Ingress in a standard cluster, you can secure your apps at the cluster level. Check out the <a href="/docs/containers/cs_annotations.html#appid-auth">{{site.data.keyword.appid_short_notm}} authentication Ingress annotation</a> or the <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Announcing {{site.data.keyword.appid_short_notm}} integration to {{site.data.keyword.containerlong_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> blog post to get started.</dd>
  <dt>{{site.data.keyword.openwhisk}} and API Connect</dt>
    <dd>When you create your APIs with [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) and [API Connect](/docs/services/apiconnect/getting-started.html), you can secure your applications at the gateway rather than in your app code. To see the integration in action, watch <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</dd>
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

![{{site.data.keyword.appid_short_notm}} architecture diagram](images/appid_architecture1.png)

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

</br>


