---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{: tip: .tip}

# 社交
{: #setting-up-idp}

使用 {{site.data.keyword.appid_full}}，您可以配置社交身分提供者，來設定應用程式的單一登入體驗。藉由容許使用者利用其社交設定檔進行登入，他們不再需要記住不同應用程式的數個不同密碼。
{: shortdesc}


## 預設配置
{: #default}

{{site.data.keyword.appid_short_notm}} 提供預設配置，以協助您快速開始進行服務。
{: shortdesc}

預設認證是針對 Facebook 及 Google 設定。您有每天每個實例 100 次認證使用的限制。因為它們是 IBM 認證，表示只能在開發模型中使用它們。在發佈應用程式之前，請將配置更新為您自己的認證。


## 配置 Facebook
{: #facebook}

您可以配置 {{site.data.keyword.appid_short}} 服務，以使用 Facebook 作為身分提供者。
{: shortdesc}

### 從 Facebook 取得應用程式 ID 及密碼

若要使用 Facebook 作為身分提供者，您必須在 Facebook 應用程式上新增及配置網站平台。

1. 在 <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for Developers 網站 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 上登入您的帳戶。
2. 記下 Facebook 應用程式 ID 及密碼。在服務儀表板中，需要這些值才能配置 Web 專案以進行鑑別。
3. 新增 Web 平台，並輸入網站 URL。
4. 從產品清單中，選取 **Facebook 登入**。
5. 在**有效的 OAuth 重新導向 URL**欄位中，輸入授權伺服器回呼端點 URL。
6. 按一下**儲存變更**。


### 配置 {{site.data.keyword.appid_short_notm}} 進行 Facebook 鑑別

若您具有 Facebook 應用程式 ID 及密碼，並已配置 Facebook for Developers 應用程式來服務 Web 用戶端，即可在服務儀表板中編輯 Facebook 鑑別。

1. 從服務儀表板的**管理**標籤中，選取 **Facebook**，然後按一下**編輯**。
2. 輸入自 Facebook for Developers 網站取得的 Facebook 應用程式 ID 及密碼。
3. 複製 **Facebook for Developers 的重新導向 URI** 欄位中的 URI。將 URI 貼入「Facebook Developers 入口網站」的 **Facebook 登入**區段中的**有效 OAuth 重新導向 URI** 欄位。
4. 按一下**儲存**。
5. 選用項目：針對 Web 應用程式，在 **Web 應用程式重新導向 URL** 欄位中輸入重新導向 URL。此值是由開發人員所判定，並且用來在授權處理程序完成之後存取重新導向 URL。URL 必須遵循 `http` 或 `https` 架構。若要獲得更高安全等級，請使用 `https` 架構。


## 配置 Google
{: #google}

您可以配置 {{site.data.keyword.appid_short}} 服務，以使用 Google 作為身分提供者。
{: shortdesc}

### 從 Google 取得用戶端 ID 及密碼

在 <a href="https://developers.google.com/" target="_blank">Google Developers Console <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 建立專案、配置專案以服務 Web 用戶端，及取得用戶端 ID 和密碼。

1. 建立專案。
2. 將 Google+ API 新增至您的 Google 專案。
3. 將認證新增至 Google+ API。
    1. 選取 Google+ API 作為 API 的類型。
    2. 選取 **Web 瀏覽器**作為呼叫 API 的位置。
    3. 選擇**使用者資料**。
    4. 完成必要欄位以建立用戶端 ID。會同時建立密碼。
4. 記下 Google 用戶端 ID 及密碼。在認證標籤中，選取您建立的 ID 以取得密碼和用戶端 ID。

### 配置 {{site.data.keyword.appid_short}} 進行 Google 鑑別

在配置 Google 專案並取得用戶端 ID 和密碼之後，您可以編輯服務儀表板以進行 Google 鑑別。

1. 從服務儀表板的**管理**頁面中，選取 **Google**，然後按一下**編輯**。
2. 輸入自 GoogleDevelopers Console 取得的用戶端 ID 及密碼。
3. 授權 {{site.data.keyword.appid_short}} URL。
    1. 從 Google 身分提供者詳細資料複製 **Google Developer Console 的重新導向 URL**。
    2. 在您的 Google 專案的認證頁面上，選取您為此整合建立的用戶端 ID。
    3. 將來自 {{site.data.keyword.appid_short}} 的 URL 貼到**已授權的重新導向 URI** 欄位，然後按一下**儲存**。
4. 按一下**儲存**以在 {{site.data.keyword.appid_short}} 中更新您的 Google 配置。
5. 若為 Web 應用程式，在**管理**標籤中輸入重新導向 URL。授權處理程序完成之後，使用者會被傳送至這個 URL。URL 必須遵循 `http` 或 `https` 架構。若要獲得更高安全等級，請使用 `https` 架構。
