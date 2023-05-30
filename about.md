---

copyright:
  years: 2017, 2023
lastupdated: "2023-05-30"

keywords: authentication, authorization, identity, app security, cloud directory, user data, identity provider, oauth, protocols, oauth, oidc, disaster recovery, dr, compliance, high availability, ha, secure, HA, DR

subcollection: appid

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}
{:release-note: data-hd-content-type='release-note'}


# About {{site.data.keyword.appid_short_notm}}
{: #about}

Application security can be incredibly complicated. For most developers, it's one of the hardest parts of creating an app. How can you be sure that you are protecting your user's information? By integrating {{site.data.keyword.appid_full}} into your apps, you can secure resources and add authentication - even when you don't have much security experience.
{: shortdesc}

What can {{site.data.keyword.appid_short_notm}} do for you? Check out the following video to learn more.

![About {{site.data.keyword.appid_short_notm}}](https://www.youtube.com/embed/XlrCjHdK43Q){: video output="iframe" data-script="#transcript-about-appid" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}


## Video transcript
{: #transcript-about-appid}
{: notoc}

The following section provides the transcript for the introduction to {{site.data.keyword.appid_short_notm}} video for users who might need an alternative format or a translated version.

Wouldn't it be awesome if the barista at your local coffee shop remembered your name and your usual brew. If you're building an application, you might want to build that kind of tailored experience for your users to make them feel special or save them time. Of course, no matter how great your idea is, the success of your app depends on your ability to build trust with your users - which comes down to securing your users data and protecting the systems that your app accesses. Knowing who is using your app is a key part of this. It starts with adding sign in functionality. But, as a lot of developers know, adding authentication and authorization to your app is both risky and complex. That's why we built {{site.data.keyword.appid_short_notm}} on {{site.data.keyword.cloud_notm}}. {{site.data.keyword.appid_short_notm}} helps developers to easily add authentication to their mobile and web apps and hosts user data in the cloud that developers can use to build custom app experiences.

To make the sign-in experience easy for your users, with {{site.data.keyword.appid_short_notm}}, you can let users sign in directly from your app and then sign in with their email and password. Or, you can let users sign in through their Facebook or Google accounts with credentials they already know. Once your users authenticate, you can authorize access to backend resources that your app uses.

{{site.data.keyword.appid_short_notm}} also helps you deliver tailored experiences for your users based on a variety of factors. In {{site.data.keyword.appid_short_notm}} you can store information about your users and let developers use this information for their apps. {{site.data.keyword.appid_short_notm}} is available for iOS, Android, and the web. And of course, it's built with open standards like OAuth 2.0 and OIDC. To get started, check out the {{site.data.keyword.appid_short_notm}} service in the {{site.data.keyword.cloud_notm}} catalog.



## Reasons to use the service
{: #about-reasons}

{{site.data.keyword.appid_short_notm}} helps developers to easily add authentication to their web and mobile apps with few lines of code, and secure their Cloud-native applications and services on {{site.data.keyword.cloud_notm}}. By requiring users to sign in to your app, you can store user data such as app preferences, or information from public social profiles, and then leverage that data to customize each user's experience within the app. {{site.data.keyword.appid_short_notm}} provides a log-in framework for you, but you can also bring your own branded screens to use with Cloud Directory.
{: shortdesc}

| Scenario | Solution |
|-----|----|
| You need to add [authorization and authentication](/docs/appid?topic=appid-key-concepts) to your mobile and web apps but don't have a background in security. | {{site.data.keyword.appid_short_notm}} makes it easy to add an authentication step to your apps. You can add email or user name, social, or enterprise sign-in to your apps with APIs, SDKs, prebuilt UIs, or your own branded UIs. |
| You want to limit access to your apps and back-end resources. | You can secure your apps, back-end resources, and APIs easily by using the standards-based authentication provided by {{site.data.keyword.appid_short_notm}}. |
| You want to build personalized app experiences for your users. | With {{site.data.keyword.appid_short_notm}}, you can [store user data](/docs/appid?topic=appid-profiles) such as app preferences or information from their public social profiles, and then use that data to customize each experience of your app. |
| You want to manage users in a scalable way. | With {{site.data.keyword.appid_short_notm}} you can create a [Cloud Directory](/docs/appid?topic=appid-cloud-directory), which makes it possible for you to add user sign-up and sign-in to your apps. Cloud Directory provides you with the framework to maintain a user registry that can scale with your user base. With the pre-built functionality for self-service, such as email verification and password resets, you can be sure that your app is authenticating users securely. |
{: caption="Table 1. Reasons to use the {{site.data.keyword.appid_short_notm}} service" caption-side="top"}


## How it works
{: #about-how-it-works}

With {{site.data.keyword.appid_short_notm}}, you can add a level of security to your apps by requiring users to sign in. You can also use the server SDK or APIs to protect your back-end resources.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} architecture diagram](images/appid_architecture1.png){: caption="Figure 1. How {{site.data.keyword.appid_short_notm}} works" caption-side="bottom"}

Application
:   **Server SDK**: You can protect your back-end resources that are hosted on {{site.data.keyword.cloud_notm}} and your web apps by using the server SDK. It extracts the access token from a request and validates it with {{site.data.keyword.appid_short_notm}}.
    **Client SDK**: You can protect your mobile apps with the Android or iOS client SDK. The client SDK communicates with your cloud resources to start the authentication process when it detects an authorization challenge.

{{site.data.keyword.cloud_notm}}
:   **{{site.data.keyword.appid_short_notm}}**: After successful authentication, {{site.data.keyword.appid_short_notm}} returns access and identity tokens to your app.
    **Cloud Directory**: Users can sign up for your service with their email and a password. You can then manage your users in a list view through the UI. With Cloud Directory, {{site.data.keyword.appid_short_notm}} functions as your identity provider.

External (third party)
:   **Social and enterprise identity providers**: {{site.data.keyword.appid_short_notm}} supports Facebook, Google+, and  SAML 2.0 Federation as identity provider options. The service arranges a redirect to the identity provider and verifies the returned authentication tokens. If the tokens are valid, the service grants access to your app.


## Integrations
{: #about-integrations}

You can use {{site.data.keyword.appid_short_notm}} with other {{site.data.keyword.cloud_notm}} offerings.
{: shortdesc}


{{site.data.keyword.containershort_notm}}
:   By configuring Ingress in a standard cluster you can secure your apps at the cluster level. Check out the [{{site.data.keyword.appid_short_notm}} authentication Ingress annotation](/docs/containers?topic=containers-comm-ingress-annotations#app-id-authentication) or the [Announcing {{site.data.keyword.appid_short_notm}} integration to {{site.data.keyword.containerlong_notm}}](https://www.ibm.com/cloud/blog/announcing-app-id-integration-ibm-cloud-kubernetes-service){: external} blog post to get started.

{{site.data.keyword.openwhisk_short}} and {{site.data.keyword.apiconnect_short}}
:   When you create your APIs with [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk?topic=openwhisk-getting-started) and [API Connect](/docs/apiconnect?topic=apiconnect-getting-started), you can secure your applications at the gateway rather than in your app code.

{{site.data.keyword.at_short}}
:   You can monitor administrative activity that is made in {{site.data.keyword.appid_short_notm}} such as changes to the dashboard configuration, by using the [{{site.data.keyword.at_short}} service](/docs/activity-tracker?topic=activity-tracker-getting-started).


## Standards and certifications
{: #about-standards}

{{site.data.keyword.appid_short_notm}} has successfully completed several certifications, audits, and standards.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} is based on a set of well-known, industry standard protocols and specifications that are frequently found in both enterprise and consumer facing applications, the OAuth 2.0 Authorization Framework and Open ID Connect. OAuth 2.0 is used to obtain and verify authorization for accessing protected resources. Open ID Connect then adds a layer of authentication and identity protection to your application.

See section 5.4 of the {{site.data.keyword.appid_short_notm}} software product compatibility report to review a complete list of [certifications](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=BF31C8008D7C11E59F9AD7336D7D0FFB){: external}. In addition to the certifications, {{site.data.keyword.appid_short_notm}} is also compliant in the following specifications: OAuth 2.0, OpenID Connect, JSON Web Token (JWT), JSON Web Signature (JWS), System for Cross-domain Identity Management (SCIM).



