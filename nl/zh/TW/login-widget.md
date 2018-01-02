---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 管理登入體驗
您可以使用登入小組件，在幾分鐘內啟動並執行登入流程。您可以隨時更新小組件或佈景主題，無需新增、移除變更登入原始碼。
{: shortdesc}



## 自訂登入小組件
{: #login-widget}

您可以配置登入小組件，以顯示您選擇的標誌及顏色。
{: shortdesc}

當 {{site.data.keyword.appid_short}} 服務配置有兩個以上的身分提供者時，使用者可以在登入小組件中選取身分提供者。您可以完成下列步驟來自訂登入小組件：

1. 開啟 {{site.data.keyword.appid_short_notm}} 服務儀表板。
2. 選取**登入自訂**區段，您可以在其中修改登入小組件的外觀以符合公司品牌。
3. 選取本端系統中的 PNG 或 JPG 檔案，以上傳公司的標誌。建議的影像大小是 320 x 320 像素。檔案大小上限是 100 KB。
4. 從顏色選取器中選取小組件的標頭顏色，或輸入另一個顏色的十六進位碼。
5. 檢查預覽窗格，然後在滿意自訂時按一下**儲存變更**。即會顯示一則確認訊息。

**附註**：您不需要重建應用程式。影像會儲存在 {{site.data.keyword.appid_short}} 資料庫中，並在下次登入時顯示。

## 使用 Android SDK 執行登入小組件
{: #authenticate-android}

當您配置多個身分提供者時，會在使用者造訪您的應用程式時顯示登入小組件。預設為若您只配置一個，會將使用者重新導向至已配置的身分提供者鑑別畫面。


起始設定 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 之後，即可執行登入小組件來鑑別使用者。

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

## 使用 iOS SDK 執行登入小組件
{: #authenticate-ios}

當您配置多個身分提供者時，會在使用者造訪您的應用程式時顯示登入小組件。預設為若您只配置一個，會將使用者重新導向至已配置的身分提供者鑑別畫面。


1. 將下列 import 新增至您要在其中使用 SDK 的檔案。

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. 執行下列指令，以啟動小組件。

  ```swift
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

## 使用 Node.js SDK 執行登入小組件
{: #authenticate-nodejs}

您可以使用 `WebAppStrategy` 來保護 Web 應用程式資源。

  ```JavaScript

var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {: codeblock}


## 使用 Swift SDK 執行登入小組件
{: #authenticate-swift}

WebAppKituraCredentialsPlugin 是根據 OAuth2 authorization_code 授與流程，而且必須用於使用瀏覽器的 Web 應用程式。此外掛程式提供工具來實作鑑別及授權流程。此外掛程式也提供機制來偵測未經鑑別的受保護資源存取嘗試，並且會自動將使用者的瀏覽器重新導向至鑑別頁面。成功鑑別之後，會將使用者帶至 Web 應用程式的回呼 URL，以使用此外掛程式自 {{site.data.keyword.appid_short_notm}} 中取得存取及身分記號。取得這些記號之後，外掛程式會將它們儲存在 HTTP 階段作業的 WebAppKituraCredentialsPlugin.AuthContext 下方。

下列程式碼示範如何在 Kitura 應用程式中使用 WebAppKituraCredentialsPlugin 來保護 `/protected` 端點。

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
