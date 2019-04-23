---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, 

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

# 在應用程式中使用自訂身分
{: #custom-auth}

當您鑑別時，可以使用自己的自訂身分提供者。您的身分提供者可以符合任何鑑別機制，只要其為 {{site.data.keyword.appid_full}} 支援之鑑別機制的替代方案，包括專屬或舊式鑑別機制。
{: shortdesc}

## 概觀
{: #custom-auth-overview}

帶入自己的身分提供者，您可以建立使用專屬通訊協定的自訂鑑別流程。您具有更多的控制權，例如您要共用的資訊，或所儲存的資訊。
{: shortdesc}

務必先[配置您的自訂提供者](/docs/services/appid?topic=appid-custom-identity)，然後再將其新增至您的應用程式。
{: tip}

### 我何時該使用此流程？
{: #custom-auth-when}

當 {{site.data.keyword.appid_short_notm}} 沒有提供特定身分提供者的直接支援時，您可以使用自訂身分流程，將鑑別通訊協定橋接至 {{site.data.keyword.appid_short_notm}} 的現有鑑別流程。例如，您要使用 GitHub 或 LinkedIn 來容許使用者登入。您可以使用身分提供者的現有 SDK 來協助使用者鑑別資訊，然後將其包裝並與 {{site.data.keyword.appid_short_notm}} 交換。

有許多情境，需要不同的鑑別流程：

 - 專屬的內部身分提供者
 - 第三方身分提供者
 - 複雜的鑑別流程，其中可以包括專屬的多因子機制

有時，舊式提供者可能會使用自己的自訂鑑別通訊協定。因為自訂身分流程會完全取消鑑別與授權的連結，所以您可以採用任何您選擇的鑑別機制，然後將產生的鑑別資訊提供給 {{site.data.keyword.appid_short_notm}}。完全不公開使用者認證。

</br>

### 在技術上，這個流程如何運作？
{: #custom-auth-tech}

自訂身分工作流程是在 Assertion Framework for OAuth 2.0 Authorization Grants [[RFC7521]](https://tools.ietf.org/html/rfc7523#section-2.1) 中定義的 JWT - Bearer 延伸授權類型上建置的。為了以使用者資訊交換 {{site.data.keyword.appid_short_notm}} 記號，您的鑑別架構會使用非對稱 RSA 金鑰組，建立與 {{site.data.keyword.appid_short_notm}} 的信任關係。一旦建立信任，您就可以使用 JWT-Bearer 授權類型，以已簽署 JWT 內的已驗證使用者資訊交換 {{site.data.keyword.appid_short_notm}} 記號。

### 流程具有怎樣的外觀？
{: #custom-auth-flow}

與所有鑑別流程一樣，自訂身分需要應用程式能夠建立與 {{site.data.keyword.appid_short_notm}} 的某種程度信任，以確保身分提供者使用者資訊的完整性。自訂身分會採用非對稱的 RSA 公開和私密金鑰組，來建立其信任關係。取決於您的架構需求，自訂身分支援兩個僅在儲存體位置與使用私密金鑰方面有所不同的信任模型。

![自訂鑑別要求流程](images/customauth.png)
圖. 自訂鑑別的要求流程

<dl>
  <dt>1. 已簽署身分提供者</dt>
    <dd>就像傳統 OAuth 2.0 流程一樣，最安全的信任模型會直接在您的身分提供者與授權伺服器之間建立關係；在此情況下，指的是 {{site.data.keyword.appid_short_notm}}。在此模型下，您的身分提供者負責儲存私密金鑰並簽署 JWT 主張。傳遞給 {{site.data.keyword.appid_short_notm}} 時，會以符合的公開金鑰來驗證這些主張，如此可確保在傳輸期間不會惡意地變更您身分提供者中的使用者資訊。</dd>
  <dt>2. 已簽署應用程式</dt>
    <dd>或者，您也可以根據應用程式與 {{site.data.keyword.appid_short_notm}} 之間的關係來建立信任模型的基礎。在此工作流程中，您的私密金鑰會儲存在伺服器端應用程式中。在成功鑑別之後，您的應用程式會負責將身分提供者回應轉換為 JWT，並在應用程式將記號傳送至 {{site.data.keyword.appid_short_notm}} 之前，以其私密金鑰進行簽署。由於這個身分提供者與 {{site.data.keyword.appid_short_notm}} 沒有關係，因此此架構會建立較弱的信任模型。雖然 {{site.data.keyword.appid_short_notm}} 可以信任伺服器端應用程式所傳送的資訊，但它無法確定資料是由身分提供者所傳送的原始資料。</dd>
</dl>


## 產生 JSON Web 記號
{: #generating-jwts}

您可以藉由產生 <a href="https://tools.ietf.org/html/rfc7515" target="blank">JSON Web 記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，來將已驗證的使用者資料轉換為自訂身分 JWT。必須使用符合您預先配置之公開金鑰的私密金鑰來簽署記號。如需記號簽署程式庫的清單，請參閱 <a href="https://jwt.io/" target="blank">jwt.io <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{: shortdesc}

### JWT 格式範例
{: #jwts-example}

記號標頭：
  ```
  {
  "alg": "RS256",
  "typ": "JOSE"
  }
  ```
  {: screen}

記號有效負載：
  ```
  {
    // Required
    iss: String, // Should reference your identity provider
    aud: String, // Must be the OAuth server URL name
    exp: Int,    // Should be a value with a short lifespan
    sub: String, // Must be the unique user ID provided by your identity provider

    // Normalized claims (optional)
    name: String
    email: String
    locale: String
    picture: String
    gender: String

    // Custom Scopes to add to access token (optional)
    scope="custom_scope1 custom_scope2"

    // Other custom claims (optional)
    role="admin"
  }
  ```
  {: screen}

  <table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> JWS 欄位</th>
  </thead>
  <tbody>
    <tr>
      <td><code>iss</code></td>
      <td>應包含身分提供者的參照。</td>
    </tr>
    <tr>
      <td><code>aud</code></td>
      <td>OAuth 伺服器 URL。格式：https://{region}.appid.cloud.ibm.com/oauth/v4/{tenantId}。</td>
    </tr>
    <tr>
      <td><code>exp</code></td>
      <td>記號有效的時間長度。基於安全考量，它應該具有短的有效期限，且是特定的。</td>
    </tr>
    <tr>
      <td><code>sub</code></td>
      <td>身分提供者所提供的唯一使用者 ID。</td>
    </tr>
    <tr>
      <td>正規化要求</td>
      <td>所有[正規化要求](/docs/services/appid?topic=appid-tokens#tokens)都是在身分記號中提供，而這個身分記號是為了回應此要求而傳回的。可使用 [`/userinfo` 端點](/docs/services/appid?topic=appid-custom-attributes#custom-attributes)來找到更多的自訂宣告。</td>
    </tr>
    <tr>
      <td>Scope</td>
      <td>依預設，所有 {{site.data.keyword.appid_short_notm}} 記號都包含一組預設範圍。您可以執行下列其中一個動作來要求額外的範圍：<ul><li> 在 JWS 記號的範圍欄位中指定範圍。</li> <li>透過 `/token` 要求的 url-form 範圍參數來指定範圍。</li></ul></td>
    </tr>
  </tbody>
  </table>

## 擷取 {{site.data.keyword.appid_short_notm}} 記號
{: #exchanging-jwts}

若要在您的自訂提供者與 {{site.data.keyword.appid_short_notm}} 之間建立橋接器，您需要具有 {{site.data.keyword.appid_short_notm}} 記號。若要取得服務記號，請使用 [`/token` 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/token)，來交換您已驗證的使用者資訊。
{: shortdesc}

  ```
  Post /token
  Content-Type: application/x-www-from-urlencoded
  grant_type=urn:ietf:params:oauth:grant-type:jwt-bearer
  assertion=<payload>
  scope="<space separated scope array>"
  ```
  {: codeblock}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 要求建構</th>
    </thead>
    <tbody>
      <tr>
        <td>Content-type</td>
        <td><code>applications/x-www-from-urlencoded</code></td>
      </tr>
      <tr>
        <td>grant_type</td>
        <td><code>urn:ietf:params:oauth:grant-type:jwt-bearer</code></td>
      </tr>
      <tr>
        <td>assertion</td>
        <td>JWS 有效負載字串。</td>
      </tr>
      <tr>
        <td>scope</td>
        <td>以空格區隔的自訂範圍清單。</td>
      </tr>
    </tbody>
  </table>
