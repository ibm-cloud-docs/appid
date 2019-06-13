---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

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


# OIDC ディスカバリー文書
{: #discovery}

OpenID Connect は、アプリを構成してユーザーを認証するために使用できる情報 (トークンや公開鍵など) を格納するディスカバリー・プロトコルをサポートします。
{: shortdesc}


## エンドポイントの呼び出し
{: #call-wellknown}

`.well-known` エンドポイントを呼び出すことにより、ディスカバリー文書とそれに含まれている情報を取得できます。
{: shortdesc}


**このエンドポイントはどこにありますか?**

このエンドポイントは以下の URL にあります。

```
https://{region}.appid.ibm.cloud.com/oauth/v4/{tenantId}/.well-known/openid-configuration
```
{: codeblock}

<table>
  <tr>
    <th>地域</th>
    <th>エンドポイント</th>
  </tr>
  <tr>
    <td>ダラス</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>フランクフルト</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>シドニー</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>ロンドン</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>東京</td>
    <td><code> jp-tok </code></td>
  </tr>
</table>



**このエンドポイントを呼び出すにはどうすればよいですか?**

このエンドポイントを呼び出すには、有効なテナント ID があること、およびディスカバリー文書 URI をアプリケーション・コードにハードコーディングすることが必要です。

以下のサンプル cURL 要求を参照してください。

```bash
curl -X GET "https://{region}.appid.cloud.ibm.com/oauth/v4/{tenant-id}/.well-known/openid-configuration" -H "accept: application/json"
```
{:codeblock}

**この呼び出しによって何が返されますか?**

返される応答は、以下の例のようになります。

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
    <th> コンポーネント </th>
    <th> 説明 </th>
  </tr>
  <tr>
  <td><code>issuer</code></td>
  <td>OIDC プロバイダーの場所。</td>
  </tr>
  <tr>
    <td><code>authorization_endpoint</code></td>
    <td>{{site.data.keyword.appid_short_notm}} OAuth 2.0 許可エンドポイントの URL。</td>
  </tr>
  <tr>
    <td><code>token_endpoint</code></td>
    <td>{{site.data.keyword.appid_short_notm}} OAuth 2.0 トークン・エンドポイントの URL。</td>
  </tr>
  <tr>
    <td><code>jwks_uri</code></td>
    <td>{{site.data.keyword.appid_short_notm}} Web 鍵セット文書の URL。</td>
  </tr>
  <tr>
    <td><code>subject_types_supported</code></td>
    <td>{{site.data.keyword.appid_short_notm}} によってサポートされるサブジェクト ID タイプのリストを格納する JSON 配列。</td>
  </tr>
  <tr>
    <td><code>id_token_signing_alg_values_supported</code></td>
    <td>{{site.data.keyword.appid_short_notm}} サーバーによってサポートされる JWS 署名アルゴリズムのリストを格納する JSON 配列。</td>
  </tr>
  <tr>
    <td><code>userinfo_endpoint</code></td>
    <td>{{site.data.keyword.appid_short_notm}} <code>/userinfo</code> エンドポイントの URL。</td>
  </tr>
  <tr>
    <td><code>scopes_supported</code></td>
    <td>{{site.data.keyword.appid_short_notm}} によってサポートされる OAuth 2.0 スコープ値のリストを格納する JSON 配列。</td>
  </tr>
  <tr>
    <td><code>response_types_supported</code></td>
    <td>{{site.data.keyword.appid_short_notm}} によってサポートされる OAuth 2.0 response_type 値のリストを格納する JSON 配列。</td>
  </tr>
  <tr>
    <td><code>claims_supported</code></td>
    <td>クレーム名のリストを格納する JSON 配列。</td>
  </tr>
  <tr>
    <td><code>grant_types_supported</code></td>
    <td>{{site.data.keyword.appid_short_notm}} によってサポートされる OAuth 2.0 付与タイプ値のリストを格納する JSON 配列。</td>
  </tr>
  <tr>
    <td><code>profiles_endpoint</code></td>
    <td>{{site.data.keyword.appid_short_notm}} ユーザー・プロファイル・エンドポイントの URL。</td>
  </tr>
</table>


