---

copyright:
  years: 2021
lastupdated: "2021-07-13"

keywords: user registry, sign up, sign in, username, email, password, account settings, reset password, email sender, email verification, app security

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

# What is Cloud Directory?
{: #cd-concept}

With {{site.data.keyword.appid_full}}, you can let your users sign up directly from your mobile or web app and sign in with their email and password. You can use Cloud Directory to create a scalable user registry that leverages a pre-built functionality to enhance security and self-service. (Short desc)
{: shortdesc}

## Cloud Directory Features
{: #cd-features}

Cloud Directory hosts many features that enable you to manage the experience and security of the users of your app. With Cloud Directory, you can:
* enhance the security of your app with email verification
* allow greater user control with default sign-up and sign-in widget and flows
* brand your app with custom UIs and flows
* gather deeper user insights by integrating {{site.data.keyword.appid_short_notm}} with your own mail provider. 
{: shortdesc}

### Enhance security with email verification
{: #cd-email-verify}

To sign-up your users, you can leverage the pre-built [email verification](/docs/appid?topic=appid-cd-types) flow that comes with Cloud Directory. If you enable email verification on the Cloud Directory settings page, users who sign-up for your app will need to verify their email. After they've signed up, you can allow your users to have limited interactions with your app until they verify their email address.

### Allow greater user control with default sign-up and sign-in widget and flows
{: #cd-login-widget}

{{site.data.keyword.appid_short_notm}} provides a default sign-up and sign-in widget with out-of-the-box user flows, such as reset password and email verification. By default, Cloud Directory is available to your users through the Login Widget, in addition to Facebook and Google. You can choose which identity providers you want to configure at any time. For more information, see how to use the [Login Widget](/docs/appid?topic=appid-login-widget). 

In the Cloud Directory dashboard, you can [configure the level of self-service](/docs/appid?topic=appid-cd-users) you want to allow in your application. You can use the Cloud Directory APIs and dashboard to allow users to change their account details and password through {{site.data.keyword.appid_short_notm}}'s prebuilt screens for those functions. You can update the settings at any time without needing to change your code or redeploy your application. 

### Brand your app with custom UIs and flows
{: #cd-custom-ui}

You can [replace the default {{site.data.keyword.appid_short_notm}} sign-in](/blogs/cloud-archive/2018/06/custom-login-page-app-id-integration/) and sign-up UIs and flows with customized options to support your brand recognition and policies. For more information, see how to brand your app. When a user signs-up for your app, you can customize the flow in various ways. For example, you can add extra fields to the flow (e.g. phone number), validate the [password length by policy](/docs/appid?topic=appid-cd-strength), and accept only specific email addresses or check emails against a black-list. 

You can customize the sign-in flow by [configuring the forgot password process](/docs/appid?topic=appid-cd-strength).  Additionally, you can [enable single sign-on (SSO)](/docs/appid?topic=appid-cd-sso) to provide your users a smooth authentication experience between multiple web apps. {{site.data.keyword.appid_short_notm}} provides SSO for Cloud Directory users. Therefore, if enabled, your users are not required to reenter their credentials every time they sign-in. Instead, users are automatically signed in to any of your apps that are protected by the same {{site.data.keyword.appid_short_notm}} instance. 

With {{site.data.keyword.appid_short_notm}} Cloud Directory, you can make the sign-in flow more secure by requiring [multiple authentication factors](/docs/appid?topic=appid-cd-mfa). With a second authentication factor, you can increase the security of your application by not only confirming that a user possesses the knowledge of their credentials, but also can access their registered email or phone number.

### Integrate {{site.data.keyword.appid_short_notm}} with your own mail provider

With Cloud Directory, you can send email messages to your users to verify their email address, allow them to reset their password, and more. By default, you can use {{site.data.keyword.appid_short_notm}} to deliver the email messages, but there are some benefits if you choose to define a custom extension point to be invoked when an email needs to be sent. 

For example, [using your own mail provider](/docs/appid?topic=appid-cd-types) can help you reduce the chance of your emails being filtered as spam by removing the default appid.bluemix.net domain. Additionally, you can gain deeper insights directly from your email provider, such as the status of delivered and opened emails. The email insights can help you identify and solve issues since you can track individual messages and see overall statistics. For more information, see a [working example](/blogs/cloud-archive/2018/10/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users/) of the custom mail provider feature.  

