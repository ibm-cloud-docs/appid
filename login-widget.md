---

copyright:
  years: 2017, 2018
lastupdated: "2018-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Managing the sign-in experience

{{site.data.keyword.appid_full}} provides a login widget that lets you give your users secure sign-in options.
{: shortdesc}

When your app is configured to use an identity provider, visitors to your app are directed to a sign in screen by the login widget. As a default, when only one provider is set to on, visitors are redirected to that identity providers authentication screen. With the login widget you can display a default sign in screen or, with cloud directory, you can reuse your existing UI's.

You can update your sign-in flow at any time, without changing your source code in any way!
{: tip}

The service uses OAuth 2 grant types to map the authorization process. When you configure social identity providers such as Facebook, the [Oauth2 Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) is used to call the log in widget. When you display your own UI screens, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) is used to log in and gain access and identity tokens.


## Customizing the default sign-in screen
{: #login-widget}

You can customize the preconfigured sign-in screen to display the logo and colors of your choice.
{: shortdesc}

To customize the screen:

1. Open the {{site.data.keyword.appid_short_notm}} service dashboard.
2. Select the **Login Customization** section. You can modify the appearance of the login widget to align with your company's brand.
3. Upload your company's logo by selecting a PNG or JPG file from your local system. The recommended image size is 320 x 320 pixels. The maximum file size is 100 Kb.
4. Select a header color for the widget from the color picker, or enter the hex code for another color.
5. Inspect the preview pane, and click **Save Changes** when you are happy with your customizations. A confirmation message is displayed.
6. In your browser, refresh your login page to verify your changes.


## Displaying the default screens
{: #default}

{{site.data.keyword.appid_short_notm}} provides a default login screen that you can call if you don't have your own UI screens to display.
{: shortdesc}

Depending on your identity provider configuration, the screens that you can display differ. The service doesn't provide advanced functionality for social identity providers because we never have access to a users account information. Users have to go to the identity provider to manage their information. For example, if they wanted to change their Facebook password, they would need to go to www.facebook.com.

Check out the following table to see which screens you can display for each type of identity provider.

<table>
  <thead>
    <tr>
      <th>Display screen</th>
      <th>Social identity provider</th>
      <th>Cloud directory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Sign in</td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Sign up</td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Forgot password</td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Change password</td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Account details</td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

After you've configured your settings for [social identity providers](/docs/services/appid/identity-providers.html), and [cloud directory](/docs/services/appid/cloud-directory.html), click on the language of your choice in the following image to start implementing the code.


Click on the language of your choice in the following image to start implementing the code.

<img usemap="#default-options-map" border="0" class="image" id="options" src="images/default-options.png" width="750" alt="Click an SDK language icon to get started with cloud directory in your apps." style="width:750px;" />
<map name="default-options-map" id="default-options-map">
<area href="login-widget.html#android" alt="Managing the sign in experience with the Android SDK" shape="rect" coords="113, 8, 224, 123" />
<area href="login-widget.html#ios-swift" alt="Managing the sign in experience with the iOS Swift SDK." shape="rect" coords="251, 12, 362, 127" />
<area href="login-widget.html#nodejs" alt="Managing the sign in experience with the Node.js SDK." shape="rect" coords="387, 10, 498, 125" />
<area href="login-widget.html#swift" alt="Managing the sign in experience with the Swift SDK." shape="rect" coords="525, 10, 636, 125" />
</map>
</br>

### Displaying the default screens with the Android SDK
{: #android}

You can call the preconfigured screens with the Android SDK.
{: shortdesc}

</br>

**Sign in**
1. Place the following command in your code.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
            //Exception occurred
          }

          @Override
          public void onAuthorizationCanceled () {
            //Authentication canceled by the user
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
            //User authenticated
          }
        });
    ```
  {: pre}

</br>
**Sign up**

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the sign-up flow.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
  		 @Override
  		 public void onAuthorizationFailure (AuthorizationException exception) {
  		 }

  		 @Override
  		 public void onAuthorizationCanceled () {
  		 }

  		 @Override
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: pre}

</br>
**Forgot password**

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the forgot password flow.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
   			 public void onAuthorizationCanceled () {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
    ```
    {: pre}

