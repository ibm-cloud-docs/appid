---

copyright:
  years: 2017, 2018
lastupdated: "2018-03-09"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Managing the sign-in experience

With {{site.data.keyword.appid_full}}, you can display default sign in screens. With cloud directory, you can also display sign-up, reset or forgot password, and account details screens. By using the login widget, you can update your sign-in flow at any time without adding, removing, or changing the source code.
{: shortdesc}

When your app is configured to use an identity provider, visitors to your app are directed to a sign in screen. As a default, when only one provider is set to on, visitors are redirected to the that identity providers authentication screen. You can use social identity providers or you can manage your own user registry with cloud directory.

The service uses OAuth 2 grant types to map the authorization process. When you configure social identity providers such as Facebook, the [Oauth2 Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) is used to call the log in widget. When you display your own UI screens, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) is used to log in and gain access and identity tokens.


## Customizing the default sign-in screen
{: #login-widget}

You can customize the preconfigured sign-in screen to display the logo and colors of your choice.
{: shortdesc}

![Customized sign in experience example](/images/customize.gif)

To customize the screen:

1. Open the {{site.data.keyword.appid_short_notm}} service dashboard.
2. Select the **Login Customization** section. You can modify the appearance of the login widget to align with your company's brand.
3. Upload your company's logo by selecting a PNG or JPG file from your local system. The recommended image size is 320 x 320 pixels. The maximum file size is 100 Kb.
4. Select a header color for the widget from the color picker, or enter the hex code for another color.
5. Inspect the preview pane, and click **Save Changes** when you are happy with your customizations. A confirmation message is displayed.
6. In your browser, refresh your login page to verify your changes.

You can make changes at any time without rebuilding your app. Your image is stored in the {{site.data.keyword.appid_short}} database and is displayed the next time the login widget is called.
{: tip}


## Displaying the default screens
{: #default}

{{site.data.keyword.appid_short_notm}} provides a default login screen that you can call if you don't have your own UI screens to display.
{: shortdesc}

Depending on your identity provider configuration, the screens that you can display differ. Check out the following table to see which screens you can display for each type of identity provider.

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
      <td><img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Sign up</td>
      <td> </td>
      <td><img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Forgot password</td>
      <td> </td>
      <td><img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Change password</td>
      <td> </td>
      <td><img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Account details</td>
      <td> </td>
      <td><img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /></td>
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

Want to use screens that you've already coded? Check out the docs for [branding your UI](/docs/services/appid/branded.html).
{: tip}

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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
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
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
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
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
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
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?, response:Response?) {
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
  {: pre}

</br>
**Forgot password**

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the forgot password flow.
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
  {: pre}

</br>
**Account details**

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the change details flow.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

1. Add the following command to your code.
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


## Branding the sign-in experience
{: #branding}

You can display your own customized screens and take advantage of the authentication and authorization capabilities of {{site.data.keyword.appid_full}}. With cloud directory as your identity provider, your users are able to interact with your app with less help from you. They're able to sign in, sign up, reset their password, and more without asking for help.
{: shortdesc}

In order for it to be possible {{site.data.keyword.appid_full}} exposed REST APIs (link to the mgmt swagger cloud directory operations section).

You can use this REST APIs to build a backend server that will serve your web applications, or to interact with a mobile application with your own custom screens.
If you choose a Node.js backend you can use our self-Service module that in the App ID Node.js SDK (link).
Otherwise you can always call directly to the REST APIs.

All the REST APIs protected with IAM token, click here for more information on IAM(link to IAM doc).
Once you gain an IAM token you can trigger the REST APIs in


**Customized Sign in**

When a user clicks on sign-in in your customized sign-in screen, you can use the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)
to gain access and identity tokens directly from your web or mobile application.

link to ROP web
link to ROP android
link to ROP iOS

**Customized Sign up**

Use the "/sign_up" endpoint in order to sign-up a new user.
supply your tenantId and the cloud directory user data in the request body.
The cloud directory user data must include at least one email address (in the emails array with primary true property),  
and 'password' attribute.
Full user data that supported can be found here: https://tools.ietf.org/html/rfc7643#section-8.2
The "/sign_up" endpoint returns the created new user.

If your "Email verification" is turned ON in your App ID instance email setting,
after your user has sign_up App ID will send a verification email to the new sign up user.
The email will contain a verification button, when the new user click it he will be mark as verified, (when then user will sign-in the retrieved id token will have verified property that set to true).

After the user marked as verified he will be presented with the a "thank you for verifying" screen of App ID.
(App ID will also send a welcome email to the new sign up user if "Welcome email" is turned On in the App ID dashboard).
You can present your own post verification screen by supply "URL for your custom email address verification page" in App ID dashboard under "Custom Landing pages" tab.
If you supplied this URL, after the user clicks verify and marked as verified App ID will call this URL along with a "context" query parameter.
Use the "context" parameter in order to receive the sign_up confirmation result by calling, to "/sign_up/confirmation_result"
The "/sign_up/confirmation_result" will return the result of the user verification process, according to if it was successful or not.
You can use the return result to present to the user with your own custom "thank you for verifying" screen in case of successful result, or other screen in case the result was unsuccessful.


**Customized Forgot password**

Use the "/forgot_password" endpoint in order to start a forgot password process.
supply your tenantId and the email of the cloud directory user that forgot his password.
The "/forgot_password" endpoint returns the Cloud directory user that forgot his password.

After calling the "/forgot_password" endpoint App ID will send a reset password email to the email address that was supplied.

The reset password email will contain a RESET button, when the new user click it he will be presented with the reset password screen of App ID.
You can present your own reset password form screen by suppling "URL for your custom reset password page" in App ID dashboard under "Custom Landing pages" tab.
If you supplied this URL, after the user clicks  the RESET button on the reset password email, App ID will call this URL along with a "context" query parameter.
Use the "context" parameter in order to receive the forgot password confirmation result by calling, to "/forgot_password/confirmation_result"
The "/forgot_password/confirmation_result" will return the result of the forgot password process, according to if it was successful or not.
You can use the return result to present to the user with your own custom reset password screen in case of successful result, or other screen in case the result was unsuccessful.

When the user clicks on the submit button of your reset password page, use the "/change_password" endpoint in order to change the password of the user.
simply supply your tenantId, the user new password and the cloud directory user uuid.
You can also pass the IP address that the reset password was performed from, then the placeholder %{passwordChangeInfo.ipAddress} will be available with that ip value, for the change password email template.
After the user password will be change, App ID will send a the "password changed" email if the "Password change email" is set to On, in App ID dashboard.

Note:
When a user clicks on the reset password submit button, its crucial to validate that its a legitimate reset password request in your backend, before calling the "/change_password" endpoint. Otherwise your backend reset password endpoint will be vulnerable.
This can be fulfill for example by adding some random string to your custom reset password page that will be send to your backend reset password submit, your handler should validate the random string and only if it valid call to the "/change_password" endpoint.
Check the Cloud Land Node.js backend (link) for example.

** Resend **

Use the "/resend/{templateName}" endpoint in order to resend an email.
Supply your tenantId, the templateName and the Cloud directory user uuid.
This can be helpful in case the cloud directly user did not receive an email from some reason.  

** change password **

When a user is signed in to your application, you can use the "/change_password" endpoint to change the user password.
As a best practice your change password page should prompt the user to re-enter his current password, along with the new one.
Your backend should validate the user current password with ROP API, and if its valid, call the "/change_password" with the new user password.
After calling this endpoint App ID will send a the "password changed" email if the "Password change email" is set to On, in App ID dashboard.

** change details **

When a user is signed-in to your application, you can allow him to change one or more of his details (email address can not be change).
Use the "/Users/{userId}" endpoint (link https://appid-management.stage1.eu-gb.bluemix.net/swagger-ui/#/Users) in order to get and update the user details.

Note:
When updating the user details, the "/Users/{userId}" endpoint gets the updated user data in the request body as a SCIM format. (https://tools.ietf.org/html/rfc7643#section-8.2), make sure you change only the relevant details.
