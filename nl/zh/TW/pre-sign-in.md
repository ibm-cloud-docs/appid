---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, development, user information, attributes, profiles, 

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

# 在使用者登入之前新增屬性
{: #preregister}

使用 {{site.data.keyword.appid_full}}，針對您知道即將需要存取您應用程式的使用者，您可以在其起始登入之前開始建置設定檔。
{: shortdesc}

若要進一步瞭解屬性類型，請參閱[瞭解使用者設定檔](/docs/services/appid?topic=appid-user-profile)。若要進一步瞭解自訂屬性及其安全考量，請參閱[自訂屬性](/docs/services/appid?topic=appid-custom-attributes)。
{: tip}

## 瞭解預先登錄
{: #preregister-understand}

### 為何我要使用預先登錄？
{: #preregister-why}

請考慮使用下列應用程式：您使用 {{site.data.keyword.appid_short_notm}} 來聯合 SAML 身分提供者中的現有使用者。您可能想要讓某些使用者在第一次登入應用程式時，立即具有 `admin` 存取權。為了實現此目標，您可以使用預先登錄端點來設定那些使用者的自訂 `admin` 屬性，並將管理主控台的存取權授與他們，而您不需要採取任何進一步動作。請務必考量變更預設值所可能產生的[安全問題](/docs/services/appid?topic=appid-custom-attributes#custom-attributes)。

### 如何識別使用者？
{: #preregister-identify-user}

您可以使用下列其中一項來識別您的使用者：

* 身分提供者中稱為 **GUID** 的使用者唯一 ID。雖然此 ID 一律存在且保證一定是唯一的，但不一定會隨時可用或易於瞭解。例如，Cloud Directory 會使用隨機 16 位元組 GUID。
* 如果有的話，則為使用者的**電子郵件**。

### 身分提供者提供何種資訊？
{: #preregister-idp-provide}

請參閱下表，以查看您可以使用的身分資訊類型。

<table>
  <thead>
    <tr>
      <th>身分提供者</th>
      <th>GUID</th>
      <th>電子郵件</th>
      <th>Sub</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cloud Directory</td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td></td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>自訂</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

### 如何處理 Cloud Directory？
{: #preregister-cd}


為了能夠確保預先登錄之使用者屬性的完整性，「雲端目錄」對其使用者有其他需求。只有在啟用及驗證電子郵件驗證時，才能執行預先登錄。如果您使用特定屬性來預先登錄「雲端目錄」使用者，則這些屬性適用於特定人員。如果未先驗證電子郵件，則另一位使用者可能會要求電子郵件位址，以及指派給它的任何屬性。

1. 將「雲端目錄」設為電子郵件及密碼模式。您可以在**雲端目錄**標籤的一般設定中，透過使用者介面完成此作業。您也可以透過[管理 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser) 予以設定。

2. 使用下列其中一種方式來驗證使用者電子郵件位址，以確認其身分：

  * 若要透過電子郵件來驗證使用者身分，請在服務儀表板的**雲端目錄**標籤中，將**電子郵件驗證**設為**開啟**。如果使用者由您所新增，並且在未先驗證其電子郵件的情況下登入您的應用程式，則登入會順利完成，但會刪除其預先定義的屬性。
  * 若要手動驗證使用者，您必須是管理者，並使用「雲端目錄」[管理 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser)。建立或更新使用者時，您應該在使用者資料有效負載內明確地將 `status` 欄位設為 `CONFIRMED`。

**使用自訂身分提供者時我需要執行任何特殊動作嗎？**

當您事先將使用者資訊新增至應用程式時，可以使用鑑別流程所提供的任何唯一 ID。ID 必須_完全_ 符合授權要求期間所傳送之已簽署「JSON Web 記號」的 `sub`。如果 ID 不符，則不會順利鏈結您要新增的設定檔。



## 將使用者資訊新增至應用程式
{: #preregister-add-info}

現在，您已瞭解此處理程序並考量過安全含意，請嘗試新增一位使用者。

**開始之前：**

若要使用 [/users 管理 API 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.users_search_user_profile)來新增特定使用者的自訂屬性，您必須知道下列資訊：

* 使用者即將用來登入的身分提供者。
* 身分提供者所提供的使用者唯一 ID。

使用者第一次登入應用程式時，{{site.data.keyword.appid_short_notm}} 會搜尋使用者。如果找到，則使用者會繼承您所指派的身分。如果找不到使用者，則會根據身分提供者所提供的資訊來建立新的使用者。

**若要新增使用者，請執行下列動作：**

1. 登入 IBM Cloud。
  ```
  ibmcloud login
  ```
  {: pre}

2. 執行下列指令，以尋找 IAM 記號。
  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. 對 `/users` 端點發出 POST 要求，而此端點包含使用者的說明以及您要設為 JSON 物件的屬性。

  標頭：
  ```
  POST {management-url}/management/v4/{tenantId}/users
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  內文：
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes" : {
"mealPreference":"vegeterian"
           }
       }
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="構想圖示"/> 瞭解元件</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>idp</em></code></td>
        <td>使用者將向其進行鑑別的身分提供者。選項包括：`saml`、`cloud_directory`、`facebook`、`google`、`appid_custom`、`ibmid`。</td>
      </tr>
      <tr>
        <td><code><em>idp-identity</em></code></td>
        <td>身分提供者所提供的唯一 ID。</td>
      </tr>
      <tr>
        <td><code><em>profile</em></code></td>
        <td>包含自訂屬性 JSON 對映的使用者設定檔。</td>
      </tr>
    </tbody>
  </table>

  要求範例：
  ```
  $ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
  ```
  {: screen}

3. 使用下列其中一種方式來驗證登錄成功：
  * 檢查回應中的使用者 ID。
    ```
    {
        "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
    }
    ```
    {: screen}
  * 檢查已建立的使用者設定檔。

請記住，在進行第一鑑別之前，使用者的預先定義屬性會是空的，但對於所有目的及用途而言，該使用者即是完整鑑別的使用者。您可以使用他們的唯一 ID，就像是使用已登入的使用者一樣。例如，您可以修改、搜尋或刪除設定檔。

現在，您已建立使用者與特定屬性的關聯，請嘗試[存取或更新屬性](/docs/services/appid?topic=appid-custom-attributes)！


</br>
