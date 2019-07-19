---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: Authentication, authorization, identity, app security, secure, application identity, app to app, access token, activity

subcollection: appid

---

{:external: target="_blank" .external}
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


# {{site.data.keyword.cloudaccesstrailshort}} 事件
{: #at-events}

您可以使用 {{site.data.keyword.cloudaccesstrailshort}} 服務，來檢視、管理及分析在 {{site.data.keyword.appid_full}} 服務實例中進行的使用者起始活動。
{: shortdesc}





如需服務運作方式的相關資訊，請參閱 [{{site.data.keyword.cloudaccesstrailshort}} 文件](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started)。






## 檢視管理事件
{: #at-monitor-admin}

您可以使用 {{site.data.keyword.at_short}} 服務，來檢視、管理及分析在 {{site.data.keyword.appid_short_notm}} 實例中進行的配置活動。
{: shortdesc}

若要監視管理活動，請執行下列動作：

1. 登入您的 {{site.data.keyword.cloud_notm}} 帳戶。
2. 從型錄中，在與 {{site.data.keyword.appid_short_notm}} 實例相同的帳戶中佈建 {{site.data.keyword.cloudaccesstrailshort}} 服務的實例。
3. 在 {{site.data.keyword.cloudaccesstrailshort}} 儀表板中，按一下**管理**標籤。
4. 從下拉清單中，讓下列配置搜尋 {{site.data.keyword.appid_short_notm}} 所產生的事件。
    * 對於**檢視日誌**，選取**帳戶日誌**。
    * 對於**搜尋**，選取 **target.Management**。
    * 對於**過濾器**，輸入 `appid`。
5. 按一下**過濾**。

</br>

## 管理事件清單
{: #at-events-admin}

請參閱下表，以取得傳送至 {{site.data.cloudaccesstrailshort}} 的事件清單。

<table>
  <tr>
    <th>動作</th>
    <th>說明</th>
    <th>使用者介面位置</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>檢視最近的活動。</td>
    <td>可在<strong>概觀</strong>標籤的<strong>活動日誌</strong>框中找到。</td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>檢視身分提供者配置。</td>
    <td>可在<strong>身分提供者 > 管理</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>更新身分提供者配置。</td>
    <td>可在<strong>身分提供者 > 管理</strong>標籤中更新。</td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>檢視記號有效期限配置。</td>
    <td>可在<strong>身分提供者 > 記號有效期限</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>檢視使用者設定檔儲存空間配置。</td>
    <td>可在<strong>概觀</strong>標籤的<strong>活動日誌</strong>中找到。</td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>更新使用者設定檔儲存空間配置。</td>
    <td>可在<strong>設定檔</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>檢視登入小組件標頭的佈景主題顏色。</td>
    <td>可在<strong>登入自訂</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>更新登入小組件標頭的佈景主題顏色。</td>
    <td>可在<strong>登入自訂</strong>標籤中更新。</td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>檢視登入小組件中所顯示的映像檔。</td>
    <td>可在<strong>登入自訂</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>更新登入小組件中所顯示的映像檔。</td>
    <td>可在<strong>登入自訂</strong>標籤中更新。</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>檢視登入小組件使用者介面配置，其中包括標頭顏色及影像。</td>
    <td>可在<strong>登入自訂</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>檢視所支援語言的清單。</td>
    <td>必須從 API 檢視。</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>更新您支援的語言。</td>
    <td>必須透過 API 更新。</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>檢視 {{site.data.keyword.appid_short_notm}} SAML meta 資料。</td>
    <td>可在<strong>身分提供者 > SAML 2.0 Federation</strong> 標籤中找到。</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>檢視「雲端目錄」使用者。</td>
    <td>可在<strong>使用者</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>更新「雲端目錄」使用者。</td>
    <td>可在<strong>使用者</strong>標籤中更新。</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>刪除「雲端目錄」使用者。</td>
    <td>可在<strong>使用者</strong>標籤中刪除。</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>檢視您的「雲端目錄」使用者清單。</td>
    <td>可在<strong>使用者</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>更新您的「雲端目錄」使用者清單。</td>
    <td>可在<strong>使用者</strong>標籤中更新。</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>刪除「雲端目錄」使用者清單。</td>
    <td>可在<strong>使用者</strong>標籤中刪除。</td>
  </tr>
  <tr>
    <td><code>read.emailTemplate</code></td>
    <td>檢視電子郵件範本。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 範本</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.emailTemplate</code></td>
    <td>更新電子郵件範本。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 範本</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>delete.emailTemplate</code></td>
    <td>刪除要重設為預設值的電子郵件範本。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 範本</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>read.senderDetails</code></td>
    <td>檢視寄件者詳細資料。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 設定</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.senderDetails</code></td>
    <td>更新寄件者詳細資料</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 設定</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.resendNotification</code></td>
    <td>重新傳送使用者通知。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 設定</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>更新忘記密碼處理程序。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 設定</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>檢視忘記密碼確認結果。</td>
    <td>必須透過 API 執行。</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>更新註冊處理程序。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 設定</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>檢視註冊結果確認。</td>
    <td>必須透過 API 執行。</td>
  </tr>
  <tr>
    <td><code>read.action_url</code></td>
    <td>檢視在執行動作時所呼叫的自訂 URL。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 自訂登陸頁面</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>更新在執行動作時所呼叫的自訂 URL。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 設定</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.changePassword</code></td>
    <td>變更「雲端目錄」使用者密碼。</td>
    <td>可在<strong>身分提供者 > 雲端目錄 > 設定</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>read.loginWidgetConfig</code></td>
    <td>檢視您的登入小組件配置。</td>
    <td>可在<strong>登入自訂</strong>標籤中找到。</td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>更新您的登入小組件配置。</td>
    <td>可在<strong>登入自訂</strong>標籤中更新。</td>
  </tr>
</table>



