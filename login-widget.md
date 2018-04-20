---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-18"

---

{:generic: .ph data-hd-programlang='generic'}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:php: .ph data-hd-programlang='PHP'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Managing sign-in

{{site.data.keyword.appid_full}} provides a login widget that lets you give your users secure sign-in options.
{: shortdesc}

When your app is configured to use an identity provider, visitors to your app are directed to a sign in screen by the login widget. As a default, when only one provider is set to on, visitors are redirected to that identity providers authentication screen. With the login widget you can display a default sign in screen or, with cloud directory, you can reuse your existing UI's.

You can update your sign-in flow at any time, without changing your source code in any way!
{: tip}

The service uses OAuth 2 grant types to map the authorization process. When you configure social identity providers such as Facebook, the [Oauth2 Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) is used to call the log in widget. When you display your own UI screens, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) is used to log in and gain access and identity tokens.


## Customizing the default sign-in screen
{: #login-widget}

You can customize the default sign-in screen to display the logo and colors of your choice.
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
      <th>Enterprise identity provider</th>
      <th>Cloud directory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Sign in</td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Sign up</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Forgot password</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Change password</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Account details</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

</br>
### Calling the sign in screen

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
    {: java}

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
    {: swift}

    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
      successRedirect: LANDING_PAGE_URL,
      failureRedirect: ROP_LOGIN_PAGE_URL,
      failureFlash : true // allow flash messages
    }));
    ```
    {: pre}
    {: nodejs}

    `WebAppStrategy` allows users to sign in to your web apps with a username and password. After a successful login, a user's access token is stored in the HTTP session and is available during the session. Once the HTTP session is destroyed or expired, the token is invalid.
    {: tip}
    {: javascript}

    ```
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
    {: pre}
    {: swift}

</br>
### Calling the sign up screen

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the sign-up flow.
  ```
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
  {: android}
</br>

### Calling the forgot password screen

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the forgot password flow.
    ```
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
    {: android}
</br>
### Calling the account details screen
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

### Calling the change password screen

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
   {: android}
</br>
</br>
