---

copyright:
  years: 2017
lastupdated: "2017-11-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 關於
{: #about}

{{site.data.keyword.appid_full}} 讓您能以對使用者友善的方式管理應用程式的存取權。
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
    <td> 您想要新增行動及 Web 應用程式的安全。</td>
    <td> {{site.data.keyword.appid_short_notm}} 讓您能輕鬆為應用程式新增鑑別步驟。您可以使用服務與身分提供者通訊，以管理應用程式的存取權。</td>
  </tr>
  <tr>
    <td> 您想要限制應用程式及後端資源的存取權。</td>
    <td> 服務讓您能保護已鑑別及匿名使用者的資源。</td>
  </tr>
  <tr>
    <td> 您想要為使用者建置個人化的應用程式體驗。</td>
    <td> {{site.data.keyword.appid_short_notm}} 容許您儲存使用者資料（例如其公用社交設定檔中的應用程式喜好設定或資訊）。您可以使用該資料來確定使用者擁有為他們而自訂的體驗。</td>
  </tr>
</table>

**附註**：實作的通訊協定完全符合 OpenID Connect (OIDC) 的標準。


## 架構
{: #architecture}

使用 {{site.data.keyword.appid_short_notm}}，您可以藉由要求使用者登入，為您的應用程式增加一個安全等級。您也可以使用伺服器 SDK 來保護後端資源。

下圖顯示 {{site.data.keyword.appid_short_notm}} 服務運作方式的概觀。


![{{site.data.keyword.appid_short_notm}} 架構圖](/images/appid_architecture2.png)

圖 1. {{site.data.keyword.appid_short_notm}} 架構圖



<dl>
  <dt> 應用程式</dt>
    <dd> 用戶端 SDK 提供要求類別以便與您的雲端資源通訊。用戶端 SDK 會在偵測到授權盤查時自動開始鑑別處理程序。</dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd>  伺服器 SDK 從要求擷取存取記號，並向 {{site.data.keyword.appid_short_notm}} 驗證它。成功鑑別之後，{{site.data.keyword.appid_short_notm}} 會傳回存取及身分記號給您的應用程式。</dd>
  <dt> 身分提供者</dt>
    <dd> 服務會安排對身分提供者的重新導向，並驗證鑑別以提供應用程式的存取權。{{site.data.keyword.appid_short_notm}} 會驗證認證而不必具有實際通行詞組的存取權。</dd>
</dl>


## 要求流程
{: #request}

下圖說明要求如何從用戶端 SDK 流向後端應用程式及身分提供者。

![{{site.data.keyword.appid_short_notm}} 要求流程](/images/appidrequestflow.png)

圖 2. {{site.data.keyword.appid_short_notm}} 要求流程


* {{site.data.keyword.appid_short_notm}} 用戶端 SDK 會對使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 保護的後端資源提出要求。
* {{site.data.keyword.appid_short_notm}} 伺服器 SDK 偵測到未獲授權的要求，並傳回 HTTP 401 及授權範圍。
* 用戶端 SDK 自動偵測到 HTTP 401，並啟動鑑別處理程序。
* 當用戶端 SDK 與服務聯絡時，如果已配置多個身分提供者，伺服器 SDK 會傳回登入小組件。{{site.data.keyword.appid_short_notm}} 呼叫身分提供者，並提出該提供者的登入表單，或是在沒有配置任何身分提供者的情況傳回一個授權碼，允許他們鑑別。
* {{site.data.keyword.appid_short_notm}} 提供鑑別盤查，以要求用戶端應用程式進行鑑別。
* 如果使用者登入時已配置身分提供者，則會由個別的 OAuth 流程來處理鑑別。
* 如果鑑別最後具有相同的授權碼，授權碼會傳送給記號端點。端點傳回兩個記號：存取記號，與身分記號。從此時起，使用用戶端 SDK 所提出的所有要求都會有新取得的授權標頭。
* 用戶端 SDK 自動重新傳送已觸發授權流程的原始要求。
* 伺服器 SDK 從要求擷取授權標頭、向服務驗證授權標頭，然後授與對後端資源的存取權。


## 元件
{: #components}

服務包含下列元件。

<dl>
  <dt> 儀表板</dt>
    <dd> 在服務儀表板中，您可以下載上線範例、查看活動日誌，以及配置鑑別及身分提供者。</dd>
  <dt> 用戶端 SDK</dt>
    <dd> 您可以使用用戶端 SDK 搭配您的行動及 Web 應用程式，來實作使用者鑑別。</br></br>
    Android 的必要條件：
    <ul><ul><li> API 25 或更高版本</li>
    <li> Java 8.x </li>
    <li> Android SDK 工具 25.2.5 或更高版本</li>
    <li> Android SDK 平台工具 25.0.3 或更高版本</li>
    <li> Android Build Tools 25.0.2 版或更高版本</li></ul></ul></br>
    iOS 的必要條件：
    </br>
    <ul><ul><li> iOS9 或更高版本</li>
    <li> MacOS 10.11.5 </li>
    <li>Xcode 8.2 </li></ul></ul></dd>
  <dt> 伺服器 SDK</dt>
    <dd> 您可以保護 {{site.data.keyword.Bluemix_notm}} 上所裝載的後端資源</br>
    支援的運行環境：
    <ul><ul><li> Node.js </li>
    <li> Liberty for Java </li>
    <li> Swift </li></ul></ul></dd>
</dl>