</br>
**Account details**

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the change details flow.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  			 }

  			 @Override
  			 public void onAuthorizationCanceled () {
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 }
  		 });
   ```
   {: pre}

</br>
**Change password**

1. Set **Allow users to sign up and reset their password** to **ON**, in the settings for cloud directory.
2. Call the LoginWidget to start the change password flow.
   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
   			 public void onAuthorizationCanceled () {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
   ```
   {: pre}
</br>
</br>

### Displaying the default screens with the iOS Swift SDK
{: #ios-swift}

You can call the preconfigured screens with the iOS Swift SDK.
{: shortdesc}

</br>
**Sign in**

1. Place the following command in your code.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}


</br>
**Sign up**

1. Set **Allow users to sign up and reset their password** to **On**, in the settings for cloud directory.
2. Call the LoginWidget to start the sign-up flow.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
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
  {: pre}

</br>
**Forgot password**

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the forgot password flow.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
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
  {: pre}

</br>
**Account details**

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the change details flow.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
       }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>
**Change password**

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the change password flow.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
       }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}
</br>
</br>

### Displaying the default screens with the Node.js SDK
{: #nodejs}

You can call the preconfigured screens with the Node.js SDK.
{: shortdesc}

</br>
**Sign in**
1. Set cloud directory to **On** in your identity provider settings and specify a callback endpoint.
2. Add a post route to your app that can be called with the username and password parameters and log in by using the resource owner password.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // allow flash messages
    }));
    ```
    {: pre}
    `WebAppStrategy` allows users to sign in to your web apps with a username and password. After a successful login, a user's access token is stored in the HTTP session and is available during the session. Once the HTTP session is destroyed or expired, the token is invalid.
    {: tip}

</br>
**Sign up**

1. Set **Allow users to sign up and reset their password** to **On** in the cloud directory settings. If set to no, the process ends without retrieving access and identity tokens.
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**Forgot password**

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **ON** in the cloud directory settings. If set to no, the process ends without retrieving access and identity tokens.
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>
**Account details**
1. Set **Allow users to sign up and reset their password** to **On** in the cloud directory settings
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>
**Change password**
1. Set **Allow users to sign up and reset their password** to **On** in the cloud directory settings.
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: pre}

</br>
</br>
### Displaying the default UI with the Swift SDK
{: #swift}

With social identity providers enabled, you can call the preconfigured sign-in screen with the Swift SDK.
{: shortdesc}

1. The following code demonstrates how to use WebAppKituraCredentialsPlugin in a Kitura app to protect the `/protected` endpoint.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // The following URLs will be used for AppID OAuth flows
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Setup Kitura to use session middleware
  // Must be configured with proper session storage for production
  // environments. See https://github.com/IBM-Swift/Kitura-Session for
  // additional documentation
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)

  let options = [
  	"clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)

  // Explicit login endpoint
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback to finish the authorization process. Will retrieve access and identity tokens from AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Logout endpoint. Clears authentication information from session
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Protected area
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
      let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]

      guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
          response.status(.unauthorized)
          return next()
      }

      response.send(json: identityTokenPayload!)
      next()
  })
  var port = 3000
  if let portString = ProcessInfo.processInfo.environment["PORT"]{
      port = Int(portString)!
  }
  print("Starting on \(port)")

  // Add an HTTP server and connect it to the router
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start the Kitura runloop (this call never returns)
  Kitura.run()
  ```
  {: codeblock}
</br>
</br>


