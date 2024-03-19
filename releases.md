---

copyright:
  years: 2017, 2024
lastupdated: "2024-03-19"

keywords: release notes, new, spa, single sign on, mfa, cloud directory, saml, app security, application identity

subcollection: appid
content-type: release-note

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
{:terraform: .ph data-hd-interface='terraform'}
{:release-note: data-hd-content-type='release-note'}


# Release notes for {{site.data.keyword.appid_short_notm}}
{: #release-notes}

## 21 March 2023
{: #appid-march2123}
{: release-note}

App ID deprecation
:   Effective 31 March 2025 App ID will be deprecated. Starting on 1 May 2024, no new instances of App ID can be provisioned in any regions. You can continue to use your existing App ID instances until 31 March 2025. Any instances that still exist on that date will be deleted. It's recommended to migrate to {{site.data.keyword.IBM_notm}} Security Verify for authentication to your workloads, including SAML Federation and App ID identities managed with App IDs Cloud Directory. For more information, see the deprecation details. 

## 22 June 2023
{: #appid-jun2223}
{: release-note}

IdP-initiated login is now available
:   If you want to log in to your applications on IBM Cloud from your identity provider's UI, you can enable IdP-initiated login. [Learn more](/docs/appid?topic=appid-enterprise&interface=ui#saml-configure).



## 4 May 2023
{: #appid-may0423}
{: release-note}

IBM Cloud Foundry service broker unsupported
:   All services that use the Cloud Foundry service broker will stop working on 1 June 2023, when Cloud Foundry enters the [End-of-Support stage](/docs/cloud-foundry-public?topic=cloud-foundry-public-deprecation). 

   **Does this change affect me?**

   Not sure if your {{site.data.keyword.appid_short_notm}} instance is using the Cloud Foundry service broker? In the [Cloud Foundry services](https://cloud.ibm.com/cloudfoundry/public){: external} section, check whether your {{site.data.keyword.appid_short_notm}} instance is listed as an alias. If your instance is already an alias, you do not need to take any action.  
   
   If your instance is not an alias and you want to keep it, please contact [IBM Cloud support](https://cloud.ibm.com/unifiedsupport/supportcenter){: external} to discuss next steps.


## 1 February 2023
{: #appid-feb0123}
{: release-note}

Ability to bulk delete Cloud Directory users
:   It's now more efficient for users to clean up {{site.data.keyword.appid_short_notm}} instances. You can now use the `bulk_remove` API endpoint to remove multiple users from an {{site.data.keyword.appid_short_notm}} instance at once. [Learn more](/docs/appid?topic=appid-cd-users#delete-users).


## 15 December 2022
{: #appid-Dec1522}
{: release-note}

New {{site.data.keyword.appid_short_notm}} API endpoints
:   {{site.data.keyword.appid_short_notm}} added options to make it more efficient for you to migrate your users from one service instance to another. You can now use the [`export_all`](/docs/appid?topic=appid-cd-users#cd-export-all) or [`import_all`](/docs/appid?topic=appid-cd-users#cd-import-all) API endpoints to migrate all of your users (up to approximately 16,000).

## 27 June 2022
{: #appid-Jun2722}
{: release-note}

Swift Server SDK unsupported 
:   {{site.data.keyword.cloud_notm}} no longer supports the Swift Server SDK for {{site.data.keyword.appid_short_notm}}. To continue to receive support for your App ID integration, you can move to directly calling the APIs.


## 21 January 2022
{: #appid-Jan2122}
{: release-note}

{{site.data.keyword.appid_short_notm}} availability in Configuration Governance
:   {{site.data.keyword.cloud_notm}} {{site.data.keyword.appid_short_notm}} is now available as part of the Configuration Governance component of the Security and Compliance Center. You can create guardrails for {{site.data.keyword.appid_short_notm}} such as enforcing whether monitoring of runtime activity made by application users is tracked. 



## 15 December 2021
{: #appid-dec1521}
{: release-note}

Logging enhancement
:   As of 15 December 2021, {{site.data.keyword.appid_short_notm}} now logs email addresses from login attempts even if the user is unknown to the service. Previously, email addresses were logged only if the user was known to {{site.data.keyword.appid_short_notm}}.


## 27 September 2021
{: #appid-sept2721}
{: release-note}

New region availability
:   As of 27 September 2021, {{site.data.keyword.appid_short_notm}} is now available in the Sao Paulo region. For a detailed list of the regions in which the service is available, see [Regions and endpoints](/docs/appid?topic=appid-regions-endpoints).

## 12 July 2021
{: #appid-jul1221}
{: release-note}

New region availability
:   As of 12 July 2021, {{site.data.keyword.appid_short_notm}} is now available in the Toronto and Osaka regions. For a detailed list of the regions in which the service is available, see [Regions and endpoints](/docs/appid?topic=appid-regions-endpoints).

## 21 February 2021
{: #appid-feb2121}
{: release-note}

Kubernetes Ingress annotation
:   As of 21 February 2021, the custom Kubernetes Service Ingress image is deprecated. The {{site.data.keyword.appid_short_notm}} docs are now updated to include information for integrating with the community Kubernetes image. To get started, see [Containerized apps with Ingress](/docs/appid?topic=appid-kube-auth). For more detailed deployment information, see the [{{site.data.keyword.containershort_notm}} documentation](/docs/containers?topic=containers-comm-ingress-annotations#app-id-authentication).

## 20 November 2020
{: #appid-nov2020}
{: release-note}

App to app access control
:   You can now control which actions that an application is able to perform in your apps by using role-based app-to-app access control. For more information, see the [access control docs](/docs/appid?topic=appid-access-control).

## 18 June 2020
{: #appid-jun1820}
{: release-note}

Securing your data in {{site.data.keyword.appid_short_notm}}
:   You can now restore deleted instances of {{site.data.keyword.appid_short_notm}} during the data retention period. [Learn more](/docs/appid?topic=appid-mng-data).

## 27 January 2020
{: #appid-jan2720}
{: release-note}

Cloud Directory: Connect your own email provider
:   You can now bring your own custom email provider or connect your SendGrid account to have more control over your email communication with your users. For more information, see the [configuring email settings docs](/docs/appid?topic=appid-cd-types#cd-email-settings).

Import and export user roles
:   You can now include any roles that are assigned to a user as part of using the export and import APIs. For more information, see the [migrating profiles](/docs/appid?topic=appid-user-admin#migrating-profiles) or [managing Cloud Directory users](/docs/appid?topic=appid-cd-users#user-migration) documentation.

Post-MFA extensions
:   You can now create post-MFA extensions to help you to monitor and improve your users MFA experiences. For more information, see the [extending MFA docs](/docs/appid?topic=appid-cd-mfa#cd-mfa-extensions).

Pre-MFA extensions
:   You can now create pre-MFA extensions that allow you to make custom decisions at runtime about which users must complete your MFA flow. For more information, see the [extending MFA docs](/docs/appid?topic=appid-cd-mfa#cd-mfa-extensions).

## 15 December 2019
{: #appid-dec1519}
{: release-note}

Access control
:   You can now define which users are able to access your app data, use specific features, or perform specific actions in your apps by using role-based access control. For more information, see the [access control docs](/docs/appid?topic=appid-access-control).

Cloud Directory: Custom MFA flows
:   You can now make custom decisions about who must complete the MFA flow by configuring your own extension and registering it with {{site.data.keyword.appid_short_notm}}. For more information, see [Customizing MFA](/docs/appid?topic=appid-cd-mfa#cd-premfa).


## 22 November 2019
{: #appid-nov2219}
{: release-note}

Single-page applications: SDK
:   Don't manage a backend for your app? You can now easily secure your browser applications by using the JavaScript SDK. For more information, see the [SPA docs](/docs/appid?topic=appid-single-page).

## 12 September 2019
{: #appid-sept1219}
{: release-note}

Increase the security of your SAML flow
:   You can now increase the security of your SAML work flows by enabling request signing and response encryption. For more information, see [SAML](/docs/appid?topic=appid-enterprise).

## 8 August 2019
{: #appid-aug0819}
{: release-note}

Track runtime authentication events with {{site.data.keyword.at_short}}
:   Now you can track, manage, and analyze authentication events that are performed by your app users at runtime by [integrating {{site.data.keyword.at_short}} and {{site.data.keyword.appid_short_notm}}](/docs/appid?topic=appid-at-events#at-monitor-runtime). Releasing your secured custom, mobile, or web app to your users is only the beginning of your journey toward adoption. After your app is deployed, you need to have insights into how your users are interacting with your app. For example, the number and trends of active users. In regulatory markets, such as with HIPAA, you must have a way to share the detailed records of both successful and failed authentication events with auditors. With {{site.data.keyword.appid_short_notm}}, you can now have a very detailed view of runtime events that are related to user authentication.

Edit user profile information directly in the dashboard
:   You can now update profiles for users of your application through the {{site.data.keyword.appid_short_notm}} dashboard. Then, you can use that information to personalize their experience of your app. For more information, see [user profiles](/docs/appid?topic=appid-profiles).

## 30 July 2019
{: #appid-jul3019}
{: release-note}

Create future user profiles through the dashboard
:   You can now start building profiles for users that you know will use your application in the future through the {{site.data.keyword.appid_short_notm}} dashboard. For more information, see [Preregistering future users](/docs/appid?topic=appid-preregister).

Slack channel
:   Have questions while working with {{site.data.keyword.appid_short_notm}}? Get in touch directly with the development team on [Slack](https://www.ibm.com/blog/announcement/get-help-with-ibm-cloud-app-id-related-questions-on-slack/){: external}!

The {{site.data.keyword.appid_short_notm}} Identity and Access Istio adapter
:   Centralize all your identity management in a single place with the App Identity and Access adapter. The adapter can be configured to work with any OIDC-compliant identity provider, which enables it to control authentication and authorization policies in all environments including both front and backend apps. And, it does it all without any change to your code or the need to redeploy your application. For more information, see [Securing multicloud apps with Istio](/docs/appid?topic=appid-istio-adapter).

Access user profile information through the GUI
:   View information about all your users that you can leverage to build personalized app experiences. For more information, see [Storing and accessing profiles](/docs/appid?topic=appid-profiles).

Cloud Directory: Automatically associate users with a profile
:   Automatically associate Cloud Directory users with an {{site.data.keyword.appid_short_notm}} profile as you create them. For more information, see [Managing users](/docs/appid?topic=appid-cd-users).

## 18 May 2019
{: #appid-may1819}
{: release-note}

Cloud Directory: View user information
:   View information about your Cloud Directory users that you can leverage to build personalized app experiences. For more information, see [Viewing user information](/docs/appid?topic=appid-cd-users#cd-user-info).

## 24 April 2019
{: #appid-apr2419}
{: release-note}

Version 4 of the runtime APIs
:   Update your apps! To further the standards on which {{site.data.keyword.appid_short_notm}} is based, we've made a few changes. With those changes, we were able to tighten interoperability within the OIDC workflow and broaden the frameworks that are able to use the service. For more information about the changes that you must make before September 2019, see the blog [{{site.data.keyword.cloud_notm}} {{site.data.keyword.appid_short_notm}}: Updated runtime APIs](https://www.ibm.com/cloud/blog/ibm-cloud-app-id-v4-runtime-apis-update){: external}.

Cloud Directory: Single sign-on
:   Provide smooth authentication experiences between multiple web apps with single sign-on (SSO) for Cloud Directory. With SSO enabled, user's are not prompted to reenter their credentials the next time they attempt to access your app. Instead, they are automatically signed in to any of your apps that are protected by the same {{site.data.keyword.appid_short_notm}} instance. For more information, see [Single sign-on](/docs/appid?topic=appid-cd-sso).

Updated dashboard
:   Navigate through your Cloud Directory information quickly! Using [IBM Design Thinking](https://www.ibm.com/design/thinking/){: external}, the {{site.data.keyword.appid_short_notm}} dashboard has been redesigned to give you an even better user experience.

## 7 February 2019
{: #appid-feb0719}
{: release-note}

Cloud Directory: Multi-factor authentication - SMS
:   Require users to enter a second form of authentication during sign-in to increase the security of your app. With Cloud Directory, the first factor is the user's password that they would normally use. Then, the service sends the user a one-time code through SMS that the user must enter before they can gain access to your app. For more information, see [Multi-factor authentication](/docs/appid?topic=appid-cd-mfa).

## 11 December 2018
{: #appid-dec1118}
{: release-note}

Cloud Directory: Multi-factor authentication - Email
:   Require users to enter a second form of authentication during sign-in to increase the security of your app. With Cloud Directory, the first factor is the user's password that they would normally use. Then, the service sends the user a one-time code through the email that is registered that the user must enter before they can gain access to your app. For more information, see [Multi-factor authentication](/docs/appid?topic=appid-cd-mfa).

Cloud Directory: Password policies
:   Further enforce app security by specifying rules that users must adhere to when they create the password that they use to sign in. For example, you can set an advanced policy that dictates the number of times a password must change before a user can reuse a previous password. Or, you can prevent users from creating a password that contains their username or email address. For more information, see [Defining password policies](/docs/appid?topic=appid-cd-strength).

## 17 March 2017
{: #appid-mar1717}
{: release-note}

Introducing {{site.data.keyword.appid_short_notm}}
:   IBM Cloud App ID allows you to easily add authentication to web and mobile apps. You no longer have to worry about setting up infrastructure for identity, ensuring geo-availability, and confirming compliance regulations. Instead, you can enhance your apps with advanced security capabilities like multifactor authentication and single sign-on.
