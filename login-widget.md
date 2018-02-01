---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Managing the sign in experience

With the login widget, you can update your sign in flow at any time without adding, removing, or changing the source code. You can be up and running in minutes by using the code provided in our sample apps.
{: shortdesc}

**Note**: When you configure social identity providers such as Facebook, the [Oauth2 Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) is used to call the login widget.

</br>
## Customizing the sample app code
{: #login-widget}

You can customize the preconfigured sign in screen to display the logo and colors of your choice. If you want to display your own branded UI's, check out [cloud directory](/docs/services/appid/cloud-directory.html).
{: shortdesc}

![Customized sign in experience example](/images/customize.gif)

To customize the screen:

1. Open the {{site.data.keyword.appid_short_notm}} service dashboard.
2. Select the **Login Customization** section, where you can modify the appearance of the login widget to align with your company's brand.
3. Upload your company's logo by selecting a PNG or JPG file from your local system. The recommended image size is 320 x 320 pixels. The maximum file size is 100 Kb.
4. Select a header color for the widget from the color picker, or enter the hex code for another color.
5. Inspect the preview pane, and click **Save Changes** when you are happy with your customizations. A confirmation message is displayed.
6. Verify your changes by visiting your app. You are not required to rebuild your app. Your images are stored in the {{site.data.keyword.appid_short}} database and is displayed the next time the login widget is called.


</br>
## Calling the login widget with the Android SDK

With social identity providers enabled, you can call the preconfigured sign in screen with the Android SDK.
{: shortdesc}

1. Configure your identity providers.
2. Place the following command in your code.
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
    {: codeblock}


</br>
## Calling the login widget with the iOS Swift SDK

With social identity providers enabled, you can call the preconfigured sign in screen with the iOS Swift SDK.
{: shortdesc}

1. Configure your identity providers.
2. Add the following command to your app code.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
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
  {: codeblock}


</br>
## Calling the login widget with the Node.js SDK

With social identity providers enabled, you can call the preconfigured sign in screen with the Node.js SDK.
{: shortdesc}

1. Configure your identity providers.
2. Add the following command to your code.
    ```JavaScript

    var express = require('express');
    var passport = require('passport');
    var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
    ```
    {: codeblock}


</br>
## Calling the login widget with the Swift SDK

With social identity providers enabled, you can call the preconfigured sign in screen with the Swift SDK.
{: shortdesc}

The WebAppKituraCredentialsPlugin is based on the OAuth2 authorization code grant flow and must be used for web applications that use browsers. The plug-in provides tools to implement authentication and authorization flows. The plug-in also provides mechanisms to detect unauthenticated attempts to access protected resources and automatically redirects a user's browser to the authentication page. After successful authentication, a user is taken to the web application's callback URL, which uses the plug-in to obtain access and identity tokens from {{site.data.keyword.appid_short_notm}}. After obtaining these tokens, the plug-in stores them in an HTTP session under WebAppKituraCredentialsPlugin.AuthContext.

The following code demonstrates how to use WebAppKituraCredentialsPlugin in a Kitura application to protect the `/protected` endpoint.

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
