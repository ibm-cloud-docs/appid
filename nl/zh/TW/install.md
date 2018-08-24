---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# 將 {{site.data.keyword.appid_short}} 新增至應用程式
{: #configuring}

在應用程式中設定服務，以開始使用 {{site.data.keyword.appid_short}}。
{: shortdesc}


## 設定 Android SDK
{: #android-setup}

使用 {{site.data.keyword.appid_short}} 用戶端 SDK 建置 Android 應用程式、起始設定 SDK、鑑別使用者，以及對受保護資源及未受保護資源提出要求。
{:shortdesc}


### 開始之前
{: #before-android}

您需要下列資訊：
  * {{site.data.keyword.appid_short_notm}} 服務的實例。
  * 您的承租戶 ID。您的承租戶 ID 是用來起始設定您應用程式的唯一 ID，而且可以在服務儀表板的**服務認證**標籤中找到。
  * 您的 {{site.data.keyword.Bluemix}} 地區。您可以在使用者介面中尋找，以找到您的地區。此值用於起始設定應用程式。
    <table><caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地區及對應的 SDK 值</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 地區</th>
      <th>SDK 值</th>
    </tr>
    <tr>
      <td>美國南部</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>雪梨</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>英國</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>德國</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * 設定成使用 Gradle 的 <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio 專案 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

### 安裝 SDK
{: #install-android}

1. 建立 Android Studio 專案，或開啟現有專案。
2. 將 JitPack 儲存庫新增至根 `build.gradle` 檔案。

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. 尋找您應用程式之 `build.gradle` 檔案的 dependencies 區段，並新增 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 的編譯相依關係。**附註**：請務必開啟您應用程式的檔案，而非專案 `build.gradle` 檔案。


  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
  ```
  {: codeblock}

5. 尋找 `defaultConfig` 區段，並新增下列這幾行程式碼。

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. 將專案與 Gradle 同步化。按一下**工具 > Android > 將專案與 Gradle 檔案同步化**。

### 起始設定 SDK
{: #initialize-android}

將環境定義、承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 onCreate 方法。

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> 表. 說明的指令元件</caption>
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
      <td> 您可以在 UI 中找到您的地區。選項是 `AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、`AppID.REGION_Sydney` 或 `AppID.REGION_Germany`。</td>
    </tr>
  </table>

您現在已準備好配置身分提供者，並開始鑑別使用者！如需相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub 儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。


</br>

## 設定 iOS Swift SDK
{: #ios-setup}

使用 {{site.data.keyword.appid_short}} 用戶端 SDK 建置 Swift 應用程式、起始設定 SDK、鑑別使用者，以及對受保護資源及未受保護資源提出要求。
{:shortdesc}


### 開始之前
{: #before-ios}

您需要下列資訊：
  * {{site.data.keyword.appid_short_notm}} 的實例。
  * 您的承租戶 ID。您的承租戶 ID 是用來起始設定您應用程式的唯一 ID，而且可以在服務儀表板的**服務認證**標籤中找到。
  * 您的 {{site.data.keyword.Bluemix_notm}} 地區。
  您可以在使用者介面中尋找，以找到您的地區。此值用於起始設定應用程式。
    
  <table> <caption> 表. {{site.data.keyword.Bluemix_notm}} 地區及對應的 SDK 值</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 地區</th>
      <th>SDK 值</th>
    </tr>
    <tr>
      <td>美國南部</td>
      <td><code>AppID.REGION_US_SOUTH </code></td>
    </tr>
    <tr>
      <td>雪梨</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>英國</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>德國</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Xcode 專案（9.0.1 版或更高版本）。
  * CocoaPods（1.1.0 版或更高版本）。


### 安裝 SDK
{: #install-ios}

{{site.data.keyword.appid_short_notm}} 用戶端 SDK 是使用 CocoaPods（Swift 及 Objective-C Cocoa 專案的相依關係管理程式）進行配送。CocoaPods 會下載構件，並讓它們可供您的專案使用。

1. 建立 Xcode 專案，或開啟現有專案。
2. 在專案的目錄中，開啟或建立 podfile。
3. 遵循專案的目標，新增 'IBMCloudAppID' Pod 及 `use_frameworks!` 指令的相依關係。

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. 下載 'IBMCloudAppID' 相依關係。

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. 在 Xcode 專案中啟用金鑰鏈共用。導覽至**專案設定 > 功能 > 金鑰鏈共用**，然後選取**啟用金鑰鏈共用**。
7. 開啟**專案設定 > 資訊 > URL 類型**，然後新增 **URL 類型**。將下列值同時置於 **ID** 及 **URL 架構**文字框中。
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### 起始設定 SDK
{: #initialize-ios}

1. 將承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在 Swift 應用程式中 AppDelegate 的 `application:didFinishLaunchingWithOptions` 方法。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, region: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> 表. 說明的指令元件</caption>
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
      <td> 您可以在 UI 中找到您的地區。選項是 `AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、`AppID.REGION_Sydney` 或 `AppID.REGION_Germany`。</td>
    </tr>
  </table>

2. 將下列 import 新增至 `AppDelegate` 檔案。

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. 將下列程式碼新增至 AppDelegate 檔案。

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

您現在已準備好配置身分提供者，並開始鑑別使用者！如需 iOS SDK 的相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub 儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

</br>

## 設定 Node.js SDK
{: #nodejs-setup}

### 開始之前
{: #before-nodejs}

請確定已備妥下列必要條件：
1. 安裝 [IBM Cloud CLI](../cli/index.html)。
2. 使用 <a href="http://expressjs.com/" target="_blank">Express 架構 <img src="../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 實作 Node.js 伺服器。若要安裝 Express 架構，請使用指令行來開啟含有 Node.js 應用程式的目錄，然後執行下列指令：
  ```
  npm install --save express
  ```
  {: codeblock}
3. 安裝 Passport。使用指令行，開啟含有 Node.js 應用程式的目錄，然後執行下列指令：
  ```
  npm install --save passport
  ```
  {: codeblock}

**附註**：其他架構使用 `Express` 架構（例如 LoopBack）。您可以搭配使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 與任何這些架構。


### 安裝 SDK
{: #install-nodejs}

1. 使用指令行，開啟具有 Node.js 應用程式的目錄。
2. 安裝 {{site.data.keyword.appid_short_notm}} 服務。
  ```
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### 起始設定 SDK
{: #initialize}

1. 將下列 `require` 定義新增至 `server.js` 檔案。
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. 設定 express 應用程式，以使用 express-session 中介軟體。**附註**：針對正式作業環境，您必須配置具有適當階段作業儲存空間的中介軟體。如需相關資訊，請參閱 <a href="https://github.com/expressjs/session" target="_blank">expressjs 文件 <img src="../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
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

3. 傳遞承租戶 ID 及認證來起始設定 SDK。
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

 <table summary="指令元件：Node.js 應用程式">
  <caption>Node.js 應用程式的指令元件</caption>
    <tr>
      <th>元件</th>
      <th>說明</th>
    </tr>
    <tr>
      <td><i> tenantID </i> </td>
      <td>承租戶 ID 是用來起始設定您應用程式的唯一 ID。您可以按一下**服務認證**標籤中的**檢視認證**，以在 {{site.data.keyword.appid_short_notm}} 服務儀表板中找到值。</td>
    </tr>
    <tr>
      <td><i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td>您可以在服務儀表板的**服務認證**標籤中按一下**檢視認證**，以找到這些值。</td>
    </tr>
    <tr><td><i>redirectUri</i></td>
    <td>透過三種方式，可以提供 redirectUri 值：</br>
        1. 在新的 WebAppStrategy({redirectUri: "...."}) 中手動提供</br>
        2. 作為名為 `redirectUri` 的環境變數</br>
        3. 如果未提供上述任何項目，則 App ID SDK 會嘗試擷取在 IBM Cloud 上執行之應用程式的 application_uri，並附加預設字尾 "/ibm/cloud/appid/callback"</td>
    </tr>
    <tr>
      <td><i> CALLBACK_URL </i></td> <td>使用者在登入之後看到的頁面 URL。</td>
    </tr>
  </table>

4. 使用序列化及解除序列化來配置通行證。跨 HTTP 要求的已鑑別階段作業持續性需要此配置步驟。 如需相關資訊，請參閱<a href="http://passportjs.org/docs" target="_blank">通行證文件 <img src="../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

  ```
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. 將下列程式碼新增至 `server.js` 檔案，以發出服務重新導向：
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get('/protected', passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **附註**：服務會依下列順序重新導向：
    1. 已觸發鑑別處理程序的要求的原始 URL，如 `WebAppStrategy.ORIGINAL_URL` 索引鍵的 HTTP 階段作業中所持續保存。
    2. 成功重新導向，如 `passport.authenticate(name, {successRedirect: "...."})` 中所指定。
    3. 應用程式根 ("/")

6. 重新部署應用程式。

如需相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub 儲存庫 <img src="../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

## 設定 Swift SDK
{: #swift-setup}

使用 {{site.data.keyword.appid_short}} 伺服器 SDK 保護後端及 API。
{:shortdesc}


### 開始之前
{: #before-swift}

在使用 Swift SDK 之前，您必須具有下列必備項目：

* MacOS 或 Linux
* OpenSSL 1.0.2 on Linux
* 安裝 Swift 3.0.2
* 安裝 Kitura 1.6


### 安裝 SDK
{: #install-swift}

1. 開啟 Swift 應用程式的目錄中的 `Package.swift` 檔案，並新增 `appid-serversdk-swift` 相依關係。

  ```swift
  let package = Package(
      name: “myApp",
      dependencies: [
          .package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", .upToNextMinor(from: “4.0.0")),
      ],
      targets: [
          .target(
              name: "myApp",
              dependencies: ["IBMCloudAppID"]),
      ]
  )
  ```
  {: codeblock}

2. 若為 MacOS：當您在指令行上建置時，所有套件都應該包括下列旗標。
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. 當您建立 xcodeproject 時，請使用下列指令：
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  您可以從 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 複製 openssl.xcconfig
  {: tip}

4. 將下列程式碼新增至 Swift 應用程式，以：
    * 設定 Kitura 以使用階段作業中介軟體。**附註**針對正式作業環境，您必須配置具有適當階段作業儲存空間的 Kitura。如需相關資訊，請參閱 <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura 文件 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
    * 在回呼 URL 上執行 get 指令，以從 {{site.data.keyword.appid_short_notm}} 服務擷取存取及身分記號。

    ```swift
    import Foundation
    import Kitura
    import KituraSession
    import Credentials
    import SwiftyJSON
    import IBMCloudAppID
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

5. 重新部署應用程式。

</br>

## 設定 Liberty for Java SDK
{: #lfj-setup}

您可以配置 {{site.data.keyword.appid_short_notm}} 以使用 Liberty for Java Web 應用程式。
{:shortdesc}

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

4. 在您的 `server.xml` 檔案中，將特殊主旨類型定義為 ALL_AUTHENTICATED_USERS。

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

5. 在您的 `<application-bnd>` 元素中，<a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">定義角色 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，如 Web 應用程式中的樣子：`web.xml`。

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

6. 取得憑證。

    a. 在 {{site.data.keyword.appid_short_notm}} 儀表板中，按一下「服務認證」。

    b. 按一下**檢視認證**並複製 `oauthServerUrl`。

    c. 在 URL 新增 `/token`。使用 Firefox 瀏覽輸出 URL 並取得憑證。您可以使用下列 URL 作為範例。

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. 在 Firefox 位址列中，按一下鎖定圖示 > **右移鍵** > **相關資訊** > **檢視憑證**。

    e. 在**安全**標籤中，按一下**檢視憑證** > **詳細資料**。

    f. 匯出憑證然後將它儲存成本端磁碟機上的 PEM 檔案。

7. 使用 <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 將憑證新增至您的 Liberty for Java truststore.jks 檔案，並在 OIDC 元素新增憑證別名的參照。您的 `.jks` 檔案位於伺服器目錄：**resources** > **security** > **<i>truststore 檔名</i>** > **`.jks 檔`**。您可以使用下列其中一個選項，將憑證新增至檔案中。

    * 在終端機，移至 Liberty for Java security 資料夾： wlp > usr > servers > <i>servername</i> > resources > security，然後使用下列指令新增憑證。

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **附註**：`~/Documents/[certificatename].cer` 示範您本端磁碟機上的檔案位置。

    * 您可以使用 <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來新增憑證。請開啟 KeyStore Explorer 並選取 **Open an existing KeyStore**。

    **附註**：憑證可能過期/已變更，在此情況下，您應該使用新的憑證來更新信任儲存庫。

8. 在您的 `manifest.yml` 檔案中，定義 {{site.data.keyword.appid_short_notm}} 實例。

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

  ```
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
         authFilterid="myAuthFilter"/>
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

## 將 {{site.data.keyword.appid_short_notm}} 新增至不在 {{site.data.keyword.Bluemix_notm}} 上執行的現有應用程式
{: #existing}

您可以將 {{site.data.keyword.appid_short_notm}} 新增至未在 {{site.data.keyword.Bluemix_notm}} 上執行的應用程式。您可以在本主題中看到一些範例，但這些範例並不是您可以與服務搭配使用的唯一語言。

</br>

**Node.js **

在 Node.js 應用程式中，請將 `passport.use(new WebAppStrategy());` 取代為下列程式碼。

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

  <table>
  <caption> 表. 說明之 Node.js 應用程式的指令元件</caption>
    <tr>
      <th> 元件</th>
      <th> 說明</th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> 您可以在服務儀表板的**服務認證**標籤中按一下**檢視認證**，以找到這些值。</td>
    </tr>
    <tr>
      <td><code> app-url </code></td> <td>您的應用程式 URL。</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td> <td> 使用者在登入之後看到的頁面 URL。</td>
    </tr>
  </table>

</br>

**Swift**

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
  <caption>表. 說明之 Swift 應用程式的指令元件</caption>
    <tr>
      <th> 元件</th>
      <th> 說明</th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> 您可以在服務儀表板的**服務認證**標籤中按一下**檢視認證**，以找到這些值。</td>
    </tr>
    <tr>
      <td><code> app-url </code></td> <td>您的應用程式 URL。</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td> <td> 使用者在登入之後看到的頁面 URL。</td>
    </tr>
  </table>


</br>

**Liberty for Java**

在 Liberty for Java 應用程式中，完成[設定 Liberty for Java SDK](#lfj-setup) 下的步驟，但將 OIDC 用戶端元素變數取代為下列程式碼。

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
  <caption>表. Liberty for Java 應用程式的 OIDC 元素變數</caption>
    <tr>
      <th> 元件</th>
      <th> 說明</th>
    </tr>
    <tr>
    <td><code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
    <td>您可以在服務儀表板的**服務認證**標籤中按一下**檢視認證**，以找到這些值。</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td> <td> 在 oauthServerURL 尾端新增 `/authorization`。</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td> <td>在 oauthServerURL 尾端新增 `/token`。</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td> <td>在 oauthServerURL 尾端新增 `/publickeys`。</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td> <td>根據您的地區而變更。它可以是下列其中一項： </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td> <td>指定為 "basic"。</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td> <td>指定為 "RS256"。</td>
    </tr>
    <tr>
      <td><code> authFilterid </code></td> <td>要保護的資源清單。</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td> <td>信任儲存庫內的憑證名稱。</td>
    </tr>
  </table>
