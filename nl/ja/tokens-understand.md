---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

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



# トークンについて
{: #tokens}

ユーザーが正常に認証されると、アプリケーションは {{site.data.keyword.appid_short_notm}} からトークンを受け取ります。 サービスは、主要な 3 種類のトークンを使用して認証プロセスを実行します。
{: shortdesc}


## アクセス・トークン
{: #access}

アクセス・トークンとは許可を表すものであり、{{site.data.keyword.appid_short}} で設定された許可フィルターで保護されている[バックエンド・リソース](/docs/services/appid?topic=appid-backend)との通信を可能にします。 このトークンは JavaScript Object Signing and Encryption (JOSE) 仕様に準拠しています。 トークンは、<a href="https://jwt.io/introduction/" target="blank">JSON Web トークン <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> としてフォーマットされ、RS256 アルゴリズムを使用した JSON Web Key で署名されます。

トークンの例:
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
  }
  ```
  {: screen}

## 識別トークンとは
{: #identity}

識別トークンとは認証を表すものであり、ユーザーに関する情報が含まれています。 名前、E メール、性別、場所に関する情報を提供できます。 トークンはユーザーのイメージへの URL を返すこともできます。 トークンは、<a href="https://jwt.io/introduction/" target="blank">JSON Web トークン <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> としてフォーマットされ、RS256 アルゴリズムを使用した JSON Web Key で署名されます。

トークンの例:
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "exp": 1551903163,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "iat": 1551899553,
    "email": "appid155@mailinator.com",
    "name": "appid155@mailinator.com",
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "identities": [
      {
        "provider": "cloud_directory",
        "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
    ],
    "amr": [
      "cloud_directory"
    ]
  }
  ```
  {: screen}


識別トークンには、部分的なユーザー情報のみが含まれます。 ID プロバイダーによって提供されるすべての情報を参照するには、[/userinfo エンドポイント](/docs/services/appid?topic=appid-predefined-attributes#predefined-access-api)を使用することができます。

## リフレッシュ・トークンとは
{: #refresh}

{{site.data.keyword.appid_short}} は、<a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> で定義されているように、再認証なしで新規のアクセス・トークンと識別トークンを取得する機能をサポートしています。 リフレッシュ・トークンを使用してアクセス・トークンを更新すれば、ユーザーはサインインのための操作 (資格情報の入力など) を行わなくてもよくなります。 アクセス・トークンと同様、リフレッシュ・トークンには、許可されたユーザーかどうかを {{site.data.keyword.appid_short_notm}} が判別できるようにするデータが含まれています。 ただし、このトークンは内部が見えない状態になっています。

リフレッシュ・トークンは、通常のアクセス・トークンより存続期間が長くなるように構成されているため、アクセス・トークンが期限切れになっても、リフレッシュ・トークンは引き続き有効で、アクセス・トークンを更新するために使用できます。 {{site.data.keyword.appid_short_notm}} のリフレッシュ・トークンは、1 日から 90 日の範囲で存続期間を構成できます。 リフレッシュ・トークンを最大限に活用するには、トークンの存続期間が満了するかトークンが更新されるまでトークンを持続させておきます。 ユーザーはリフレッシュ・トークンだけではリソースに直接アクセスすることができないため、アクセス・トークンを持続させておくよりリフレッシュ・トークンを持続させておく方がずっと安全です。 ベスト・プラクティスとして、リフレッシュ・トークンは、それを受信したクライアントで安全に保管し、その発行元となった許可サーバーにのみ送信するようにしてください。

利便性の向上のために、{{site.data.keyword.appid_short_notm}} は、アクセス・トークンの更新時にリフレッシュ・トークン (およびその有効期限) も更新します。これによりユーザーは、現行のリフレッシュ・トークンが期限切れになる前のいずれかの時点でアクティブであれば、ログインした状態を保つことができます。 一方、リフレッシュ・トークンを使用するものの、周期的にユーザーにログインを強制する場合は、ユーザーが資格情報を入力してログインしたときに返されるリフレッシュ・トークンのみをアプリで使用するようにします。 しかし、<a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">OAuth 2.0 仕様 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> に記載されているように、{{site.data.keyword.appid_short_notm}} から受信した最新のリフレッシュ・トークンを常に使用することをお勧めします。


このトークンはログイン・プロセスの合理化に役立つとはいえ、それに依存するアプリは作成しないようにしてください。リフレッシュ・トークンは、漏えいが疑われる場合などにいつでも取り消される可能性があるためです。 リフレッシュ・トークンを取り消す必要がある場合、リフレッシュ・トークンを取り消す方式が 2 種類あります。 リフレッシュ・トークンがある場合は、<a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> に基づいて取り消すことができます。 別の方式として、ユーザー ID がある場合は、<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用してリフレッシュ・トークンを取り消すことができます。 管理 API へのアクセスについて詳しくは、[サービス・アクセスの管理](/docs/services/appid?topic=appid-service-access-management#service-access-management)を参照してください。

リフレッシュ・トークンの処理の例や、リフレッシュ・トークンを使用してユーザー情報を記憶させる機能を実装する方法については、[概説のサンプル](/docs/services/appid?topic=appid-getting-started#getting-started)を参照してください。


## トークンの発行元
{: #where}

トークンは、{{site.data.keyword.appid_short_notm}} OAuth Server によって発行され、[JSON Web トークン (JWT)](https://jwt.io/introduction/) としてフォーマットされます。 トークンは、RS256 アルゴリズムを使用した [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) によって署名されます。

## トークンに含まれる情報の扱い
{: #contains}

アクセス・トークンには、一連の標準 JWT クレームと、一連の {{site.data.keyword.appid_short_notm}} 固有クレーム (テナント ID など) が格納されます。 識別トークンには、ユーザー固有の情報が格納されます。 トークン内の情報は、[ユーザー・プロファイル](/docs/services/appid?topic=appid-user-profile#user-profile)の一部となるクレームとして保管されます。

## トークンの受信方法
{: #received}

認証が成功すると、アプリがトークンを受信します。 アプリはトークンを使用して、ユーザーの許可と認証に関する情報を取得します。 アクセス・トークンを使用すると、保護リソースに要求を送信して、リソースへのアクセス権限を得ることができます。 要求において、アクセス・トークンは[ベアラー認証スキーム](https://tools.ietf.org/html/rfc6750#page-5)で記述されます。 アプリは、トークンを抽出するためにヘッダーを解析する必要があります。

要求例:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## トークンの設定方法
{: #set}

トークン構成は {{site.data.keyword.appid_short_notm}} ダッシュボードで有効にしたり無効にしたりできます。構成オプションについて詳しくは、[トークンの管理](/docs/services/appid?topic=appid-managing-idp#managing-idp)を参照してください。
