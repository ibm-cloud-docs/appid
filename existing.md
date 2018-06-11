---

copyright:
  years: 2017, [{CURRENT_YEAR}]
lastupdated: "[{LAST_UPDATED_DATE}]"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Adding {{site.data.keyword.appid_short_notm}} to an existing app

You can use {{site.data.keyword.appid_full}} with your existing application to authenticate and store profile information about your users.


## Prerequisites
{: prereq}

* An existing iOS Swift, Android, Node.js, Swift, or Liberty for Java application.
* An existing instance of {{site.data.keyword.appid_short_notm}}.


## Adding {{site.data.keyword.appid_short_notm}} to an existing Android app
{: #existing-android}

You can add the {{site.data.keyword.appid_short_notm}} service to your existing Android applications.

1. Add the JitPack repository to your root `build.gradle` file.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
      		}
  }
  ```
  {: codeblock}

2. Open the `build.gradle` file for your application, find the dependencies section of the file, and add a compile dependency for the {{site.data.keyword.appid_short_notm}} client SDK.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
  }
  ```
  {: codeblock}

3. Find the defaultConfig section and add the following line of code.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. Synchronize your project with Gradle.
5. Initialize the client SDK by passing the context, tenant ID, and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          }
        });
  ```
  {: codeblock}

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

## Adding {{site.data.keyword.appid_short_notm}} to an existing iOS Swift app
{: #existing-ios}

1. Open the podfile in the project's directory.
2. Under your project's target, add a dependency for the <prod>`BluemixAppID`</prod><staging>`IBMCloudAppID`</staging> pod. Be sure the `use_frameworks!` command is also under your target.
3. To download the <prod>`BluemixAppID`</prod><staging>`IBMCloudAppID`</staging> dependency, run the following command.

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. Open your Xcode project and enable keychain sharing. Under **Project Settings**, click **Capabilities** > **Keychain Sharing**.
5. Under **Project Settings** > **Info** > **URL Types**, add a **URL Type**. Fill both the **Identifier** text box and the **URL Scheme** text box with the following value.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. Add the following import to your `AppDelegate.swift` file.

  ```swift
  import <prod>BluemixAppID</prod><staging>IBMCloudAppID</staging>
  import BMSCore
  ```
  {: codeblock}

7. Initialize the client SDK by passing tenant ID and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the application:didFinishLaunchingWithOptions: method of the AppDelegate in your application.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, <prod>bluemixRegion</prod><staging>region</staging>: <AppID.Region>)
  ```
  {: codeblock}

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
        <td> You can find your region in the UI. Options are <prod>`AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, or `AppID.REGION_Sydney`.</prod><staging>`AppID.regionUSSouth`, `AppID.regionUK`, or `AppID.regionSydney`.</staging></td>
      </tr>
    </table>

8. Add the following code to your AppDelegate file.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
         	return AppID.sharedInstance.application(application, open: url, options: options)
     	}
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken? response:Response?) {
     }

     public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

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
{: #existing-node}

1. Add the `<staging>ibmcloud</staging><prod>bluemix</prod>-appid` module to your Node.js application.

  ```javaScript
  npm install --save <staging>ibmcloud</staging<prod>bluemix</prod>-appid
  ```
  {: codeblock}

2. Install the following modules if they are not installed already.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. Add the following code to your `app.js` file to:
    * Set up your express app to use express-session middleware. **Note**: You must configure the middleware with the proper session storage for production environments. For more information see the <a href="https://github.com/expressjs/session" target="_blank">expressjs docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
    * Configure passportjs with serialization and deserialization. This is required for authenticated session persistence across HTTP requests. For more information, see the <a href="http://passportjs.org/docs" target="_blank">passportjs docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.  
    * Retrieve access and identity tokens from the {{site.data.keyword.appid_short_notm}} service by running a get command on the call back URL.

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
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
    		res.json(req.user);
    });
  ```
  {: codeblock}

    **Note**: The service redirects in the following order:
    1. The original URL of the request that triggered the  authentication process, as persisted in the HTTP session under the `WebAppStrategy.ORIGINAL_URL` key.
    2. A successful redirect, as specified in `passport.authenticate(name, {successRedirect: "...."}).`
    3. Application root ("/")

4. Redeploy your application.


## Adding {{site.data.keyword.appid_short_notm}} to an existing Swift web application
{: #existing-swift}

1. Open the `Package.swift` file in the directory of your Swift app and add the `appid-serversdk-swift` dependency.
  For example:

    ```swift
    import PackageDescription

    let package = Package(
       	dependencies: [
                .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: <prod>1</prod><staging>5</staging>)
                ]
    )
    ```
    {: codeblock}

2. Add the following code to your Swift application to:
    * Set up Kitura to use session middleware. **Note**: You must configure Kitura with the proper session storage for production environments. For more information see the <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
    * Retrieve access and identity tokens from the {{site.data.keyword.appid_short_notm}} service by running a get command on the call back URL.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import <prod>BluemixAppID</prod><staging>IBMCloudAppID</staging>
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

  <table>
  <caption> Table 5. Command components explained </caption>
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



## Adding {{site.data.keyword.appid_short_notm}} to an existing Liberty for Java app
{: #existing-liberty}

You can configure {{site.data.keyword.appid_short_notm}} to work with your existing Liberty for Java web applications.

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

3. In your `server.xml` file, define your special subject type as ALL_AUTHENTICATED_USERS.

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

4. In your `<application-bnd>` element, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">define the roles <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> as found in your web app: `web.xml`.

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

5. Get a certificate.

    a. In your {{site.data.keyword.appid_short_notm}} dashboard, click Service Credentials.

    b. Click **View credentials** and copy the `oauthServerUrl`.

    c. Add `/token` to the URL. Use Firefox to browse the output URL and get the certificate. You can use the following URL as an example.

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. In the Firefox address bar, click the lock icon > **right arrow** > **more information** > **view certificate**.

    e. In the **Security** tab, click **View certificate** > **details**.

    f. Export the certificate and save it on your local drive as a PEM file.

6. Add the certificate to your Liberty for Java truststore.jks file by using the <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and add a reference to the certificate alias in the OIDC element. Your `.jks file` is located in your server directory: **resources** > **security** > **<i>truststore file name</i>** > **`.jks file`**. You can use one of the following options to add your certificate to the file.

    * In terminal, go to your Liberty for Java security folder: wlp > usr > servers > <i>servername</i> > resources > security and use the following command to add the certificate.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Note**: `~/Documents/[certificatename].cer` demonstrates the file location on your local drive.

    * You can use <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to add the certificate. Open KeyStore Explorer and select **Open an existing KeyStore**.

7. In your `manifest.yml` file, define your {{site.data.keyword.appid_short_notm}} instance.

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
         trustAliasName="my.bluemix.certificate "
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
