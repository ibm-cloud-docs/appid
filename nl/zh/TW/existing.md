---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 將 {{site.data.keyword.appid_short_notm}} 新增至現有應用程式

您可以搭配使用 {{site.data.keyword.appid_full}} 與現有應用程式，以鑑別及儲存使用者的設定檔資訊。


## 必要條件

* 現有 iOS Swift、Android、Node.js 或 Swift 應用程式。
* 現有 {{site.data.keyword.appid_short_notm}} 實例。


## 將 {{site.data.keyword.appid_short_notm}} 新增至現有 Android 應用程式

您可以將「應用程式 ID」服務新增至現有 Android 應用程式。

1. 將 JitPack 儲存庫新增至根 build.gradle 檔案。

  ```gradle
  allprojects {
      		repositories {
		    ...
         	 maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: pre}

2. 開啟應用程式的 build.gradle 檔案、尋找檔案的 dependencies 區段，並新增 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 的編譯相依關係。

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: pre}

3. 尋找 defaultConfig 區段，並新增下行程式碼。

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. 將專案與 Gradle 同步化。
5. 將環境定義、承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 onCreate 方法。

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
        });
  ```
  {: pre}

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

1. 在專案的目錄中，開啟 podfile。
2. 在專案的目標下，新增 'BluemixAppID' Pod 的相依關係。請確定，您的目標下也有 `use_frameworks!` 指令。
3. 若要下載 `BluemixAppID` 相依關係，請執行下列指令。

  ```
  pod install --repo-update
  ```
  {: pre}

4. 開啟 Xcode 專案，並啟用金鑰鏈共用。在**專案設定**下，按一下**功能** > **金鑰鏈共用**。
5. 在**專案設定** > **資訊** > **URL 類型**下，新增 **URL 類型**。請將下列值填入 **ID** 文字框及 **URL 架構**文字框。

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. 將下列 import 新增至 AppDelegate.swift 檔案。

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. 將承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在應用程式中 AppDelegate 的 application:didFinishLaunchingWithOptions: 方法。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

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

1. 將 `bluemix-appid` 模組新增至 Node.js 應用程式。

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. 如果尚未安裝下列模組，則請予以安裝。

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. 將下列程式碼新增至 app.js 檔案，以：
    * 設定 express 應用程式，以使用 express-session 中介軟體。**附註**：針對正式作業環境，您必須配置具有適當階段作業儲存空間的中介軟體。如需相關資訊，請參閱 [expressjs 文件](https://github.com/expressjs/session)。
    * 使用序列化及解除序列化來配置 passportjs。這是 HTTP 要求的已鑑別階段作業持續性的必要項目。如需相關資訊，請參閱 [passportjs 文件](http://passportjs.org/docs)。
    * 在回呼 URL 上執行 get 指令，以從「應用程式 ID」服務擷取存取及身分記號。

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

    **附註**：服務會依下列順序重新導向：
    1. 已觸發鑑別處理程序的要求的原始 URL，如 `WebAppStrategy.ORIGINAL_URL` 索引鍵的 HTTP 階段作業中所持續保存。
    2. 成功重新導向，如 `passport.authenticate(name, {successRedirect: "...."})` 中所指定。
    3. 應用程式根 ("/")

4. 重新部署應用程式。


## 將 {{site.data.keyword.appid_short_notm}} 新增至現有 Swift Web 應用程式

1. 開啟 Swift 應用程式的目錄中的 `Package.swift` 檔案，並新增 `appid-serversdk-swift` 相依關係。例如：

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
    ```
    {: pre}

2. 將下列程式碼新增至 Swift 應用程式，以：
    * 設定 Kitura 以使用階段作業中介軟體。**附註**針對正式作業環境，您必須配置具有適當階段作業儲存空間的 Kitura。如需相關資訊，請參閱 [Kitura 文件](https://github.com/IBM-Swift/Kitura-Session)。
    * 在回呼 URL 上執行 get 指令，以從「應用程式 ID」服務擷取存取及身分記號。

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
  <caption> 表 6. 說明的指令元件</caption>
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



## 將 {{site.data.keyword.appid_short_notm}} 新增至未在 {{site.data.keyword.Bluemix_notm}} 上執行的現有應用程式


如果您的 Node.js 或 Swift 應用程式未在 Bluemix 上執行，則可以配置 WebAppStrategy 或 WebAppKituraCredentialsPlugin，以在遠端工作。


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
{: pre}

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
  {: pre}

<table>
<caption> 表 7. 說明的 Swift 及 Node.js 應用程式的指令元件</caption>
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
