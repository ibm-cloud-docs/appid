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

# 關於
{: #about}

您可以使用 {{site.data.keyword.appid_full}}，將鑑別新增至應用程式，並保護後端資源。
{:shortdesc}

## 使用服務的原因
{: #reasons}

您為何想要使用 {{site.data.keyword.appid_short_notm}}？請參考下列情境，以查看是否有任何情境適合您。
{: shortdesc}

<table>
  <tr>
    <th> 情境</th>
    <th> 原因</th>
  </tr>
  <tr>
    <td> 您需要將[授權及鑑別](/docs/services/appid/authorization.html)新增至行動及 Web 應用程式，但沒有處於安全的背景。</td>
    <td> {{site.data.keyword.appid_short_notm}} 可讓您輕鬆地將鑑別步驟新增至應用程式。您可以使用服務與[身分提供者](/docs/services/appid/identity-providers.html)通訊，以管理應用程式的存取權。</td>
  </tr>
  <tr>
    <td> 您想要限制應用程式及後端資源的存取權。</td>
    <td> 服務可讓您[保護](/docs/services/appid/protecting-resources.html)已鑑別及匿名使用者的資源。</td>
  </tr>
  <tr>
    <td> 您想要為使用者建置個人化的應用程式體驗。</td>
    <td> 使用 {{site.data.keyword.appid_short_notm}}，您可以[儲存使用者資料](/docs/services/appid/user-profile.html)（例如其公用社交設定檔中的應用程式喜好設定或資訊），然後使用該資料來自訂您應用程式的每一個體驗。</td>
  </tr>
  <tr>
    <td> 您要讓使用者可以使用其電子郵件及密碼來存取您的應用程式。</td>
    <td> {{site.data.keyword.appid_short_notm}} 可讓您建立[雲端目錄](/docs/services/appid/cloud-directory.html)。這可讓您新增使用者對行動及 Web 應用程式的註冊及登入。雲端目錄提供架構來維護可隨著使用者族群調整的使用者登錄。使用自助的預先建置功能（例如電子郵件驗證及密碼重設），您可以確定應用程式安全地鑑別使用者。</td>
  </tr>
</table>


## 架構
{: #architecture}

使用 {{site.data.keyword.appid_short_notm}}，您可以藉由要求使用者登入，將安全等級新增至應用程式。您也可以使用伺服器 SDK 來保護後端資源。
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 架構圖](/images/appid_architecture.png)

<dl>
  <dt> 應用程式</dt>
    <dd> 伺服器 SDK：您可以使用伺服器 SDK，保護 {{site.data.keyword.Bluemix_notm}} 及 Web 應用程式上管理的後端資源。它會要求擷取存取記號，並向 {{site.data.keyword.appid_short_notm}} 驗證它。</br>
    用戶端 SDK：您可以使用 Android 或 iOS 用戶端 SDK 來保護行動應用程式。用戶端 SDK 會與您的雲端資源通訊，以在偵測到授權盤查時啟動鑑別處理程序。</dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd> App ID：在成功鑑別之後，{{site.data.keyword.appid_short_notm}} 會將存取及身分記號傳回給您的應用程式。</br>
    雲端目錄：使用者可以使用其電子郵件及密碼進行註冊，以取得您的服務。然後，您可以透過使用者介面以清單視圖管理您的使用者。</dd>
  <dt> 外部（協力廠商）</dt>
    <dd>  {{site.data.keyword.appid_short_notm}} 支援兩個社交身分提供者：Facebook 及 Google+。服務會安排重新導向至身分提供者，並在驗證鑑別之後提供應用程式的存取權。{{site.data.keyword.appid_short_notm}} 會驗證認證而不必具有實際通行詞組的存取權。</dd>
</dl>


## 要求流程
{: #request}

下圖說明要求如何從用戶端 SDK 流向後端資源及身分提供者。
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 要求流程](/images/appidrequestflow.png)


* {{site.data.keyword.appid_short_notm}} 用戶端 SDK 會對使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 保護的後端資源提出要求。
* {{site.data.keyword.appid_short_notm}} 伺服器 SDK 偵測到未獲授權的要求，並傳回 HTTP 401 及授權範圍。
* 用戶端 SDK 自動偵測到 HTTP 401，並啟動鑑別處理程序。
* 當用戶端 SDK 與服務聯絡時，如果已配置多個身分提供者，伺服器 SDK 會傳回登入小組件。{{site.data.keyword.appid_short_notm}} 呼叫身分提供者，並提出該提供者的登入表單，或是在沒有配置任何身分提供者的情況傳回一個授權碼，允許他們鑑別。
* {{site.data.keyword.appid_short_notm}} 提供鑑別盤查，以要求用戶端應用程式進行鑑別。
* 如果使用者登入時已配置身分提供者，則會由個別的 OAuth 流程來處理鑑別。
* 如果鑑別最後具有相同的授權碼，授權碼會傳送給記號端點。端點傳回兩個記號：存取記號，與身分記號。從此時起，使用用戶端 SDK 所提出的所有要求都會有新取得的授權標頭。
* 用戶端 SDK 自動重新傳送已觸發授權流程的原始要求。
* 伺服器 SDK 從要求擷取授權標頭、向服務驗證授權標頭，然後授與對後端資源的存取權。

**附註**：實作的通訊協定完全符合 OpenID Connect (OIDC) 的標準。
