---

copyright:
  years: 2017, 2023
lastupdated: "2023-03-06"

keywords: app log in, login widget, sign in, default screen, forgot password, mfa, multi-factor authentication, sign up, reset password, facebook, google, identity provider, social log in, saml, authentication, authorization, cloud directory

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


# Using the Login Widget
{: #login-widget}

With {{site.data.keyword.appid_full}} you can use a default UI, called a Login Widget, to allow application users the ability to choose the identity provider that they want to sign in with. If you're using Cloud Directory, the Login Widget also provides additional UI's for extra functionalities such as sign-up, forgot password, multi-factor authentication, and more.
{: shortdesc}


## Understanding the Login Widget
{: #widget-understanding}

One of the best parts of the Login Widget is that you can start using {{site.data.keyword.appid_short_notm}} before you implement any of your own authentication UIs - which makes the developer onboarding experience that much easier.

### What is the default Login Widget behavior?
{: #widget-default}

By default, the Login Widget is enabled to use Facebook, Google, and Cloud Directory. You can change the behavior at any time by choosing which identity providers that you want to configure as an option. When more than one identity provider is enabled, the Login Widget presents a screen where the user can make their identity provider selection. But, if you have a single provider that is enabled, users do not see the previously mentioned selection screen. They are taken directly to the identity provider to begin the sign-in process.

For example, if you're using the default - Facebook, Google, and Cloud Directory - users see the screen. If you enable Facebook only, user's are taken directly to Facebook for authentication.



### Which screens can be displayed for each provider?
{: #widget-options}

When you use Cloud Directory, {{site.data.keyword.appid_short_notm}} is able to provide you with the extended functionality of user management. The extended functionality also applies to the Login Widget's capabilities. User's that are stored in Cloud Directory can take advantage of the functionality such as signing up or resetting their password directly in the Login Widget. Check out the following table to see which screens you can display for each type of identity provider.

| Login Widget screen | Social identity provider | Enterprise identity provider | Cloud Directory |
|-----|----| -----| ------ |
| Sign in | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Sign up | | | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Forgot password | | | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Change password | | | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Account details | | | ![Checkmark icon](../../icons/checkmark-icon.svg) |
{: caption="Table 1. The Login Widget screens that each identity provider can display" caption-side="top"}


### Customizing an SSO login flow
{: #widget-custom-sso}

After a successful authentication, App ID creates a session cookie with encrypted access and identity tokens that your apps can use for authentication. Another way to customize the flow is to send an access token to your browser so that any browser app can use the token in its Ajax request.


## Customizing the Login Widget
{: #widget-customize}

The Login Widget is dynamic. You can customize the look and feel or identity provider configuration, and the changes are applied immediately. You do not need to update your application code or redeploy your app in any way!
{: shortdesc}

Do you need more customization than the Login Widget provides? You can implement your own, fully customized UI for user sign in, sign up, reset password, and other flows to create an experience that's unique to your app. To get started, check out [branding your app](/docs/appid?topic=appid-branded).
{: tip}

To customize the screen:

1. Open the {{site.data.keyword.appid_short_notm}} service dashboard.
2. Select the **Login Customization** section. You can modify the appearance of the Login Widget to align with your company's brand.
3. Upload your company's logo by selecting a PNG or JPG file from your local system. The recommended image size is 320 x 320 pixels. The maximum file size is 100 Kb.
4. Select a header color for the widget from the color picker, or enter the hex code for another color.
5. Inspect the preview pane, and click **Save Changes** when you are happy with your customizations. A confirmation message is displayed.
6. In your browser, refresh your login page to verify your changes.


</br>


