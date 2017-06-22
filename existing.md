---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Adding {{site.data.keyword.appid_short_notm}} to an existing app

You can use {{site.data.keyword.appid_full}} with your existing application to authenticate and store profile information about your users.


## Prerequisites

* An existing iOS Swift, Android, Node.js, or Swift application.
* An existing instance of {{site.data.keyword.appid_short_notm}}.


## Adding {{site.data.keyword.appid_short_notm}} to an existing Android app

You can add the App Id service to your existing Android applications.

1. Add the JitPack repository to your root build.gradle file.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
      		}
  }
  ```
  {: pre}

2. Open the build.gradle file for your application, find the dependencies section of the file, and add a compile dependency for the {{site.data.keyword.appid_short_notm}} client SDK.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
  }
  ```
  {: pre}

3. Find the defaultConfig section and add the following line of code.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. Synchronize your project with Gradle.
5. Initialize the client SDK by passing the context, tenant ID, and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> Table 1. Command components explained </caption>
    <tr>
      <th> Components </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> You can find this value by clicking **View credentials** in the **service credentials** tab of your service dashboard. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> You can find your region in the UI. Options are `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, or `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

6. After the {{site.data.keyword.appid_short_notm}} client SDK is initialized, you can authenticate your users by running the login widget.

  ```Java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

          @Override
          public void onAuthorizationCanceled () {
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
        });
  ```
  {: pre}

  <table>
  <caption> Table 2. Command components explained </caption>
    <tr>
      <th> Components </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> An exception occurred. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> The authentication process was canceled by the user. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> The user was authenticated. </td>
    </tr>
  </table>

## Adding {{site.data.keyword.appid_short_notm}} to an existing iOS Swift App

1. Open the podfile in the project's directory.
2. Under your project's target, add a dependency for the 'BluemixAppID' pod. Be sure the `use_frameworks!` command is also under your target.
3. To download the `BluemixAppID` dependency, run the following command.

  ```
  pod install --repo-update
  ```
  {: pre}

4. Open your Xcode project and enable keychain sharing. Under **Project Settings**, click **Capabilities** > **Keychain Sharing**.
5. Under **Project Settings** > **Info** > **URL Types**, add a **URL Type**. Fill both the **Identifier** text box and the **URL Scheme** text box with the following value.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. Add the following import to your AppDelegate.swift file.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. Initialize the client SDK by passing tenant ID and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the application:didFinishLaunchingWithOptions: method of the AppDelegate in your application.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> Table 3. Command components explained </caption>
    <tr>
      <th> Components </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> You can find this value by clicking **View credentials** in the **service credentials** tab of your service dashboard. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> You can find your region in the UI. Options are `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, or `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

8. Add the following code to your AppDelegate file.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
         	return AppID.sharedInstance.application(application, open: url, options: options)
     	}
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
     }

     public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}
  <table>
  <caption> Table 4. Command components explained </caption>
    <tr>
      <th> Components </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> The user was authenticated. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> The authentication process was canceled by the user. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> An exception occurred. </td>
    </tr>
  </table>

## Adding {{site.data.keyword.appid_short_notm}} to an existing Node.js web app

1. Add the `bluemix-appid` module to your Node.js application.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. Install the following modules if they are not installed already.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. Add the following code to your app.js file to:
    * Set up your express app to use express-session middleware. **Note**: You must configure the middleware with the proper session storage for production environments. For more information see the [expressjs docs](https://github.com/expressjs/session).
    * Configure passportjs with serialization and deserialization. This is required for authenticated session persistence across HTTP requests. For more information, see the [passportjs docs](http://passportjs.org/docs).
    * Retrieve access and identity tokens from the App ID service by running a get command on the call back URL.

  ```javaScript
  const express = require("express");
  const session = require("express-session");
  const passport = require("passport");
  const WebAppStrategy = require("bluemix-appid").WebAppStrategy;
  const app = express();
  const CALLBACK_URL = "/ibm/bluemix/appid/callback";
  app.use(session({
      secret: "123456",
      resave: true,
      saveUninitialized: true
    }));
  app.use(passport.initialize());
    app.use(passport.session());

    passport.use(new WebAppStrategy());
  passport.serializeUser(function(user, cb) {
      cb(null, user);
    });

    passport.deserializeUser(function(obj, cb) {
      cb(null, obj);
    });
  app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res)
    		res.json(req.user);
    });
  ```
  {: pre}

    **Note**: The service redirects in the following order:
    1. The original URL of the request that triggered the  authentication process, as persisted in the HTTP session under the `WebAppStrategy.ORIGINAL_URL` key.
    2. A successful redirect, as specified in `passport.authenticate(name, {successRedirect: "...."}).`
    3. Application root ("/")

4. Redeploy your application.


## Adding {{site.data.keyword.appid_short_notm}} to an existing Swift web application

1. Open the `Package.swift` file in the directory of your Swift app and add the `appid-serversdk-swift` dependency.
  For example:

    ```swift
    import PackageDescription

    let package = Package(
       	dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
       		]
    )
    ```
    {: pre}

2. Add the following code to your Swift application to:
    * Set up Kitura to use session middleware. **Note**: You must configure Kitura with the proper session storage for production environments. For more information see the [the Kitura docs](https://github.com/IBM-Swift/Kitura-Session).
    * Retrieve access and identity tokens from the App ID service by running a get command on the call back URL.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  router.get(CALLBACK_URL,
    handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
      successRedirect: LANDING_PAGE_URL,
      failureRedirect: LANDING_PAGE_URL
      ))
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
  ```
  {: pre}

  <table>
  <caption> Table 6. Command components explained </caption>
    <tr>
      <th> Components </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> var CALLBACK_URL </i> </td>
      <td> /ibm/bluemix/appid/callback </td>
    </tr>
    <tr>
      <td> <i> var LANDING_PAGE_URL </i> </td>
      <td> /index.html </td>
    </tr>
    </table>

5. Redeploy your application.



## Adding {{site.data.keyword.appid_short_notm}} to an existing application that does not run on {{site.data.keyword.Bluemix_notm}}


If you have a Node.js or Swift application that does not run on Bluemix, you can configure the WebAppStrategy or the WebAppKituraCredentialsPlugin to work remotely.


In your Node.js app, replace `passport.use(new WebAppStrategy());` with the following code.

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
{: pre}

In your Swift app, replace `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` with the following code.

  ```swift
  let options = [
        "clientId": "{client-id}",
        "secret": "{secret}",
        "tenantId": "{tenant-id}",
        "oauthServerUrl": "{oauth-server-url}",
        "redirectUri": "{app-url}" + CALLBACK_URL
    ]
    let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  ```
  {: pre}

<table>
<caption> Table 7. Command components for Swift and Node.js apps explained </caption>
  <tr>
    <th> Components </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> You can find these values by clicking **View credentials** in the **service credentials** tab of your service dashboard. </td>
  </tr>
  <tr>
    <td> <i> app-url </i> </td>
    <td> Your application URL. </td>
  </tr>
  <tr>
    <td> <i> CALLBACK_URL </i> </td>
    <td> The URL for the page users see after they login. </td>
  </tr>
</table>
