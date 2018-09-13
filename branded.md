---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-13"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Branding your app
{: #branding}

You can display your own customized screens and take advantage of the authentication and authorization capabilities of {{site.data.keyword.appid_full}}. With Cloud Directory as your identity provider, your users are able to interact with your app with less help from you. They're able to sign in, sign up, change their password, and more without asking for help.
{: shortdesc}

When you use your own screens, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) is used to provide access and identity tokens.

Customize the content and design the appearance of your message. There is an example message in the GUI that you can use, but you can update the text with your own message. You can even use a [language](cloud-directory.html#languages) other than English, but you are responsible for the translation of the text. To choose another language, use the <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="blank">language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
{: tip}


## Branding your app with the iOS Swift SDK
{: #branded-ui-ios-swift}

With Cloud Directory enabled, you can call your own branded screens with the [iOS Swift SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

</br>
**Sign in**

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI.
2. Place the following code in your application. When a user attempts to sign in, the login widget is called and the authorization and authentication process starts with your customized sign in page.
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

</br>

**Sign up**

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign-up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Place the following code in your application. When a user attempts to sign up for your application, the login widget is called and displays your custom sign up page.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
       if accessToken == nil && identityToken == nil {
        //email verification is required
        return
       }
     //User authenticated
    }

    public func onAuthorizationCanceled() {
        //Sign up canceled by the user
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Exception occurred
    }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: codeblock}

</br>

**Forgot password**

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
3. Place the following code in your application. When a user requests that their password to your app be updated, the login widget is called and the  process starts.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
        //forgot password finished, in this case accessToken and identityToken will be null.
     }

     public func onAuthorizationCanceled() {
         //forgot password canceled by the user
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //Exception occurred
     }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: codeblock}

</br>

**Change details**

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign-up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. In the **Password changed** tab of the service dashboard, set **Password changed email** to
3. Call the login widget to start the change details flow.
  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //changed details canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>

**Change password**

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign-up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Call the login widget to start the change password flow.
  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //change password canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
           //Exception occurred
      }
   }

   AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}

</br>


## Branding your app with the Android SDK
{: #branded-ui-android}

With cloud directory enabled, you can call customized screens with the Android SDK. You can choose the combination of the screens that you'd like your users to be able to interact with.<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Check out this blog<img src="../../icons/launch-glyph.svg" alt="External link icon"></a> for a detailed example!
{: shortdesc}

</br>

**Sign in**

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI.
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

**Sign up**

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign-up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Add the following code to your app. When a user signs up for your app from your custom screen, the sign up flow is started. The following call not only registers the user, but also sends a verification email to complete the registration depending on your Cloud Directory configurations.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
      public void onAuthorizationCanceled () {
          //Sign up canceled by the user
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              //User authenticated
          } else {
              //email verification is required
          }
      }
  });
  ```
  {: pre}

</br>

**Forgot password**

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
3. Add the following code to your app. When a user clicks "forgot password" in your application, the SDK calls the forgot_password API to send an email to the user that allows them to reset their password.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
   	public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
      public void onAuthorizationCanceled () {
          // Forogt password canceled by the user
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Forgot password finished, in this case accessToken and identityToken will be null.
      }
  });
  ```
  {: pre}

</br>

**Change details**

1. Set **Cloud Directory** to **On** as an identity provider.
2. Set **Allow users to sign up and reset their password** to **ON** in the Cloud Directory settings.
3. Call the login widget to start the change details flow.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Exception occurred
      }

      @Override
      public void onAuthorizationCanceled () {
          // Changed details canceled by the user
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // User authenticated, and fresh tokens received
      }
  });
  ```
  {: pre}


</br>

**Change password**

1. Set **Cloud Directory** to **On** as an identity provider.
2. Set **Allow users to sign up and reset their password** to **ON** in the Cloud Directory settings.
3. Call the login widget to start the change password flow.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Exception occurred
      }

      @Override
      public void onAuthorizationCanceled () {
          // Change password canceled by the user
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // User authenticated, and fresh tokens received
      }
  });
  ```
  {: pre}

</br>
</br>


