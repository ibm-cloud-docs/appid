---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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

# 主要概念
{: #key-concepts}

對授權與鑑別之間的差異感到困惑嗎？不是只有您而已。請參閱此頁面上的資訊，以瞭解特定術語、處理程序，以及服務使用記號的方式。
{: shortdesc}

想要進一步瞭解授權與鑑別的部分基本概念？不必再找了。在下列視訊中，您可以瞭解 OAuth 2.0、授權類型、OIDC 等等。

<iframe class="embed-responsive-item" id="about-appid-basics" title="關於 {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/ndlk-ZhKGXM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


## 術語
{: #terms}

這些重要詞彙可協助您瞭解服務中斷授權及鑑別處理程序的方式。

### OAuth 2
{: #term-oauth}
<a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 是用來提供應用程式授權的開放式標準通訊協定。


### Open ID Connect (OIDC)
{: #term-oidc}

<a href="https://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 借助 OAuth 2 而運作的鑑別層。當您將 OIDC 與 {{site.data.keyword.appid_short_notm}} 一起使用時，您的應用程式認證有助於配置 OAuth 端點。當您使用 SDK 時，會自動建置端點 URL。但是，您也可以使用服務憑證自行建置 URL。URL 採用下列格式：{{site.data.keyword.appid_short_notm}} 服務端點 + "/oauth/v4" + /tenantID。

範例：

```
{
  "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
  "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
  "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
  "name":testing",
  "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
  "profilesUrl": "https://us-south.appid.cloud.ibm.com",
  "discoveryEndpoint": "https://us-south.appid.ibm.cloud.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
}
```
{: screen}

使用此範例，URL 會是 `https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0`。然後，您要附加您想對其提出要求的端點。請參閱下表，以查看一些範例端點。

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
    <td>使用者資訊</td>
    <td>{oauthServerUrl}/userinfo</td>
  </tr>
  <tr>
    <td>JWKS</td>
    <td>{oauthServerUrl}/publickeys</td>
  </tr>
</table>

當您使用 SDK 時，會自動建置端點 URL。
{: note}

### 記號
{: #term-token}

服務使用三種不同類型的記號。存取記號代表授權，並啟用與[後端資源](/docs/services/appid?topic=appid-backend)的通訊，這些資源會受到 {{site.data.keyword.appid_short}} 所設定的授權過濾器保護。身分記號代表鑑別，並包含使用者的相關資訊。重新整理記號可以用來取得新的存取記號，而不需要重新鑑別使用者。藉由使用重新整理記號，使用者可以容許應用程式記住其資訊。如此，他們便可以保持登入狀態。記號是在 {{site.data.keyword.appid_short}} 儀表板的**身分提供者 > 管理**中設定。如需記號及如何在 {{site.data.keyword.appid_short}} 中使用它們的相關資訊，請參閱[管理記號](/docs/services/appid?topic=appid-tokens#tokens)。

### 授權標頭
{: #term-auth-header}

{{site.data.keyword.appid_short}} 符合<a href="https://tools.ietf.org/html/rfc6750" target="blank">記號載送規格 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，並使用傳送為 HTTP Authorization 標頭的存取及身分記號組合。Authorization 標頭包含依空格區隔的三個不同部分。這些記號是 base64 編碼。身分記號是選用項目。

範例：

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


### API 策略
{: #term-api-strategy}

API 策略預期要求要包含具有有效存取記號的授權標頭。要求也可以包括身分記號，但它不是必要項目。如果記號無效或過期，則 API 策略會傳回包含下列 HTTP 標頭的 HTTP 401 錯誤：
```
Www-Authenticate=Bearer scope="{scope}" error="{error}"
```
{: screen}

如果要求傳回有效的記號，則會將控制權傳遞給下一個中介軟體，並將 `appIdAuthorizationContext` 內容注入要求物件。此內容包含原始存取及身分記號，以及作為一般 JSON 物件的解碼有效負載資訊。

### Web 應用程式策略
{: #term-web-strategy}

Web 應用程式策略偵測到未獲授權的受保護資源存取嘗試時，會自動將使用者的瀏覽器重新導向至 {{site.data.keyword.appid_short}} 可提供的鑑別頁面。在成功鑑別之後，使用者會回到 Web 應用程式的回呼 URL。Web 應用程式策略會取得存取及身分記號，並將它們儲存至 HTTP 階段作業的 `WebAppStrategy.AUTH_CONTEXT` 下方。使用者可以決定是否將存取及身分記號儲存在應用程式資料庫中。

### 資料分隔及加密
{: #term-data-encryption}

{{site.data.keyword.appid_short_notm}} 儲存及加密使用者設定檔屬性。身為多方承租戶服務，每個承租戶都會有一個指定的加密金鑰，而且只會使用該承租戶的金鑰來加密每一個承租戶中的使用者資料。

{{site.data.keyword.appid_short_notm}} 確定專用資訊在儲存之前已進行加密。
{: note}


### 重新導向 URI
{: #term-redirect}

{{site.data.keyword.appid_short_notm}} 會使用完整的已核准 URI 清單，在使用者與您的應用程式互動之後將使用者重新導向。比方說，如果使用者已順利登入，{{site.data.keyword.appid_short_notm}} 會將使用者重新導向至應用程式的首頁，或重新導向至您指定的其他頁面。視您的應用程式而定，URI 的格式可能會變更。如需相關資訊，請參閱[新增重新導向 URI](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)。


### JSON Web Key Set (JWKS)
{: #term-jwks}

JWKS 代表一組加密金鑰。{{site.data.keyword.appid_short_notm}} 使用 JWKS 來驗證服務所產生之記號的確實性。藉由使用金鑰 ID 來驗證簽章，我們可以確定記號是由授信來源 {{site.data.keyword.appid_short_notm}} 所發出，且記號內的資訊從未變更過。


