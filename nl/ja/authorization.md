---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 許可と認証
{: authorization}

許可とは、アプリにアクセス権限を付与するプロセスのことです。{{site.data.keyword.appid_short}} サービスではトークン、フィルター、ヘッダーを使用してユーザーを認証します。
{: shortdesc}


## OAuth ID
{: #oauth}

このサービスが OAuth ログイン API を呼び出すと、{{site.data.keyword.appid_short_notm}} は OAuth 2.0 と OpenID Connect (OIDC) プロトコルを使用して、選択された ID プロバイダーを使って呼び出し元の認証と権限の付与を行います。認証された後、ID は {{site.data.keyword.appid_short_notm}} ユーザー・レコードと関連付けられます。 {{site.data.keyword.appid_short_notm}} は、ユーザーの属性にアクセスするために使用できるアクセス・トークンと、ID プロバイダーから提供された ID 情報を保持する識別トークンを返します。 同じ ID で認証されたすべてのクライアントから、この同じユーザー・レコードと属性に再びアクセスできます。

## アクセス・トークンと識別トークン

{{site.data.keyword.appid_short}} は、アクセス・トークンと識別トークンという 2 つのタイプのトークンを使用します。
{:shortdesc}

**注**: これらのトークンは、<a href="https://jwt.io/introduction/" target="_blank">JSON Web トークン <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> としてフォーマットされます。

### アクセス・トークン
{: #access-tokens}

アクセス・トークンによって、App ID で設定された許可フィルターで保護されている[バックエンド・リソース](/docs/services/appid/protecting-resources.html)との通信が可能になります。このトークンは JavaScript Object Signing and Encryption (JOSE) 仕様に準拠しています。

トークンの例:

```
Header: {
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
    <td><i> typ </i></td>
    <td> ヘッダー・タイプ (「JOSE」として指定)。 </td>
  </tr>
  <tr>
    <td><i> alg </i></td>
    <td> 使用されるアルゴリズム (「RS256」として指定)。 </td>
  </tr>
  <tr>
    <td><i> iss </i></td>
    <td> トークンを発行した {{site.data.keyword.appid_short}} サーバー (ストリングまたは URL として指定)。 </td>
  </tr>
  <tr>
    <td><i> sub </i></td>
    <td> トークンの発行先のユーザーの ID。</td>
  </tr>
  <tr>
    <td><i> aud </i></td>
    <td> トークンの対象のクライアント ID。 </td>
  </tr>
  <tr>
    <td><i> exp </i></td>
    <td> タイム・スタンプ満了の時刻 (エポック・タイムで指定)。 </td>
  </tr>
  <tr>
    <td><i> iat </i></td>
    <td> タイム・スタンプが出された時刻 (エポック・タイムで指定)。 </td>
  </tr>
  <tr>
    <td><i> tenant </i></td>
    <td> トークンと共に発行された固有のユーザー ID。</td>
  </tr>
  <tr>
    <td><i> amr </i></td>
    <td> 認証に使用される ID プロバイダー。 この変数は、<i>appid_facebook</i>、<i>appid_google</i>、または <i>cloud_directory</i> です。</td>
  </tr>
  <tr>
    <td><i> scope </i></td>
    <td> トークンの発行対象のスコープ。 </td>
  </tr>
</table>


### 識別トークン
{: #identity-tokens}

識別トークンには、ユーザーに関する情報が格納されます。名前、E メール、性別、場所に関する情報を提供できます。トークンはユーザーのイメージへの URL を返すこともできます。

トークンの例:

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
```
{:screen}


<table>
<caption> 表 2. 識別トークンのコンポーネントの説明 </caption>
  <tr>
    <th> コンポーネント </th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td> <i> name </i> </td>
    <td> ID プロバイダーによって報告されたユーザーのフルネーム。 これは、必ず返されなければなりません。 </td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> ID プロバイダーによって報告されたユーザーの E メール。 使用可能な場合にのみ返されます。 </td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> ID プロバイダーによって報告されたユーザーの性別 (使用可能な場合)。 </td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> ID プロバイダーによって報告されたユーザーのロケール。 </td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> ユーザーのピクチャーへの URL (使用可能な場合)。 </td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id </ul></i></td>
    <td> </br><ul><li> 認証に使用される ID プロバイダー。 この変数は、<code>appid_facebook</code>、<code>appid_google</code>、<code>cloud_directory</code> のいずれかです。必ず返されなければなりません。<li> ID プロバイダーによって報告された固有のユーザー ID。 <li> ID プロバイダーによって返されなければならない JSON オブジェクト。 </ul></li></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type </br><li> name <li> software_id <li> software_version<li> device_id <li>device_model<li>device_os<li>device_os_version </ul></i> </td>
    <td> </br><ul><li> クライアントの登録時に判別されたアプリのタイプ。この変数は、<em>serverapp</em> または <em>mobileapp</em> です。 <li> クライアントの登録時に報告されたクライアント名。 <li> クライアントの登録時に報告されたソフトウェア ID。 <li> クライアントの登録時に使用されたソフトウェアのバージョン。 <li> モバイル・クライアントのデバイス ID。<li> モバイル・クライアントのデバイス・モデル。<li> モバイル・クライアントのデバイスの OS。<li> モバイル・クライアントのデバイスの OS バージョン。</ul></td>
  </tr>
</table>

## ヘッダー
{: #auth-header}

許可ヘッダーは、返されたトークンを組み合わせたものです。{{site.data.keyword.appid_short}} の場合、許可ヘッダーは、ベアラー、アクセス、識別という 3 種類の異なるトークンを空白文字で区切ったものとして構成されます。ベアラー・トークンとアクセス・トークンは、アプリにアクセス権限を付与するために必要です。識別トークンはオプションで、主にアプリを使用するユーザーに関する情報を保管するために使用されます。

ヘッダー構造の例:

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


## フィルター
{: #auth-filter}

{{site.data.keyword.appid_short}} サーバー SDK には、API と Web アプリケーションという 2 つのタイプのリソースを保護するための戦略が用意されています。
{:shortdesc}

API の保護戦略は、非認証クライアントに対する許可を取得するために、適用範囲のリストと共に HTTP 401 応答を戻します。 Web アプリの保護戦略は、HTTP 302 リダイレクトを戻します。このリダイレクトにより、非認証クライアントは、{{site.data.keyword.appid_short_notm}} サービスがホストするサインイン・ページに送られるか、ID プロバイダーのサインイン・ページに直接送られます。どちらに送られるかは、どのように構成したかに応じて異なります。



### API 戦略
{: #api}

API 戦略では、有効なアクセス・トークンを含む許可ヘッダーが要求に含まれていなければなりません。 応答にも識別トークンを含めることができますが、これは必須ではありません。

トークンが無効または期限切れの場合、API 戦略は次の情報を含む HTTP 401 エラーを返します: Www-Authenticate=Bearer scope="{scope}" error="{error}"。 `error` の部分はオプションです。

要求から有効なトークンが返された場合、制御が次のミドルウェアに渡され、`appIdAuthorizationContext` プロパティーが要求オブジェクト内に挿入されます。 このプロパティーには、元のアクセス・トークンと識別トークン、およびデコードされたペイロード情報が平文の JSON オブジェクトとして含まれます。


### Web アプリ戦略
{: #web}

Web アプリの戦略クラスは、保護リソースに対する非認証のアクセス試行を検出すると、ユーザーのブラウザーを認証ページに自動的にリダイレクトします。 認証に成功すると、ユーザーは Web アプリのコールバック URL に返されます。サービスは、Web アプリの戦略クラスを使用して、アクセス・トークンと識別トークンを取得します。 それらのトークンを取得した後、Web アプリの戦略クラスはそれらを `WebAppStrategy.AUTH_CONTEXT` の下の HTTP セッションに保管します。 アクセス・トークンと識別トークンをアプリ・データベース内に保管するかどうかは、各ユーザーが決定します。


## 段階的な認証
{: #oauth}

{{site.data.keyword.appid_short_notm}} は OAuth 2.0 と OIDC のプロトコルを使用してユーザーの認証と権限付与を行います。認証の後、ユーザーの ID はユーザー・レコードと関連付けられます。このサービスは、ユーザーの属性にアクセスするために使用できるアクセス・トークンと、ID プロバイダーから提供されたユーザーに関する情報が含まれる識別トークンを返します。このレコードとその属性には、同じ ID で認証されたすべてのクライアントから再びアクセスできます。

サインインは、オプションにしたいときもあります。{{site.data.keyword.appid_short_notm}} は、匿名の場合を含め、段階的な認証という方法を使用して、[ユーザー・プロファイル](/docs/services/appid/user-profile.html)を作成します。続いてその情報をユーザー・サインイン後に既知のユーザー・プロファイルに転送するように設定できます。

![識別されたユーザーになるまでの経路を示すマップ。](/images/authenticationtrail.png)

図 2. 識別されたユーザーになるまでの経路を示すマップ

ユーザーが匿名のままにすることを選択すると、{{site.data.keyword.appid_short_notm}} は随時ユーザー・レコードを作成し、匿名アクセス・トークンと識別トークンを返す OAuth ログイン API を呼び出します。これらのトークンを使用して、アプリはユーザー・レコードに保管される属性の作成、読み取り、更新、削除を行うことができます。例えば、ユーザーはアプリにログインしなくてもすぐにショッピング・カートにアイテムを追加できます。


ユーザーがアプリへのサインインを選択すると、識別されたユーザーになります。ユーザーに関する情報は、サインイン時に選択した ID プロバイダーから入手します。ユーザーは、ユーザーに関する情報が含まれるアクセス・トークンと識別トークンを受け取ります。

匿名ユーザーは識別されたユーザーになることを選択できます。その方法について説明します。

匿名アクセス・トークンがログイン API に渡されます。このサービスは、ID プロバイダーを使用して呼び出しを認証します。このサービスは、アクセス・トークンを使用して匿名レコードを検出し、そこに ID を付加します。新しいアクセス・トークンと識別トークンには、ID プロバイダーに共有される公開情報が格納されます。ユーザーの識別後には、そのユーザーの匿名トークンは無効になります。しかし、引き続きユーザーは自分の属性にアクセスできます。新しいトークンを使用してアクセスできるからです。

**注**: ID を匿名レコードに割り当てられるのは、別のユーザーに割り当て済みでない場合に限られます。ID が既に別の {{site.data.keyword.appid_short_notm}} ユーザーに関連付けられている場合、トークンにはそのユーザーのレコードの情報が格納され、そのユーザーの属性にアクセスできるようになります。前の匿名ユーザーの属性に、新しいトークンを使用してアクセスすることはできません。トークンの有効期限が切れるまでは、匿名アクセス・トークンにより引き続き情報にアクセスできます。 開発中に、既知のユーザーに匿名属性をマージする方法を選択できます。