## Branding your app with the Node.js SDK
{: #branded-ui-nodejs}

With Cloud Directory enabled, you can call customized screens with the Node.js SDK.
{: shortdesc}

**Sign in**

By using the WebAppStrategy users can sign in to your web apps with their username and a password. After a user successfully signs in to your app, their access token is persisted in an HTTP session as long as it is kept alive. After the HTTP session is closed or expired, the access token is also destroyed.

1. Set Cloud Directory to **On** in your identity provider settings and specify a callback endpoint.
2. Add a post route to your app that can be called with the username and password parameters and sign in with the resource owner password flow.
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

  1. If you submit the request in HTML form, you can use [body parser](https://www.npmjs.com/package/body-parser) middle ware.
  2. To get the returned error message you can use [connect-flash](https://www.npmjs.com/package/connect-flash). For more information, see the [web app sample](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js).
  {: tip}

</br>
**Sign up**

1. Set Cloud Directory to **On** in your identity provider settings and specify a callback endpoint.
2. Set **Allow users to sign up and reset their password** to **ON** in the Cloud Directory settings.
3. Set **Allow users to sign-in without email verification** to **No**. If you don't, the {{site.data.keyword.appid_short_notm}} access and identity tokens cannot be retrieved.
4. Add a post route to your app that can be called with the username and password parameters and sign in with the resource owner password flow.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**Forgot password**

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
4. Pass the *show* property to `WebAppStrategy.FORGOT_PASSWORD` to launch the forgot password form.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**Change details**

1. Set Cloud Directory to **On** in your identity provider settings and specify a callback endpoint.
2. Set **Allow users to sign up and reset their password** to **ON** in the Cloud Directory settings.
3. Verify that the user has previously authenticated with {{site.data.keyword.appid_short_notm}}.
4. Pass the *show* property to `WebAppStrategy.CHANGE_DETAILS` to launch the forgot password form.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## Branding your app with the API
{: #branded-ui-api}

You can display your own customized screens and take advantage of the authentication and authorization capabilities of {{site.data.keyword.appid_short_notm}}. With cloud directory as your identity provider, your users are able to interact with your app with less help from you. They're able to sign in, sign up, reset their password, and more without asking for help.
{: shortdesc}

To make this possible, {{site.data.keyword.appid_short_notm}} exposes REST APIs. You can use the REST APIs to build a back-end server that serves your web apps, or to interact with a mobile app with your own custom screens.

The management API is secured with IBM Cloud Identity and Access Management generated tokens. This means that account owners can specify who on their team has which level of access for each service instance. For more information about how IAM and {{site.data.keyword.appid_short_notm}} work together, see [Service access management](/docs/services/appid/iam.html).

After you've configured your [settings](/docs/services/appid/cloud-directory.html), you can call the following endpoints to display each screen.


**Sign up**
You can use the `/sign_up` endpoint to allow users to sign themselves up for your app.
Supply the following data in the request body:
  * Your tenantID.
  * Cloud directory user data. See [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) for more details.
    * A `password` attribute.
    * In the email array with a `primary` attribute that is set to `true`, you must have at least 1 email address.

Depending on your [email configurations](/docs/services/appid/cloud-directory.html), a user might receive a request for verification, or an email that welcomes them when they sign up for you app. Both types of emails are triggered when a user signs up for your app. The verification email contains a **Verify** button. After they press the button and confirm their identity, a screen is displayed by {{site.data.keyword.appid_short_notm}} that thanks them for verifying.  

You can present your own post verification page:

1. Navigate to the **Custom Landing Pages** tab of the {{site.data.keyword.appid_short_notm}} dashboard.
2. Input the URL for your landing page in the **URL for your custom email address verification page**

When this value is provided, {{site.data.keyword.appid_short_notm}} calls the URL along with a `context` query. When you call the `/sign_up/confirmation_result` endpoint and pass the received `context` parameter, the result tells you whether your user has verified their account. If they have, then you can display your custom page.

</br>
**Forgot password**

You can use the `/forgot_password` endpoint to allow users to recover their password should they forget it.

Supply the following data in the request body:
  * Your tenantID.
  * The email of the cloud directory user.

When the endpoint is called, a reset password email is sent to the user. The email contains a **Reset** button. After they press the button, a screen is displayed by {{site.data.keyword.appid_short_notm}} that allows them to reset their password.

You can present your own post reset password page:

1. Configure your Cloud Directory [settings](cloud-directory.html#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
3. Input the URL for your landing page in the **URL for your custom reset password page**  

When this value is provided, {{site.data.keyword.appid_short_notm}} calls the URL along with a `context` query. The `context` parameter is used to receive the result when `/forgot_password/confirmation_result` is called. If the result is successful, then you can display your custom page.

Add a random string to your custom reset password page and pass it to your back-end when the request is submitted. Have your handler validate the string and call the `/change_password` endpoint only if it is valid. By doing so you can reduce vulnerability of your back-end reset password endpoint.
{: tip}

</br>
**Change password**

You can use the `/change_password` endpoint  in two ways. When a user submits a reset request, or when a user is signed in to your app and wants to update their password.

Supply the following data in the request body to update their password after a reset request:
  * Your tenantID.
  * The users new password
  * The cloud directory user UUID.
  * Optional: the IP address from which the password reset was performed. If you choose to pass the IP address, then the placeholder `%{passwordChangeInfo.ipAddress}` is available for the change password email template.

Depending on your configuration, when a password is changed {{site.data.keyword.appid_short_notm}} might send an email to the user letting them know that there was a change.

</br>
To allow users to change their password while signed in to your app:

Supply the following data in the request body:
  * Your tenantID.
  * The users new password
  * The cloud directory user UUID.

Your change password page should prompt the user to enter their current password and their new password.
{: tip}

Your back-end validates the user's current password with the ROP API, and if valid, calls the endpoint with the new password. Depending on your configuration, when a password is changed {{site.data.keyword.appid_short_notm}} might send an email to the user letting them know that there was a change.

</br>
**Resend**

You can use the `/resend/{templateName}` to resend an email when a user does not receive it for some reason.

Supply the following data in the request body:
  * The tenantID.
  * The template name
  * The cloud directory user UUID.


**Change details**

When a user is signed in to your app, they can update some of their information. You can use the `/Users/{userId}` to get and update their information.

When the user details are updated, the endpoint gets the updated user data in the request body in [SCIM format](https://tools.ietf.org/html/rfc7643#section-8.2). Be sure that you change only the relevant details.

Their email address cannot be changed.
{: tip}
