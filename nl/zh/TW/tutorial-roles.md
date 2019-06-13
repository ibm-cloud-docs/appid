---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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


# 指導教學：設定使用者角色
{: #tutorial-roles}

當您撰寫應用程式的程式碼時，要確保對的人在對的時間具有對的存取權可能很困難。為了協助完成這項處理程序，您可以使用 {{site.data.keyword.appid_full}} 來定義自訂屬性，例如 `role`，它可讓您指派不同類型的使用者。然後，您可以使用應用程式來針對每一種類型的使用者施行不同層次的許可權。藉由使用此逐步指引，您可以瞭解如何設定使用者屬性，更新它們，然後使用 {{site.data.keyword.appid_short_notm}} API 將它們注入記號中。
{: shortdesc}

初次使用 API？請透過這個 [Postman 集合](https://github.com/ibm-cloud-security/appid-postman)來試用它們。
{: tip}

## 情境
{: #roles-scenario}

您是虛構主題公園的開發人員。您的任務是管理 [Web 應用程式](/docs/services/appid?topic=appid-web-apps)的存取，您覺得最容易達成此目的的作法是為每一種類型的使用者設定角色。您有數種不同類型的角色，例如，公園工作人員和訪客，他們全都需要不同層次的許可權。您想要能夠簡化此處理程序，並確保在使用者第一次登入應用程式時，能獲指派正確的角色。  
{: shortdesc}

沒有問題！您可以使用 {{site.data.keyword.appid_short_notm}} 的[自訂屬性特性](/docs/services/appid?topic=appid-profiles)，來儲存任何類型的使用者相關資訊。因此，由於您使用的是角色型存取控制，您可以建立一個稱為 `role` 的屬性，並指派不同的值來指定角色類型。例如，主題公園可能有 `visitors` 或 `staff`，這些可能是 `role` 屬性的不同值。然後，您可以確保應用程式碼施行您所指派的存取原則及專用權。

雖然本指導教學是專門針對 Web 應用程式及 Cloud Directory 而撰寫，但屬性可以有更廣泛的應用。自訂屬性可以是您想要的任何項目。只要不超過 10 萬個屬性，而且將它們格式化為一般 JSON 物件，您就可以儲存所有類型的資訊！
{: note}


## 開始之前
{: #roles-before}

準備好了嗎？讓我們開始吧！

開始之前，請確定您具有下列必備項目：
- {{site.data.keyword.appid_short_notm}} 服務的實例
- 一組服務認證
- 您可以存取及驗證的電子郵件位址


## 步驟 1：配置 {{site.data.keyword.appid_short_notm}} 實例
{: #roles-configure-app}

您需要先配置 {{site.data.keyword.appid_short_notm}} 的實例，然後才能開始新增 Cloud Land 使用者的屬性。
{: shortdesc}

1. 在服務儀表板的**身分提供者**標籤中，啟用 **Cloud Directory**。雖然本指導教學使用 [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)，但您也可以選擇使用任何其他 IdP，例如 [SAML](/docs/services/appid?topic=appid-enterprise)、[Facebook](/docs/services/appid?topic=appid-social#facebook)、[Google](/docs/services/appid?topic=appid-social#google) 或[自訂提供者](/docs/services/appid?topic=appid-custom-identity)。

2. 在 **Cloud Directory > 電子郵件驗證**標籤中啟用驗證，並將**容許使用者登入您的應用程式，而不需要先驗證其電子郵件位址**設為**否**。當您使用自訂屬性來設定許可權相關角色時，請確定使用者在採用您設定的屬性之前必須先驗證其身分。

3. 在**設定檔**標籤中，將**變更來自應用程式的自訂屬性**設為**已停用**。

  依預設，任何具有存取記號的人都可以變更自訂屬性。為了確保應用程式安全，您必須配置 {{site.data.keyword.appid_short_notm}}，使得只有管理者或應用程式的擁有者才能變更自訂屬性。這可防止使用者變更自己的自訂屬性及授與自己不應該具備的許可權。
  {: important}

太棒了！您的儀表板已完成配置，您可以準備開始設定角色。


## 步驟 2：在登入之前代表另一個使用者設定角色
{: #roles-set-before}

Cloud Land 有新進職員！您知道他們的一切資訊，但好幾天了他們都還沒有開始。您可以[預先登錄他們](/docs/services/appid?topic=appid-preregister)，方法是建立 {{site.data.keyword.appid_short_notm}} 使用者及設定檔來包含諸如 `staff` 角色等屬性。
{: shortdesc}

此處理程序並未完成 Cloud Directory 登錄。使用者仍必須註冊應用程式，才能繼承您所建立之設定檔中的屬性。
{: tip}

1. 使用 CLI 登入 {{site.data.keyword.cloud_notm}}。

  ```
  ibmcloud login
  ```
  {: codeblock}

2. 取得 IAM 存取記號。

  ```
  ibmcloud iam oauth-tokens
  ```
  {: codeblock}

3. 提出 POST 要求，為新使用者建立包含 `staff` 屬性的使用者設定檔。請確定您可以存取及驗證您所使用的電子郵件。

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": “user@email.com“,
    "profile": {
      "attributes" : {
“role”: “staff”
      }
    }
  }'
  ```
  {: codeblock}

  成功的回應輸出：

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. 驗證已建立具有 `staff` 角色的設定檔。

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  成功的回應內文：

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

做得好！您已為應用程式預先登錄使用者。現在，當他們以您用於預先登錄的 ID 登入應用程式時，即會建立 Cloud Directory 使用者，而且他們會繼承 {{site.data.keyword.appid_short_notm}} 使用者設定檔。接下來，請瞭解要如何更新屬性。


## 步驟 3：更新使用者屬性
{: #roles-update-attributes}

Cloud Land 正在成長！為了跟上成長的腳步，貴公司將僱用新進人員。步驟 2 中的 `staff` 使用者現在是經理。您可以透過[指派新角色](/docs/services/appid?topic=appid-profiles#profile-set-custom)來更新其設定檔。
{: shortdesc}

1. 更新設定檔。

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes" : {
“role”: “manager”
      }
    }
  }'
  ```
  {: codeblock}

3. 檢視設定檔，以驗證其已正確更新。

  ```
  curl --request POST \
  GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  成功的回應輸出：

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

做得好！


## 步驟 4：將屬性注入記號中
{: #roles-map-claims}

越來越受歡迎的主題公園持續成長中！因為新訪客及職員人數很多，您想要限制所提出的要求數。為了提高效能，您可以將使用者設定檔屬性對映至您的存取及身分記號宣告。透過對映自訂宣告，您能夠將自訂屬性儲存在記號本身。
{: shortdesc}

[記號配置](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)是廣域的，這表示它適用於具有 `role` 屬性的每一位使用者，而不論他們獲指派的實際角色為何。
{: tip}


1. 對記號配置端點提出要求。

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
           "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: codeblock}

  <table>
    <tr>
      <th>變數</th>
      <th>說明</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td> <td>承租戶 ID 是在要求中識別 {{site.data.keyword.appid_short_notm}} 實例的工具。您可以在儀表板的<em>服務認證</em> 標籤中找到您的 ID。如果您沒有設定，則可以遵循 GUI 中的步驟來建立認證。</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>對於 <code>accessTokenClaim</code> 及 <code>idTokenClaims</code>，請將來源設為 <code>attribute</code>。</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>對於 <code>accessTokenClaim</code> 及 <code>idTokenClaims</code>，請將來源宣告設為 <code>role</code>。</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>此值適用於每一個記號類型，而且必須在每一個要求中設定。如果您先前在 GUI 中設定此值，然後執行這個要求，則要求中的值會置換先前設定的值。請務必將有效期限設為正確的配置值。</td>
    </tr>
  </table>

  成功的回應輸出：

  ```
  {
      "access": {
           "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## 步驟 5：檢視存取記號
{: #roles-view-token}

您可以選擇性地檢視存取記號，以驗證步驟 4 已順利完成。
{: shortdesc}

1. 基於測試目的，使用 {{site.data.keyword.appid_short_notm}} GUI 來建立 Cloud Directory 使用者。

  1. 在**使用者**標籤中，按一下**新增使用者**。即會顯示表單。
  2. 輸入名字和姓氏、電子郵件及密碼。
  3. 按一下**儲存**。

2. 將用戶端 ID 及密碼編碼。

  1. 在 {{site.data.keyword.appid_short_notm}} GUI 的**服務認證**標籤中，複製您的用戶端 ID 及密碼。
  2. 使用 base64 編碼器來編碼您的授權資訊。
  3. 複製要在下列指令中使用的輸出。

4. 使用 API 來登入，以取得您的存取記號資訊。傳回的記號已編碼。

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: codeblock}

5. 將存取記號解碼。
  1. 複製前一個指令之回應輸出中的記號。
  2. 在瀏覽器中，導覽至 https://jwt.io/。
  3. 將記號貼到標示為**已編碼**的方框中。

6. 在**已解碼**區段中，確認您可以看到該角色。

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "role": "manager"
  }
  ```
  {: screen}



## 後續步驟
{: #roles-next}

做得很好！您已完成指導教學。接下來，您可以嘗試配置[多因子鑑別](/docs/services/appid?topic=appid-cd-mfa)，或設定[您自己的品牌 GUI](/docs/services/appid?topic=appid-branded)。
