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

# 管理登入體驗

使用登入小組件，您隨時可以更新登入流程，而不需要新增、移除或變更原始碼。使用範例應用程式中所提供的程式碼，即可立即開始進行。
{: shortdesc}

**附註**：當您配置社交身分提供者（例如 Facebook）時，[Oauth2 授權授與流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)是用來呼叫登入小組件。

</br>

## 自訂範例應用程式碼
{: #login-widget}

您可以自訂預先配置的登入畫面，以顯示您選擇的標誌及顏色。如果您要顯示自己的品牌化使用者介面，請查看[雲端目錄](/docs/services/appid/cloud-directory.html)。
{: shortdesc}

![自訂的登入體驗範例](/images/customize.gif)

若要自訂畫面，請執行下列動作：

1. 開啟 {{site.data.keyword.appid_short_notm}} 服務儀表板。
2. 選取**登入自訂**區段，您可以在其中修改登入小組件的外觀以符合公司品牌。
3. 選取本端系統中的 PNG 或 JPG 檔案，以上傳公司的標誌。建議的影像大小是 320 x 320 像素。檔案大小上限是 100 KB。
4. 從顏色選取器中選取小組件的標頭顏色，或輸入另一個顏色的十六進位碼。
5. 檢查預覽窗格，然後在滿意自訂時按一下**儲存變更**。即會顯示一則確認訊息。
6. 造訪應用程式，以驗證變更。您不需要重建應用程式。影像會儲存在 {{site.data.keyword.appid_short}} 資料庫中，並在下次呼叫登入小組件時顯示。


</br>

## 使用 Android SDK 呼叫登入小組件
{: #android}

啟用社交身分提供者之後，即可使用 Android SDK 呼叫預先配置的登入畫面。
{: shortdesc}

1. 配置身分提供者。
2. 在您的程式碼中放置下列指令。
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

## 使用 iOS Swift SDK 呼叫登入小組件
{: ios-swift}

啟用社交身分提供者之後，即可使用 iOS Swift SDK 呼叫預先配置的登入畫面。
{: shortdesc}

1. 配置身分提供者。
2. 將下列指令新增至應用程式碼。
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

## 使用 Node.js SDK 呼叫登入小組件
{: #nodejs}

啟用社交身分提供者之後，即可使用 Node.js SDK 呼叫預先配置的登入畫面。
{: shortdesc}

1. 配置身分提供者。
2. 將下列指令新增至程式碼。
    ```JavaScript
var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
    {: codeblock}


</br>

## 使用 Swift SDK 呼叫登入小組件
{: #swift}

啟用社交身分提供者之後，即可使用 Swift SDK 呼叫預先配置的登入畫面。
{: shortdesc}

WebAppKituraCredentialsPlugin 是根據 OAuth2 授權碼授與流程，而且必須用於使用瀏覽器的 Web 應用程式。此外掛程式提供工具來實作鑑別及授權流程。此外掛程式也提供機制來偵測未經鑑別的受保護資源存取嘗試，並且會自動將使用者的瀏覽器重新導向至鑑別頁面。成功鑑別之後，會將使用者帶至 Web 應用程式的回呼 URL，以使用此外掛程式自 {{site.data.keyword.appid_short_notm}} 中取得存取及身分記號。取得這些記號之後，外掛程式會將它們儲存在 HTTP 階段作業的 WebAppKituraCredentialsPlugin.AuthContext 下方。

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
