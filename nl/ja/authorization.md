---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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


## 用語
{: #terms}

以下の重要な用語は、このサービスが許可と認証のプロセスをどのように分けているかを理解するのに役立ちます。

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> は、アプリに許可を実装するために使用されているオープン・スタンダードのプロトコルです。</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> は、OAuth 2 を基礎として機能する認証レイヤーです。</p>
    <p>OIDC と {{site.data.keyword.appid_short_notm}} を一緒に使用する場合、OAuth エンドポイントを構成するときにアプリケーション資格情報が役立ちます。 SDK を使用する場合、エンドポイント URL は自動的に作成されます。 しかし、サービス資格情報を使用して、URL を自分で作成することもできます。</p> <p>URL には、{{site.data.keyword.appid_short_notm}} service endpoint + "/oauth/v4" + /tenantID の形式を使用します。</p>
    <p><pre class="codeblock">
    <code>{
      "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
      "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
      "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
      "name":testing",
      "oAuthServerUrl": "https://us-south.appid-oauth.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
      "profilesUrl": "https://us-south.appid.cloud.ibm.com",
      "discoveryEndpoint": "https://us-south.appid-oauth.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
    }</code></pre></p>
    <p>この例を使用すると、URL は <code>https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0</code> になります。次に、要求先のエンドポイントを付加します。次の表を参照して、いくつかのエンドポイントの例を確認してください。</p>
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
    <p><strong>注</strong>: SDK を使用する場合、エンドポイント URL は自動的に作成されます。</p></dd>
  <dt>トークン</dt>
    <dd>サービスは、3 種類の異なるトークンを使用します。 アクセス・トークンとは許可を表すものであり、{{site.data.keyword.appid_short}} で設定された許可フィルターで保護されている[バックエンド・リソース](/docs/services/appid?topic=appid-backend)との通信を可能にします。 識別トークンとは認証を表すものであり、ユーザーに関する情報が含まれています。 リフレッシュ・トークンは、ユーザーの再認証なしで新規アクセス・トークンを取得するために使用できます。 リフレッシュ・トークンを使用すると、ユーザーは自分の情報をアプリケーションに記憶させることができます。 これにより、サインインした状態を保つことができます。 トークンの設定は、{{site.data.keyword.appid_short}} ダッシュボードの<b>「ID プロバイダー」>「管理」</b>で行います。トークンおよび {{site.data.keyword.appid_short}} でトークンを使用する方法について詳しくは、[トークンの管理](/docs/services/appid?topic=appid-tokens#tokens)を参照してください。
  </dd>
  <dt>許可ヘッダー</dt>
    <dd><p>{{site.data.keyword.appid_short}} は <a href="https://tools.ietf.org/html/rfc6750" target="blank">トークン・ベアラー仕様 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> に準拠しており、HTTP 許可ヘッダーとして送信されるアクセス・トークンと識別トークンの組み合わせを使用します。 許可ヘッダーは、空白文字で区切られた 3 つの部分で構成されます。 これらのトークンは base64 でエンコードされます。 識別トークンはオプションです。</br>
    例:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]
</code></pre></dd>
  <dt>API 戦略</dt>
    <dd><p>API 戦略では、有効なアクセス・トークンを含む許可ヘッダーが要求に含まれていなければなりません。 識別トークンも要求に含めることができますが、これは必須ではありません。 トークンが無効または期限切れの場合、API 戦略は、次の HTTP ヘッダーを含む HTTP 401 エラーを返します。</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>要求から有効なトークンが返された場合、制御が次のミドルウェアに渡され、<code>appIdAuthorizationContext</code> プロパティーが要求オブジェクト内に挿入されます。 このプロパティーには、元のアクセス・トークンと識別トークン、およびデコードされたペイロード情報が平文の JSON オブジェクトとして含まれます。</dd>
  <dt>Web アプリ戦略</dt>
    <dd>Web アプリ戦略は、保護リソースに対する無許可のアクセス試行を検出すると、ユーザーのブラウザーを認証ページ ({{site.data.keyword.appid_short}} で提供可能) に自動的にリダイレクトします。 認証に成功すると、ユーザーは Web アプリのコールバック URL に返されます。 Web アプリ戦略は、アクセス・トークンと識別トークンを取得し、HTTP セッションの <code>WebAppStrategy.AUTH_CONTEXT</code> の下に保管します。 アクセス・トークンと識別トークンをアプリ・データベース内に保管するかどうかは、各ユーザーが決定します。</dd>
  <dt>データ分離と暗号化</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} は、ユーザー・プロファイル属性を保管して暗号化します。 マルチテナント・サービスでは、すべてのテナントには指定された暗号鍵がありそれぞれのテナントのユーザー・データはそのテナントの鍵だけで暗号化されます。</p>
    <p>{{site.data.keyword.appid_short_notm}} は必ず、プライベートな資料を暗号化してから保管します。</p></dd>
  <dt>リダイレクト URI</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} は、アプリとの対話後に、承認された完全修飾 URI のリストを使用してユーザーをリダイレクトします。例えば、ユーザーが正常にサインインした場合、{{site.data.keyword.appid_short_notm}} は、アプリのホーム・ページまたは指定された別のページにユーザーをリダイレクトします。URI の形式はアプリケーションによって変わる可能性があります。詳しくは、[リダイレクト URI の追加](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)を確認してください。</p></dd>
  <dt>JSON Web Key Set (JWKS)</dt>
    <dd>JWKS は、暗号鍵のセットを表します。{{site.data.keyword.appid_short_notm}} は JWKS を使用して、サービスによって生成されたトークンの真正性を検証します。鍵 ID を使用して署名を検証することにより、信頼できるソース {{site.data.keyword.appid_short_notm}} によってトークンが発行されたこと、およびトークン内の情報が変更されてはいないことを確認できます。</dd>
</dl>

