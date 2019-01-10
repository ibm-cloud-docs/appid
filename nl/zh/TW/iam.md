---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

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

使用 {{site.data.keyword.appid_full}} 及 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)，帳戶擁有者可以管理您帳戶中的使用者存取權。
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
    <td>檢視雲端目錄的 SAML 服務提供者 (SP) meta 資料。</td>
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
    <td>以使用者的使用者 ID 來撤銷使用者的重新整理記號。</td>
    <td>作者、管理員</td>
  </tr>
</table>

</br>

## 範例：授權另一位使用者可以存取 {{site.data.keyword.appid_short_notm}} 的實例
{: #example}

在此情境中，管理者已建立 {{site.data.keyword.appid_short_notm}} 的實例，且需要將檢視者存取權授與另一位團隊成員。
{: shortdesc}

開始之前：
* 安裝 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html)。

若要更新存取權，管理者會完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。
2. 遵循 [IAM 文件](/docs/iam/mngiam.html)中所列出的步驟，將檢視權授與員工。
3. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的**服務認證**標籤。按一下**檢視認證**並複製 **tentantID**。
4. 在您的終端機中使用 {{site.data.keyword.Bluemix_notm}} CLI 登入。
    ```
    ibmcloud login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. 取得 IAM 記號並記下它。
    ```
    ibmcloud iam oauth-tokens
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
    ibmcloud login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. 取得 IAM 記號並記下它。
    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}
3. 使用 cURL 檢視 Facebook 的身分提供者配置。
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    結果為 200 訊息，其中包含身分提供者資訊。
