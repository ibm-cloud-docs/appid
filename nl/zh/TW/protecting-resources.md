---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# 保護後端資源
{: #secure-back-end}

您可以使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 來保護及存取應用程式中的端點。您也可以使用用戶端 SDK 來存取受保護資源。
{: shortdesc}

呼叫受保護資源會啟動登入小組件（必要的話）。如果已取得有效記號，則不會啟動登入小組件，並且會直接存取資源。
{: tip}

## 保護 Liberty for Java 中的資源
{: #protecting-liberty}

您可以使用 {{site.data.keyword.appid_short_notm}} 在 IBM Liberty for Java 應用程式中保護端點。Liberty for Java 有內建的功能，可以處理 Open ID Connect (OIDC) 要求。
{: shortdesc}



開始之前：
* 您需要現有、未連結的 <a href="https://console.bluemix.net/catalog/starters/liberty-for-java" target="_blank">{{site.data.keyword.Bluemix_notm}} Liberty for Java 應用程式 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。若要熟悉開發 Liberty for Java 應用程式，請參閱[文件](/docs/runtimes/liberty/index.html)。
* 請確定您已安裝 <a href="https://maven.apache.org/download.cgi" target="_blank">Apache Maven <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
* 瞭解 OIDC 與 Liberty for Java 搭配運作的情形。



若要保護您的資源，請執行下列動作：

1. 從使用者介面下載 Liberty for Java 範例。此範例包含具有標準 Liberty 檔案的壓縮檔案。
2. 遵循使用者介面中提供的指示，將您的應用程式部署至 IBM-Cloud。
3. 在瀏覽器中開啟您的應用程式，並使用您的認證登入，以檢閱鑑別活動。

## 保護 Node.js 中的資源
{: #protecting-resources-nodesdk}

{{site.data.keyword.appid_short_notm}} 伺服器 SDK 提供 {{site.data.keyword.Bluemix_notm}} 上所部署的後端應用程式中使用的 ApiStrategy 通行證策略。若要保護應用程式免於遭受未經授權的存取，您必須使用 ApiStrategy 來檢測 Node.js 伺服器。`appid-serversdk-nodejs npm 模組`提供 ApiStrategy 通行證策略及驗證方法，以驗證 {{site.data.keyword.appid_short_notm}} 所發出的存取記號及 ID 記號。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 伺服器 SDK 使用 <a href="http://passportjs.org/" target="_blank">Passport 架構 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來強制執行授權。

下列 Snippet 示範如何在簡式 Express 應用程式中使用 `APIStrategy` 來保護 `/protected` 端點 GET 方法。
  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {: codeblock}


## 使用 Swift SDK 保護資源
{: #protecting-swift}

您可以使用 {{site.data.keyword.appid_short_notm}}，利用 Swift SDK 來保護伺服器端資源。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} Swift 伺服器 SDK 提供一個用來保護後端應用程式的 API 保護中介軟體外掛程式。藉由建立 API 與中介軟體的關聯，您可以保護應用程式免於未獲授權的存取。在 API 受到保護之後，中介軟體可確保驗證由 {{site.data.keyword.appid_short_notm}} 產生的記號。然後，您可以根據驗證結果來修改 API 的行為。

請參閱下列程式碼 Snippet，以取得如何保護 `/protectedendpoint` API 的範例。

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// setup routes
let router = Router()

// mandatory option to be passed in if app not deployed on IBM Cloud
let options = [
    "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/d8438de6-c325-4956-ad34-abd49194affd",
]
let apiCreds = Credentials()

// Minimum macOS version required
if #available(OSX 10.12, *) {

    // setup API protection
    let apiKituraCredentialsPlugin = APIKituraCredentialsPlugin(options: options)
    apiCreds.register(plugin: apiKituraCredentialsPlugin)

    // associate route with API protection
    router.all(middleware: apiCreds)

    // create protected API
    router.get("/protectedendpoint") { request, response, next in

        response.headers["Content-Type"] = "text/html; charset=utf-8"
        do {
            if let userProfile = request.userProfile  {
                try response.status(.OK).send(
                    "<!DOCTYPE html><html><body>" +
                        "Welcome " + userProfile.displayName  +
                        "! You are logged in with " + userProfile.provider + ".
" +
                    "</body></html>\n\n").end()
                next()
                return
            }
            try response.status(.unauthorized).send(
                "<!DOCTYPE html><html><body>” + “You are not authorized!" +
                "</body></html>\n\n").end()
        }
        catch {}
        next()
    }

    // Start server
    Kitura.addHTTPServer(onPort: 8090, with: router)

    Kitura.run()  
}
```


## 使用 iOS Swift SDK 存取受保護資源
{: #requesting-swift}

您可以使用 {{site.data.keyword.appid_short_notm}} 在 iOS Swift 應用程式中保護端點。
{: shortdesc}

1. 匯入 BMSCore。
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. 呼叫受保護的資源要求。
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## 使用 Android SDK 存取受保護資源
{: #requesting-android}

您可以使用 {{site.data.keyword.appid_short_notm}} 在 Android 應用程式中保護端點。
{: shortdesc}

1. 呼叫受保護的資源要求。
  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
	public void onSuccess (Response response) {
		//code handling the response here
  }
  @Override
	public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
		//code handling the failure here
  });
  ```
  {: codeblock}
