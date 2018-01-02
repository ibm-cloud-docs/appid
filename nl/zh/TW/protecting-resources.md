---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 保護後端資源

您可以使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 來保護及存取應用程式中的端點。您也可以使用用戶端 SDK 來存取受保護資源。

**附註**：呼叫受保護資源會啟動登入小組件（必要的話）。如果已取得有效記號，則不會啟動登入小組件，並且會直接存取資源。

## 保護 Liberty for Java 中的資源
{: #protecting-liberty}

您可以使用 {{site.data.keyword.appid_short_notm}} 在 IBM Liberty for Java 應用程式中保護端點。Liberty for Java 有內建的功能，可以處理 Open ID Connect (OIDC) 要求。

開始之前：
* 您需要現有、未連結的 [IBM Liberty for Java 應用程式](https://console.bluemix.net/catalog/starters/liberty-for-java)。若要熟悉開發 Liberty for Java 應用程式，請參閱[文件](/docs/runtimes/liberty/index.html)。
* 務必要安裝 [Apache Maven](https://maven.apache.org/download.cgi)。
* 瞭解 OIDC 與 Liberty for Java 搭配運作的情形。

若要保護您的資源，請執行下列動作：

1. 從使用者介面下載 Liberty for Java 範例。範例包含具有標準 Liberty 檔案的壓縮檔案。
2. 在您擷取範例所在的目錄開啟終端機。
3. 使用 Cloud Foundry 指令行登入 {{site.data.keyword.Bluemix_notm}}。提示時，輸入您的認證。

  ```
  cf login
  ```
  {: codeblock}

4. 部署應用程式。執行下列指令會建立名稱與承租戶 ID 相關的 Liberty for Java 實例。

  ```
  cf push
  ```
  {: codeblock}

5. 將您的服務實例連結至新的 Liberty for Java 實例，然後重新部署應用程式。
6. 在瀏覽器中開啟您的應用程式，並使用您的認證登入，以檢閱鑑別活動。

## 保護 Node.js 中的資源
{: #protecting-resources-nodesdk}

{{site.data.keyword.appid_short_notm}} 伺服器 SDK 提供 {{site.data.keyword.Bluemix_notm}} 上所部署的後端應用程式中使用的 ApiStrategy 通行證策略。若要保護應用程式免於遭受未經授權的存取，您必須使用 ApiStrategy 來檢測 Node.js 伺服器。`appid-serversdk-nodejs npm 模組`提供 ApiStrategy 通行證策略及驗證方法，以驗證 {{site.data.keyword.appid_short_notm}} 所發出的存取記號及 ID 記號。

{{site.data.keyword.appid_short_notm}} 伺服器 SDK 使用 <a href="http://passportjs.org/" target="_blank">Passport 架構 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來強制執行授權。

下列 Snippet 示範如何在簡式 Express 應用程式中使用 `APIStrategy` 來保護 `/protected` 端點 GET 方法。

  ```JavaScript

var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

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


## 使用 iOS Swift SDK 存取受保護資源
{: #requesting-swift}

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
