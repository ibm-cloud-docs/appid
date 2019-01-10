---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}




# 主要概念
{: #key-concepts}

對授權與鑑別之間的差異感到困惑嗎？不是只有您而已。請參閱此頁面上的資訊，以瞭解特定術語、處理程序，以及服務使用記號的方式。
{: shortdesc}


## 術語
{: #terms}


這些重要詞彙可協助您瞭解服務中斷授權及鑑別處理程序的方式。

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 是用來提供應用程式授權的開放式標準通訊協定。</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 是比 OAuth 2 優先使用的鑑別層。</p>
    <p>當您同時使用 OIDC 及 {{site.data.keyword.appid_short_notm}} 時，您的服務認證有助於配置 OAuth 端點。當您使用 SDK 時，會自動建置端點 URL。但是，您也可以使用服務憑證自行建置 URL。您可以在下列範例及表格中看到如何組合 URL。</p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
      "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
      "profilesUrl": "https://appid-profiles.ng.bluemix.net/"
    }</code></pre>
    <table>
      <tr>
        <th>端點</th>
        <th>格式</th>
      </tr>
      <tr>
        <td>授權</td>
        <td>{oauthServerUrl}/authorization</td>
      </tr>
      <tr>
        <td>記號</td>
        <td>{oauthServerUrl}/token</td>
      </tr>
      <tr>
        <td>Userinfo</td>
        <td>{oauthServerUrl}/userinfo</td>
      </tr>
      <tr>
        <td>JWKS</td>
        <td>{oauthServerUrl}/publickeys</td>
      </tr>
    </table>
    <p><strong>附註</strong>：當您使用 SDK 時，會自動建置端點 URL。</p></dd>
  <dt>記號</dt>
    <dd>服務使用三種不同類型的記號。存取記號代表授權，並啟用與[後端資源](/docs/services/appid/backend-apps.html)的通訊，這些資源會受到 {{site.data.keyword.appid_short}} 所設定的授權過濾器保護。身分記號代表鑑別，並包含使用者的相關資訊。重新整理記號可以用來取得新的存取記號，而不需要重新鑑別使用者。藉由使用重新整理記號，使用者可以容許應用程式記住其資訊。如此，他們便可以保持登入狀態。如需記號及如何在 {{site.data.keyword.appid_short}} 中使用它們的相關資訊，請參閱[驗證記號](tokens.html#remote-validation)。</dd>
  <dt>授權標頭</dt>
    <dd><p>{{site.data.keyword.appid_short}} 符合<a href="https://tools.ietf.org/html/rfc6750" target="blank">記號載送規格 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，並使用傳送為 HTTP Authorization 標頭的存取及身分記號組合。Authorization 標頭包含依空格區隔的三個不同部分。這些記號是 base64 編碼。身分記號是選用項目。</br>
範例：</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API 策略</dt>
    <dd><p>API 策略預期要求要包含具有有效存取記號的授權標頭。要求也可以包括身分記號，但它不是必要項目。如果記號無效或過期，則 API 策略會傳回包含下列 HTTP 標頭的 HTTP 401 錯誤：</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>如果要求傳回有效的記號，則會將控制權傳遞給下一個中介軟體，並將 <code>appIdAuthorizationContext</code> 內容注入要求物件。此內容包含原始存取及身分記號，以及作為一般 JSON 物件的解碼有效負載資訊。</dd>
  <dt>Web 應用程式策略</dt>
    <dd>Web 應用程式策略偵測到未獲授權的受保護資源存取嘗試時，會自動將使用者的瀏覽器重新導向至 {{site.data.keyword.appid_short}} 可提供的鑑別頁面。在成功鑑別之後，使用者會回到 Web 應用程式的回呼 URL。Web 應用程式策略會取得存取及身分記號，並將它們儲存至 HTTP 階段作業的 <code>WebAppStrategy.AUTH_CONTEXT</code> 下方。使用者可以決定是否將存取及身分記號儲存在應用程式資料庫中。</dd>
  <dt>資料分隔及加密</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} 儲存及加密使用者設定檔屬性。身為多方承租戶服務，每個承租戶都會有一個指定的加密金鑰，而且只會使用該承租戶的金鑰來加密每一個承租戶中的使用者資料。</p>
    <p>{{site.data.keyword.appid_short_notm}} 確定專用資訊在儲存之前已進行加密。</p></dd>
</dl>

</br>
</br>


## 瞭解記號
{: #tokens}

當順利鑑別使用者時，應用程式會從 {{site.data.keyword.appid_short_notm}} 收到記號。服務會使用三種主要類型的記號來完成鑑別處理程序。
{: shortdesc}


**何謂存取記號？**

存取記號代表授權，並啟用與[後端資源](/docs/services/appid/backend-apps.html)的通訊，這些資源會受到 {{site.data.keyword.appid_short}} 所設定的授權過濾器保護。此記號符合「JavaScript 物件簽署及加密 (JOSE)」規格。記號會格式化為 <a href="https://jwt.io/introduction/" target="blank">JSON Web 記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，其是以使用 RS256 演算法的「JSON Web 金鑰」進行簽署。

範例記號：
  ```
Header: {

    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
      "exp": "1495562664",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "amr": ["facebook"],
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "iat": "1495559064",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
  ```
  {: screen}

**何謂身分記號？**

身分記號代表鑑別，並包含使用者的相關資訊。它可以將使用者名稱、電子郵件、性別及位置的相關資訊提供給您。記號也可以傳回使用者影像的 URL。記號會格式化為 <a href="https://jwt.io/introduction/" target="blank">JSON Web 記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，其是以使用 RS256 演算法的「JSON Web 金鑰」進行簽署。

範例記號：
  ```
Header: {

    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "exp: "1495562664",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "iat": "1495559064",
      "name": "John Smith",
      "email": "js@mail.com",
      "gender", "male",
      "locale": "en",
      "picture": "<URL-to-photo>",
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "identities": [
          "provider": "facebook"
        "id": "377440159275659"
    ],
    "amr": ["facebook"],
    "oauth_client":{
      "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
}
  ```
  {: screen}

身分記號僅包含局部使用者資訊。若要查看身分提供者所提供的所有資訊，您可以使用[使用者資訊端點](/docs/services/appid/predefined.html#api)。

**何謂重新整理記號？**

{{site.data.keyword.appid_short}} 支援在沒有重新鑑別的情況下獲得新存取和身分記號的能力，如 <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 中所定義。
      重新整理記號可以用來更新存取記號，因此使用者不需要採取任何動作即可登入，例如提供認證。與存取記號類似，重新整理記號包含容許 {{site.data.keyword.appid_short_notm}} 判定您是否已獲授權的資料。不過，這些記號是不透明的。

重新整理記號會配置為具有比一般存取記號還要長的有效期限，因此當存取記號到期時，重新整理記號仍然有效，且可用來更新存取記號。{{site.data.keyword.appid_short_notm}} 的重新整理記號可以配置為持續 1 到 90 天。若要充分利用重新整理記號，請持續保存這些記號，直到其完整有效期限結束，或直到它們已更新。使用者無法只利用重新整理記號來直接存取資源，這使得它們比存取記號更能安全地持續保存。最佳作法是，重新整理記號應該由接收它們的用戶端安全地儲存，且只傳送至發出它們的授權伺服器。

為了方便新增，{{site.data.keyword.appid_short_notm}} 也會在更新存取記號時，更新其重新整理記號及其到期日，讓使用者可以保持登入狀態，只要他們在現行重新整理記號到期之前的某個時間點處於作用中狀態。另一方面，如果您想要使用重新整理記號，但強制使用者定期登入，則您的應用程式只能使用在使用者輸入其認證登入時所傳回的重新整理記號。不過，我們建議一律使用從 App ID 接收的最新重新整理記號，如 <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">Oauth 規格<img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>所述。


雖然這些記號可以簡化登入處理程序，但您的應用程式不應該依賴它們，因為可以隨時撤銷它們，例如您認為重新整理記號已受損時。如果您需要撤銷重新整理記號，則有兩種撤銷重新整理記號的方法。如果您有重新整理記號，則可以根據 <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來撤銷它。或者，如果您具有使用者 ID，則可以使用<a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來撤銷重新整理記號。如需存取管理 API 的相關資訊，請參閱[管理服務存取](iam.html#service-access-management)。

如需使用重新整理記號，以及如何使用它們來實作 remember me 功能的範例，請參閱[入門範例](index.html)。


**記號來自哪裡？**

記號是透過 {{site.data.keyword.appid_short_notm}}OAuth Server 發出，且會格式化為 [JSON Web 記號 (JWT)](https://jwt.io/introduction/)。這些記號已使用 [JSON Web 金鑰 (JWK)](https://tools.ietf.org/html/rfc7517) 搭配 RS256 演算法來進行簽署。

**記號包含的資訊發生什麼情況？**

存取記號包含一組標準 JWT 要求，以及一組 {{site.data.keyword.appid_short_notm}}特定要求（如承租戶 ID）。身分記號包含使用者特定資訊。記號中的資訊儲存為要求，作為[使用者設定檔](/docs/services/appid/user-profile.html)的一部分。

**如何接收記號？**

在順利鑑別之後，您的應用程式會收到記號。您的應用程式可以使用記號，來擷取使用者授權和鑑別的相關資訊。存取記號可以用來透過將要求傳送至資源來取得受保護資源的存取權。在要求中，存取記號載明於[載送鑑別方法](https://tools.ietf.org/html/rfc6750#page-5)中。若要擷取記號，您的應用程式必須剖析標頭。

範例要求：

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

</br>
</br>
