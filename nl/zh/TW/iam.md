---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 管理服務存取
{: #service-access-management}

使用 {{site.data.keyword.appid_full}} 及 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 帳戶，擁有者可以管理您帳戶中的使用者存取權。
{: shortdesc}

身為帳戶擁有者，您可以在帳戶內設定原則，為不同的使用者建立不同的存取層次。例如，特定使用者可對某個實例具有**唯讀**權，但對另一個實例具有**寫入**權。您可以決定容許哪位人員可以建立、更新及刪除 {{site.data.keyword.appid_short_notm}} 的實例。

如需 IAM 的相關資訊，請參閱 [IAM 存取](/docs/iam/users_roles.html)。

## 使用者角色
{: #roles}

存取原則的範圍是基於使用者的指派角色。
{: shortdesc}

原則可讓您在不同層次授與存取權。部分選項包括：
<ul><ul>
  <li>在您的帳戶中跨所有服務實例存取</li>
  <li>存取您帳戶中的個別服務實例</li>
  <li>存取實例內的特定資源</li>
  <li>存取您帳戶中所有已啟用 IAM 功能的服務</li>
</ul></ul>

平台管理角色可讓使用者在平台層次對服務資源執行作業。例如，可以指派角色來決定誰可以建立或刪除 ID、建立實例，以及將實例連結至應用程式。下表詳述與平台管理角色產生關聯的動作。

<table>
  <tr>
    <th>平台角色</th>
    <th>許可權</th>
    <th>範例動作</th>
  </tr>
  <tr>
    <td><i>檢視者</i></td>
    <td>檢視 {{site.data.keyword.appid_short_notm}} 實例。</td>
    <td>您可以看到 Cloud Directory 使用者的資料或身分提供者配置。</td>
  </tr>
  <tr>
    <td><i>編輯者</i></td>
    <td>檢視及連結 {{site.data.keyword.appid_short_notm}} 實例。</td>
    <td>您可以將應用程式連結至 {{site.data.keyword.appid_short_notm}} 的實例。</td>
  </tr>
  <tr>
    <td><i>操作員</i></td>
    <td>建立、刪除、編輯、暫停、回復、檢視或連結 {{site.data.keyword.appid_short_notm}} 實例。</td>
    <td>您可以建立或刪除型錄中的 {{site.data.keyword.appid_short_notm}} 實例。</td>
  </tr>
  <tr>
    <td><i>管理者</i></td>
    <td>帳戶中所有服務的所有管理動作。</td>
    <td>您可以執行所有操作員動作，而且能夠將原則指派給其他使用者。</td>
  </tr>
</table>

</br>
</br>
下表詳述對映至服務存取角色的動作。服務存取角色可讓使用者存取 {{site.data.keyword.appid_short_notm}}，以及能夠呼叫 {{site.data.keyword.appid_short_notm}} API。


<table>
  <tr>
    <th>服務角色</th>
    <th>許可權</th>
    <th>範例動作</th>
  </tr>
  <tr>
    <td><i>讀者</i></td>
    <td>檢視 {{site.data.keyword.appid_short_notm}} 實例資料。</td>
    <td>可以檢視服務實例的詳細資料，例如使用者資料或身分提供者資訊。</td>
  </tr>
  <tr>
    <td> <i>作者或管理員</i></td>
    <td>檢視及變更 {{site.data.keyword.appid_short_notm}} 實例。</td>
    <td>可以執行所有「讀者」動作並編輯服務實例，例如編輯身分提供者配置。</li></ul></td>
  </tr>
</table>

如需在使用者介面中指派使用者角色的相關資訊，請參閱[管理 IAM 存取](/docs/iam/mngiam.html#iammanidaccser)。


## {{site.data.keyword.appid_short_notm}} 存取原則
{: #access}

在您的帳戶中存取 {{site.data.keyword.appid_short_notm}} 服務的每位使用者，都必須獲指派已定義 IAM 使用者角色的存取原則。該原則會決定使用者可以在您選取之服務或實例的環境定義中執行哪些動作。
{: shortdesc}

這些動作是自訂的，並由 {{site.data.keyword.Bluemix_notm}} 服務定義為可在服務中執行的作業。然後，這些動作會對映至 IAM 使用者角色。您可以使用 {{site.data.keyword.cloudaccesstrailshort}} 服務來追蹤一些採取的動作。在下表中，會對映 {{site.data.keyword.appid_short_notm}} 的動作與必要許可權。

<table>
  <tr>
    <th>動作</th>
    <th>說明</th>
    <th>必要的角色</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>檢視後置鑑別重新導向 URL。</td>
    <td>讀者、作者、管理員</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>新增或更新後置鑑別重新導向 URL。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>更新您的身分提供者配置。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>檢視您的身分提供者配置。</td>
    <td>讀者、作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>以清單方式檢視任何最近的鑑別事件。</td>
    <td>讀者、作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>檢視登入小組件配置，例如標誌和顏色。</td>
    <td>讀者、作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>更新登入小組件配置。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>檢視使用者設定檔配置。</td>
    <td>讀者、作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>檢視使用者設定檔配置。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>檢視使用者設定檔配置。</td>
    <td>讀者、作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>新增使用者至雲端目錄。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>更新雲端目錄使用者的詳細資料。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>從雲端目錄中刪除使用者。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>檢視雲端目錄電子郵件範本。</td>
    <td>讀者、作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>使用您自己的內容更新電子郵件範本。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>刪除雲端目錄電子郵件範本。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>檢視雲端目錄的 SAML 服務提供者 (SP) 中繼資料。</td>
    <td>讀者、作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>在 SAML 身分提供者的登入小組件中設定或更新映像檔。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>根據範本將電子郵件傳送給使用者。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>檢視電子郵件的寄件者詳細資料。</td>
    <td>讀者、作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>更新寄件者詳細資料。</td>
    <td>作者、管理員</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>使用使用者的使用者 ID 撤銷使用者的重新整理記號。</td>
    <td>作者、管理員</td>
  </tr>
</table>

## 追蹤對 {{site.data.keyword.appid_short_notm}} 實例的變更
{: #tracking}

您可以使用 {{site.data.keyword.cloudaccesstrailshort}} 服務來檢視、管理及審核在 {{site.data.keyword.appid_short_notm}} 實例中進行的配置活動。
{: shortdesc}

若要監視管理活動，請執行下列動作：

1. 登入您的 {{site.data.keyword.Bluemix_notm}} 帳戶。
2. 從型錄中，在與 {{site.data.keyword.appid_short_notm}} 實例相同的帳戶中佈建 {{site.data.keyword.cloudaccesstrailshort}} 服務的實例。
3. 在 {{site.data.keyword.cloudaccesstrailshort}} 儀表板中，按一下**管理**標籤。
4. 從下拉清單中，讓下列配置搜尋 {{site.data.keyword.appid_short_notm}} 所產生的事件。
    * 對於**檢視日誌**，選取**帳戶日誌**。
    * 對於**搜尋**，選取 **target.Management**。
    * 對於**過濾器**，輸入 **appid**。
5. 按一下**過濾**。


請查看下表，以取得傳送至 {{site.data.keyword.cloudaccesstrailshort}} 的事件清單。

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
    <td>檢視登入小組件使用者介面配置（包括標頭顏色及影像）。</td>
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
    <td>檢視 App ID SAML 中繼資料。</td>
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


如需服務運作方式的相關資訊，請參閱 [{{site.data.keyword.cloudaccesstrailshort}} 文件](/docs/services/cloud-activity-tracker/index.html)。

</br>
</br>

## 範例：授權另一位使用者可以存取 {{site.data.keyword.appid_short_notm}} 的實例
{: #example}

在此情境中，管理者已建立 {{site.data.keyword.appid_short_notm}} 的實例，且需要將檢視者存取權授與另一位團隊成員。
{: shortdesc}

開始之前：
* 安裝 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html)。

若要更新存取權，管理者會完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。
2. 遵循 [IAM 文件](/docs/iam/iamusermanage.html#iamusermanage)中所列出的步驟，將檢視權授與員工。
3. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的**服務認證**標籤。按一下**檢視認證**並複製 **tentantID**。
4. 在您的終端機中使用 {{site.data.keyword.Bluemix_notm}} CLI 登入。
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. 取得 IAM 記號並記下它。
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
6. 驗證團隊成員無法進行變更。
    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    結果是 403 未獲授權訊息。

若要檢視來自 CLI 的 {{site.data.keyword.appid_short_notm}} 配置，團隊成員會完成下列步驟：

1. 在您的終端機中使用 {{site.data.keyword.Bluemix_notm}} CLI，登入。
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. 取得 IAM 記號並記下它。
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. 使用 cURL 檢視 Facebook 的身分提供者配置。
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    結果為 200 訊息，其中包含身分提供者資訊。
