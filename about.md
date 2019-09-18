---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-18"

keywords: Authentication, authorization, identity, app security, secure, compliance, high availability, ha, disaster recovery, dr, protocols, oauth, oidc

subcollection: appid

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# About {{site.data.keyword.appid_short_notm}}
{: #about}

Application security can be incredibly complicated. For most developers, it's one of the hardest parts of creating an app. How can you be sure that you are protecting your user's information? By integrating {{site.data.keyword.appid_full}} into your apps, you can secure resources and add authentication - even when you don't have much security experience.
{: shortdesc}

What can {{site.data.keyword.appid_short_notm}} do for you? Check out this video to learn more!

<iframe class="embed-responsive-item" id="about-appid" title="About {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/XlrCjHdK43Q?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Video transcript
{: #transcript-about-appid}
{: script}
{: notoc}

The following section provides the transcript for the introduction to {{site.data.keyword.appid_short_notm}} video for users who might need an alternative format or a translated version.

Wouldn't it be awesome if the barista at your local coffee shop remembered your name and your usual brew. If you're building an application, you might want to build that kind of tailored experience for your users to make them feel special or save them time. Of course, no matter how great your idea is, the success of your app depends on your ability to build trust with your users - which comes down to securing your users data and protecting the systems that your app accesses. Knowing who is using your app is a key part of this. It starts with adding sign in functionality. But, as a lot of developers know, adding authentication and authorization to your app is both risky and complex. That's why we built {{site.data.keyword.appid_short_notm}} on {{site.data.keyword.cloud_notm}}. {{site.data.keyword.appid_short_notm}} helps developers to easily add authentication to their mobile and web apps and hosts user data in the cloud that developers can use to build custom app experiences.

To make the sign in experience easy for your users, with {{site.data.keyword.appid_short_notm}}, you can let users sign in directly from your app and then sign in with their email and password. Or, you can let users sign in through their Facebook or Google accounts with credentials they already know. Once your users authenticate, you can authorize access to backend resources that your app uses. 

{{site.data.keyword.appid_short_notm}} also helps you deliver tailored experiences for your users based on a variety of factors. In {{site.data.keyword.appid_short_notm}} you can store information about your users and let developers use this info for their apps. {{site.data.keyword.appid_short_notm}} is available for iOS, Android, and the web. And of course, it's built with open standards like OAuth 2.0 and OIDC. To get started, check out the {{site.data.keyword.appid_short_notm}} service in the {{site.data.keyword.cloud_notm}} catalog.

## Reasons to use the service
{: #about-reasons}

{{site.data.keyword.appid_short_notm}} helps developers to easily add authentication to their web and mobile apps with few lines of code, and secure their Cloud-native applications and services on {{site.data.keyword.cloud_notm}}. By requiring users to sign in to your app, you can store user data such as app preferences, or information from public social profiles, and then leverage that data to customize each user's experience within the app. {{site.data.keyword.appid_short_notm}} provides a log-in framework for you, but you can also bring your own branded screens to use with Cloud Directory.
{: shortdesc}

<table>
  <caption>Table 1. Reasons to use the {{site.data.keyword.appid_short_notm}} service</caption>
  <tr>
    <th>Scenario</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td>You need to add [authorization and authentication](/docs/services/appid?topic=appid-key-concepts) to your mobile and web apps but don't have a background in security.</td>
    <td>{{site.data.keyword.appid_short_notm}} makes it easy to add an authentication step to your apps. You can add email or user name, social, or enterprise sign in to your apps with APIs, SDKs, prebuilt UIs, or your own branded UIs.</td>
  </tr>
  <tr>
    <td>You want to limit access to your apps and back-end resources.</td>
    <td>You can secure your apps, back-end resources, and APIs easily by using the standards-based authentication provided by {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td>You want to build personalized app experiences for your users.</td>
    <td>With {{site.data.keyword.appid_short_notm}}, you can [store user data](/docs/services/appid?topic=appid-profiles) such as app preferences or information from their public social profiles, and then use that data to customize each experience of your app.</td>
  </tr>
  <tr>
    <td>You want to manage users in a scalable way.</td>
    <td> With {{site.data.keyword.appid_short_notm}} you can create a [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), which makes it possible for you to add user sign-up and sign-in to your apps. Cloud Directory provides you with the framework to maintain a user registry that can scale with your user base. With the pre-built functionality for self-service, such as email verification and password resets, you can be sure that your app is authenticating users securely.</td>
  </tr>
</table>


## How it works
{: #about-how-it-works}

With {{site.data.keyword.appid_short_notm}}, you can add a level of security to your apps by requiring users to sign in. You can also use the server SDK or APIs to protect your back-end resources.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} architecture diagram](images/appid_architecture1.png){: caption="Figure 1. How {{site.data.keyword.appid_short_notm}} works" caption-side="bottom"}

<dl>
  <dt>Application</dt>
    <dd><strong>Server SDK</strong>: You can protect your back-end resources that are hosted on {{site.data.keyword.cloud_notm}} and your web apps by using the server SDK. It extracts the access token from a request and validates it with {{site.data.keyword.appid_short_notm}}. </br>
    <strong>Client SDK</strong>: You can protect your mobile apps with the Android or iOS client SDK. The client SDK communicates with your cloud resources to start the authentication process when it detects an authorization challenge.</dd>
  <dt>{{site.data.keyword.cloud_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: After successful authentication, {{site.data.keyword.appid_short_notm}} returns access and identity tokens to your app.</br>
    <strong>Cloud Directory</strong>: Users can sign up for your service with their email and a password. You can then manage your users in a list view through the UI. With Cloud Directory, {{site.data.keyword.appid_short_notm}} functions as your identity provider.</dd>
  <dt>External (third party)</dt>
    <dd><strong>Social and enterprise identity providers</strong>: {{site.data.keyword.appid_short_notm}} supports Facebook, Google+, and  SAML 2.0 Federation as identity provider options. The service arranges a redirect to the identity provider and verifies the returned authentication tokens. If the tokens are valid, the service grants access to your app without ever having access to the actual passphrase.</dd>
</dl>


## Integrations
{: #about-integrations}

You can use {{site.data.keyword.appid_short_notm}} with other {{site.data.keyword.cloud_notm}} offerings.
{:shortdesc}

<dl>
  <dt>{{site.data.keyword.containershort_notm}}</dt>
    <dd>By configuring Ingress in a standard cluster, you can secure your apps at the cluster level. Check out the <a href="/docs/containers?topic=containers-ingress_annotation#appid-auth">{{site.data.keyword.appid_short_notm}} authentication Ingress annotation</a> or the <a href="https://www.ibm.com/cloud/blog/announcing-app-id-integration-ibm-cloud-kubernetes-service">Announcing {{site.data.keyword.appid_short_notm}} integration to {{site.data.keyword.containerlong_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> blog post to get started.</dd>
  <dt>{{site.data.keyword.openwhisk_short}} and {{site.data.keyword.apiconnect_short}}</dt>
    <dd>When you create your APIs with [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk?topic=cloud-functions-getting-started) and [API Connect](/docs/services/apiconnect?topic=apiconnect-getting-started), you can secure your applications at the gateway rather than in your app code. To see the integration in action, watch <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAuth with API Connect and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Try out one of the provided sample Cloud Foundry apps to see how you can integrate {{site.data.keyword.appid_short_notm}} into your apps.</dd>
  <dt>{{site.data.keyword.at_short}}</dt>
    <dd>You can monitor administrative activity that is made in {{site.data.keyword.appid_short_notm}} such as changes to the dashboard configuration, by using the [{{site.data.keyword.at_short}} service](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started).</dd>
  <dt>iOS Programming Guide</dt>
    <dd>Do you develop apps for Apple? Try out the [iOS programming guide](/docs/swift?topic=swift-getting-started) to learn, experiment, and enhance your existing iOS apps with {{site.data.keyword.cloud_notm}}.</dd>
  <dt>Node.js programming guide</dt>
    <dd>Do you develop apps in Node.js? Try out the [Node.js programming guide](/docs/node?topic=nodejs-getting-started) to learn, experiment, and enhance your existing Node.js apps with {{site.data.keyword.cloud_notm}}.</dd>
</dl>


## Compliance and standards
{: #about-compliance}

{{site.data.keyword.appid_short_notm}} has successfully completed several certifications, audits, and standards. 
{: shortdesc}

{{site.data.keyword.appid_short_notm}} is based on a set of well-known, industry standard protocols and specifications that are frequently found in both enterprise and and consumer facing applications, the OAuth 2.0 Authorization Framework and Open ID Connect. OAuth 2.0 is used to obtain and verify authorization for accessing protected resources. Open ID Connect then adds a layer of a authentication and identity protection to your application.

See section 5.4 of the {{site.data.keyword.appid_short_notm}} software product compatibility report to review a complete list of [certifications](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=BF31C8008D7C11E59F9AD7336D7D0FFB){: external}. In addition to the certifications, {{site.data.keyword.appid_short_notm}} is also compliant in the following specifications: OAuth 2.0, OpenID Connect, JSON Web Token (JWT), JSON Web Signature (JWS), System for Cross-domain Identity Management (SCIM). 


## Regional high-availability
{: #ha-dr}

{{site.data.keyword.appid_short_notm}} is a highly available, regional service that runs in multiple zones.
{: shortdesc}

In each supported multizone region, every zone has its own {{site.data.keyword.containerlong_notm}} cluster with several worker nodes. Each worker node runs several instances of {{site.data.keyword.appid_short_notm}} components. Each region is fronted by a global load balancer and a web application firewall.

Data that is stored in {{site.data.keyword.appid_short_notm}} is encrypted and persisted in a database cluster that is spread across availability zones. The data is also back up in a separate encrypted object storage.

Because {{site.data.keyword.appid_short_notm}} is a regional service, it does not provide automated cross-regional failover or cross-regional disaster recovery. However, {{site.data.keyword.appid_short_notm}} does provide an [extensive API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external} that developers can use to manually synchronize their service configuration with another instance or instances of {{site.data.keyword.appid_short_notm}}.

## Data separation and encryption
{: #data-encryption}

{{site.data.keyword.appid_short_notm}} stores and encrypts user profile attributes. As a multi-tenant service, every tenant has a designated encryption key and user data in each tenant is encrypted with only that tenant's key.

{{site.data.keyword.appid_short_notm}} ensures that private information is encrypted before it is stored.
{: note}


