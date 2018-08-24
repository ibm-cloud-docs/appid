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

# 許可と認証
{: #authorization}

{{site.data.keyword.appid_full}} を利用すれば、ユーザーはトークンと許可フィルターを使用して、アプリを確実に保護できます。 ユーザーがアプリに許可を付与するためには、その前に ID プロバイダーがそのユーザーの ID を認証しておく必要があります。
{: shortdesc}


## 主要な概念
{: #key-concepts}

以下の重要な用語は、このサービスが許可と認証のプロセスをどのように分けているかを理解するのに役立ちます。

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> は、アプリに許可を実装するために使用されているオープン・スタンダードのプロトコルです。</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> は、OAuth 2 を基礎として機能する認証レイヤーです。</p>
    <p>OIDC と {{site.data.keyword.appid_short_notm}} を一緒に使用する場合、OAuth エンドポイントを構成するときにサービス資格情報が役立ちます。SDK を使用する場合、エンドポイント URL は自動的に作成されます。しかし、サービス資格情報を使用して、URL を自分で作成することもできます。以下の例と表で、URL を構成する方法を示します。</p>
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
        <td>Userinfo</td>
        <td>{oauthServerUrl}/userinfo</td>
      </tr>
      <tr>
        <td>JWKS</td>
        <td>{oauthServerUrl}/publickeys</td>
      </tr>
    </table>
    <p><strong>注</strong>: SDK を使用する場合、エンドポイント URL は自動的に作成されます。</p></dd>
  <dt>トークン</dt>
    <dd>サービスは、3 種類の異なるトークンを使用して認証を実現します。アクセス・トークンとは許可を表すものであり、{{site.data.keyword.appid_short}} で設定された許可フィルターで保護されている[バックエンド・リソース](/docs/services/appid/protecting-resources.html)との通信を可能にします。 識別トークンとは認証を表すものであり、ユーザーに関する情報が含まれています。 リフレッシュ・トークンとは、存続期間が延長されたアクセス・トークンです。リフレッシュ・トークンを使用すると、ユーザーは自分の情報をアプリケーションに記憶させることができます。これにより、サインインした状態を保つことができます。
  </dd>
  <dt>許可ヘッダー</dt>
    <dd><p>{{site.data.keyword.appid_short}} は <a href="https://tools.ietf.org/html/rfc6750" target="blank">トークン・ベアラー仕様 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> に準拠しており、HTTP 許可ヘッダーとして送信されるアクセス・トークンと識別トークンの組み合わせを使用します。 許可ヘッダーは、空白文字で区切られた 3 つの部分で構成されます。 これらのトークンは base64 でエンコードされます。 識別トークンはオプションです。</br>
    例:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API 戦略</dt>
    <dd><p>API 戦略では、有効なアクセス・トークンを含む許可ヘッダーが要求に含まれていなければなりません。 識別トークンも要求に含めることができますが、これは必須ではありません。 トークンが無効または期限切れの場合、API 戦略は、次の HTTP ヘッダーを含む HTTP 401 エラーを返します。</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>要求から有効なトークンが返された場合、制御が次のミドルウェアに渡され、<code>appIdAuthorizationContext</code> プロパティーが要求オブジェクト内に挿入されます。 このプロパティーには、元のアクセス・トークンと識別トークン、およびデコードされたペイロード情報が平文の JSON オブジェクトとして含まれます。</dd>
  <dt>Web アプリ戦略</dt>
    <dd>Web アプリ戦略は、保護リソースに対する無許可のアクセス試行を検出すると、ユーザーのブラウザーを認証ページ ({{site.data.keyword.appid_short}} で提供可能) に自動的にリダイレクトします。 認証に成功すると、ユーザーは Web アプリのコールバック URL に返されます。 Web アプリ戦略は、アクセス・トークンと識別トークンを取得し、HTTP セッションの <code>WebAppStrategy.AUTH_CONTEXT</code> の下に保管します。 アクセス・トークンと識別トークンをアプリ・データベース内に保管するかどうかは、各ユーザーが決定します。</dd>
  <dt>データ分離と暗号化</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} は、ユーザー・プロファイル属性を保管して暗号化します。 マルチテナント・サービスでは、すべてのテナントには指定された暗号鍵がありそれぞれのテナントのユーザー・データはそのテナントの鍵だけで暗号化されます。</p>
    <p>{{site.data.keyword.appid_short_notm}} は必ず、プライベートな資料を暗号化してから保管します。</p></dd>
</dl>

</br>

## このプロセスの仕組み
{: #process}

アプリをコーディングするときの重要な問題の 1 つはセキュリティーです。 適切な権限を持つユーザーだけがアプリを使用できるようにするには、どうすればよいでしょうか? 許可プロセスを使用します。 ほとんどのプロセスでは、許可と認証は一体化されるため、セキュリティー・ポリシーと ID プロバイダーの変更が複雑になる場合があります。 {{site.data.keyword.appid_short}} では、許可と認証は別々のプロセスです。
{: shortdesc}

Facebook などのソーシャル ID プロバイダーを構成した場合は、[Oauth2 許可付与フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)によってログイン・ウィジェットが呼び出されます。 クラウド・ディレクトリーを ID プロバイダーとして使用する場合は、[リソース所有者のパスワード資格情報フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)によってアクセス・トークンと識別トークンを取得できます。

![識別されたユーザーになるまでの道のり](/images/authenticationtrail.png)

サインインを選択したユーザーは、識別されたユーザーになります。 ID プロバイダーは、ユーザーの情報が入ったアクセス・トークンと識別トークンを {{site.data.keyword.appid_short}} に返します。 サービスは、それらの提供されたトークンを取得し、アプリにアクセスできる適切な資格情報をユーザーが持っているかどうかを判別します。 トークンが有効であることが検証されると、サービスはユーザーにアクセスを許可します。 ユーザーが許可されると、ユーザーのレコードに認証情報が関連付けられます。 このレコードとその属性には、同じ ID で認証されたすべてのクライアントから再びアクセスできます。

### 段階的な認証

{{site.data.keyword.appid_short_notm}} では、匿名ユーザーが、識別されたユーザーになることを選択できます。

その仕組みを説明します。

すぐにサインインしないことを選択したユーザーは、匿名ユーザーと見なされます。 例えば、ユーザーはサインインしなくても、すぐにショッピング・カートにアイテムを追加し始めることができます。 匿名ユーザーの場合、{{site.data.keyword.appid_short_notm}} は一時的なユーザー・レコードを作成し、匿名のアクセス・トークンと識別トークンを返す OAuth ログイン API を呼び出します。 これらのトークンを使用して、アプリはユーザー・レコードに保管される属性の作成、読み取り、更新、削除を行うことができます。

![匿名で開始したユーザーが、識別されたユーザーになるまでの道のり。](/images/anon-authenticationtrail.png)

匿名ユーザーがサインインすると、そのユーザーのアクセス・トークンがログイン API に渡されます。 このサービスは、ID プロバイダーを使用して呼び出しを認証します。 このサービスは、アクセス・トークンを使用して匿名レコードを検出し、そこに ID を付加します。 新しいアクセス・トークンと識別トークンには、ID プロバイダーから提供された公開情報が入っています。 ユーザーが識別されると、そのユーザーの匿名トークンは無効になります。 しかし、引き続きユーザーは自分の属性にアクセスできます。新しいトークンを使用してアクセスできるからです。

匿名レコードに ID を割り当てることができるのは、その ID が別のユーザーにまだ割り当てられていない場合に限ります。
{: tip}

ID が既に別の {{site.data.keyword.appid_short_notm}} ユーザーに関連付けられている場合、トークンにはそのユーザーのレコードの情報が入っているので、ユーザー属性にアクセスできます。 前の匿名ユーザーの属性に、新しいトークンを使用してアクセスすることはできません。 トークンの有効期限が切れるまでは、匿名アクセス・トークンにより引き続き情報にアクセスできます。 開発中に、既知のユーザーに匿名属性をマージする方法を選択できます。
