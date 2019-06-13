---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-09"

keywords: authentication, authorization, identity, app security, secure, backend, back-end, oauth, 

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}

# 後端應用程式
{: #backend}

您可以使用 {{site.data.keyword.appid_full}} SDK 及 API 來保護後端應用程式端點及 API。
{: shortdesc}


## 瞭解流程
{: #backend-understanding}

開發後端應用程式的一部分工作是驗證您的 API 受到保護，不會遭到未獲授權的存取。{{site.data.keyword.appid_short_notm}} SDK 可讓您保護 API 端點，並確保應用程式的安全。


### 何謂流程的技術基準？
{: #backend-technical-flow}

{{site.data.keyword.appid_short_notm}} 會實作 [OAuth 2.0](https://tools.ietf.org/html/rfc6749) 及 OIDC 規格，其使用載送記號來進行鑑別及授權。這些記號會格式化為 [JSON Web 記號](https://tools.ietf.org/html/rfc7519)，其是以數位方式簽署，且包含說明正在鑑別之主題及身分提供者的要求。應用程式的 API 受存取記號及身分記號保護。需要存取 API 的用戶端可以透過 {{site.data.keyword.appid_short_notm}} 向身分提供者進行鑑別，以交換這些記號。必須驗證記號中的要求，才能授與對受保護 API 的存取權。

如需如何在 {{site.data.keyword.appid_short_notm}}中使用記號的相關資訊，請參閱[瞭解記號](/docs/services/appid?topic=appid-tokens#tokens)。
{: tip}


### 此流程具有怎樣的外觀？
{: #backend-flow}

![{{site.data.keyword.appid_short_notm}} 後端流程。影像後面依序列出步驟。](images/backend-flow.png)

1. 用戶端向 {{site.data.keyword.appid_short_notm}} 授權伺服器提出 POST 要求，以取得存取記號。POST 要求通常會採用下列格式：

  ```
  POST/oauth/v4/{tenantId}/token HTTP/1.1
  Content_type: application/x-www-form-urlencoded
  Authorization header = "Basic" + base64encode({clientId}:{secret})
  FormData = {grant_type}
  ```
  {: screen}

2. 如果客戶符合資格，則授權伺服器會傳回存取記號。

3. 用戶端會將要求傳送至受保護的資源。可以使用多種方式來傳送要求，這會隨著所使用的 HTTP 用戶端檔案庫而不同，但要求通常會採用下列格式：

  ```
  curl -H 'Authorization: Bearer {access_token}' {https://my-protected-resource.com}
  ```
  {: screen}

4. 受保護的資源或 API 會驗證記號。如果記號有效，則會將資源的存取權授與用戶端。如果無法驗證記號，則會拒絕存取。



## 使用 SDK 保護資源
{: #backend-secure}

您可以使用 {{site.data.keyword.appid_short_notm}} SDK，對伺服器端應用程式施行鑑別及授權。`ApiStrategy` 藉由在要求過程中要求驗證存取記號及身分記號，致力於保護後端資源的安全。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} Node.js SDK 與 [Passport 架構](http://www.passportjs.org/)一起使用。
{: ph data-hd-programlang='javascript'}

{{site.data.keyword.appid_short_notm}} 伺服器端 Swift SDK 提供一個用來保護後端應用程式的 API 保護中介軟體外掛程式。藉由建立 API 與中介軟體的關聯，您可以保護應用程式免於遭受未獲授權的存取。在 API 受到保護之後，中介軟體可確保驗證由 {{site.data.keyword.appid_short_notm}} 產生的記號。然後，您可以根據驗證結果來修改 API 的行為。
{: ph data-hd-programlang='swift'}

請參閱下列程式碼 Snippet，以取得如何保護 `/protectedendpoint` API 的範例。
{: ph data-hd-programlang='swift'}

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// setup routes
let router = Router()

// mandatory option to be passed in if app not deployed on IBM Cloud
let options = [
    "oauthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/d8438de6-c325-4956-ad34-abd49194affd",
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
                        "! You are logged in with " + userProfile.provider + "." +
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
{: codeblock}
{: ph data-hd-programlang='swift'}

請觀看下列視訊，瞭解如何使用 {{site.data.keyword.appid_short_notm}} 保護後端 Node 應用程式。然後，使用[簡單的 Node 應用程式範例](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02b-simple-node-backend-app)自行嘗試。
{: ph data-hd-programlang='javascript'}

<iframe class="embed-responsive-item" id="appid-backend-nodejs" title="關於 {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/jJLSgkHpZwA?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
{: ph data-hd-programlang='javascript'}


請觀看下列視訊，瞭解如何使用 {{site.data.keyword.appid_short_notm}} 保護後端 Liberty for Java 應用程式。然後，使用[簡單的 Liberty for Java 應用程式範例](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02d-simple-liberty-backend-app)自行嘗試。
{: ph data-hd-programlang='java'}

<iframe class="embed-responsive-item" id="appid-backend-liberty" title="關於 {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/QA6DY2qqLaw?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
{: ph data-hd-programlang='java'}


### 開始之前
{: #backend-secure-before}
{: ph data-hd-programlang='javascript'}

開始之前，您必須具有下列必備項目。
{: ph data-hd-programlang='javascript'}
  * {{site.data.keyword.appid_short_notm}} 的實例。
  * NPM 第 4 版或更新版本
  * Node 第 6 版或更新版本
  {: ph data-hd-programlang='javascript'}

### 安裝 SDK
{: #backend-secure-install}
{: ph data-hd-programlang='javascript'}

1. 將 {{site.data.keyword.appid_short_notm}} Node.js SDK 新增至應用程式的 `package.json` 檔案。
{: ph data-hd-programlang='javascript'}
  ```
  "dependencies": {
      "ibmcloud-appid": "^6.0.0"
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

2. 執行下列指令。
{: ph data-hd-programlang='javascript'}

  ```
  npm install
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

### 起始設定 SDK
{: #backend-secure-initialize}
{: ph data-hd-programlang='javascript'}

1. 取得您的 `oauth server url`。
  1. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的**服務認證**標籤。
  2. 如果您還沒有一組認證，請按一下**新建認證**，然後按一下**新增**來建立一組新的認證。如果已有一組認證，請跳過此步驟。
  3. 按一下**檢視認證**切換開關，以查看您的資訊。
  4. 複製 `oauth server url`，以在下一步中使用。
  {: ph data-hd-programlang='javascript'}

2. 起始設定 {{site.data.keyword.appid_short_notm}} 通行證策略，如下列範例所示。
{: ph data-hd-programlang='javascript'}
  ```javascript
  var express = require('express'); 
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy; 
  passport.use(new APIStrategy({ oauthServerUrl: "{oauth-server-url}" })); 
  var app = express();
  app.use(passport.initialize());
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}


如果您的 Node.js 應用程式在 {{site.data.keyword.cloud_notm}} 上執行，且連結至您的 {{site.data.keyword.appid_short_notm}} 實例，則不需要提供 API 策略配置。{{site.data.keyword.appid_short_notm}} 配置會使用 VCAP_SERVICES 環境變數來取得資訊。
{: tip}
{: ph data-hd-programlang='javascript'}


### 保護 API 的安全
{: #backend-secure-api-strategy}
{: ph data-hd-programlang='javascript'}

下列 Snippet 示範如何在 Express 應用程式中使用 `ApiStrategy` 來保護 `/protected` GET API。
{: ph data-hd-programlang='javascript'}

  ```javascript
   app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', { session: false }), function(request, response){
      console.log("Security context", request.appIdAuthorizationContext);
      response.send(200, "Success!");
      }
   );
   ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

當記號有效時，會呼叫要求鏈中的下一個中介軟體，並將 `appIdAuthorizationContext` 內容新增至要求物件。此內容包含原始存取記號及身分記號，以及記號的解碼有效負載資訊。
{: ph data-hd-programlang='javascript'}


## 手動保護資源
{: #backend-secure-api}

若要保護後端應用程式及受保護資源的安全，您需要驗證記號。當用戶端向您的資源傳送要求時，您可以驗證該記號符合已定義的規格。記號可能包括識別資訊、範圍或您已擁有的任何其他配置。您可以採用數種方式來驗證 {{site.data.keyword.appid_short_notm}} 存取及身分記號。如需協助，請參閱[驗證記號](/docs/services/appid?topic=appid-token-validation#token-validation)。


## 後續步驟
{: #backend-next}

在您的應用程式中安裝 {{site.data.keyword.appid_short_notm}} 之後，您幾乎已備妥可以開始鑑別使用者了！接下來，請嘗試執行下列其中一個動作：

* 配置您的[身分提供者](/docs/services/appid?topic=appid-social)
* 自訂並配置[登入小組件](/docs/services/appid?topic=appid-login-widget)
* 進一步瞭解 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK<img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>
* 進一步瞭解 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">Swift SDK<img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>
