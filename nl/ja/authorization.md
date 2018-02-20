---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 許可と認証
{: authorization}

{{site.data.keyword.appid_full}} を利用すれば、ユーザーはトークンと許可フィルターを使用して、アプリを確実に保護できます。許可を付与するには、その前にユーザー ID が ID プロバイダーで認証される必要があります。
{: shortdesc}


## 主要な概念
{: key-concepts}

このサービスが許可と認証のプロセスをどのように分けているのかを理解するには、いくつかの重要な用語を理解する必要があります。

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> は、アプリに許可を実装するために使用されているオープン・スタンダードのプロトコルです。</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> は、OAuth 2 を基礎として機能する認証レイヤーです。</dd>
  <dt>アクセス・トークン</dt>
    <dd><p>アクセス・トークンとは許可を表すものであり、{{site.data.keyword.appid_short}} で設定された許可フィルターで保護されている、[バックエンド・リソース](/docs/services/appid/protecting-resources.html)との通信を可能にします。このトークンは JavaScript Object Signing and Encryption (JOSE) 仕様に準拠しています。これらのトークンは、<a href="https://jwt.io/introduction/" target="blank">JSON Web トークン<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>としてフォーマットされます。
</br>
例:</p>
    <pre><code>Header: {
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
    </code></pre></dd>
  <dt>識別トークン</dt>
    <dd><p>識別トークンとは認証を表すものであり、ユーザーに関する情報が含まれています。名前、E メール、性別、場所に関する情報を提供できます。 トークンはユーザーのイメージへの URL を返すこともできます。</br>
例:</p>
    <pre><code>Header: {
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
        "picture": "<URL-to-photo>",
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
    </pre></code></dd>
  <dt>許可ヘッダー</dt>
    <dd><p>{{site.data.keyword.appid_short}} は <a href="https://tools.ietf.org/html/rfc6750" target="blank">トークン・ベアラー仕様 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> に準拠しており、HTTP 許可ヘッダーとして送信されるアクセス・トークンと識別トークンの組み合わせを使用します。許可ヘッダーは、空白文字で区切られた 3 つの部分で構成されます。これらのトークンは base64 でエンコードされます。識別トークンはオプションです。</br>
例:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API 戦略</dt>
    <dd><p>API 戦略では、有効なアクセス・トークンを含む許可ヘッダーが要求に含まれていなければなりません。 識別トークンも要求に含めることができますが、これは必須ではありません。トークンが無効または期限切れの場合、API 戦略は、次の HTTP ヘッダーを含む HTTP 401 エラーを返します。</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>要求から有効なトークンが返された場合、制御が次のミドルウェアに渡され、<code>appIdAuthorizationContext</code> プロパティーが要求オブジェクト内に挿入されます。このプロパティーには、元のアクセス・トークンと識別トークン、およびデコードされたペイロード情報が平文の JSON オブジェクトとして含まれます。</dd>
  <dt>Web アプリ戦略</dt>
    <dd>Web アプリ戦略は、保護リソースに対する無許可のアクセス試行を検出すると、ユーザーのブラウザーを認証ページ ({{site.data.keyword.appid_short}} で提供可能) に自動的にリダイレクトします。認証に成功すると、ユーザーは Web アプリのコールバック URL に返されます。 Web アプリ戦略は、アクセス・トークンと識別トークンを取得し、HTTP セッションの <code>WebAppStrategy.AUTH_CONTEXT</code> の下に保管します。アクセス・トークンと識別トークンをアプリ・データベース内に保管するかどうかは、各ユーザーが決定します。</dd>
</dl>

</br>

## このプロセスの仕組み
{: #process}

アプリをコーディングするときの重要な問題の 1 つはセキュリティーです。適切な権限を持つユーザーだけがアプリを使用できるようにするには、どうすればよいでしょうか? 許可プロセスを使用します。大多数のアプリケーションでは、許可と認証のプロセスが一緒になっているため、セキュリティー・ポリシーと ID プロバイダーを変更することが複雑になります。{{site.data.keyword.appid_short}} では、許可と認証は別々のプロセスです。{: shortdesc}

Facebook などのソーシャル ID プロバイダーを構成した場合は、[Oauth2 許可付与フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)によってログイン・ウィジェットが呼び出されます。クラウド・ディレクトリーを ID プロバイダーとして使用する場合は、[リソース所有者のパスワード資格情報フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)によってアクセス・トークンと識別トークンを取得できます。

![識別されたユーザーになるまでの道のり](/images/authenticationtrail.png)

サインインを選択したユーザーは、識別されたユーザーになります。ユーザーがサインインに使用した ID プロバイダーから、ユーザーの情報を取得できます。ID プロバイダーは、ユーザーの情報が入ったアクセス・トークンと識別トークンを {{site.data.keyword.appid_short}} に返します。サービスは、それらの提供されたトークンを取得し、アプリにアクセスできる適切な資格情報をユーザーが持っているかどうかを判別します。トークンが有効であることが検証されると、サービスはユーザーにアクセスを許可します。許可されたユーザーの認証情報には、ユーザー・レコードが関連付けられます。このレコードとその属性には、同じ ID で認証されたすべてのクライアントから再びアクセスできます。

### 段階的な認証

{{site.data.keyword.appid_short_notm}} では、匿名ユーザーが、識別されたユーザーになることを選択できます。

その仕組みを説明します。

すぐにサインインしないことを選択したユーザーは、匿名ユーザーと見なされます。例えば、ユーザーはサインインしなくても、すぐにショッピング・カートにアイテムを追加し始めることができます。匿名ユーザーに対して、{{site.data.keyword.appid_short_notm}} は一時的なユーザー・レコードを作成し、匿名のアクセス・トークンと識別トークンを返す OAuth ログイン API を呼び出します。これらのトークンを使用して、アプリはユーザー・レコードに保管される属性の作成、読み取り、更新、削除を行うことができます。

![匿名で開始したユーザーが、識別されたユーザーになるまでの道のり。](/images/anon-authenticationtrail.png)

匿名ユーザーがサインインすると、匿名のアクセス・トークンがログイン API に渡されます。このサービスは、ID プロバイダーを使用して呼び出しを認証します。 このサービスは、アクセス・トークンを使用して匿名レコードを検出し、そこに ID を付加します。 新しいアクセス・トークンと識別トークンには、ID プロバイダーから提供された公開情報が入っています。ユーザーの識別後には、そのユーザーの匿名トークンは無効になります。 しかし、引き続きユーザーは自分の属性にアクセスできます。新しいトークンを使用してアクセスできるからです。

**注**: ID を匿名レコードに割り当てられるのは、別のユーザーに割り当て済みでない場合に限られます。 ID が既に別の {{site.data.keyword.appid_short_notm}} ユーザーに関連付けられている場合、トークンにはそのユーザーのレコードの情報が入っているので、ユーザー属性にアクセスできます。前の匿名ユーザーの属性に、新しいトークンを使用してアクセスすることはできません。 トークンの有効期限が切れるまでは、匿名アクセス・トークンにより引き続き情報にアクセスできます。 開発中に、既知のユーザーに匿名属性をマージする方法を選択できます。
