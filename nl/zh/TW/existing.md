---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 將 {{site.data.keyword.appid_short_notm}} 新增至現有應用程式

您可以搭配使用 {{site.data.keyword.appid_full}} 與現有應用程式，以鑑別及儲存使用者的設定檔資訊。


## 必要條件
{: prereq}

* 現有 iOS Swift、Android、Node.js、Swift 或 Liberty for Java 應用程式。
* 現有 {{site.data.keyword.appid_short_notm}} 實例。


## 將 {{site.data.keyword.appid_short_notm}} 新增至現有 Android 應用程式
{: #existing-android}

您可以將 {{site.data.keyword.appid_short_notm}} 服務新增至現有 Android 應用程式。

1. 將 JitPack 儲存庫新增至根 `build.gradle` 檔案。

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
      		}
  }
  ```
  {: codeblock}

2. 開啟應用程式的 `build.gradle` 檔案、尋找檔案的 dependencies 區段，並新增 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 的編譯相依關係。

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
  }
  ```
  {: codeblock}

3. 尋找 defaultConfig 區段，並新增下行程式碼。

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. 將專案與 Gradle 同步化。
5. 將環境定義、承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 onCreate 方法。

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

    <table>
    <caption> 表 1. 說明的指令元件</caption>
      <tr>
        <th> 元件</th>
        <th> 說明</th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> 您可以在服務儀表板的**服務認證**標籤中按一下**檢視認證**，以找到此值。</td>
      </tr>
      <tr>
        <td> <i> AppID.REGION </i> </td>
        <td> 您可以在 UI 中找到您的地區。選項是 `AppID.REGION_US_SOUTH`、`AppID.REGION_UK` 或 `AppID.REGION_Sydney`。</td>
      </tr>
    </table>

6. 起始設定 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 之後，即可執行登入小組件來鑑別使用者。

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
    <caption> 表 2. 說明的指令元件</caption>
      <tr>
        <th> 元件</th>
        <th> 說明</th>
      </tr>
      <tr>
        <td> <i> onAuthorizationFailure </i> </td>
        <td> 發生異常狀況。</td>
      </tr>
      <tr>
        <td> <i> onAuthorizationCanceled </i> </td>
        <td> 使用者已取消鑑別處理程序。</td>
      </tr>
      <tr>
        <td> <i> onAuthorizationSuccess </i> </td>
        <td> 已鑑別使用者。</td>
      </tr>
    </table>

## 將 {{site.data.keyword.appid_short_notm}} 新增至現有 iOS Swift 應用程式
{: #existing-ios}

1. 在專案的目錄中，開啟 podfile。
2. 在專案的目標下，新增 'BluemixAppID' Pod 的相依關係。請確定，您的目標下也有 `use_frameworks!` 指令。
3. 若要下載 `BluemixAppID` 相依關係，請執行下列指令。

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. 開啟 Xcode 專案，並啟用金鑰鏈共用。在**專案設定**下，按一下**功能** > **金鑰鏈共用**。
5. 在**專案設定** > **資訊** > **URL 類型**下，新增 **URL 類型**。請將下列值填入 **ID** 文字框及 **URL 架構**文字框。

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. 將下列 import 新增至 `AppDelegate.swift` 檔案。

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: codeblock}

7. 將承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在應用程式中 AppDelegate 的 application:didFinishLaunchingWithOptions: 方法。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: codeblock}

    <table>
    <caption> 表 3. 說明的指令元件</caption>
      <tr>
        <th> 元件</th>
        <th> 說明</th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> 您可以在服務儀表板的**服務認證**標籤中按一下**檢視認證**，以找到此值。</td>
      </tr>
      <tr>
        <td> <i> AppID.REGION </i> </td>
        <td> 您可以在 UI 中找到您的地區。選項是 `AppID.REGION_US_SOUTH`、`AppID.REGION_UK` 或 `AppID.REGION_Sydney`。</td>
      </tr>
    </table>

8. 將下列程式碼新增至 AppDelegate 檔案。

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
    <caption> 表 4. 說明的指令元件</caption>
      <tr>
        <th> 元件</th>
        <th> 說明</th>
      </tr>
      <tr>
        <td> <i> onAuthorizationSuccess </i> </td>
        <td> 已鑑別使用者。</td>
      </tr>
      <tr>
        <td> <i> onAuthorizationCanceled </i> </td>
        <td> 使用者已取消鑑別處理程序。</td>
      </tr>
      <tr>
        <td> <i> onAuthorizationFailure </i> </td>
        <td> 發生異常狀況。</td>
      </tr>
    </table>

