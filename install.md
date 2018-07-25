---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Adding {{site.data.keyword.appid_short}} to your app
{: #configuring}


## Setting up the Android SDK
{: #android-setup}

Build your Android apps with the {{site.data.keyword.appid_short}} client SDK, initialize the SDK, authenticate users, and make requests to protected and unprotected resources.
{:shortdesc}


### Before you begin
{: #before-android}

You need the following information:
  * An instance of the {{site.data.keyword.appid_short_notm}} service.
  * Your tenant ID. Your tenant ID is a unique identifier that is used to initialize your app and can be found in the **Service Credentials** tab of your service dashboard.
  * Your {{site.data.keyword.Bluemix}} region. You can find your region by looking in the UI. The value is used for initializing your app.
    <table><caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding SDK values</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} Region</th>
      <th>SDK value</th>
    </tr>
    <tr>
      <td>US South</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY</code></td>
    </tr>
    <tr>
      <td>United Kingdom</td>
      <td><code>AppID.REGION_UK</code></td>
    </tr>
    <tr>
      <td>Germany</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * An <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio project<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, set up to work with Gradle.

### Installing the client SDK
{: #install-android}

1. Create an Android Studio project, or open an existing project.
2. Add the JitPack repository to your root `build.gradle` file.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. Find the dependencies section of the `build.gradle` file for your app, and add a compile dependency for the {{site.data.keyword.appid_short_notm}} client SDK. **Note**: Be sure to open the file for your app, not the project `build.gradle` file.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
  ```
  {: codeblock}

5. Find the `defaultConfig` section and add the following lines of code.

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. Synchronize your project with Gradle. Click **Tools > Android > Sync Project with Gradle Files**.

### Initializing the client SDK
{: #initialize-android}

Initialize the client SDK by passing the context, tenant ID, and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> Table. Command components explained </caption>
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
      <td> You can find your region in the UI. Options are `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney`, or `AppID.REGION_Germany`. </td>
    </tr>
  </table>

Now you're ready to configure your identity providers and start authenticating users! For more information, see the <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub repository<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.


</br>

## Setting up the iOS Swift SDK
{: #ios-setup}

Build your Swift applications with the {{site.data.keyword.appid_short}} client SDK, initialize the SDK, authenticate users, and make requests to protected and unprotected resources.
{:shortdesc}


### Before you begin
{: #before-ios}

You need the following information:
  * An instance of {{site.data.keyword.appid_short_notm}}.
  * Your tenant ID. Your tenant ID is a unique identifier that is used to initialize your app and can be found in the **Service Credentials** tab of your service dashboard.
  * Your {{site.data.keyword.Bluemix_notm}} Region.
  You can find your region by looking in the UI. The value is used for initializing your app.
  <table> <caption> Table. {{site.data.keyword.Bluemix_notm}} regions and corresponding SDK values </caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} Region</th>
      <th>SDK value</th>
    </tr>
    <tr>
      <td>US South</td>
      <td><code>AppID.REGION_US_SOUTH</code></td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY</code></td>
    </tr>
    <tr>
      <td>United Kingdom</td>
      <td><code>AppID.REGION_UK</code></td>
    </tr>
    <tr>
      <td>Germany</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * An Xcode project (version 9.0.1 or higher).
  * CocoaPods (version 1.1.0 or higher).


### Installing the client SDK
{: #install-ios}

The {{site.data.keyword.appid_short_notm}} client SDK is distributed with CocoaPods, a dependency manager for Swift and Objective-C Cocoa projects. CocoaPods downloads artifacts, and makes them available to your project.

1. Create an Xcode project, or open an existing project.
2. Open, or create, the podfile in the project's directory.
3. Following your project's target, add a dependency for the 'BluemixAppID' pod and the `use_frameworks!` command.

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. Download the `BluemixAppID` dependency.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Enable keychain sharing in your Xcode project. Navigate to **Project Settings > Capabilities > Keychain Sharing** and select **Enable keychain sharing**.
7. Open **Project Settings > Info > URL Types**, and add a **URL Type**. Place the following value in both the **Identifier** and the **URL Scheme** text boxes.
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### Initializing the client SDK
{: #initialize-ios}

1. Initialize the client SDK by passing the tenant ID and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of the AppDelegate in your Swift application.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> Table. Command components explained </caption>
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
      <td> You can find your region in the UI. Options are `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney`, or `AppID.REGION_Germany`.</td>
    </tr>
  </table>

2. Add the following import to your `AppDelegate` file.

    ```swift
    import BluemixAppID
    ```
    {: codeblock}

3. Add the following code to your AppDelegate file.

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Now you're ready to configure your identity providers and start authenticating users! For more information about the iOS SDK, see the <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

</br>

## Setting up the Node.js SDK
{: #nodejs-setup}

### Before you begin
{: #before-nodejs}

Be sure that you have the following prerequisites ready to go:
1. Install the [IBM Cloud CLI](../cli/index.html).
2. Implement your Node.js server with the <a href="http://expressjs.com/" target="_blank">Express framework <img src="../icons/launch-glyph.svg" alt="External link icon"></a>. To install the Express framework, use the command line to open the directory with your Node.js app, and run the following command:
  ```
  npm install --save express
  ```
  {: codeblock}
3. Install Passport. Use the command line to open the directory with your Node.js app, and run the following command:
  ```
  npm install --save passport
  ```
  {: codeblock}

**Note**: Other frameworks use `Express` frameworks, such as LoopBack. You can use the {{site.data.keyword.appid_short_notm}} server SDK with any of these frameworks.


### Installing the server SDK
{: #install-nodejs}

1. Using the command line, open the directory with your Node.js app.
2. Install the {{site.data.keyword.appid_short_notm}} service.
  ```
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

## Step 3. Initializing the SDK
{: #initialize}

1. Add the following `require` definitions to your `server.js` file.
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. Set up your express app to use express-session middleware. **Note**: You must configure the middleware with the proper session storage for production environments. For more information see the <a href="https://github.com/expressjs/session" target="_blank">expressjs docs <img src="../icons/launch-glyph.svg" alt="External link icon"></a>.
    ```
    const app = express();
    app.use(session({
        secret: "123456",
        resave: true,
        saveUninitialized: true
        }));
    app.use(passport.initialize());
    app.use(passport.session());
    ```
    {: codeblock}

3. Pass the tenant ID and credentials to initialize the SDK.
    ```
    passport.use(new WebAppStrategy({
    tenantId: "{tenant-id}",
    clientId: "{client-id}",
    secret: "{secret}",
    oauthServerUrl: "{oauth-server-url}",
    redirectUri: "{app-url}" + CALLBACK_URL
    }));
    ```
    {: codeblock}

 <table summary="Command components: Node.js apps">
  <caption>Command components for Node.js apps</caption>
    <tr>
      <th>Components</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><i> tenantID </i></td>
      <td>The tenant ID is a unique identifier that is used to initialize your app. You can find the value in the {{site.data.keyword.appid_short_notm}} service dashboard by clicking **View Credentials** in the **Service Credentials** tab.</td>
    </tr>
    <tr>
      <td><i>clientID</i> </br> <i>secret</i> </br> <i>oauth-server-url</i> </br> </td>
      <td>You can find these values by clicking **View Credentials** in the **Service Credentials** tab of your service dashboard.</td>
    </tr>
    <tr><td><i>redirectUri</i></td>
    <td>The redirectUri value can be supplied in three ways:</br>
        1. Manually in new WebAppStrategy({redirectUri: "...."})</br>
        2. As environment variable named `redirectUri`</br>
        3. If none of the above was supplied, the App ID SDK will try to retrieve application_uri of the application that is running on IBM Cloud and append a default suffix "/ibm/cloud/appid/callback"</td>
    </tr>
    <tr>
      <td><i>CALLBACK_URL</i></td>
      <td>The URL for the page that users see after they log in.</td>
    </tr>
  </table>

4. Configure passport with serialization and deserialization. This configuration step is required for authenticated session persistence across HTTP requests. For more information, see the <a href="http://passportjs.org/docs" target="_blank">passport docs <img src="../icons/launch-glyph.svg" alt="External link icon"></a>.

  ```
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. Add the following code to your `server.js` file to issue the service redirects:
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **Note**: The service redirects in the following order:
    1. The original URL of the request that triggered the  authentication process, as persisted in the HTTP session under the `WebAppStrategy.ORIGINAL_URL` key.
    2. A successful redirect, as specified in `passport.authenticate(name, {successRedirect: "...."}).`
    3. Application root ("/")

6. Redeploy your application.

For more information, see the <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub repository <img src="../icons/launch-glyph.svg" alt="External link icon"></a>.

## Setting up the Swift SDK
{: #swift-setup}

Protect your back-ends and APIs with the {{site.data.keyword.appid_short}} server SDK.
{:shortdesc}


### Before you begin
{: #before-swift}

Prior to working with the Swift SDK, you must have the following prerequisites:

* Either MacOS or Linux
* OpenSSL 1.0.2 on Linux
* Install Swift 3.0.2
* Install Kitura 1.6


### Installing the SDK
{: #install-swift}

1. Open the `Package.swift` file in the directory of your Swift app and add the `appid-serversdk-swift` dependency.

  ```swift
  let package = Package(
      name: “myApp",
      dependencies: [
          .package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", .upToNextMinor(from: “4.0.0")),
      ],
      targets: [
          .target(
              name: "myApp",
              dependencies: ["BluemixAppID"]),
      ]
  )
  ```
  {: codeblock}

2. For MacOS: When you build on the command line, all packages should include the following flags.
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. Use the following command when you create an xcodeproject:
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  You can copy the openssl.xcconfig from the <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
  {: tip}

4. Add the following code to your Swift application to:
    * Set up Kitura to use session middleware. **Note**: You must configure Kitura with the proper session storage for production environments. For more information see the <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
    * Retrieve access and identity tokens from the {{site.data.keyword.appid_short_notm}} service by running a get command on the call back URL.

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
    {: codeblock}

5. Redeploy your application.

</br>

## Setting up the Liberty for Java SDK
{: #lfj-setup}

You can configure {{site.data.keyword.appid_short_notm}} to work with your existing Liberty for Java web applications.
{:shortdesc}

1. Add an <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect feature <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to your `server.xml`.

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. In your Open ID Connect Client feature, define the following placeholders. They are filled automatically by {{site.data.keyword.Bluemix_notm}} later. The instance name variable must match your {{site.data.keyword.appid_short_notm}} instance name exactly.

  ```
  clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
  clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
  authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
  tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
  jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
  issuerIdentifier='appid-oauth.ng.bluemix.net'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  ```
  {: codeblock}

  **Note**: The issuerIdentifier variable changes according to your region. It can be one of the following variables:
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. Define an authorization filter to specify protected resources. If a filter is not <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">defined <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, the service will protect all resources.
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

4. In your `server.xml` file, define your special subject type as ALL_AUTHENTICATED_USERS.

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample"
  location="${server.config.dir}/apps/libertySample-1.0.0.war">
    <application-bnd>
        <security-role name="myrole">
        <special-subject type="ALL_AUTHENTICATED_USERS"/>
        </security-role>
            </application-bnd>
        </application>
  ```
  {: codeblock}

5. In your `<application-bnd>` element, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">define the roles <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> as found in your web app: `web.xml`.

  ```xml
  <security-role>
  <role-name>myrole</role-name>
  </security-role>

  <security-constraint>
  <web-resource-collection>
  <web-resource-name>ProtectedServlet</web-resource-name>
  <url-pattern>/ProtectedServlet/*</url-pattern>
  <http-method>GET</http-method>
  <http-method>PUT</http-method>
  <http-method>POST</http-method>
  <http-method>DELETE</http-method>
  </web-resource-collection>

  <auth-constraint>
  <role-name>myrole</role-name>
  </auth-constraint>
  <user-data-constraint>
  <transport-guarantee>NONE</transport-guarantee>
  </user-data-constraint>
  </security-constraint>
  ```
  {: codeblock}

6. Get a certificate.

    a. In your {{site.data.keyword.appid_short_notm}} dashboard, click Service Credentials.

    b. Click **View credentials** and copy the `oauthServerUrl`.

    c. Add `/token` to the URL. Use Firefox to browse the output URL and get the certificate. You can use the following URL as an example.

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. In the Firefox address bar, click the lock icon > **right arrow** > **more information** > **view certificate**.

    e. In the **Security** tab, click **View certificate** > **details**.

    f. Export the certificate and save it on your local drive as a PEM file.

7. Add the certificate to your Liberty for Java truststore.jks file by using the <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and add a reference to the certificate alias in the OIDC element. Your `.jks file` is located in your server directory: **resources** > **security** > **<i>truststore file name</i>** > **`.jks file`**. You can use one of the following options to add your certificate to the file.

    * In terminal, go to your Liberty for Java security folder: wlp > usr > servers > <i>servername</i> > resources > security and use the following command to add the certificate.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Note**: `~/Documents/[certificatename].cer` demonstrates the file location on your local drive.

    * You can use <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to add the certificate. Open KeyStore Explorer and select **Open an existing KeyStore**.

    **Note**: The certificate might be expired/changed, in this case you should update your trustore with the new certificate.

8. In your `manifest.yml` file, define your {{site.data.keyword.appid_short_notm}} instance.

  ```yml
  services:
  - <appid service name>

  Manifest.yml file example:
  applications:
  - name: LibertyExampl
  buildpack: liberty-for-java
  instances: 1
  random-route: true
  memory: 512M
  disk_quota: 1024M
  timeout: 180
  services:
  - AppID-Instance-Name
  ```
  {: codeblock}

    An example `server.xml` file that is configured for {{site.data.keyword.appid_short_notm}}:

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <server description="sample server">

      <featureManager>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>  
      </featureManager>

      <openidConnectClient id="MyDefaultRP"
         clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
         clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
         authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
         tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
         jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
         issuerIdentifier='${cloud.services.AppID-Instance-Name.credentials.appid-oauth.ng.bluemix.net}'
         tokenEndpointAuthMethod="basic"
         signatureAlgorithm="RS256"
         authFilterid="myAuthFilter"
      />
      <authFilter id="myAuthFilter">
               <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
      </authFilter>

      <application type="war" id="ProtectedServlet" context-root="/appidSample" location="${server.config.dir}/apps/libertySample-1.0.0.war">
          <application-bnd>
              <security-role name="myrole">
                  <special-subject type="ALL_AUTHENTICATED_USERS" />
              </security-role>
          </application-bnd>
      </application>

   <applicationManager autoExpand="true"/>

  <keyStore id="defaultKeyStore" password="Password"/>
  <keyStore id="defaulttrustore" password="Liberty" location="<FileContainingCertificated>.jks"/>

  <ssl id="defaultSSLSettings" keyStoreRef="defaultKeyStore" trustStoreRef="defaulttrustore"/>
  <sslDefault sslRef="defaultSSLSettings"/>

      <httpEndpoint id="defaultHttpEndpoint" httpPort="9080" host="*" httpsPort="9443" />


      <applicationManager autoExpand="true"/>

  </server>
  ```
  {: codeblock}


</br>

## Adding {{site.data.keyword.appid_short_notm}} to an existing application that does not run on {{site.data.keyword.Bluemix_notm}}
{: #existing}

If you have a Node.js or Swift application that does not run on {{site.data.keyword.Bluemix_notm}}, you can configure the WebAppStrategy or the WebAppKituraCredentialsPlugin to work remotely. For a Liberty for Java app that doesn't run on Bluemix, configure the OIDC element variables.


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
  {: codeblock}

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
  {: codeblock}

  <table>
  <caption> Table 6. Command components for Swift and Node.js apps explained </caption>
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

In your Liberty for Java apps, complete the steps under [Adding {{site.data.keyword.appid_short_notm}} to an existing Liberty for Java app](/docs/services/appid/existing.html#existing-liberty), but replace the OIDC client element variables with the following code.

  ```
  clientId='App ID client_ID'
  clientSecret='App Id Secret'      
  authorizationEndpointUrl='oauthServerUrl/authorization'       
  tokenEndpointUrl='oauthServerUrl/token'
  jwkEndpointUrl='oauthServerUrl/publickeys'
  issuerIdentifier='Changed according to the region'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  trustAliasName="my.bluemix.certificate"
  ```
  {: codeblock}

  <table>
  <caption> Table 7. OIDC element variables for Liberty for Java apps that do not run on Bluemix </caption>
    <tr>
      <th> Component </th>
      <th> Description </th>
    </tr>
    <tr>
    <td> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> You can find these values by clicking **View credentials** in the **service credentials** tab of your service dashboard. </td>
    </tr>
    <tr>
      <td> <i> authorizationEndpointURL </i> </td>
      <td> Add `/authorization` to the end of your oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> tokenEndpointUrl </i> </td>
      <td> Add `/token` to the end of your oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> jwkEndpointUrl </i> </td>
      <td> Add `/publickeys` to the end of your oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> issuerIdentifier </i> </td>
      <td> Changes based on your region. It can be one of the following: </br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net" </ul></td>
    </tr>
    <tr>
      <td> <i> tokenEndpointAuthMethod </i> </td>
      <td> Specified as "basic". </td>
    </tr>
    <tr>
      <td> <i> signatureAlgorithm </i> </td>
      <td> Specified as "RS256". </td>
    </tr>
    <tr>
      <td> <i> authFilterid </i> </td>
      <td> The list of resources to protect. </td>
    </tr>
    <tr>
      <td> <i> trustAliasName </i> </td>
      <td> The name of your certificate within your truststore. </td>
    </tr>
  </table>
