---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, discovery endpoint, oidc, public keys, tokens, well known endpoint

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


# 使用 OIDC 探索端點
{: #discovery}

OpenID Connect 所支援的探索通訊協定包含可用來配置應用程式以及鑑別使用者（例如記號及公開金鑰）的資訊。
{: shortdesc}


## 呼叫端點
{: #call-wellknown}

您可以呼叫 `.well-known` 端點，來取得探索文件及其包含的資訊。
{: shortdesc}


**在何處可以找到端點？**

您可以在下列 URL 找到端點：

```
https://[region].appid.ibm.cloud.com/oauth/v4/{tenantId}/.well-known/openid-configuration
```
{: pre}

<table>
  <tr>
    <th>地區</th>
    <th>端點</th>
  </tr>
  <tr>
    <td>達拉斯</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>法蘭克福</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>雪梨</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>倫敦</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>東京</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



**如何呼叫端點？**

若要呼叫端點，您必須具有有效的`承租戶 ID`，而且必須將探索文件 URI 寫在應用程式中。

請參閱下列範例 cURL 要求：

```bash
curl -X GET "https://us-south.appid.cloud.ibm.com/oauth/v4/asd/.well-known/openid-configuration" -H "accept: application/json"
```
{:codeblock}

**預期呼叫會傳回哪些內容？**

回應應該與下列範例類似：

```bash
{
  "issuer": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61",
  "authorization_endpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/authorization",
  "token_endpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/token",
  "jwks_uri": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/publickeys",
  "subject_types_supported": [
    "public"
    ],
    "id_token_signing_alg_values_supported": [
      "RS256"
    ],
  "userinfo_endpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/userinfo",
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
  "profiles_endpoint": "https://us-south.appid.cloud.ibm.com",
  "management_endpoint": "https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61",
  "service_documentation": "https://cloud.ibm.com/docs/services/appid?topic=appid-getting-started#getting-started"
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
    <td>JSON 陣列，包含 {{site.data.keyword.appid_short_notm}} 所支援的主旨 ID 類型清單。</td>
  </tr>
  <tr>
    <td><code>id_token_signing_alg_values_supported</code></td>
    <td>JSON 陣列，包含 {{site.data.keyword.appid_short_notm}} 伺服器所支援的 JWS 簽署演算法清單。</td>
  </tr>
  <tr>
    <td><code>userinfo_endpoint</code></td>
    <td>{{site.data.keyword.appid_short_notm}} userinfo 端點的 URL。</td>
  </tr>
  <tr>
    <td><code>scopes_supported</code></td>
    <td>JSON 陣列，包含 {{site.data.keyword.appid_short_notm}} 所支援的 OAuth 2.0 範圍值清單。</td>
  </tr>
  <tr>
    <td><code>response_types_supported</code></td>
    <td>JSON 陣列，包含 {{site.data.keyword.appid_short_notm}} 所支援的 OAuth 2.0 response_type 值清單。</td>
  </tr>
  <tr>
    <td><code>claims_supported</code></td>
    <td>JSON 陣列，包含要求名稱清單。</td>
  </tr>
  <tr>
    <td><code>grant_types_supported</code></td>
    <td>JSON 陣列，包含 {{site.data.keyword.appid_short_notm}} 所支援的 OAuth 2.0 授權類型值清單。</td>
  </tr>
  <tr>
    <td><code>profiles_endpoint</code></td>
    <td>{{site.data.keyword.appid_short_notm}} 使用者設定檔端點的 URL。</td>
  </tr>
</table>


