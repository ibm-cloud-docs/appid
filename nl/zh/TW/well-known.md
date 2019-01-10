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


# 使用 OIDC 探索端點
{: #discovery}

OpenID Connect 所支援的探索通訊協定包含可用來配置應用程式以及鑑別使用者（例如記號及公開金鑰）的資訊。
{: shortdesc}


## 呼叫端點
{: #call-wellknown}

您可以呼叫 `.well-known` 端點，來取得探索文件及其包含的資訊。
{: shortdesc}


**我可以在何處找到端點？**

您可以在下列 URL 找到端點：

  ```
  https://appid-oauth.[region].bluemix.net/oauth/v3/{tenantId}/.well-known/openid-configuration
  ```
  {: codeblock}

</br>

**如何呼叫端點？**

若要呼叫端點，您必須具有有效的 `tenantID`，而且必須將探索文件 URI 寫在應用程式中。

請查看下列範例 cURL 要求：

  ```bash
  curl -X GET --header 'Accept: application/json'  'https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/.well-known/openid-configuration'
  ```
  {:codeblock}

</br>

**我預期呼叫傳回什麼？**

回應應該類似下列範例：

  ```bash
  {
    "issuer" : "appid-oauth.ng.bluemix.net",
    "authorization_endpoint": "https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/authorization",
    "token_endpoint": "https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/token",
    "jwks_uri": "https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/publickeys",
    "subject_types_supported": [
      "public"
    ],
    "id_token_signing_alg_values_supported": [
      "RS256"
    ],
    "userinfo_endpoint": "https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/userinfo",
    "scopes_supported": [
      "openid"
    ],
    "response_types_supported": [
      "code"
    ],
    "claims_supported": [
      "iss",
      "aud",
      "exp",
      "tenant",
      "iat",
      "sub",
      "nonce",
      "amr",
      "oauth_client"
    ],
    "grant_types_supported": [
      "authorization_code",
      "password",
      "refresh_token",
      "client_credentials",
      "urn:ietf:params:oauth:grant-type:jwt-bearer"
    ],
    "profiles_endpoint": "https://appid-profiles.ng.bluemix.net",
    "service_documentation": "https://console.bluemix.net/docs/services/appid/index.html"
  }
  ```
  {: screen}

  <table>
    <tr>
      <th> 元件</th>
      <th> 說明</th>
    </tr>
    <tr>
    <td><code>issuer</code></td>
    <td>OIDC 提供者的位置。</td>
    </tr>
    <tr>
      <td><code>authorization_endpoint</code></td>
      <td>{{site.data.keyword.appid_short_notm}} OAuth 2.0 授權端點的 URL。</td>
    </tr>
    <tr>
      <td><code>token_endpoint</code></td>
      <td>{{site.data.keyword.appid_short_notm}} OAuth 2.0 記號端點的 URL。</td>
    </tr>
    <tr>
      <td><code>jwks_uri</code></td>
      <td>{{site.data.keyword.appid_short_notm}} Web 金鑰集文件的 URL。</td>
    </tr>
    <tr>
      <td><code>subject_types_supported</code></td>
      <td>JSON 陣列，內含 {{site.data.keyword.appid_short_notm}} 所支援的主旨 ID 類型清單。</td>
    </tr>
    <tr>
      <td><code>id_token_signing_alg_values_supported</code></td>
      <td>JSON 陣列，內含 {{site.data.keyword.appid_short_notm}} 伺服器所支援的 JWS 簽署演算法清單。</td>
    </tr>
    <tr>
      <td><code>userinfo_endpoint</code></td>
      <td>{{site.data.keyword.appid_short_notm}} userinfo 端點的 URL。</td>
    </tr>
    <tr>
      <td><code>scopes_supported</code></td>
      <td>JSON 陣列，內含 {{site.data.keyword.appid_short_notm}} 所支援的 OAuth 2.0 範圍值清單。</td>
    </tr>
    <tr>
      <td><code>response_types_supported</code></td>
      <td>JSON 陣列，內含 {{site.data.keyword.appid_short_notm}} 所支援的 OAuth 2.0 response_type 值清單。</td>
    </tr>
    <tr>
      <td><code>claims_supported</code></td>
      <td>JSON 陣列，內含要求名稱清單。</td>
    </tr>
    <tr>
      <td><code>grant_types_supported</code></td>
      <td>JSON 陣列，內含 {{site.data.keyword.appid_short_notm}} 所支援的 OAuth 2.0 授權類型值清單。</td>
    </tr>
    <tr>
      <td><code>profiles_endpoint</code></td>
      <td>{{site.data.keyword.appid_short_notm}} 使用者設定檔端點的 URL。</td>
    </tr>
  </table>

</br>
</br>


