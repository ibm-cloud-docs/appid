---

copyright:
  years: 2017
lastupdated: "2017-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 存取及身分記號
{: #access-and-identity}

{{site.data.keyword.appid_short}} 使用兩種類型的記號：存取及身分。記號會格式化為 <a href="https://jwt.io/introduction/" target="_blank">JSON Web 記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{:shortdesc}


## 存取記號
{: #access-tokens}

存取記號會啟用與 {{site.data.keyword.appid_short_notm}} 授權過濾器所保護的[後端資源](/docs/services/appid/protecting-resources.html)進行通訊。記號符合「JavaScript 物件簽署及加密 (JOSE)」規格，並且具有下列格式：

```
Header: {

    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": "facebook",
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
    <td> <i> typ </i> </td>
    <td> 標頭類型，指定為 "JOSE"。</td>
  </tr>
  <tr>
    <td> <i> alg </i> </td>
    <td> 已使用的演算法，指定為 "RS256"。</td>
  </tr>
  <tr>
    <td> <i> iss </i> </td>
    <td> 發出記號的 {{site.data.keyword.appid_short}} 伺服器；指定為字串或 URL。</td>
  </tr>
  <tr>
    <td> <i> sub </i> </td>
    <td> 對其發出記號的使用者的 ID。</td>
  </tr>
  <tr>
    <td> <i> aud </i> </td>
    <td> 要對其使用記號的用戶端 ID。</td>
  </tr>
  <tr>
    <td> <i> exp </i> </td>
    <td> 時間戳記的到期時間，以新紀元時間為單位指定。</td>
  </tr>
  <tr>
    <td> <i> iat </i> </td>
    <td> 時間戳記的發出時間，以新紀元時間為單位指定。</td>
  </tr>
  <tr>
    <td> <i> tenant </i> </td>
    <td> 對其發出記號的承租戶 ID。</td>
  </tr>
  <tr>
    <td> <i> amr </i> </td>
    <td> 用於鑑別的身分提供者。此變數可以是 <i>appid_facebook</i> 或 <i>appid_google</i>。</td>
  </tr>
  <tr>
    <td> <i> scope </i> </td>
    <td> 對其發出記號的範圍。</td>
  </tr>
</table>


## 身分記號
{: #identity-tokens}

身分記號包含使用者的相關資訊，包括姓名、電子郵件、性別、圖片及位置。

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
        "id": "377440159275659",
        "amr: "facebook",
    ],
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
    <td> <i> identities：</br> <ul><li> provider <li> id <li> amr </ul></i></td>
    <td> </br><ul><li> 用於鑑別的身分提供者。此變數可以是 <code>appid_facebook</code>、<code>appid_google</code> 或 <code>appid_ibmid</code>，而且必須予以傳回。<li> 身分提供者所報告的唯一使用者 ID。<li> 身分提供者必須傳回的 JSON 物件。</ul></i></td>
  </tr>
  <tr>
    <td> <i> oauth_client：</br> <ul><li> type <li> name <li> software_id <li> software_version</ul></i> </td>
    <td> </br><ul><li> 用戶端登錄期間所判定的應用程式類型。變數可以是 <i>serverapp</i> 或 <i>mobileapp</i>。<li> 用戶端登錄期間所報告的用戶端名稱。<li> 用戶端登錄期間所報告的軟體 ID。<li> 用戶端登錄期間所使用的軟體版本。</ul></td>
  </tr>
</table>
