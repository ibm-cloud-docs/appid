---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 授權及鑑別
{: authorization}

授權是您授與應用程式存取權的處理程序。{{site.data.keyword.appid_short}} 服務會使用記號、過濾器及標頭來鑑別使用者。
{: shortdesc}


## OAuth 身分
{: #oauth}

此服務呼叫 OAuth 登入 API 時，{{site.data.keyword.appid_short_notm}} 會使用 OAuth 2.0 及 OpenID Connect (OIDC) 通訊協定，以透過選取的身分提供者來授權及鑑別呼叫者。鑑別之後，身分會與 {{site.data.keyword.appid_short_notm}} 使用者記錄相關聯。{{site.data.keyword.appid_short_notm}} 會傳回可用來存取使用者屬性的存取記號，以及保留身分提供者所提供的身分資訊的身分記號。從這個相同身分所鑑別的任何用戶端，都可以存取相同的使用者記錄及其屬性。

## 存取及身分記號

{{site.data.keyword.appid_short}} 使用兩種類型的記號：存取及身分。
{:shortdesc}

**附註**：記號會格式化為 <a href="https://jwt.io/introduction/" target="_blank">JSON Web 記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

### 存取記號
{: #access-tokens}

存取記號會啟用[後端資源](/docs/services/appid/protecting-resources.html)通訊，這些資源會受到 App ID 所設定的授權過濾器保護。此記號符合「JavaScript 物件簽署及加密 (JOSE)」規格。

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
}
```
{:screen}

<table>
<caption> 表 1. 說明的存取記號元件</caption>
  <tr>
    <th> 元件</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td><i> typ </i> </td>
    <td> 標頭類型，指定為 "JOSE"。</td>
  </tr>
  <tr>
    <td><i> alg </i> </td>
    <td> 已使用的演算法，指定為 "RS256"。</td>
  </tr>
  <tr>
    <td><i> iss </i> </td>
    <td> 發出記號的 {{site.data.keyword.appid_short}} 伺服器；指定為字串或 URL。</td>
  </tr>
  <tr>
    <td><i> sub </i> </td>
    <td> 對其發出記號之使用者的 ID。</td>
  </tr>
  <tr>
    <td><i> aud </i> </td>
    <td> 要對其使用記號的用戶端 ID。</td>
  </tr>
  <tr>
    <td><i> exp </i> </td>
    <td> 時間戳記的到期時間，以新紀元時間為單位指定。</td>
  </tr>
  <tr>
    <td><i> iat </i> </td>
    <td> 時間戳記的發出時間，以新紀元時間為單位指定。</td>
  </tr>
  <tr>
    <td><i> tenant </i> </td>
    <td> 搭配記號發出的唯一使用者 ID。</td>
  </tr>
  <tr>
    <td><i> amr </i> </td>
    <td> 用於鑑別的身分提供者。此變數可以是 <i>appid_facebook</i>、<i>appid_google</i> 或 <i>cloud_directory</i>。</td>
  </tr>
  <tr>
    <td><i> scope </i> </td>
    <td> 對其發出記號的範圍。</td>
  </tr>
</table>


### 身分記號
{: #identity-tokens}

身分記號包含使用者的相關資訊。它可以將使用者名稱、電子郵件、性別及位置的相關資訊提供給您。記號也可以傳回使用者影像的 URL。

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
    "picture": "https://url.to.photo",
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
{:screen}


<table>
<caption> 表 2. 說明的身分記號元件</caption>
  <tr>
    <th> 元件</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td> <i> name </i> </td>
    <td> 身分提供者所報告的使用者完整名稱。這是必須傳回的項目。</td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> 身分提供者所報告的使用者電子郵件。只有在可用時才傳回。</td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> 身分提供者所報告的使用者性別（可用時）。</td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> 身分提供者所報告的使用者語言環境。</td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> 使用者照片的 URL（可用時）。</td>
  </tr>
  <tr>
    <td> <i> identities：</br> <ul><li> provider <li> id </ul></i></td>
    <td> </br><ul><li> 用於鑑別的身分提供者。此變數可以是 <code>appid_facebook</code>、<code>appid_google</code> 或 <code>cloud_directory</code>，而且必須予以傳回。<li> 身分提供者所報告的唯一使用者 ID。<li> 身分提供者必須傳回的 JSON 物件。</ul></li></td>
  </tr>
  <tr>
    <td> <i> oauth_client：</br> <ul><li> type </br><li> name <li> software_id <li> software_version<li> device_id <li>device_model<li>device_os<li>device_os_version </ul></i> </td>
    <td> </br><ul><li> 用戶端登錄期間所判定的應用程式類型。變數可以是 <em>serverapp</em> 或 <em>mobileapp</em>。<li> 用戶端登錄期間所報告的用戶端名稱。<li> 用戶端登錄期間所報告的軟體 ID。<li> 用戶端登錄期間所使用的軟體版本。<li> 行動用戶端裝置 ID。<li> 行動用戶端裝置模型。<li> 行動用戶端裝置作業系統。<li> 行動用戶端裝置作業系統版本。</ul></td>
  </tr>
</table>

## 標頭
{: #auth-header}

授權標頭是所傳回之記號的組合。若為 {{site.data.keyword.appid_short}}，授權標頭由下列三個以空格區隔的不同記號組成：Bearer、Access 及 Identity。需有 Bearer 及存取記號，才能授與應用程式存取權。身分記號是選用項目，而且主要用來儲存那些使用應用程之項目的相關資訊。

範例標頭結構：

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


## 過濾器
{: #auth-filter}

{{site.data.keyword.appid_short}} 伺服器 SDK 提供策略來保護兩種類型的資源：API 及 Web 應用程式。
{:shortdesc}

API 保護策略會傳回 HTTP 401 回應，其具有可取得未經鑑別用戶端授權的範圍清單。Web 應用程式保護策略會傳回 HTTP 302 重新導向。重新導向會將未經鑑別的用戶端傳送至 {{site.data.keyword.appid_short_notm}} 服務所管理的登入頁面，或直接傳送至身分提供者登入頁面（視您的配置而定）。



### API 策略
{: #api}

API 策略預期要求要包含具有有效存取記號的授權標頭。回應也可以包括身分記號，但它不是必要項目。

如果記號無效或過期，則 API 策略會傳回包含下列資訊的 HTTP 401 錯誤：Www-Authenticate=Bearer scope="{scope}" error="{error}"。`error` 是選用元件。

如果要求傳回有效的記號，則會將控制權傳遞給下一個中介軟體，並將 `appIdAuthorizationContext` 內容注入要求物件。此內容包含原始存取及身分記號，以及作為一般 JSON 物件的解碼有效負載資訊。


### Web 應用程式策略
{: #web}

Web 應用程式策略類別偵測到未經鑑別的受保護資源存取嘗試時，會自動將使用者的瀏覽器重新導向至鑑別頁面。在成功鑑別之後，使用者會回到 Web 應用程式的回呼 URL。此服務會使用 Web 應用程式策略類別來取得存取及身分記號。取得這些記號之後，Web 應用程式策略類別會將它們儲存在 HTTP 階段作業的 `WebAppStrategy.AUTH_CONTEXT` 下方。使用者可以決定是否將存取及身分記號儲存在應用程式資料庫中。


## 漸進鑑別
{: #oauth}

{{site.data.keyword.appid_short_notm}} 會使用 OAuth 2.0 及 OIDC 通訊協定，來授權並鑑別使用者。在鑑別之後，其身分會與使用者記錄相關聯。服務會傳回可用來存取使用者屬性的存取記號，而且包含使用者相關資訊的身分記號是由身分提供者提供的。可從相同身分所鑑別的任何用戶端中，重新存取記錄及其屬性。

現在，您可能會問「如果我想要選擇性登入，怎麼辦？」{{site.data.keyword.appid_short_notm}} 會使用所謂的漸進鑑別來建立[使用者設定檔](/docs/services/appid/user-profile.html)，即使他們是匿名也一樣。然後，您可以在使用者登入之後，將該資訊傳送給已知的使用者設定檔。

![顯示要成為已識別使用者的路徑地圖。](/images/authenticationtrail.png)

圖 2. 顯示要成為已識別使用者的路徑地圖

當使用者選擇維持匿名時，{{site.data.keyword.appid_short_notm}} 會建立特定的使用者記錄，並呼叫 OAuth 登入 API，傳回匿名存取及身分記號。使用那些記號，應用程式可以建立、讀取、更新及刪除使用者記錄中所儲存的屬性。舉例來說，使用者可以在其中立即開始將項目新增至購物車，而不需要登入應用程式。


當使用者選擇登入應用程式時，他們變成已識別的使用者。使用者的相關資訊取自於他們選擇藉由其登入的身分提供者。他們會收到包含使用者相關資訊的存取及身分記號。

匿名使用者可以選擇變成已識別的使用者。但是，作法為何？

匿名存取記號會傳遞至登入 API。服務會向身分提供者鑑別呼叫。服務會使用存取記號，來尋找匿名記錄並將身分附加至其中。新的存取身分記號包含身分提供者所共用的公用資訊。在識別使用者之後，其匿名記號會變成無效。不過，使用者仍然能夠存取其屬性，因為可使用新記號存取它們。

**附註**：如果身分尚未指派給另一個使用者，則它只能指派給匿名記錄。如果身分已與另一個 {{site.data.keyword.appid_short_notm}} 使用者相關聯，則記號會包含該使用者記錄的資訊，並提供其屬性的存取權。透過新的記號，無法存取先前匿名使用者屬性。除非記號到期，否則仍然可以透過匿名存取記號來存取這項資訊。開發期間，您可以選擇如何將匿名屬性合併至已知使用者。
