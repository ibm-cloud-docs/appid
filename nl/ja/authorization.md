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

# 主要な概念
{: #key-concepts}

許可と認証の違いは間違えやすいので、注意が必要です。 このページの情報を参照して、特定の用語とプロセスについて、またサービスでトークンを使用する仕組みについて把握してください。
{: shortdesc}

許可と認証の基本的な概念についてもっと詳しく知りたいですか? ここにあります。次のビデオで、OAuth 2.0、付与タイプ、OIDC などについて説明しています。

<iframe class="embed-responsive-item" id="about-appid-basics" title="{{site.data.keyword.appid_short_notm}} の概要" type="text/html" width="640" height="390" src="//www.youtube.com/embed/ndlk-ZhKGXM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


## 用語
{: #terms}

以下の重要な用語は、このサービスが許可と認証のプロセスをどのように分けているかを理解するのに役立ちます。

### OAuth 2
{: #term-oauth}
<a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> は、アプリに許可を実装するために使用されているオープン・スタンダードのプロトコルです。


### Open ID Connect (OIDC)
{: #term-oidc}

<a href="https://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> は、OAuth 2 の上で機能する認証レイヤーです。OIDC と {{site.data.keyword.appid_short_notm}} を一緒に使用する場合、OAuth エンドポイントを構成するときにアプリケーション資格情報が役立ちます。SDK を使用する場合、エンドポイント URL は自動的に作成されます。 しかし、サービス資格情報を使用して、URL を自分で作成することもできます。 URL には、{{site.data.keyword.appid_short_notm}} service endpoint + "/oauth/v4" + /tenantID の形式を使用します。

例:

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

この例の場合、URL は `https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0` になります。 これに、要求先のエンドポイントを付加します。 次の表を参照して、いくつかのエンドポイントの例を確認してください。

<table>
  <tr>
    <th>エンドポイント</th>
    <th>フォーマット</th>
  </tr>
  <tr>
    <td>許可</td>
    <td>{oauthServerUrl}/authorization</td>
  </tr>
  <tr>
    <td>トークン</td>
    <td>{oauthServerUrl}/token</td>
  </tr>
  <tr>
    <td>ユーザー情報</td>
    <td>{oauthServerUrl}/userinfo</td>
  </tr>
  <tr>
    <td>JWKS</td>
    <td>{oauthServerUrl}/publickeys</td>
  </tr>
</table>

SDK を使用する場合、エンドポイント URL は自動的に作成されます。
{: note}

### トークン
{: #term-token}

サービスは、3 種類の異なるトークンを使用します。 アクセス・トークンとは許可を表すものであり、{{site.data.keyword.appid_short}} で設定された許可フィルターで保護されている[バックエンド・リソース](/docs/services/appid?topic=appid-backend)との通信を可能にします。 識別トークンとは認証を表すものであり、ユーザーに関する情報が含まれています。 リフレッシュ・トークンは、ユーザーの再認証なしで新規アクセス・トークンを取得するために使用できます。 リフレッシュ・トークンを使用すると、ユーザーは自分の情報をアプリケーションに記憶させることができます。 これにより、サインインした状態を保つことができます。 トークンの設定は、{{site.data.keyword.appid_short}} ダッシュボードの**「ID プロバイダー」>「管理」**で行います。 トークンおよび {{site.data.keyword.appid_short}} でトークンを使用する方法について詳しくは、[トークンの管理](/docs/services/appid?topic=appid-tokens#tokens)を参照してください。

### 許可ヘッダー
{: #term-auth-header}

{{site.data.keyword.appid_short}} は <a href="https://tools.ietf.org/html/rfc6750" target="blank">トークン・ベアラー仕様 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> に準拠しており、HTTP 許可ヘッダーとして送信されるアクセス・トークンと識別トークンの組み合わせを使用します。 許可ヘッダーは、空白文字で区切られた 3 つの部分で構成されます。 これらのトークンは base64 でエンコードされます。 識別トークンはオプションです。

例:

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


### API 戦略
{: #term-api-strategy}

API 戦略では、有効なアクセス・トークンを含む許可ヘッダーが要求に含まれていなければなりません。 識別トークンも要求に含めることができますが、これは必須ではありません。 トークンが無効または期限切れの場合、API 戦略は、次の HTTP ヘッダーを含む HTTP 401 エラーを返します。
```
Www-Authenticate=Bearer scope="{scope}" error="{error}"
```
{: screen}

要求から有効なトークンが返された場合、制御が次のミドルウェアに渡され、`appIdAuthorizationContext` プロパティーが要求オブジェクト内に挿入されます。 このプロパティーには、元のアクセス・トークンと識別トークン、およびデコードされたペイロード情報が平文の JSON オブジェクトとして含まれます。

### Web アプリ戦略
{: #term-web-strategy}

Web アプリ戦略は、保護リソースに対する無許可のアクセス試行を検出すると、ユーザーのブラウザーを認証ページ ({{site.data.keyword.appid_short}} で提供可能) に自動的にリダイレクトします。 認証に成功すると、ユーザーは Web アプリのコールバック URL に返されます。 Web アプリ戦略は、アクセス・トークンと識別トークンを取得し、HTTP セッションの `WebAppStrategy.AUTH_CONTEXT` の下に保管します。 アクセス・トークンと識別トークンをアプリ・データベース内に保管するかどうかは、各ユーザーが決定します。

### データ分離と暗号化
{: #term-data-encryption}

{{site.data.keyword.appid_short_notm}} は、ユーザー・プロファイル属性を保管して暗号化します。 マルチテナント・サービスでは、すべてのテナントには指定された暗号鍵がありそれぞれのテナントのユーザー・データはそのテナントの鍵だけで暗号化されます。

{{site.data.keyword.appid_short_notm}} は必ず、プライベートな資料を暗号化してから保管します。
{: note}


### リダイレクト URI
{: #term-redirect}

{{site.data.keyword.appid_short_notm}} は、アプリとの対話後に、承認された完全修飾 URI のリストを使用してユーザーをリダイレクトします。 例えば、ユーザーが正常にサインインした場合、{{site.data.keyword.appid_short_notm}} は、アプリのホーム・ページまたは指定された別のページにユーザーをリダイレクトします。 URI の形式はアプリケーションによって変わる可能性があります。 詳しくは、[リダイレクト URI の追加](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)を確認してください。


### JSON Web Key Set (JWKS)
{: #term-jwks}

JWKS は、暗号鍵のセットを表します。 {{site.data.keyword.appid_short_notm}} は JWKS を使用して、サービスによって生成されたトークンの真正性を検証します。 鍵 ID を使用して署名を検証することにより、信頼できるソース {{site.data.keyword.appid_short_notm}} によってトークンが発行されたこと、およびトークン内の情報が変更されてはいないことを確認できます。


