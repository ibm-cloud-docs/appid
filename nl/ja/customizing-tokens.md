---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

keywords: authentication, authorization, identity, app security, secure, custom, tokens, access, claim, attributes

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


# トークンのカスタマイズ
{: #customizing-tokens}

アプリケーションの特定のニーズを満たすように {{site.data.keyword.appid_short_notm}} トークンを構成できます。
{: shortdesc}

## カスタマイズについて
{: #understanding-customization}

{{site.data.keyword.appid_short_notm}} は、さまざまなタイプのトークンを使用してアプリケーションを保護します。

* アクセス・トークン: 許可フィルターによって保護されている、バックエンド・リソースとの通信を可能にします。 アクセス・トークンが特定のユーザーに関連付けられていない場合、そのトークンの機能は限定的なものとなります。
* 識別トークン: 個人情報を格納し、ユーザーの認証に使用されます。 アプリの構成によっては、ユーザーが認証される前に識別トークンを発行できます。 これにより、ユーザーがアプリケーションにサインインする前に、ユーザーと属性の関連付けを開始できます。
* リフレッシュ・トークン: ユーザーが再認証せずにログイン状態を保持できる時間を延長するために使用できます。

トークンについて詳しくは、 [トークンについて](/docs/services/appid?topic=appid-tokens#tokens)を参照してください。
{: tip}


トークンのカスタマイズは、[GUI で](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-ui)行えます。あるいは、[API](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-api) を使用して、有効存続期間を設定するか、カスタム・クレームをトークンに追加することによって行うこともできます。 存続期間の構成方法を確認する場合は以下の表を参照してください。カスタム属性のマッピングについて学習する場合はこのまま読み進めてください。

<table>
  <tr>
    <th>トークンのタイプ</th>
    <th>値のタイプ</th>
    <th>デフォルト</th>
    <th>オプション</th>
  </tr>
  <tr>
    <td>アクセス</td>
    <td>分</td>
    <td>60</td>
    <td>5 から 1440 までの任意の値</td>
  </tr>
  <tr>
    <td>ID</td>
    <td>分</td>
    <td>60</td>
    <td>5 から 1440 までの任意の値</td>
  </tr>
  <tr>
    <td>リフレッシュ</td>
    <td>日</td>
    <td>30</td>
    <td>1 から 9 までの任意の値</td>
  </tr>
  <tr>
    <td>匿名</td>
    <td>日</td>
    <td>30</td>
    <td>1 から 9 までの任意の値</td>
  </tr>
</table>


トークンはユーザーの識別とリソースの保護に使用されるため、トークンの存続期間の影響を受ける要素がいくつかあります。 トークンの構成をカスタマイズすることにより、セキュリティーとユーザー・エクスペリエンスのニーズを満たすことができます。 ただし、万一トークンが漏えいした場合は、悪意のあるユーザーがアプリケーションに影響を与えることができる時間が長くなります。 セキュリティーに関する考慮事項の詳細は、[カスタム属性の設定](/docs/services/appid?topic=appid-profiles#profile-set-custom)で確認できます。
{: important}


## カスタム属性およびクレームについて
{: #custom-claims}

ユーザー・プロファイルの属性をアクセス・トークンと識別トークンのクレームにマップできます。 これは、[/userinfo エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo)に移動したり、後でカスタム属性をプルしたりする必要がないことを意味します。それらは既にトークンに格納されているからです。
{: shortdesc}

### クレームとは?
{: #custom-claims-defined}

クレームとは、エンティティーが自身について、または他者のために出すステートメントのことです。 例えば、あるユーザーが ID プロバイダーを使用してあるアプリケーションにサインインした場合、プロバイダーはそのユーザーに関連した一連のクレーム (つまりステートメント) をそのアプリケーションに送信します。アプリケーションは、それをそのユーザーに関する既知の情報と一緒にグループ化することができます。 このように、サインインすると、構成されたとおりにそのユーザーの情報がアプリにセットアップされます。 JSON オブジェクトのフォーマット設定を次の例で確認してください。

```
{
  "accessTokenClaims": [
            {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
       "idTokenClaims": [
           {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
  "access": {
    "expires_in": 3600
  },
  "refresh": {
    "expires_in": 2592000,
    "enabled": true
  },
  "anonymousAccess": {
    "expires_in": 2592000,
    "enabled": true
  }
}
```
{: screen}

トークンの有効期限情報をカスタマイズした場合は、どの要求にもその有効期限情報を設定する必要があります。 設定しない場合、その要求は現在の構成をオーバーライドし、未定義のままのものにはデフォルトが使用されます。
{: note}

### トークンにクレームを追加するメリットは何ですか?
{: #why-custom-claims}

追加のネットワーク呼び出しを行わなくても、アプリで必要になる可能性がある、ユーザーに関する情報や、ユーザーが実行できる操作に関する情報をすべて、前もってトークンに入れておくことができます。 大量のデータを扱うのでなければ、この方が効率的です。 また、マップされたこれらの属性は、署名済みトークンに格納されるため、ネットワーク上を送信されるときにその整合性を確保できます。


### どんなタイプのクレームを定義できますか?
{: #custom-claim-types}

{{site.data.keyword.appid_short_notm}} で提供されるクレームは、カスタマイズのレベルが異なるいくつかのカテゴリーに分類されます。

*登録済みクレーム*: {{site.data.keyword.appid_short_notm}} で定義されている、アクセス・トークンおよび識別トークンのクレームのいくつかは、カスタム・マッピングによってオーバーライドできません。 クレームが制限されている場合、そのクレームはサービスで無視されます。 この種類のクレームとして、`iss`、`aud`、`sub`、`iat`、`exp`、`amr`、`tenant` があります。

*制限付きクレーム*: クレームのマップ先となるトークンに応じて、一部のクレームではカスタマイズの自由度が制限されます。 アクセス・トークンの場合、制限付きクレームは `scope` のみです。 これをカスタム・マッピングでオーバーライドすることはできませんが、独自のスコープを使用して拡張することはできます。 scope クレームをアクセス・トークンにマップするとき、その値はストリングでなければならず、その接頭部が `appid_` であってもなりません。そうでないと無視されます。 識別トークンの場合、クレーム `identities` および `oauth_clients` を変更およびオーバーライドすることはできません。

*正規化クレーム*: すべての識別トークンには、{{site.data.keyword.appid_short_notm}} によって正規化クレームとして認識される一連のクレームがあります。 それらは、使用可能な場合に ID プロバイダーからトークンに直接マップされます。 それらのクレームは明示的に省略することはできませんが、トークン内でカスタム・クレームで上書きできます。この種類のクレームとして、`name`、`email`、`picture`、`local`、`gender` があります。 注: これによって属性が変更または除去されるわけではありません。実行時に、トークン内に存在する情報が変更されるだけです。


### クレームはトークンにどのようにマップされますか?
{: #custom-claims-mapping}

各マッピングは、データ・ソース・オブジェクトと、クレームの取得に使用される鍵によって定義されます。 各カスタム・クレームは、トークンごとに別個に設定され、順次適用されます。 トークン 1 つにつき最大 100 個のクレームを登録可能で、最大ペイロードは 100KB です。

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="アイデア・アイコン"/> クレーム・マッピング・オブジェクトについて</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>必須</td>
        <td>クレームのソースを定義します。 ID プロバイダーのユーザー情報またはユーザーの {{site.data.keyword.appid_short_notm}} カスタム属性を参照できます。 </br> オプションとして、`saml`、`cloud_directory`、`facebook`、`google`、`appid_custom`、`ibmid`、`attributes` があります。</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>必須</td>
        <td>ソース・データのクレームを定義します。 </td>
      </tr>
    </tbody>
  </table>

ドット構文を使用すると、ネストされたクレームをマッピングで参照できます。 例: `nested.attribute`
{:tip}

</br>

## {{site.data.keyword.appid_short_notm}} トークンの構成
{: #configuring-tokens}

GUI または管理 API を使用して、{{site.data.keyword.appid_short_notm}} トークンを構成できます。
{: shortdesc}


### GUI を使用したトークン存続期間の構成
{: #configuring-tokens-ui}

1. サービス・ダッシュボードにナビゲートします。
2. ナビゲーションの**「ID プロバイダー」**セクションで、**「管理」**ページを選択します。
3. **「設定」**タブで、トークンを構成します。
  1. ユーザー対話なしでサインインできるようにするには、**「リフレッシュ・トークン」**を**「オン」**に設定します。
  2. リフレッシュ・トークンの存続期間を設定します。 有効期限は日単位で設定され、1 から 90 の範囲の値を使用できます。 数値が小さいほど、ユーザーはより頻繁にサインインする必要があります。
  3. アクセス・トークンの存続期間を設定します。 有効期限は分単位で設定され、5 から 1440 の範囲の値を使用できます。 値が小さいほど、トークンの盗用に対する保護を強化できます。
  4. 匿名トークンの存続期間を設定します。 [匿名トークン](/docs/services/appid?topic=appid-anonymous#anonymous)は、ユーザーがアプリとの対話を開始するときにユーザーに割り当てられます。 ユーザーがサインインすると、匿名トークン内の情報が、そのユーザーに関連付けられたトークンに転送されます。 有効期限は日単位で設定され、1 から 90 までの値を使用できます。

</br>

### 管理 API を使用したトークンの構成
{: #configuring-tokens-api}

**始める前に**

以下の前提条件を満たしていることを確認してください。

* {{site.data.keyword.appid_short_notm}} インスタンスのテナント ID。 これは、GUI の**「サービス資格情報」**セクションにあります。
* Identity and Access Management (IAM) トークン。 IAM トークンの取得については、[IAM の資料](/docs/iam?topic=iam-iamtoken_from_apikey)を参照してください。

**クレームのマッピング**

1. トークンの構成によって、`/config/tokens` エンドポイントへの PUT 要求を行います。

  ヘッダー:
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: codeblock}

  本体:
  ```
   {
       "access": {
           "expires_in": 3600,
       },
       "refresh": {
           "expires_in": 2592000,
           "enabled": true
       },
       "anonymous": {
           "expires_in": 2592000,
           "enabled": true
       },
       "accessTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "name_id"
           }
       ],
       "idTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "attributes.uid"
           }
       ]
   }
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="アイデア・アイコン"/> トークンの構成について</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>オプション</td>
        <td>アクセス・トークンと識別トークンの有効期限 `expires_in` (分単位) を格納するオブジェクト。 </br> </br> デフォルトの有効期限は 60 分です。 </td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>オプション</td>
          <td>リフレッシュ・トークンの有効期限 `expires_in` (日単位) を格納するオブジェクト。 </br> </br> デフォルトの有効期限は 30 日です。 </td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>オプション</td>
          <td>匿名アクセスおよび識別トークンの有効期限 `expires_in` (日単位) を格納するオブジェクト。 </br> </br> デフォルトの有効期限は 30 日です。
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>オプション</td>
          <td>アクセス・トークンに関連したクレームのマップ時に作成されるオブジェクトを格納する配列。</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>オプション</td>
          <td>識別トークンに関連したクレームのマップ時に作成されるオブジェクトを格納する配列。</td>
      </tr>
    </tbody>
  </table>

  要求例:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
           }
          ],
       "idTokenClaims": [
           {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
  }' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