### Displaying customized screens with the Android SDK
{: #branded-ui-android}

With cloud directory enabled, you can call customized screens with the Android SDK. You can choose the combination of the screens that you'd like your users to be able to interact with.<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Check out this blog<img src="../../icons/launch-glyph.svg" alt="External link icon"></a> for a detailed example!
{: shortdesc}

</br>
**Sign in**

1. Set **Cloud Directory** to **On** as an identity provider.
2. Place the following command in your code.
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
             //Exception occurred
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //User authenticated
          }
         });
  ```
  {: pre}

</br>
</br>

### Displaying customized screens with the iOS Swift SDK
{: #branded-ui-ios-swift}

With cloud directory enabled, you can call customized screens with the iOS Swift SDK.
{: shortdesc}

</br>
**Sign in**

1. In the identity provider tab on the GUI, set cloud directory to **On**.
2. Log in by using the resource owner password. Access and identity tokens are obtained when a user attempts to log in by using their username and password.
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
  {: pre}
</br>
</br>

### Displaying customized screens with the Node.js SDK
{: #branded-ui-nodejs}

With cloud directory enabled, you can call customized screens with the Node.js SDK. You can choose the combination of the screens that you'd like your users to be able to interact with. If you choose a Node.js backend you can use our self-Service module that in the App ID Node.js SDK (link).
{: shortdesc}

**Sign in**
1. Set cloud directory to **On** in your identity provider settings and specify a callback endpoint.
2. Add a post route to your app that can be called with the username and password parameters and log in by using the resource owner password.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // allow flash messages
    }));
    ```
    {: pre}
    `WebAppStrategy` allows users to sign in to your web apps with a username and password. After a successful login, a user's access token is stored in the HTTP session and is available during the session. Once the HTTP session is destroyed or expired, the token is invalid.
    {: tip}

</br>
</br>

## Displaying customized screens with the API
{: #branding}

You can display your own customized screens and take advantage of the authentication and authorization capabilities of {{site.data.keyword.appid_short_notm}}. With cloud directory as your identity provider, your users are able to interact with your app with less help from you. They're able to sign in, sign up, reset their password, and more without asking for help.
{: shortdesc}

To make this possible, {{site.data.keyword.appid_short_notm}} exposed REST APIs. You can use the REST API to build a back-end server that serves your web apps, or to interact with a mobile app with your own custom screens.

The management API is secured with IBM Cloud Identity and Access Management generated tokens. This means that account owners can specify who on their team has which level of access for each service instance. For more information about how IAM and {{site.data.keyword.appid_short_notm}} work together, see [Service access management](/docs/services/appid/iam.html).

When a user clicks sign-in from your customized screen, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) is used to gain access and identity tokens directly from your web or mobile apps.

After you've configured your [settings](/docs/services/appid/cloud-directory.html),


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

1. Navigate to the **Custom Landing Pages** tab of the {{site.data.keyword.appid_short_notm}} dashboard.
2. Input the URL for your landing page in the **URL for your custom reset password page**  

When this value is provided, {{site.data.keyword.appid_short_notm}} calls the URL along with a `context` query. The `context` parameter is used to receive the result when `/forgot_password/confirmation_result` is called. If the result is successful, then you can display your custom page.

Add a random string to your custom reset password page and pass it to your back-end when the request is submitted. Have your handler validate the string and call the `/change_password` endpoint only if it is valid. By doing so you can reduce vulnerability of your back-end reset password endpoint.
{: tip}

</br>
**Change password**

You can use the `/change_password` endpoint  in two ways. When a user submits a reset request, or when a user is signed in to your app and wants to update their password.

To update their password after a reset request:

Supply the following data in the request body:
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

You can use the `/resend/{templateName}` to resent an email when a user does not receive it for some reason.

Supply the following data in the request body:
    * The tenantID.
    * The template name
    * The cloud directory user UUID.


**Change details**

When a user is signed in to your app, they can update some of their information. You can use the `/Users/{userId}` to get and update their information.

When the user details are updated, the endpoint gets the updated user data in the request body in [SCIM format](https://tools.ietf.org/html/rfc7643#section-8.2). Be sure that you change only the relevant details.

Their email address cannot be changed.
{: tip}
