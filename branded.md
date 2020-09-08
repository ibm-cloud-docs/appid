---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-04"

keywords: bring your own screens, branded app, sign up, custom, directory, registry, app security, password, authorization flow, authentication,

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


# Branding your app
{: #branded}

With {{site.data.keyword.appid_full}}, you can customize the entire sign-up experience of your application by using your own branded screens. You can replace the provided sign in widget with your own, add extra fields, validate password strength and verify email addresses against a blocklist!
{: shortdesc}


## Understanding screen reuse
{: #branded-understand}

When you reuse your existing UIs, you can create a cohesive sign-in flow for your app. By using the same imagery, colors, and branding, your users are more likely to recognize your brand, even when not directly interacting with your app.


Want to use a [language](/docs/appid?topic=appid-cd-types#cd-languages) other than English? You can choose another language by using the [language management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization){: external}, to display your own translated content.
{: tip}


## What information do I need to obtain with my sign in or sign up screen?
{: #branded-form-submit}

When you make the request to submit your sign-in form, it must contain both username and password parameters in your request body. This means that your sign in or sign up page must ask that information from your users.


### Can I use some of my own and some of the default screens?
{: #branded-hybrid}

Yes! You can create a hybrid flow that uses some of your screens and some of the default screens. However, you can use only one option per flow. As an example, you can use your own sign-in screen and also use the default sign-up screen. But, if you choose to use the default sign-up screen, then you must continue to use the default through entire sign-up flow, including sign-up verification.

### How are the flows technically different?
{: #branded-technically}

The service uses OAuth 2.0 grant flows to map the authorization process. When you configure social identity providers such as Facebook, the [Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html){: external} is used to call the Login Widget. When you use your own screens, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html){: external} is used to provide access and identity tokens that you can use to call your screens.



### Examples
{: #branded-examples}

Yes! Check out any of the following examples to see Cloud Directory in action:

* [Use your own branded UI for user sign-in with {{site.data.keyword.appid_short_notm}}](https://www.ibm.com/cloud/blog/use-branded-ui-user-sign-app-id){: external}
* [Use your own UI and Flows for User Sign-Up and Sign-in with {{site.data.keyword.appid_short_notm}}](https://www.ibm.com/cloud/blog/use-ui-flows-user-sign-sign-app-id){: external}
* [Use a custom login page with {{site.data.keyword.appid_short_notm}}](https://www.ibm.com/cloud/blog/custom-login-page-app-id-integration){: external}


## Branding your app with the Android SDK
{: #branded-ui-android}

With Cloud Directory enabled, you can call customized screens with the Android SDK. You can choose the combination of the screens that you'd like your users to be able to interact with. For a detailed example, [check out this blog](https://www.ibm.com/cloud/blog/use-branded-ui-user-sign-app-id){: external}.
{: shortdesc}



### Sign in
{: #branded-android-sign-in}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI.
2. Add the following code to your application. The sign-in flow is triggered when a user clicks sign in on your custom screen. You get access, identity, and refresh tokens by supplying the user's user name and password.

  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password, new TokenResponseListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //User authenticated
      }
  });
  ```
  {: codeblock}



## Branding your app with the iOS Swift SDK
{: #branded-ui-ios-swift}

With Cloud Directory enabled, you can call your own branded screens with the [iOS Swift SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift){: external}.
{: shortdesc}



### Sign in
{: #branded-ios-sign-in}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI.
2. Place the following code in your application. When a user attempts to sign in, your customized screen is called and the authorization and authentication process starts with your customized sign-in page.

  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}


## Branding your app with the Node.js SDK
{: #branding-ui-nodejs}

With Cloud Directory enabled, you can call customized screens with the Node.js SDK.
{: shortdesc}

### Sign in
{: #branded-node-sign-in}

By using `WebAppStrategy`, users can sign in to your web apps with their user name and a password. After a user successfully signs in to your app, their access token is persisted in an HTTP session as long as it is kept alive. After the HTTP session is closed or expired, the access token is also destroyed.


1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI.
2. Place the following code in your application. When a user attempts to sign in, your customized screen is called and the authorization and authentication process starts.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    <tr>
    <tr>
      <td><code>successRedirect</code></td>
      <td>The URL that you want to redirect the user after a successful authentication.</td>
    </tr>
    <tr>
      <td><code>failureRedirect</code></td>
      <td>The URL that you want to redirect the user to if authentication fails.</td>
    </tr>
    <tr>
      <td><code>failureFlash</code></td>
      <td>When set to <code>true</code> an error message is returned from the Cloud Directory service. By default, the value is set to <code>false</code>.</td>
    </tr>
  </table>

**Note**: If you submit the request in HTML, you can use [body parser](https://www.npmjs.com/package/body-parser){: external} middleware. To see the returned error message, you can use [connect-flash](https://www.npmjs.com/package/connect-flash){: external}. To see it in action, check out the [web app sample](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js){: external}.



## Branding your app with the API
{: #branded-ui-api}

You can display your own customized screens and take advantage of the authentication and authorization capabilities of {{site.data.keyword.appid_short_notm}}. With Cloud Directory as your identity provider, your users are able to interact with your app with less help from you. They're able to sign in, sign up, reset their password, and more without asking for help.
{: shortdesc}

To make this possible, {{site.data.keyword.appid_short_notm}} exposes REST APIs. You can use the REST APIs to build a back-end server that serves your web apps, or to interact with a mobile app with your own custom screens.

The management API is secured with IBM Cloud Identity and Access Management generated tokens, which means that account owners can specify who on their team has which level of access for each service instance. For more information about how IAM and {{site.data.keyword.appid_short_notm}} work together, see [Service access management](/docs/appid?topic=appid-service-access-management).

After you configure your [settings](/docs/appid?topic=appid-cloud-directory#cd-settings), you can call the following endpoints to display each screen.

### Sign up
{: #branded-api-signup}

You can use the `/sign_up` endpoint to allow users to sign themselves up for your app.
Supply the following data in the request body:
  * Your tenantID.
  * Cloud Directory user data with the following required attributes. See [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2){: external} for more details.
    * A `password` attribute.
    * An `emails` array with at least one email address and a `primary` attribute that is set to `true`.

Depending on your [email configuration](/docs/appid?topic=appid-cd-types), a user might receive a request for verification, an email that welcomes them when they sign up for your app, or both. Both types of emails are triggered when a user signs up for your app. The verification email contains a link that the user can click to confirm their identity; a screen is displayed, that thanks them for verifying or confirms that their verification is complete.  

To present your own post verification page:

1. Navigate to the Cloud Directory identity provider in the {{site.data.keyword.appid_short_notm}} dashboard.
2. Click the **Email verification** tab.
3. In the **custom verification page URL**, enter the URL for your landing page.

When this value is provided, {{site.data.keyword.appid_short_notm}} calls the URL along with a `context` query. When you call the `/sign_up/confirmation_result` endpoint and pass the received `context` parameter, the result tells you whether your user verified their account. If they have, then you can display your custom page.


### Forgot password
{: #branded-api-forgot-password}

You can use the `/forgot_password` endpoint to allow users to recover their password if they forget it.

Supply the following data in the request body:
  * Your tenant ID.
  * The email of the Cloud Directory user.

When the endpoint is called, a reset password email is sent to the user. The email contains a **Reset** button. After they press the button, a screen is displayed by {{site.data.keyword.appid_short_notm}} where they can reset their password.

You can present your own post reset password page:

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
3. Enter the URL for your landing page in the **URL for your custom reset password page**  

When this value is provided, {{site.data.keyword.appid_short_notm}} calls the URL along with a `context` query. The `context` parameter is used to receive the result when `/forgot_password/confirmation_result` is called. If the result is successful, then you can display your custom page.

Add a random string to your custom reset password page and pass it to your back-end when the request is submitted. Have your handler validate the string and call the `/change_password` endpoint only if it is valid. By doing so, you can reduce vulnerability of your back-end reset password endpoint.
{: tip}


### Change password
{: #branded-api-change-password}

You can use the `/change_password` endpoint in two ways: when a user submits a reset request, or when a user is signed in to your app and wants to update their password.

Before you call the `/change_password` API to allow a user to reset their password, it is highly recommended to check whether the `context` has a successful result by using the `/forgot_password/confirmation_result` endpoint. This operation adds a higher level of security to your back-end reset password process and ensures that a user can modify their password only if the `context` is still valid.
{: note}

To update a user's password after a reset request, supply the following data in the request body:
  * Your tenantID.
  * The user's new password.
  * The Cloud Directory user UUID.
  * Optional: The IP address from which the password reset was performed. If you choose to pass the IP address, then the placeholder `%{passwordChangeInfo.ipAddress}` is available for the change password email template.

Depending on your configuration, when a password is changed {{site.data.keyword.appid_short_notm}} sends an email to the user that lets them know that a change was made.

To allow users to change their password while they are signed in to your app, supply the following data in the request body:

  * Your tenantID.
  * The user's new password.
  * The Cloud Directory user UUID.

Your change password page must prompt the user to enter their current password and their new password.
{: tip}

Your back-end validates the user's current password with the ROP API, and if valid, calls the endpoint with the new password. Depending on your configuration, when a password is changed {{site.data.keyword.appid_short_notm}} might send an email to the user letting them know that there was a change.


### Resend
{: #branded-api-resend}

You can use the `/resend/{templateName}` to resend an email when a user does not receive it for some reason.

Supply the following data in the request body:
  * The tenantID.
  * The template name
  * The Cloud Directory user UUID.

### Change details
{: #branded-api-change-details}

When a user is signed in to your app, they can update some of their information. You can use the `/Users/{userId}` to get and update their information.

When the user details are updated, the endpoint gets the updated user data in the request body in [SCIM format](https://tools.ietf.org/html/rfc7643#section-8.2){: external}. Be sure that you change only the relevant details.

Their email address cannot be changed.
{: tip}
