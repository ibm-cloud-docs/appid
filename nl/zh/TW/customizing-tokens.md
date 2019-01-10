---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-25"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# 自訂記號
{: #customizing-tokens}

您可以配置 {{site.data.keyword.appid_short_notm}} 記號，以符合應用程式的特定需求。
{: shortdesc}

**有哪些類型的記號？**

{{site.data.keyword.appid_short_notm}} 有不同類型的記號來保護您的應用程式。

* 存取記號：啟用與受到授權過濾器保護之後端資源的通訊。如果存取記號未與特定使用者相關聯，則記號將具備有限功能。
* 身分記號：包含個人資訊，並用來鑑別使用者。根據您的應用程式配置，可以在鑑別使用者之前發出身分記號。這可讓您在使用者登入應用程式之前，開始建立屬性與使用者的關聯。
* 重新整理記號：可以用來延長使用者不必重新鑑別的時間量。

想要進一步瞭解記號嗎？請深入閱讀[瞭解記號](authorization.html#tokens)。
{: tip}

</br>

**我的自訂作業選項是什麼？**

您可以設定有效期限有效性，或將自訂要求新增至您的記號，來自訂您的記號。請參閱下表，以查看如何配置有效期限，或繼續閱讀以瞭解對映自訂屬性。

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

</br>

**為何我想要將要求新增至記號？**

有數個您可能想要追蹤額外屬性的原因。當您與應用程式開發人員合作時，可以對映角色及許可權。或者，當您對一般使用者建置設定檔時，可以追蹤額外資訊，協助您建立個人化體驗。

</br>

**有任何安全考量嗎？**

是。因為記號是用來識別使用者並保護資源，所以記號的有效期限會影響數個不同的事物。藉由自訂記號配置，您可以確保符合安全和使用者體驗。不過，若記號曾經受損，惡意使用者會有更多時間影響您的應用程式。

想要進一步瞭解您應該做出的安全考量嗎？請參閱[自訂屬性](custom-attributes.html)。
{: tip}

</br>
</br>

## 瞭解自訂屬性及要求
{: #custom-claims}

您可以將使用者設定檔屬性對映至存取及身分記號要求。這表示，您不必移至 [/userinfo 端點](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/userInfo)或稍後取回自訂屬性，因為它們已儲存在記號中！
{: shortdesc}


**為何我要將屬性新增至要求？**

不必進行額外的網路呼叫，您的應用程式可能需要瞭解使用者或其可做之事的一切都已在記號中！如果您沒有大量資料，這會讓您更有效率。此外，在透過網路傳送這些對映屬性時，您可以確保這些屬性的完整性，因為它們是儲存在已簽署的記號中。

</br>

**我可以定義什麼類型的要求？**

{{site.data.keyword.appid_short_notm}} 提供的要求會分成數個種類，它們依其自訂作業的層次進行區分。

*已登錄要求*：在存取及身分記號中，有一些要求是由 {{site.data.keyword.appid_short_notm}} 所定義，自訂對映無法加以置換。如果您的要求受到限制，則服務會忽略它。這些要求為 `iss`、`aud`、`sub`、`iat`、`exp`、`amr` 及 `tenant`。

*受限要求*：根據要求對映至的記號，部分要求具有受到限制的自訂作業可能性。若為存取記號，`scope` 是唯一的受限要求。自訂對映無法置換它，但您可以利用自己的範圍來延伸它。當範圍要求對映至存取記號時，該值必須是字串，且不得附加 `appid_` 作為字首，否則將忽略它。在身分記號中，無法修改或置換要求 `identities` 及 `oauth_clients`。

*正規化要求*：每個身分記號都包含一組要求，其被 {{site.data.keyword.appid_short_notm}} 辨識為正規化要求。當它們可用時，它們會直接從您的身分提供者對映至記號。無法明確地省略這些要求，但自訂要求對映可以將其置換。這些要求包括 `name`、`email`、`picture`、`local` 及 `gender`。

</br>

**如何定義要求？**

每一個對映都是由資料來源物件以及用來擷取要求的金鑰所定義。每一個自訂要求都是分別針對每一個記號而設定的，並循序套用。您可以針對每一個記號最多登錄 100 個要求，而有效負載上限為 100KB。

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="構想圖示"/> 瞭解要求對映物件</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>必要</td>
        <td>定義要求的來源。它可以參照身分提供者的使用者資訊或使用者的 {{site.data.keyword.appid_short_notm}} 自訂屬性。</br> </br> 選項包括：`saml`、`cloud_directory`、`facebook`、`google`、`appid_custom`、`ibmid` 及 `attributes`。</td>
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
  2. 設定您的重新整理記號生命期限。有效期限是以天來設定，且可以是範圍 1 到 90 內的任何值。數字越小，使用者必須自行登入就越頻繁。
  3. 設定您的存取記號生命期限。有效期限是以分鐘來設定，且可以在範圍 5 到 1440 內。值越小，您就有越多保護以防記號竊取。
  4. 設定您的匿名記號生命期限。在使用者開始與您的應用程式互動時，即會將[匿名記號](/docs/services/appid/progressive.html#anonymous)指派給使用者。當使用者登入時，匿名記號中的資訊隨後會傳送至與使用者相關聯的記號。有效期限是以天來設定，且可以是介於 1 與 90 之間的任何值。

</br>

### 使用管理 API 配置記號
{: #configuring-tokens-api}

**開始之前**

確定您具有下列必備項目：

* 您的 {{site.data.keyword.appid_short_notm}} 實例的承租戶 ID。這可以在 GUI 的**服務認證**區段中找到。
* 您的 Identity and Access Management (IAM) 記號。如需協助取得 IAM 記號，請參閱 [IAM 文件](/docs/iam/apikey_iamtoken.html)。

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

  範例要求：
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
