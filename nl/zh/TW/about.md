---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-27"

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
    <td> {{site.data.keyword.appid_short_notm}} 可讓您建立[雲端目錄](/docs/services/appid/cloud-directory.html)，使您可新增使用者註冊並登入至您的應用程式。雲端目錄提供架構來維護可隨著使用者族群調整的使用者登錄。使用自助的預先建置功能（例如電子郵件驗證及密碼重設），您可以確定應用程式安全地鑑別使用者。</td>
  </tr>
</table>


## 整合
{: #integrations}

您可以使用 {{site.data.keyword.appid_short_notm}} 與其他 {{site.data.keyword.Bluemix_notm}} 供應項目搭配。
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>藉由在標準叢集中配置 Ingress，您可以在叢集層次上保護應用程式的安全。請查看 {{site.data.keyword.appid_short_notm}} 鑑別 Ingress 註釋以開始。</dd>
  <dt>{{site.data.keyword.openwhisk}} 及 API Connect</dt>
    <dd>使用 [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) 和 [API Connect](/docs/apis/management/manage_apis.html) 來建立 API 時，您可以在閘道而不是在應用程式碼中保護應用程式的安全。若要查看動作中的整合，請觀看 <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。</dd>
  <dt>Cloud Foundry</dt>
    <dd>試用我們的其中一個範例 Cloud Foundry 應用程式，以瞭解如何將 App ID 整合至應用程式。</dd>
  <dt>iOS Programming Guide</dt>
    <dd>您要為 Apple 開發應用程式嗎？請嘗試 <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS Programming Guide <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，以學習、實驗及加強您現有的 iOS 應用程式與 {{site.data.keyword.Bluemix_notm}} 的搭配。</dd>
</dl>


## 架構
{: #architecture}

使用 {{site.data.keyword.appid_short_notm}}，您可以藉由要求使用者登入，將安全等級新增至應用程式。您也可以使用伺服器 SDK 來保護後端資源。
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 架構圖](/images/appid_architecture.png)

<dl>
  <dt> 應用程式</dt>
    <dd><strong>伺服器 SDK</strong>：您可以使用伺服器 SDK，來保護 {{site.data.keyword.Bluemix_notm}} 及 Web 應用程式上管理的後端資源。它會要求擷取存取記號，並向 {{site.data.keyword.appid_short_notm}} 驗證它。</br>
    <strong>用戶端 SDK</strong>：您可以使用 Android 或 iOS 用戶端 SDK 來保護行動應用程式。用戶端 SDK 會與您的雲端資源通訊，以在偵測到授權盤查時啟動鑑別處理程序。</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>：在成功鑑別之後，{{site.data.keyword.appid_short_notm}} 會將存取及身分記號傳回給您的應用程式。</br>
    <strong>雲端目錄</strong>：使用者可以使用其電子郵件及密碼進行註冊，以取得您的服務。然後，您可以透過使用者介面以清單視圖管理您的使用者。搭配雲端目錄，{{site.data.keyword.appid_short_notm}} 可以作為您的身分提供者。</dd>
  <dt>外部（協力廠商）</dt>
    <dd><strong>社交及企業身分提供者</strong>：{{site.data.keyword.appid_short_notm}} 支援兩種社交身分提供者：Facebook 及 Google+，以及一種企業身分提供者：SAML 2.0 Federation。服務會安排重新導向至身分提供者，並驗證所傳回的鑑別記號。如果記號有效，則服務甚至不必對實際通行詞組具有存取權，即可有權存取您的應用程式。</dd>
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