## 將 {{site.data.keyword.appid_short_notm}} 新增至現有 Node.js Web 應用程式
{: #existing-node}

1. 將 `bluemix-appid` 模組新增至 Node.js 應用程式。

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: codeblock}

2. 如果尚未安裝下列模組，則請予以安裝。

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. 將下列程式碼新增至 `app.js` 檔案，以：
    * 設定 express 應用程式，以使用 express-session 中介軟體。**附註**：針對正式作業環境，您必須配置具有適當階段作業儲存空間的中介軟體。如需相關資訊，請參閱 <a href="https://github.com/expressjs/session" target="_blank">expressjs 文件 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
    * 使用序列化及解除序列化來配置 passportjs。這是 HTTP 要求的已鑑別階段作業持續性的必要項目。如需相關資訊，請參閱 <a href="http://passportjs.org/docs" target="_blank">passportjs 文件 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。  
    * 在回呼 URL 上執行 get 指令，以從 {{site.data.keyword.appid_short_notm}} 服務擷取存取及身分記號。

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

    **附註**：服務會依下列順序重新導向：
    1. 已觸發鑑別處理程序的要求的原始 URL，如 `WebAppStrategy.ORIGINAL_URL` 索引鍵的 HTTP 階段作業中所持續保存。
    2. 成功重新導向，如 `passport.authenticate(name, {successRedirect: "...."})` 中所指定。
    3. 應用程式根 ("/")

4. 重新部署應用程式。


