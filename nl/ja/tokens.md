---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, tokens, jwt, development

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


# トークンの検証
{: #token-validation}

トークン検証は、最近のアプリ開発において重要な部分になっています。 トークンを検証することで、無許可ユーザーからアプリや API を保護できます。 {{site.data.keyword.appid_full}} は、アクセス・トークンと ID トークンを使用して、アクセス権限を付与する前に必ずユーザーまたはアプリを認証します。 {{site.data.keyword.appid_short_notm}} が提供するいずれかの SDK を使用している場合は、トークンの取得と検証の両方が自動的に行われます。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} でのトークンの使用方法について詳しくは、[トークンについて](/docs/services/appid?topic=appid-tokens#tokens)を参照してください。
{: tip}

トークンは、個人が本人であることを検証するために使用されます。 また、指定された期間、ユーザーが保持するアクセス許可が正しいことを確認します。 ユーザーがアプリケーションにサインインしてトークンが発行されると、アプリは、アクセス権限を付与する前にそのユーザーを検証する必要があります。

</br>

**{{site.data.keyword.appid_short_notm}} に該当の SDK がない言語で作業している場合はどうすればよいですか?**

心配無用です! 次の 3 つのオプションがあります。

* {{site.data.keyword.appid_short_notm}} API を使用して作業する
* 独自の検証ロジックを実装する
* OIDC 準拠のオープン・ソース SDK を使用する

フィードバックによれば、通常はオプション 1 が最も簡単な方法です。
{: tip}

</br>
</br>

## {{site.data.keyword.appid_short_notm}} API の使用
{: #remote-validation}

イントロスペクションを使用することにより、{{site.data.keyword.appid_short_notm}} を使用してトークンを検証できます。
{: shortdesc}

1. [/introspect](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token) API エンドポイントに POST 要求を送信してトークンを検証します。 要求には、トークンと、クライアント ID およびシークレットを入れた基本許可ヘッダーを含める必要があります。

  要求例:

    ```
    POST /oauth/v4/{tenant_id}/introspect HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. サーバーは、トークンの有効期限と署名を検査し、トークンがアクティブか非アクティブかを示す JSON オブジェクトを返します。

  応答例:

    ```
    {
      "active": true
    }
    ```
    {: screen}


## トークンの手動検証
{: #local-validation}

トークンを構文解析し、トークンの署名を検証し、トークンに保管されているクレームを検証することによって、トークンをローカルで検証できます。
{: shortdesc}


1. トークンを解析します。 [JSON Web トークン (JWT)](https://tools.ietf.org/html/rfc7519) は、情報を安全に渡すための標準的な方法です。 これはヘッダー、ペイロード、および署名という 3 つの主要部分で構成されています。 これらは base64URL でエンコードされ、ドット (.) で区切られます。 使用できる任意の base64URL デコーダーを使用して、トークンを解析することができます。 別の方法として、[リストされているライブラリー](https://jwt.io/#libraries-io)のいずれかを使用してトークンを解析することもできます。

  エンコードされたトークンの例:

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  デコードされたヘッダーの例:

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  デコードされたペイロード:

    ```
    {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. [/publickeys エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys)に対して呼び出しを行って、公開鍵を取得します。 返される公開鍵は、[JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) としてフォーマット設定されます。

  要求例:

    ```
    GET /oauth/v4/{tenant_id}/publickeys HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Cache-Control: no-cache
    ```
    {: screen}

3. 後で使用できるように、鍵をアプリ・キャッシュに保管します。 鍵を保管すると、プロセスが高速化され、別の呼び出しが行われた場合のネットワーク遅延が防止されます。

4. 公開鍵のパラメーターをインポートします。

  応答例:

    ```
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> 公開鍵のパラメーター </th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>使用するアルゴリズムを定義します。</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>鍵の目的を定義します。</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>鍵の固有 ID を定義します。</td>
      </tr>
      <tr>
        <td>その他</td>
        <td>同様にインポートする必要のある、ご使用のアルゴリズムに固有の他のパラメーターも存在している可能性があります。</td>
      </tr>
    </tbody>
  </table>

5. トークンの署名を検査します。 トークン・ヘッダーには、トークンの署名に使用されたアルゴリズムと、対応する公開鍵の鍵 ID (つまり `kid` クレーム) が含まれます。 公開鍵は頻繁には変更されないため、公開鍵をアプリのキャッシュに入れて、時々リフレッシュすることができます。 キャッシュに入れられた鍵に `kid` クレームがない場合は、それらのトークンをローカル側で検証できます。

  1. アプリケーションで、着信トークン・ヘッダーの内容が公開鍵のパラメーターと一致することを検査します。
  2. 特に、同じアルゴリズムが使用されたことと、公開鍵キャッシュの中に、関連する鍵 ID を持つ鍵が含まれていることを検査します。
  3. ハッシュ値が PEM 形式の公開鍵の署名と同じであることを確認します。 ハッシュ値は、トークンのペイロードのヘッダーを結合してハッシュすることによって取得できます。 このプロセスの手動による実装は複雑になることがあるので、[リストされているライブラリー](https://jwt.io/)のいずれかを使用して署名を検証すると役立つ場合があります。

6. トークンに保管されているクレームを検証します。 今後の検査を検証するには、[このリスト](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation)を使用できます。
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> 検証する必要があるクレーム </th>
    </thead>
    <tbody>
      <tr>
        <td><code> iss </code></td>
        <td>発行者は、{{site.data.keyword.appid_short_notm}} OAuth サーバーと同じでなければなりません。</td>
      </tr>
      <tr>
        <td><code> exp </code></td>
        <td>現在時刻は有効期限時刻より前でなければなりません。</td>
      </tr>
      <tr>
        <td><code> aud </code></td>
        <td>オーディエンスには、アプリのクライアント ID が含まれている必要があります。</td>
      </tr>
      <tr>
        <td><code> tenant </code></td>
        <td>テナントには、アプリのテナント ID が含まれている必要があります。</td>
      </tr>
      <tr>
        <td><code>scope</code></td>
        <td>ユーザーに付与される許可のスコープ。 これはアクセス・トークンに固有のものです。</td>
      </tr>
    </tbody>
  </table>
