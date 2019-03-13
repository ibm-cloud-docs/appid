---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

keywords: authentication, authorization, identity, app security, secure, customizing apps, directory, registry, 

subcollection: appid

---

{:new_window: target="_blank"}
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

# Branding your app
{: #branded}

You can display your own customized screens, use your own sign in flows, and take advantage of the authentication and authorization capabilities of {{site.data.keyword.appid_full}}. By using Cloud Directory as your identity provider, your users are able to interact with your app with less help from you. They're able to sign in, sign up, change their password, and more without asking for help.
{: shortdesc}


## Understanding screen reuse
{: #branded-understand}

When you reuse your existing UIs, you can create a cohesive sign in flow for your app. By using the same imagery, colors, and branding, your users are more likely to recognize your brand, even when not directly interacting with your app.

### Are there any requirements to us my own screens?
{: #branded-requirements}


To display your own UIs, you must use [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) as your identity provider. There are several different ways that Cloud Directory can be [configured](/docs/services/appid?topic=appid-cloud-directory). You can decide the types of messages that you want to send, and customize the content and design. Don't know what to say? Not a problem. There are example messages in the GUI that you can use.


Want to use a [language](/docs/services/appid?topic=appid-cloud-directory#cd-languages) other than English? You can choose another language by using the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization" target="_blank">language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, to display your own translated content.
{: tip}


### Can I use some of my own and some of the default screens?
{: #branded-hybrid}

Yes! You can create a hybrid flow that uses some of your screens and some of the default screens. However, you can use only one option per flow. This means that you can use your own sign in screen and also use the default sign up screen. But, if you choose to use the default sign up screen, then you must continue to use the default through entire sign up flow, including sign up verification.

### How are the flows technically different?
{: #branded-technically}

The service uses OAuth 2.0 grant flows to map the authorization process. When you configure social identity providers such as Facebook, the <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html" target="_blank">Authorization Grant flow <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is used to call the Login Widget. When you use your own screens, the <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html" target="_blank">Resource Owner Password Credentials flow <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is used to provide access and identity tokens that allow you to call your sign in screens.



### Examples
{: #branded-examples}

Yes! Check out any of the following examples to see Cloud Directory in action:

* <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="_blank">Use your own branded UI for user sign-in with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/use-ui-flows-user-sign-sign-app-id/" target="_blank">Use your own UI and Flows for User Sign-Up and Sign-in with with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/custom-login-page-app-id-integration/" target="_blank">Use a custom login page with  {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>


## Branding your app with the Android SDK
{: #branded-ui-android}

With Cloud Directory enabled, you can call customized screens with the Android SDK. You can choose the combination of the screens that you'd like your users to be able to interact with.<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Check out this blog<img src="../../icons/launch-glyph.svg" alt="External link icon"></a> for a detailed example!
{: shortdesc}



### Sign in
{: #branded-android-sign-in}

1. Configure your Cloud Directory [settings](/docs/services/appid?topic=appid-cloud-directory#cd-settings) in the GUI.
2. Add the following code to your application. The sign in flow is triggered when a user clicks sign in on your custom screen. You get access, identity, and refresh tokens by supplying the end user's username and password.

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
  {: pre}

</br>
</br>

## Branding your app with the iOS Swift SDK
{: #branded-ui-ios-swift}

With Cloud Directory enabled, you can call your own branded screens with the [iOS Swift SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

</br>

### Sign in
{: #branded-ios-sign-in}

1. Configure your Cloud Directory [settings](/docs/services/appid?topic=appid-cloud-directory#cd-settings) in the GUI.
2. Place the following code in your application. When a user attempts to sign in, your sign in screen is called and the authorization and authentication process starts with your customized sign in page.

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

By using the WebAppStrategy users can sign in to your web apps with their username and a password. After a user successfully signs in to your app, their access token is persisted in an HTTP session as long as it is kept alive. After the HTTP session is closed or expired, the access token is also destroyed.


1. Configure your Cloud Directory [settings](/docs/services/appid?topic=appid-cloud-directory#cd-settings) in the GUI.
2. Place the following code in your application. When a user attempts to sign in, your customized sign in screen is called and the authorization and authentication process starts.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="More information icon"/> Command parameters </th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>The URL that you want to redirect the user to after a successful authentication.</td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>The URL that you want to redirect the user to if authentication fails.</td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td>When set to <code>true</code> an error message is returned from the Cloud Directory service. By default, the value is set to <code>false</code>.</td>
      </tr>
    </tbody>
  </table>

**Note**: If you submit the request in HTML, you can use <a href="https://www.npmjs.com/package/body-parser" target="blank">body parser <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> middleware. To see the returned error message you can use <a href="https://www.npmjs.com/package/connect-flash" target="blank">connect-flash <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. To see it in action, check out the <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js" target="blank">web app sample <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.


## Branding your app with the API
{: #branded-ui-api}

You can display your own customized screens and take advantage of the authentication and authorization capabilities of {{site.data.keyword.appid_short_notm}}. With Cloud Directory as your identity provider, your users are able to interact with your app with less help from you. They're able to sign in, sign up, reset their password, and more without asking for help.
{: shortdesc}

To make this possible, {{site.data.keyword.appid_short_notm}} exposes REST APIs. You can use the REST APIs to build a back-end server that serves your web apps, or to interact with a mobile app with your own custom screens.

The management API is secured with IBM Cloud Identity and Access Management generated tokens. This means that account owners can specify who on their team has which level of access for each service instance. For more information about how IAM and {{site.data.keyword.appid_short_notm}} work together, see [Service access management](/docs/services/appid?topic=appid-service-access-management).

After you've configured your [settings](/docs/services/appid?topic=appid-cloud-directory), you can call the following endpoints to display each screen.

### Sign up
{: #branded-api-signup}

You can use the `/sign_up` endpoint to allow users to sign themselves up for your app.
Supply the following data in the request body:
  * Your tenantID.
  * Cloud Directory user data. See [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) for more details.
    * A `password` attribute.
    * In the email array with a `primary` attribute that is set to `true`, you must have at least 1 email address.

Depending on your [email configuration](/docs/services/appid?topic=appid-cloud-directory), a user might receive a request for verification, an email that welcomes them when they sign up for you app, or both. Both types of emails are triggered when a user signs up for your app. The verification email contains a link that the user can click to confirm their identity; a screen is displayed, that thanks them for verifying or confirms that their verification is complete.  

To present your own post verification page:

1. Navigate to the Cloud Directory identity provider in the {site.data.keyword.appid_short_notm}} dashboard.
2. Click the **Email verification** tab.
3. In the **custom verification page URL** enter the URL for your landing page.

When this value is provided, {{site.data.keyword.appid_short_notm}} calls the URL along with a `context` query. When you call the `/sign_up/confirmation_result` endpoint and pass the received `context` parameter, the result tells you whether your user has verified their account. If they have, then you can display your custom page.


### Forgot password
{: #branded-api-forgot-password}

You can use the `/forgot_password` endpoint to allow users to recover their password should they forget it.

Supply the following data in the request body:
  * Your tenantID.
  * The email of the Cloud Directory user.

When the endpoint is called, a reset password email is sent to the user. The email contains a **Reset** button. After they press the button, a screen is displayed by {{site.data.keyword.appid_short_notm}} that allows them to reset their password.

You can present your own post reset password page:

1. Configure your Cloud Directory [settings](/docs/services/appid?topic=appid-cloud-directory#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
3. Enter the URL for your landing page in the **URL for your custom reset password page**  

When this value is provided, {{site.data.keyword.appid_short_notm}} calls the URL along with a `context` query. The `context` parameter is used to receive the result when `/forgot_password/confirmation_result` is called. If the result is successful, then you can display your custom page.

Add a random string to your custom reset password page and pass it to your back-end when the request is submitted. Have your handler validate the string and call the `/change_password` endpoint only if it is valid. By doing so you can reduce vulnerability of your back-end reset password endpoint.
{: tip}


### Change password
{: #branded-api-change-password}

You can use the `/change_password` endpoint  in two ways. When a user submits a reset request, or when a user is signed in to your app and wants to update their password.

Supply the following data in the request body to update their password after a reset request:
  * Your tenantID.
  * The users new password
  * The Cloud Directory user UUID.
  * Optional: the IP address from which the password reset was performed. If you choose to pass the IP address, then the placeholder `%{passwordChangeInfo.ipAddress}` is available for the change password email template.

Depending on your configuration, when a password is changed {{site.data.keyword.appid_short_notm}} might send an email to the user letting them know that there was a change.


To allow users to change their password while signed in to your app:

Supply the following data in the request body:
  * Your tenantID.
  * The users new password
  * The Cloud Directory user UUID.

Your change password page should prompt the user to enter their current password and their new password.
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

When the user details are updated, the endpoint gets the updated user data in the request body in [SCIM format](https://tools.ietf.org/html/rfc7643#section-8.2). Be sure that you change only the relevant details.

Their email address cannot be changed.
{: tip}
