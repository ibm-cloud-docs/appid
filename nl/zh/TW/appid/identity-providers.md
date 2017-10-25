---

copyright:
  years: 2017
lastupdated: "2017-06-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 配置身分提供者
{: #setting-up-idp}

您可以配置 Facebook、Google、IBM ID 或這三者的組合，來設定使用者的單一登入經驗。藉由使用身分提供者，使用者可以用他們已經熟悉的認證登入。
{:shortdesc}


## 配置 Facebook 鑑別
{: #facebook}

配置 {{site.data.keyword.appid_short}} 服務，以使用 Facebook 作為身分提供者。


### 從 Facebook 取得應用程式 ID 及密碼
{: #getting-facebook-appid}

若要使用 Facebook 作為行動或 Web 應用程式上的身分提供者，您必須在 Facebook 應用程式上新增及配置網站平台。

1. 在 <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for Developers 網站 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 上登入您的帳戶。
2. 記下 Facebook 應用程式 ID 及密碼。在服務儀表板中，需要這些值才能配置 Web 專案以進行鑑別。
3. 新增 Web 平台，並輸入網站 URL。
4. 從產品清單中，選取 **Facebook 登入**。
5. 在「有效 OAuth 重新導向 URL」欄位中，輸入授權伺服器回呼端點 URL。配置服務實例之後，即可新增此值。
6. 按一下**儲存變更**。

### 配置 {{site.data.keyword.appid_short_notm}} 進行 Facebook 鑑別
{: #configuring-facebook-appid}

若您具有 Facebook 應用程式 ID 及密碼，並已配置 Facebook for Developers 應用程式來服務 Web 用戶端，即可在服務儀表板中編輯 Facebook 鑑別。

1. 從服務儀表板的**管理**標籤中，選取 **Facebook**，然後按一下**編輯**。
2. 輸入自 Facebook for Developers 網站取得的 Facebook 應用程式 ID 及密碼。
3. 複製 **Facebook for Developers 的重新導向 URI** 欄位中的 URI。將 URI 貼入「Facebook Developers 入口網站」的 **Facebook 登入**區段中的**有效 OAuth 重新導向 URI** 欄位。
4. 按一下**儲存**。
5. 選用項目：針對 Web 應用程式，在 **Web 應用程式重新導向 URL** 欄位中輸入重新導向 URL。此值是由開發人員所判定，並且用來在授權處理程序完成之後存取重新導向 URL。


## 配置 Google 鑑別
{: #google}

配置 {{site.data.keyword.appid_short_notm}} 服務，以使用 Google 作為身分提供者。


### 從 Google 取得用戶端 ID 及密碼
{: #google-client-id}

若要使用 Google 作為身分提供者，請取得 Google 用戶端 ID 及密碼，並在 Google Developer Console 中建立專案。

1. 在 <a href="https://console.developers.google.com/apis/library" target="_blank">Google Developer Console <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 中，開啟 Google 應用程式。
2. 新增 Google+ API。
3. 使用 OAuth 建立認證。在**應用程式類型**欄位中，選取 **Web 應用程式**。在**授權重新導向 URI** 欄位中，輸入{{site.data.keyword.appid_short_notm}} 重新導向 URI。您可以從服務儀表板的 Google 配置畫面中取得{{site.data.keyword.appid_short_notm}} 重新導向授權 URI。
4. 記下 Google 用戶端 ID 及密碼，並儲存變更。



### 配置 {{site.data.keyword.appid_short_notm}} 進行 Google 鑑別
{: #google-client-appid}

若您具有 Google 用戶端及密碼，並已配置 Google Developers 主控台來服務 Web 用戶端，即可在服務儀表板中編輯 Google 鑑別。

1. 從服務儀表板的**管理**標籤中，選取 **Google**，然後按一下**編輯**。
3. 輸入自 Google Developers 主控台取得的「Google 用戶端 ID」及「密碼」。
4. 複製 **Google for Developers 的重新導向 URI** 欄位中的 URI。將 URI 貼入**授權重新導向 URI** 欄位，此欄位位於「Google Developers 入口網站」的 **Web 應用程式的用戶端 ID** 區段的**重新導向**中。
5. 按一下**儲存**。
6. 選用項目：針對 Web 應用程式，在 **Web 應用程式重新導向 URI** 欄位中輸入重新導向 URI。此值是由開發人員所判定，並且用來在授權處理程序完成之後存取重新導向 URI。


## 配置 IBM ID 鑑別

若要使用 IBM ID 作為身分提供者，請使用 <a href="https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide" target="_blank">IBMid-Federation-Guide <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。如果您已有 BlueID 應用程式，請取得 BlueID 用戶端 ID 及密碼。


### 從 IBM ID 取得用戶端 ID 及密碼

若要取得用戶端 ID 及密碼，請使用下列步驟。

1. 在 <a href="https://w3.innovate.ibm.com/tools/sso/home.html" target="_blank">SSO 自助佈建程式 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 上，登入 BlueID 帳戶。
2. 登錄 BlueID 應用程式。請務必針對身分提供者選取**正式作業前**或**正式作業**。
3. 在**用戶端詳細資料**中，輸入「應用程式 ID」重新導向 URL。您可以從服務儀表板的 IBM ID 配置畫面中取得重新導向授權 URI。
4. 一定要選取**授權碼**。
5. 記下 BlueID 用戶端 ID、密碼及帳戶身分提供者類型。按一下**繼續並完成**。

### 配置進行 IBM ID 鑑別的應用程式 ID

在您具有 BlueID 用戶端及密碼並配置具有正確重新導向 URI 的 BlueID 應用程式之後，即可編輯服務儀表板的 BlueID 鑑別區段。

1. 從服務儀表板的**管理**標籤中，選取 **IBM ID**，然後按一下**編輯**。
2. 輸入 BlueID 用戶端 ID 及密碼。
3. 複製 **IBMid for Developers 的重新導向 URI** 欄位中的 URI，並將它貼入**重新導向 URI**。
4. 針對身分提供者選取**正式作業前**或**正式作業**，然後按一下**儲存**。
5. 選用項目：針對 Web 應用程式，將重新導向 URI 輸入 **Web 應用程式重新導向 URI** 欄位中。此值是由開發人員所判定，並且用來在授權之後存取重新導向 URI。