## 將 {{site.data.keyword.appid_short_notm}} 新增至現有 Swift Web 應用程式
{: #existing-swift}

1. 開啟 Swift 應用程式的目錄中的 `Package.swift` 檔案，並新增 `appid-serversdk-swift` 相依關係。例如：

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
    ```
    {: codeblock}

2. 將下列程式碼新增至 Swift 應用程式，以：
    * 設定 Kitura 以使用階段作業中介軟體。**附註**針對正式作業環境，您必須配置具有適當階段作業儲存空間的 Kitura。如需相關資訊，請參閱 <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura 文件 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
    * 在回呼 URL 上執行 get 指令，以從 {{site.data.keyword.appid_short_notm}} 服務擷取存取及身分記號。

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

  <table>
  <caption> 表 5. 說明的指令元件</caption>
    <tr>
      <th> 元件</th>
      <th> 說明</th>
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

5. 重新部署應用程式。



## 將 {{site.data.keyword.appid_short_notm}} 新增至現有 Liberty for Java 應用程式
{: #existing-liberty}

您可以配置 {{site.data.keyword.appid_short_notm}} 以使用現有的 Liberty for Java Web 應用程式。

1. 新增 <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect 特性 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 至 `server.xml`。

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. 在您的 Open ID Connect Client 特性中，定義下列位置保留元。稍後 {{site.data.keyword.Bluemix_notm}} 會自動填入它們。實例名稱變數必須完全符合您的 {{site.data.keyword.appid_short_notm}} 實例名稱。

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

  **附註**：issuerIdentifier 變數會根據您的地區而變更。它可以是下列其中一個變數：
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. 定義授權過濾器以指定受保護的資源。如果過濾器<a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">未定義 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，服務將保護所有資源。
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

3. 在您的 `server.xml` 檔案中，將特殊主旨類型定義為 ALL_AUTHENTICATED_USERS。

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

4. 在您的 `<application-bnd>` 元素中，<a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">定義角色 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，如 Web 應用程式中的樣子：`web.xml`。

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

5. 取得憑證。

    a. 在 {{site.data.keyword.appid_short_notm}} 儀表板中，按一下「服務認證」。

    b. 按一下**檢視認證**並複製 `oauthServerUrl`。

    c. 在 URL 新增 `/token`。使用 Firefox 瀏覽輸出 URL 並取得憑證。您可以使用下列 URL 作為範例。

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. 在 Firefox 位址列中，按一下鎖定圖示 > **右移鍵** > **相關資訊** > **檢視憑證**。

    e. 在**安全**標籤中，按一下**檢視憑證** > **詳細資料**。

    f. 匯出憑證然後將它儲存成本端磁碟機上的 PEM 檔案。

6. 使用 <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 將憑證新增至您的 Liberty for Java truststore.jks 檔案，並在 OIDC 元素新增憑證別名的參照。您的 `.jks` 檔案位於伺服器目錄：**resources** > **security** > **<i>truststore 檔名</i>** > **`.jks 檔`**。您可以使用下列其中一個選項，將憑證新增至檔案中。

    * 在終端機，移至 Liberty for Java security 資料夾： wlp > usr > servers > <i>servername</i> > resources > security，然後使用下列指令新增憑證。

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **附註**：`~/Documents/[certificatename].cer` 示範您本端磁碟機上的檔案位置。

    * 您可以使用 <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來新增憑證。請開啟 KeyStore Explorer 並選取 **Open an existing KeyStore**。

7. 在您的 `manifest.yml` 檔案中，定義 {{site.data.keyword.appid_short_notm}} 實例。

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

    針對 {{site.data.keyword.appid_short_notm}} 配置的範例 `server.xml` 檔案：

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



## 將 {{site.data.keyword.appid_short_notm}} 新增至不在 {{site.data.keyword.Bluemix_notm}} 上執行的現有應用程式
{: #existing}

如果您的 Node.js 或 Swift 應用程式未在 {{site.data.keyword.Bluemix_notm}} 上執行，則可以配置 WebAppStrategy 或 WebAppKituraCredentialsPlugin，以在遠端工作。對於不在 Bluemix 上執行的 Liberty for Java 應用程式，請配置 OIDC 元素變數。


在 Node.js 應用程式中，請將 `passport.use(new WebAppStrategy());` 取代為下列程式碼。

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

在 Swift 應用程式中，請將 `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` 取代為下列程式碼。

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
  <caption> 表 6. 說明的 Swift 及 Node.js 應用程式的指令元件</caption>
    <tr>
      <th> 元件</th>
      <th> 說明</th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td> 您可以在服務儀表板的**服務認證**標籤中按一下**檢視認證**，以找到這些值。</td>
    </tr>
    <tr>
      <td> <i> app-url </i> </td>
      <td> 您的應用程式 URL。</td>
    </tr>
    <tr>
      <td> <i> CALLBACK_URL </i> </td>
      <td> 使用者在登入之後看到的頁面 URL。</td>
    </tr>
  </table>

在您的 Liberty for Java 應用程式中，完成[將 {{site.data.keyword.appid_short_notm}} 新增至現有 Liberty for Java 應用程式](/docs/services/appid/existing.html#existing-liberty)底下的步驟，但將 OIDC 用戶端元素取代為下列程式碼。

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
  <caption> 表 7. 不在 Bluemix 上執行之 Liberty for Java 應用程式的 OIDC 元素變數</caption>
    <tr>
      <th> 元件</th>
      <th> 說明</th>
    </tr>
    <tr>
    <td> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> 您可以在服務儀表板的**服務認證**標籤中按一下**檢視認證**，以找到這些值。</td>
    </tr>
    <tr>
      <td> <i> authorizationEndpointURL </i> </td>
      <td> 在 oauthServerURL 尾端新增 `/authorization`。</td>
    </tr>
    <tr>
      <td> <i> tokenEndpointUrl </i> </td>
      <td> 在 oauthServerURL 尾端新增 `/token`。</td>
    </tr>
    <tr>
      <td> <i> jwkEndpointUrl </i> </td>
      <td> 在 oauthServerURL 尾端新增 `/publickeys`。</td>
    </tr>
    <tr>
      <td> <i> issuerIdentifier </i> </td>
      <td> 根據您的地區而變更。它可以是下列其中一項： </br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net" </ul></td>
    </tr>
    <tr>
      <td> <i> tokenEndpointAuthMethod </i> </td>
      <td> 指定為 "basic"。</td>
    </tr>
    <tr>
      <td> <i> signatureAlgorithm </i> </td>
      <td> 指定為 "RS256"。</td>
    </tr>
    <tr>
      <td> <i> authFilterid </i> </td>
      <td> 要保護的資源清單。</td>
    </tr>
    <tr>
      <td> <i> trustAliasName </i> </td>
      <td> 信任儲存庫內的憑證名稱。</td>
    </tr>
  </table>
