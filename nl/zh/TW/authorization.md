---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# 授權及鑑別
{: #authorization}

使用 {{site.data.keyword.appid_full}}，使用者可以運用記號及授權過濾器，確保其應用程式受到保護。在使用者能夠授與應用程式授權之前，身分提供者必須先鑑別其身分。
{: shortdesc}


## 主要概念
{: #key-concepts}

這些重要詞彙可協助您瞭解服務中斷授權及鑑別處理程序的方式。

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 是用來提供應用程式授權的開放式標準通訊協定。</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 是比 OAuth 2 優先使用的鑑別層。</p>
    <p>當您同時使用 OIDC 及 {{site.data.keyword.appid_short_notm}} 時，您的服務認證有助於配置 OAuth 端點。當您使用 SDK 時，會自動建置端點 URL。但是，您也可以使用服務憑證自行建置 URL。您可以看到如何將 URL 放在下列範例及表格中。</p>
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
    <dd>服務使用三種不同類型的記號來提供鑑別。存取記號代表授權，並啟用與[後端資源](/docs/services/appid/protecting-resources.html)的通訊，這些資源會受到 {{site.data.keyword.appid_short}} 所設定的授權過濾器保護。身分記號代表鑑別，並包含使用者的相關資訊。重新整理記號是具有延伸生命期限的存取記號。藉由使用重新整理記號，使用者可以容許應用程式記住其資訊。因此，他們可以保持登入狀態。
  </dd>
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

## 處理程序運作方式
{: #process}

編寫應用程式碼時，其中一個最大的問題是安全。如何確定只有具有正確存取權的使用者才能使用應用程式？您可以使用授權處理程序。在大部分處理程序中，授權和鑑別會連結在一起，這樣做會讓變更您的安全原則和身分提供者更加複雜。使用 {{site.data.keyword.appid_short}} 時，授權及鑑別是不同的處理程序。
{: shortdesc}

當您配置社交身分提供者（例如 Facebook）時，[Oauth2 授權授與流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)是用來呼叫登入小組件。使用雲端目錄作為身分提供者，會使用[資源擁有者密碼認證流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)來提供存取及身分記號。

![要成為已識別使用者的路徑。](/images/authenticationtrail.png)

使用者選擇登入時，就會變成已識別的使用者。身分提供者會將存取及身分記號傳回給包含使用者相關資訊的 {{site.data.keyword.appid_short}}。此服務會採用提供的記號，並判斷使用者是否有適當的認證可以存取應用程式。如果已驗證記號，則服務會將存取權授與使用者。鑑別資訊在經過授權之後，會與使用者的記錄相關聯。可從相同身分所鑑別的任何用戶端中，重新存取記錄及其屬性。

### 漸進鑑別

使用 {{site.data.keyword.appid_short_notm}}，匿名使用者可以選擇變成已識別的使用者。

但是，作法為何？

使用者選擇不要立即登入時，就會將他們視為匿名使用者。例如，使用者可以在其中立即開始將項目新增至購物車，而不需要登入。針對匿名使用者，{{site.data.keyword.appid_short_notm}} 會建立特定的使用者記錄，並呼叫 OAuth 登入 API，傳回匿名存取及身分記號。使用那些記號，應用程式可以建立、讀取、更新及刪除使用者記錄中所儲存的屬性。

![使用者以匿名開始時變成已識別使用者的路徑。](/images/anon-authenticationtrail.png)

匿名使用者登入時，其存取記號會傳遞至登入 API。服務會向身分提供者鑑別呼叫。服務會使用存取記號，來尋找匿名記錄並將身分附加至其中。新的存取及身分記號包含身分提供者所共用的公用資訊。在識別使用者之後，其匿名記號會變成無效。不過，使用者仍然能夠存取其屬性，因為可使用新記號存取它們。

如果身分尚未指派給另一位使用者，則它只能指派給匿名記錄。
{: tip}

如果身分已與另一個 {{site.data.keyword.appid_short_notm}} 使用者相關聯，則記號會包含該使用者記錄的資訊，並提供其屬性的存取權。透過新的記號，無法存取先前匿名使用者屬性。除非記號到期，否則仍然可以透過匿名存取記號來存取這項資訊。開發期間，您可以選擇如何將匿名屬性合併至已知使用者。
