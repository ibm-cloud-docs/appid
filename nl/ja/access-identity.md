---

copyright:
  years: 2017
lastupdated: "2017-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# アクセス・トークンと識別トークン
{: #access-and-identity}

{{site.data.keyword.appid_short}} は、アクセス・トークンと識別トークンという 2 つのタイプのトークンを使用します。これらのトークンは、<a href="https://jwt.io/introduction/" target="_blank">JSON Web トークン<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>としてフォーマットされます。
{:shortdesc}


## アクセス・トークン
{: #access-tokens}

アクセス・トークンによって、{{site.data.keyword.appid_short_notm}} 許可フィルターによって保護されている [バックエンド・リソース](/docs/services/appid/protecting-resources.html)との通信が可能になります。このトークンは JavaScript Object Signing and Encryption (JOSE) 仕様に準拠しています。形式は次のとおりです。

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
<caption> 表 1. アクセス・トークンのコンポーネントの説明 </caption>
  <tr>
    <th> コンポーネント </th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td> <i> typ </i> </td>
    <td> ヘッダー・タイプ (「JOSE」として指定)。</td>
  </tr>
  <tr>
    <td> <i> alg </i> </td>
    <td> 使用されるアルゴリズム (「RS256」として指定)。</td>
  </tr>
  <tr>
    <td> <i> iss </i> </td>
    <td> トークンを発行した {{site.data.keyword.appid_short}} サーバー (ストリングまたは URL として指定)。</td>
  </tr>
  <tr>
    <td> <i> sub </i> </td>
    <td> トークンの発行先のユーザーの ID。</td>
  </tr>
  <tr>
    <td> <i> aud </i> </td>
    <td> トークンの対象のクライアント ID。</td>
  </tr>
  <tr>
    <td> <i> exp </i> </td>
    <td> タイム・スタンプ満了の時刻 (エポック・タイムで指定)。</td>
  </tr>
  <tr>
    <td> <i> iat </i> </td>
    <td> タイム・スタンプが出された時刻 (エポック・タイムで指定)。</td>
  </tr>
  <tr>
    <td> <i> tenant </i> </td>
    <td> トークンの発行対象のテナント ID。</td>
  </tr>
  <tr>
    <td> <i> amr </i> </td>
    <td> 認証に使用される ID プロバイダー。この変数は、<i>appid_facebook</i> または <i>appid_google</i> です。</td>
  </tr>
  <tr>
    <td> <i> scope </i> </td>
    <td> トークンの発行対象のスコープ。</td>
  </tr>
</table>


## 識別トークン
{: #identity-tokens}

識別トークンには名前、E メール、性別、写真、場所などのユーザーに関する情報が含まれます。

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
<caption> 表 2. 識別トークンのコンポーネントの説明</caption>
  <tr>
    <th> コンポーネント </th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td> <i> name </i> </td>
    <td> ID プロバイダーによって報告されたユーザーのフルネーム。これは、必ず返されなければなりません。</td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> ID プロバイダーによって報告されたユーザーの E メール。使用可能な場合にのみ返されます。</td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> ID プロバイダーによって報告されたユーザーの性別 (使用可能な場合)。</td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> ID プロバイダーによって報告されたユーザーのロケール。</td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> ユーザーのピクチャーへの URL (使用可能な場合)。</td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id <li> amr </ul></i></td>
    <td> </br><ul><li> 認証に使用される ID プロバイダー。この変数は、<code>appid_facebook</code>、<code>appid_google</code>、または <code>appid_ibmid</code> です。これは、必ず返されなければなりません。<li> ID プロバイダーによって報告された固有のユーザー ID。<li> ID プロバイダーによって返されなければならない JSON オブジェクト。</ul></i></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type <li> name <li> software_id <li> software_version</ul></i> </td>
    <td> </br><ul><li> クライアントの登録時に判別されたアプリケーションのタイプ。この変数は、<i>serverapp</i> または <i>mobileapp</i> です。 <li> クライアントの登録時に報告されたクライアント名。<li> クライアントの登録時に報告されたソフトウェア ID。<li> クライアントの登録時に使用されたソフトウェアのバージョン。</ul></td>
  </tr>
</table>
