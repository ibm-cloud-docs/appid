---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-06"

keywords: certificates, SSL,

subcollection: certificate-manager

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

# What's new
{: #release-notes}

The following features and changes to the {{site.data.keyword.appid_short_notm}} service are now available.


## July 2019
{: #July2019}

- **Create future user profiles through the dashboard**

    You can now start building profiles for users that you know will use your application in the future through the {{site.data.keyword.appid_short_notm}} dashboard. For more information, see [Preregistering future users](/docs/services/appid?topic=appid-preregister).

- **Slack channel**

    Have questions while working with {{site.data.keyword.appid_short_notm}}? Get in touch directly with the development team on [Slack](https://ibm-container-service.slack.com){: external}!

- **The {{site.data.keyword.appid_short_notm}} Identity and Access Istio adapter**  

    Centralize all of your identity management in a single place with the App Identity and Access adapter. The adapter can be configured to work with any OIDC-compliant identity provider, which enables it to control authentication and authorization policies in all environments including both front and backend apps. And, it does it all without any change to your code or the need to redeploy your application. For more information, see [Securing multicloud apps with Istio](/docs/services/appid?topic=appid-istio-adapter).

- **Access user profile information through the GUI**

    View information about all of your users that you can leverage to build personalized app experiences. For more information, see [Storing and accessing profiles](/docs/services/appid?topic=appid-profiles).

- **Cloud Directory: Automatically associate users with a profile**

    Automatically associate Cloud Directory users with an {{site.data.keyword.appid_short_notm}} profile as you create them. For more information, see [Adding and deleting users](/docs/services/appid?topic=appid-cd-users#add-delete-users).



## May 2019
{: #May2019}

- **Cloud Directory: View user information**  

    View information about your Cloud Directory users that you can leverage to build personalized app experiences. For more information, see [Viewing user information](/docs/services/appid?topic=appid-cd-users#cd-user-info).



## April 2019
{: #April2019}

- **Version 4 of the runtime APIs**  

    Update your apps! To further the standards on which {{site.data.keyword.appid_short_notm}} is based, we've made a few changes. With those changes, we were able to tighten interoperability within the OIDC workflow and broaden the frameworks that are able to use the service. For more information about the changes that you must make before September 2019, see the blog [{{site.data.keyword.cloud_notm}} {{site.data.keyword.appid_short_notm}}: Updated runtime APIs](https://www.ibm.com/cloud/blog/ibm-cloud-app-id-v4-runtime-apis-update){: external}. 

- **Cloud Directory: Single sign on**  

    Provide smooth authentication experiences between multiple web apps with single sign-on (SSO) for Cloud Directory. With SSO enabled, user's are not prompted to reenter their credentials the next time they attempt to access your app. Instead, they are automatically signed in to any of your apps that are protected by the same {{site.data.keyword.appid_short_notm}} instance. For more information, see [Single sign-on](/docs/services/appid?topic=appid-cd-sso).

- **Updated dashboard**  

    Navigate through your Cloud Directory information quickly! Using [{{site.data.keyword.cloud_notm}} Design Thinking](https://www.ibm.com/design/thinking/){: external}, the {{site.data.keyword.appid_short_notm}} dashboard has been redesigned to give you an even better user experience.



## February 2019
{: #February2019}

- **Cloud Directory: Multi-factor authentication - SMS**    
    
    Require users to enter a second form of authentication during sign in to increase the security of your app. With Cloud Directory, the first factor is the user's password that they would normally use. Then, the service sends the user a one-time code through SMS that the user must enter before they can gain access to your app. For more information, see [Multi-factor authentication](/docs/services/appid?topic=appid-cd-mfa).



## December 2018
{: #December2018}

- **Cloud Directory: Multi-factor authentication - Email**    
    
    Require users to enter a second form of authentication during sign in to increase the security of your app. With Cloud Directory, the first factor is the user's password that they would normally use. Then, the service sends the user a one-time code through the email that is registered that the user must enter before they can gain access to your app. For more information, see [Multi-factor authentication](/docs/services/appid?topic=appid-cd-mfa).

- **Cloud Directory: Password policies**  

    Further enforce app security by specifying rules that users must adhere to when they create the password that they use to sign in. For example, you can set an advanced policy that dictates the number of times a password must change before a user can reuse a previous password. Or, you can prevent users from creating a password that contains their username or email address. For more information, see [Defining password policies](/docs/services/appid?topic=appid-cd-strength).
