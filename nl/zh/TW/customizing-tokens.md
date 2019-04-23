---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, tokens, access, claim, attributes

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


# 自訂記號
{: #customizing-tokens}

您可以配置 {{site.data.keyword.appid_short_notm}} 記號，以符合應用程式的特定需求。
{: shortdesc}

## 瞭解自訂作業
{: #understanding-customization}

{{site.data.keyword.appid_short_notm}} 使用不同類型的記號來保護您的應用程式。

* 存取記號：啟用與受到授權過濾器保護之後端資源的通訊。如果存取記號未與特定使用者相關聯，則記號將具備有限功能。
* 身分記號：包含個人資訊，並用來鑑別使用者。取決於您的應用程式配置，可以在鑑別使用者之前發出身分記號。這容許您在使用者登入應用程式之前，開始建立屬性與使用者的關聯。
* 重新整理記號：可以用來延長使用者不必重新鑑別的時間量。

想要進一步瞭解記號嗎？請深入閱讀[瞭解記號](/docs/services/appid?topic=appid-tokens#tokens)。
{: tip}


您可以透過下列方式來自訂記號：[在 GUI 中](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-ui)或使用 [API](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-api) 設定有效期限的有效性，或將自訂宣告新增至記號中。請參閱下表，以查看如何配置有效期限，或繼續閱讀以瞭解對映自訂屬性。

<table>
  <tr>
    <th>記號類型</th>
    <th>值類型</th>
    <th>預設值</th>
    <th>選項</th>
  </tr>
  <tr>
    <td>存取</td>
    <td>分鐘</td>
    <td>60</td>
    <td>介於 5 與 1440 之間的任何值</td>
  </tr>
  <tr>
    <td>身分</td>
    <td>分鐘</td>
    <td>60</td>
    <td>介於 5 與 1440 之間的任何值</td>
  </tr>
  <tr>
    <td>重新整理</td>
    <td>日</td>
    <td>30</td>
    <td>介於 1 與 9 之間的任何值</td>
  </tr>
  <tr>
    <td>匿名</td>
    <td>日</td>
    <td>30</td>
    <td>介於 1 與 9 之間的任何值</td>
  </tr>
</table>


因為記號是用來識別使用者並保護資源，所以記號的有效期限會影響數個不同的事物。自訂記號配置，您可以確保符合安全和使用者體驗。不過，若記號曾經受損，惡意使用者會有更多時間影響您的應用程式。您可以在[自訂屬性](/docs/services/appid?topic=appid-custom-attributes)中進一步瞭解安全考量。
{: important}


## 瞭解自訂屬性及要求
{: #custom-claims}

您可以將使用者設定檔屬性對映至存取及身分記號要求。這表示，您不必移至 [/userinfo 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo)或稍後取回自訂屬性，因為它們已儲存在記號中！
{: shortdesc}

### 何謂宣告？
{: #custom-claims-defined}

宣告是指實體對其本身或代表其他人發出的聲明。比方說，如果您使用身分提供者來登入應用程式，則提供者會將一組關於您對應用程式的宣告或聲明傳送給應用程式，使其可以與關於您的已知資訊形成群組。如此一來，當您登入時，就會以您配置的方式，使用您的資訊來設定應用程式。請查看下列範例，以瞭解如何將 JSON 物件格式化。

```
{
  "accessTokenClaims": [
            {
              "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
          "idTokenClaims": [
            {
              "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
  "access": {
    "expires_in": 3600
  },
  "refresh": {
    "expires_in": 2592000,
    "enabled": true
  },
  "anonymousAccess": {
    "expires_in": 2592000,
    "enabled": true
  }
}
```
{: screen}

如果您已自訂記號的有效期限資訊，則必須在每個要求中加以設定。如果您未這麼做，這個要求會置換您的現行配置，且任何尚未定義的項目都會使用預設值。
{: note}

### 為何我要將宣告新增至記號？
{: #why-custom-claims}

不必進行額外的網路呼叫，您的應用程式可能需要瞭解使用者或其可做的每一件事都已在記號中！如果您沒有大量資料，這會讓您更有效率。此外，在透過網路傳送這些對映屬性時，您可以確保這些屬性的完整性，因為它們是儲存在已簽署的記號中。


### 我可以定義哪些類型的宣告？
{: #custom-claim-types}

{{site.data.keyword.appid_short_notm}} 提供的要求會分成數個種類，它們依其自訂作業的層次進行區分。

*已登錄要求*：在存取及身分記號中，有一些要求是由 {{site.data.keyword.appid_short_notm}} 所定義，自訂對映無法加以置換。如果您的要求受到限制，則服務會忽略它。這些要求為 `iss`、`aud`、`sub`、`iat`、`exp`、`amr` 及 `tenant`。

*受限要求*：取決於要求對映至的記號，部分要求具有受限制的自訂作業可能性。若為存取記號，`scope` 是唯一的受限要求。自訂對映無法置換它，但您可以利用自己的範圍來延伸它。當範圍要求對映至存取記號時，該值必須是字串，且不得附加 `appid_` 作為字首，否則將忽略它。在身分記號中，無法修改或置換要求 `identities` 及 `oauth_clients`。

*正規化要求*：每個身分記號都包含一組要求，其被 {{site.data.keyword.appid_short_notm}} 辨識為正規化要求。當它們可用時，它們會直接從您的身分提供者對映至記號。無法明確地省略這些要求，但自訂要求對映可以將其置換。宣告包括 `name`、`email`、`picture`、`local` 及 `gender`。


### 如何將宣告對映至記號？
{: #custom-claims-mapping}

每一個對映都是由資料來源物件以及用來擷取要求的金鑰所定義。每一個自訂要求都是分別針對每一個記號而設定的，並循序套用。您可以針對每一個記號最多登錄 100 個要求，而有效負載上限為 100KB。

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="構想圖示"/> 瞭解要求對映物件</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>必要</td>
        <td>定義要求的來源。它可以參照身分提供者的使用者資訊或使用者的 {{site.data.keyword.appid_short_notm}} 自訂屬性。</br> 選項包括：`saml`、`cloud_directory`、`facebook`、`google`、`appid_custom`、`ibmid` 及 `attributes`。</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>必要</td>
        <td>定義來源資料的要求。</td>
      </tr>
    </tbody>
  </table>

您可以使用點語法，在對映中參照巢狀要求。範例：`nested.attribute`
{:tip}

</br>

## 配置 {{site.data.keyword.appid_short_notm}} 記號
{: #configuring-tokens}

您可以使用 GUI 或管理 API 來配置 {{site.data.keyword.appid_short_notm}} 記號。
{: shortdesc}


### 使用 GUI 來配置記號有效期限
{: #configuring-tokens-ui}

1. 導覽至服務儀表板。
2. 在導覽的**身分提供者**區段中，選取**管理**頁面。
3. 在**設定**標籤中，配置您的記號。
  1. 若要容許登入而不需要使用者互動，請將**重新整理記號**設為**開啟**。
  2. 設定您的重新整理記號生命期限。有效期限是以天為單位設定，且可以是範圍 1 到 90 內的任何值。數字越小，使用者必須自行登入的頻率就越高。
  3. 設定您的存取記號生命期限。有效期限是以分鐘為單位設定，且可以在範圍 5 到 1440 內。值越小，您就有越多保護以防止記號被竊取。
  4. 設定您的匿名記號生命期限。在使用者開始與您的應用程式互動時，即會將[匿名記號](/docs/services/appid?topic=appid-anonymous#anonymous)指派給使用者。當使用者登入時，匿名記號中的資訊隨後會傳送至與使用者相關聯的記號。有效期限是以天為單位設定，且可以是介於 1 與 90 之間的任何值。

</br>

### 使用管理 API 配置記號
{: #configuring-tokens-api}

**開始之前**

確定您具有下列必備項目：

* {{site.data.keyword.appid_short_notm}} 實例的承租戶 ID。您可以在 GUI 的**服務認證**區段中找到此值。
* Identity and Access Management (IAM) 記號。如需協助取得 IAM 記號，請參閱 [IAM 文件](/docs/iam?topic=iam-iamtoken_from_apikey)。

**對映您的要求**

1. 使用您的記號配置，對 `/config/tokens` 端點提出 PUT 要求。

  標頭：
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  內文：
  ```
   {
       "access": {
           "expires_in": 3600,
       },
       "refresh": {
           "expires_in": 2592000,
           "enabled": true
       },
       "anonymous": {
           "expires_in": 2592000,
           "enabled": true
       },
       "accessTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "name_id"
           }
       ],
       "idTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "attributes.uid"
           }
       ]
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="構想圖示"/> 瞭解記號配置</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>選用</td>
        <td>包含存取及身分記號之有效期限 (`expires_in`) 的物件，以分鐘為單位。</br> </br> 預設有效期限為 60 分鐘。</td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>選用</td>
          <td>包含重新整理記號之有效期限 (`expires_in`) 的物件，以日為單位。</br> </br> 預設有效期限為 30 日。</td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>選用</td>
          <td>包含匿名存取及身分記號之有效期限 (`expires_in`) 的物件，以日為單位。</br> </br> 預設有效期限為 30 日。
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>選用</td>
          <td>此陣列包含的物件是在對映與存取記號相關的要求時建立的。</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>選用</td>
          <td>此陣列包含的物件是在對映與身分記號相關的要求時建立的。</td>
      </tr>
    </tbody>
  </table>

  要求範例：
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
            }
          ],
          "idTokenClaims": [
            {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
  }' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
