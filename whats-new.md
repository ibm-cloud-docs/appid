---

copyright:
years: 2017, 2021
lastupdated: "2021-02-24"

keywords: release notes, new, spa, single sign on, mfa, cloud directory, saml, app security, application identity

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

# What's new
{: #release-notes}

The following features and changes to the {{site.data.keyword.appid_short_notm}} service are now available.

## February 2021
{: #February2021}

### Kubernetes Ingress annotation
{: #feb-21-ingress}

As of 01 December 2020, the custom Kubernetes Service Ingress image is [deprecated](/docs/containers?topic=containers-ingress-types). The {{site.data.keyword.appid_short_notm}} docs are now updated to include information for integrating with the community Kubernetes image. To get started, see [Containerized apps with Ingress](/docs/appid?topic=appid-kube-auth). For more detailed deployment information, see the [{{site.data.keyword.containershort_notm}} documentation](/docs/containers?topic=containers-ingress_annotation#appid-auth).

## 2020 Updates
{: #2020-updates}

The following releases were new in the year 2020.

### November 2020
{: #November2020}

#### App to app access control
{: #nov-20-app-access-control}

You can now control which actions that an application is able to perform in your apps by using role-based app-to-app access control. For more information, see the [access control docs](/docs/appid?topic=appid-access-control).

### June 2020
{: #June2020}

#### Securing your data in {{site.data.keyword.appid_short_notm}}
{: #june-20-secure-data}

You can now restore deleted instances of {{site.data.keyword.appid_short_notm}} during the data retention period. [Learn more](/docs/appid?topic=appid-mng-data).


## January 2020
{: #January2020}

#### Cloud Directory: Connect your own email provider
{: #jan-20-cd-connect-email-provider}

You can now bring your own custom email provider or connect your SendGrid account to have more control over your email communication with your users. For more information, see the [configuring email settings docs](/docs/appid?topic=appid-cd-types#cd-email-settings).

#### Import and export user roles
{: #jan-20-import-export}

You can now include any roles that are assigned to a user as part of using the export and import APIs. For more information, see the [migrating profiles](/docs/appid?topic=appid-user-admin#migrating-profiles) or [managing Cloud Directory users](/docs/appid?topic=appid-cd-users#user-migration) documentation.

#### Post-MFA extensions
{: #jan-20-post-mfa}

You can now create post-MFA extensions to help you to monitor and improve your users MFA experiences. For more information, see the [extending MFA docs](/docs/appid?topic=appid-cd-mfa#cd-mfa-extensions).

#### Pre-MFA extensions
{: #jan-20-pre-mfa}

You can now create pre-MFA extensions that allow you to make custom decisions at runtime about which users must complete your MFA flow. For more information, see the [extending MFA docs](/docs/appid?topic=appid-cd-mfa#cd-mfa-extensions).


## 2019 Updates
{: #2019-updates}

The following releases were new in the year 2019.

### December 2019
{: #December2019}

#### Access control
{: #dec-19-access}

You can now define which users are able to access your app data, use specific features, or perform specific actions in your apps by using role-based access control. For more information, see the [access control docs](/docs/appid?topic=appid-access-control).


#### Cloud Directory: Custom MFA flows
{: #dec-19-custom-mfa}

You can now make custom decisions about who must complete the MFA flow by configuring your own extension and registering it with {{site.data.keyword.appid_short_notm}}. For more information, see [Customizing MFA](/docs/appid?topic=appid-cd-mfa#cd-premfa).


### November 2019
{: #November2019}

#### Single-page applications: SDK
{: #nov-19-spa-sdk}

Don't manage a backend for your app? You can now easily secure your browser applications by using the JavaScript SDK. For more information, see the [SPA docs](/docs/appid?topic=appid-single-page).

### September 2019
{: #September2019}

#### Increase the security of your SAML flow
{: #sept-secure-saml}

You can now increase the security of your SAML work flows by enabling request signing and response encryption. For more information, see [SAML](/docs/appid?topic=appid-enterprise).


### August 2019
{: #August2019}

#### Track runtime authentication events with {{site.data.keyword.at_short}}
{: #aug-19-at-runtime}

Now you can track, manage, and analyze authentication events that are performed by your app users at runtime by [integrating {{site.data.keyword.at_short}} and {{site.data.keyword.appid_short_notm}}](/docs/appid?topic=appid-at-events#at-monitor-runtime). Releasing your secured custom, mobile, or web app to your users is only the beginning of your journey toward adoption. After your app is deployed, you need to have insights into how your users are interacting with your app. For example, the number and trends of active users. In regulatory markets, such as with HIPAA, you must have a way to share the detailed records of both successful and failed authentication events with auditors. With {{site.data.keyword.appid_short_notm}}, you can now have a very detailed view of runtime events that are related to user authentication.

#### Edit user profile information directly in the dashboard
{: #aug-19-ui-profile-edit}

You can now update profiles for users of your application through the {{site.data.keyword.appid_short_notm}} dashboard. Then, you can use that information to personalize their experience of your app. For more information, see [user profiles](/docs/appid?topic=appid-profiles).


### July 2019
{: #July2019}

#### Create future user profiles through the dashboard
{: #july-19-future-user}

You can now start building profiles for users that you know will use your application in the future through the {{site.data.keyword.appid_short_notm}} dashboard. For more information, see [Preregistering future users](/docs/appid?topic=appid-preregister).

#### Slack channel
{: #july-19-slack}

Have questions while working with {{site.data.keyword.appid_short_notm}}? Get in touch directly with the development team on [Slack](https://www.ibm.com/cloud/blog/announcements/get-help-with-ibm-cloud-app-id-related-questions-on-slack){: external}!

#### The {{site.data.keyword.appid_short_notm}} Identity and Access Istio adapter
{: #july-19-istio} 

Centralize all of your identity management in a single place with the App Identity and Access adapter. The adapter can be configured to work with any OIDC-compliant identity provider, which enables it to control authentication and authorization policies in all environments including both front and backend apps. And, it does it all without any change to your code or the need to redeploy your application. For more information, see [Securing multicloud apps with Istio](/docs/appid?topic=appid-istio-adapter).

#### Access user profile information through the GUI
{: #july-19-user-profile-ui}

View information about all of your users that you can leverage to build personalized app experiences. For more information, see [Storing and accessing profiles](/docs/appid?topic=appid-profiles).

#### Cloud Directory: Automatically associate users with a profile
{: #july-19-auto-associate-users}

Automatically associate Cloud Directory users with an {{site.data.keyword.appid_short_notm}} profile as you create them. For more information, see [Adding and deleting users](/docs/appid?topic=appid-cd-users#delete-users).

### May 2019
{: #May2019}

#### Cloud Directory: View user information
{: #may-19-view-user-info} 

View information about your Cloud Directory users that you can leverage to build personalized app experiences. For more information, see [Viewing user information](/docs/appid?topic=appid-cd-users#cd-user-info).



### April 2019
{: #April2019}

#### Version 4 of the runtime APIs
{: #april-19-v4-runtime-apis} 

Update your apps! To further the standards on which {{site.data.keyword.appid_short_notm}} is based, we've made a few changes. With those changes, we were able to tighten interoperability within the OIDC workflow and broaden the frameworks that are able to use the service. For more information about the changes that you must make before September 2019, see the blog [{{site.data.keyword.cloud_notm}} {{site.data.keyword.appid_short_notm}}: Updated runtime APIs](https://www.ibm.com/cloud/blog/ibm-cloud-app-id-v4-runtime-apis-update){: external}.

#### Cloud Directory: Single sign-on
{: #april-19-sso}

Provide smooth authentication experiences between multiple web apps with single sign-on (SSO) for Cloud Directory. With SSO enabled, user's are not prompted to reenter their credentials the next time they attempt to access your app. Instead, they are automatically signed in to any of your apps that are protected by the same {{site.data.keyword.appid_short_notm}} instance. For more information, see [Single sign-on](/docs/appid?topic=appid-cd-sso).

#### Updated dashboard
{: #april-19-dashboard}

Navigate through your Cloud Directory information quickly! Using [IBM Design Thinking](https://www.ibm.com/design/thinking/){: external}, the {{site.data.keyword.appid_short_notm}} dashboard has been redesigned to give you an even better user experience.


### February 2019
{: #February2019}

#### Cloud Directory: Multi-factor authentication - SMS
{: #feb-19-cd-mfa-sms} 

Require users to enter a second form of authentication during sign-in to increase the security of your app. With Cloud Directory, the first factor is the user's password that they would normally use. Then, the service sends the user a one-time code through SMS that the user must enter before they can gain access to your app. For more information, see [Multi-factor authentication](/docs/appid?topic=appid-cd-mfa).

## 2018 Updates
{: #2018-updates}

The following releases were new in the year 2018.

### December 2018
{: #December2018}

#### Cloud Directory: Multi-factor authentication - Email
{: #dec-18-cd-mfa-email}  

Require users to enter a second form of authentication during sign-in to increase the security of your app. With Cloud Directory, the first factor is the user's password that they would normally use. Then, the service sends the user a one-time code through the email that is registered that the user must enter before they can gain access to your app. For more information, see [Multi-factor authentication](/docs/appid?topic=appid-cd-mfa).

#### Cloud Directory: Password policies
{: #dec-18-cd-password policies} 

Further enforce app security by specifying rules that users must adhere to when they create the password that they use to sign in. For example, you can set an advanced policy that dictates the number of times a password must change before a user can reuse a previous password. Or, you can prevent users from creating a password that contains their username or email address. For more information, see [Defining password policies](/docs/appid?topic=appid-cd-strength).
