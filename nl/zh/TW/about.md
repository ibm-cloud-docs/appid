---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 關於
{: #about}

應用程式安全可能非常複雜。對於大部分的開發人員而言，這是建立應用程式的其中一個最難的部分。如何才能確定您正在保護使用者的資訊？藉由將 {{site.data.keyword.appid_full}} 整合至您的應用程式，您可以保護資源並新增鑑別，即使您沒有太多安全經驗也是一樣。
{:shortdesc}


## 使用服務的原因
{: #reasons}

{{site.data.keyword.appid_short_notm}} 可協助開發人員使用幾行的程式碼輕鬆地將鑑別新增至其 Web 及行動應用程式，並保護其在 {{site.data.keyword.Bluemix_notm}} 上的雲端原生應用程式及服務。藉由要求使用者登入您的應用程式，您可以儲存使用者資料（例如應用程式喜好設定）或來自公用社交設定檔中的資訊，然後利用該資料來自訂每位使用者在應用程式內的體驗。{{site.data.keyword.appid_short_notm}} 為您提供一種登入架構，但您也可以帶入自己的特有風格登入畫面，以與雲端目錄搭配使用。
{: shortdesc}

您為何想要使用 {{site.data.keyword.appid_short_notm}}？請參考下列情境，以查看是否有任何情境適合您。


<table>
  <tr>
    <th>情境</th>
    <th>解決方案</th>
  </tr>
  <tr>
    <td>您需要將[授權及鑑別](/docs/services/appid/authorization.html)新增至行動及 Web 應用程式，但沒有處於安全的背景。</td>
    <td>{{site.data.keyword.appid_short_notm}} 可讓您輕鬆地將鑑別步驟新增至應用程式。您可以使用 API、SDK、預先建置的使用者介面或自己的品牌使用者介面，來新增應用程式的電子郵件或使用者名稱登入、社交登入或企業登入。</td>
  </tr>
  <tr>
    <td>您想要限制應用程式及後端資源的存取權。</td>
    <td>您可以使用 {{site.data.keyword.appid_short_notm}} 所提供的標準型鑑別，輕鬆地保護應用程式、後端資源及 API。</td>
  </tr>
  <tr>
    <td>您想要為使用者建置個人化的應用程式體驗。</td>
    <td>使用 {{site.data.keyword.appid_short_notm}}，您可以[儲存使用者資料](/docs/services/appid/user-profile.html)（例如其公用社交設定檔中的應用程式喜好設定或資訊），然後使用該資料來自訂您應用程式的每一個體驗。</td>
  </tr>
  <tr>
    <td>您要以可擴充的方式來管理使用者。</td>
    <td> {{site.data.keyword.appid_short_notm}} 可讓您建立[雲端目錄](/docs/services/appid/cloud-directory.html)，使您可新增應用程式的使用者註冊及登入。「雲端目錄」提供架構來維護可隨著使用者族群調整的使用者登錄。使用自助的預先建置功能（例如電子郵件驗證及密碼重設），您可以確定應用程式安全地鑑別使用者。</td>
  </tr>
</table>


## 整合
{: #integrations}

您可以使用 {{site.data.keyword.appid_short_notm}} 與其他 {{site.data.keyword.Bluemix_notm}} 供應項目搭配。
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>藉由在標準叢集中配置 Ingress，您可以在叢集層次上保護應用程式的安全。請查看 <a href="/docs/containers/cs_annotations.html#appid-auth">{{site.data.keyword.appid_short_notm}} 鑑別 Ingress 註釋</a>或<a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">發表 App ID 與 IBM Cloud Kubernetes 服務的整合 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 部落格文章以開始。</dd>
  <dt>{{site.data.keyword.openwhisk}} 及 API Connect</dt>
    <dd>使用 [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) 和 [API Connect](/docs/apis/management/manage_apis.html) 來建立 API 時，您可以在閘道而不是在應用程式碼中保護應用程式的安全。若要查看動作中的整合，請觀看 <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。</dd>
  <dt>Cloud Foundry</dt>
    <dd>試用提供的其中一個範例 Cloud Foundry 應用程式，以瞭解如何將 {{site.data.keyword.appid_short_notm}} 整合至應用程式。</dd>
  <dt>iOS Programming Guide</dt>
    <dd>您要為 Apple 開發應用程式嗎？請試用 <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS 程式設計手冊 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，以學習、實驗及加強您現有 iOS 應用程式與 {{site.data.keyword.Bluemix_notm}} 的搭配。</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>您可以使用 [{{site.data.keyword.cloudaccesstrailshort}} 服務](/docs/services/cloud-activity-tracker/index.html)，監視 {{site.data.keyword.appid_short_notm}} 中所進行的管理活動（例如儀表板配置的變更）。</dd>
  <dt>Node.js 程式設計手冊</dt>
    <dd>您要使用 Node.js 開發應用程式嗎？請試用 <a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Node.js 程式設計手冊 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，以學習、實驗及加強您現有 Node.js 應用程式與 {{site.data.keyword.Bluemix_notm}} 的搭配。</dd>
</dl>


## 架構
{: #architecture}

使用 {{site.data.keyword.appid_short_notm}}，您可以藉由要求使用者登入，將安全等級新增至應用程式。您也可以使用伺服器 SDK 或 API 來保護後端資源。
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 架構圖](/images/appid_architecture1.png)

<dl>
  <dt>應用程式</dt>
    <dd><strong>伺服器 SDK</strong>：您可以使用伺服器 SDK，來保護 {{site.data.keyword.Bluemix_notm}} 及 Web 應用程式上管理的後端資源。它會要求擷取存取記號，並向 {{site.data.keyword.appid_short_notm}} 驗證它。</br>
    <strong>用戶端 SDK</strong>：您可以使用 Android 或 iOS 用戶端 SDK 來保護行動應用程式。用戶端 SDK 會與您的雲端資源通訊，以在偵測到授權盤查時啟動鑑別處理程序。</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>：在成功鑑別之後，{{site.data.keyword.appid_short_notm}} 會將存取及身分記號傳回給您的應用程式。</br>
    <strong>雲端目錄</strong>：使用者可以使用其電子郵件及密碼進行註冊，以取得您的服務。然後，您可以透過使用者介面以清單視圖管理您的使用者。搭配雲端目錄，{{site.data.keyword.appid_short_notm}} 可以作為您的身分提供者。</dd>
  <dt>外部（協力廠商）</dt>
    <dd><strong>社交及企業身分提供者</strong>：{{site.data.keyword.appid_short_notm}} 支援 Facebook、Google+ 及 SAML 2.0 Federation 作為身分提供者選項。服務會安排重新導向至身分提供者，並驗證所傳回的鑑別記號。如果記號有效，則服務甚至不必對實際通行詞組具有存取權，即可有權存取您的應用程式。</dd>
</dl>


## 要求流程
{: #request}

雖然您的要求流程可能會根據應用程式配置而不同，但在使用 App ID 時可能會遇到三個主要流程。您可以建立行動應用程式流程、Web 應用程式流程，或使用不同的流程來保護資源。請查看一些範例流程，以查看您是否可以在配置應用程式時啟動。
{: shortdesc}

### Web 應用程式要求流程
{: #web-flow}

![{{site.data.keyword.appid_short_notm}} 要求流程](/images/web_flow1.png)

1. 藉由使用瀏覽器，使用者會執行動作來觸發對 App ID SDK 的要求。
2. 如果使用者未獲授權，則會啟動重新導向至 App ID。
3. App ID 會啟動登入小組件，並將它傳送至瀏覽器。
4. 使用者會選擇身分提供者以鑑別及完成登入處理程序。
5. 身分提供者會使用身分記號重新導向回 App ID SDK。
6. App ID SDK 會從 App ID 服務取得存取記號。
7. App ID SDK 會儲存記號，並發生重新導向。
8. 使用者會獲授與對應用程式的存取權。

### 行動要求流程
{: #mobile-flow}

![{{site.data.keyword.appid_short_notm}} 要求流程](/images/mobile_flow.png)

1. 使用者會執行動作來觸發用戶端應用程式對 App ID SDK 的要求。
2. 如果使用者沒有有效的存取記號，則 App ID SDK 會啟動授權處理程序。
3. 向使用者顯示登入小組件。
4. 藉由使用其中一個已配置的身分提供者，來鑑別使用者。
5. 使用者具有身分記號之後，SDK 就會從 App ID 服務取得存取記號。
6. 使用這兩個記號，SDK 都會重新執行要求。
7. 如果記號有效，則使用者會獲授與對應用程式的存取權。

### 受保護資源要求流程
{: #pr-flow}

![{{site.data.keyword.appid_short_notm}} 要求流程](/images/pr_flow.png)

1. 用戶端應用程式必須具有一組公開金鑰，才能提出對資源的要求。
2. 使用公開金鑰，用戶端應用程式會提出要求。
3. 如果沒有有效的存取記號，則應用程式會收到錯誤。
4. 取得有效的記號之後，用戶端應用程式就可以重新提出要求。但這次會包括記號。
5. 當應用程式可以驗證存取記號所授與的許可權時，應用程式會獲授與對受保護資源的存取權。
