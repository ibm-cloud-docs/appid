---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

keywords: authentication, authorization, identity, app security, secure, development, user information, attributes, profiles, 

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

# ユーザーのサインイン前に属性を追加する
{: #preregister}

{{site.data.keyword.appid_full}} では、アプリへのアクセスが必要になることが分かっているユーザーのプロファイルの作成を、そのユーザーが初めてサインインする前に開始できます。
{: shortdesc}

属性のタイプ、および、カスタム属性を使用する場合のセキュリティー上の考慮事項について詳しくは、[ユーザー・プロファイルの保管とアクセス](/docs/services/appid?topic=appid-profiles)を参照してください。
{: tip}

## 事前登録について
{: #preregister-understand}

### 事前登録を使用する目的は何ですか?
{: #preregister-why}

{{site.data.keyword.appid_short_notm}} を使用して SAML ID プロバイダーに属する既存の複数のユーザーを統合するアプリケーションについて考えてみます。 特定のユーザーには、アプリケーションに初めてサインインした直後に `admin` アクセス権限を付与したい場合もあります。 これを行うには、それらのユーザーのために事前登録エンドポイントを使用してカスタム `admin` 属性を設定し、管理コンソールへのアクセス権限を付与します。アプリ提供者側ではそれ以上の操作は必要ありません。 デフォルト設定を変更することで生じる可能性がある[セキュリティー問題](/docs/services/appid?topic=appid-profiles#profile-set-custom)について、必ず検討してください。

### ユーザーはどのようにして識別されますか?
{: #preregister-identify-user}

以下のいずれかを使用して、ユーザーを識別できます。

* ID プロバイダー内にあるユーザーの固有 ID (**GUID** という)。 この ID は常に存在し、固有であることが保証されていますが、いつでもすぐに見つかるとは限らず、容易に理解できるとも限りません。 例えば、クラウド・ディレクトリーではランダムな 16 バイトの GUID が使用されます。
* 使用可能な場合、ユーザーの **E メール**。

### ID プロバイダーはどのような情報を提供しますか?
{: #preregister-idp-provide}

以下の表を参照して、使用できる ID 情報のタイプを確認してください。

<table>
  <thead>
    <tr>
      <th>ID プロバイダー</th>
      <th>GUID</th>
      <th>E メール</th>
      <th>サブ</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>クラウド・ディレクトリー</td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td></td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>カスタム</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

### Cloud Directory はどのように扱われますか?
{: #preregister-cd}


事前登録されたユーザー属性の整合性を確保するために、クラウド・ディレクトリーはユーザーに追加の要件を課しています。 事前登録は、E メール検証が有効になっていて、検証されている場合にのみ行うことができます。 特定の属性を使ってクラウド・ディレクトリーのユーザーを事前登録する場合、それらの属性は、特定のユーザーを対象としたものとなります。 最初に E メールが検証されていない場合には、別のユーザーが、その E メール・アドレスとそれに割り当てられている属性を所有すると主張してくる可能性があります。

1. クラウド・ディレクトリーを E メールおよびパスワード・モードに設定します。 この操作は、UI では**「クラウド・ディレクトリー」**タブの一般設定で行うことができます。 [管理 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser) を使用して設定することもできます。

2. 以下のいずれかの方法でユーザーの E メール・アドレスを検証し、本人であることを確認します。

  * E メールを使用してユーザーの同一性を検証するには、サービス・ダッシュボードの**「クラウド・ディレクトリー」**タブで、**「E メールの検証」**を**「オン」**に設定します。 アプリ提供者がユーザーを追加した後、ユーザーが最初に E メールの検証を行わずにアプリにサインインした場合、サインインは正常に完了しますが、事前定義されていた属性は削除されます。
  * ユーザーを手動で検証するには、管理者がクラウド・ディレクトリーの[管理 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser) を使用する必要があります。 ユーザーを作成または更新する場合、管理者がユーザー・データ・ペイロード内で `status` フィールドを明示的に `CONFIRMED` に設定する必要があります。

**カスタム ID プロバイダーを使用する際に行う必要のある特別な事柄は何かありますか?**

事前にユーザー情報をアプリケーションに追加する場合、認証フローで提供される任意の固有 ID を使用できます。 その ID は、許可要求時に送信される署名付き JSON Web トークンの `sub` と_厳密に_ 一致している必要があります。 ID が一致しない場合、追加するプロファイルは正常にリンクされません。



## アプリへのユーザー情報の追加
{: #preregister-add-info}

プロセスについて学習し、セキュリティーへの影響を検討したので、ユーザーを追加してみてください。

**開始前に、以下のことを行います。**

特定のユーザーのカスタム属性を [/users 管理 API エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.users_search_user_profile)によって追加するには、以下の情報を知っている必要があります。

* ユーザーがサインインに使用する ID プロバイダー。
* ID プロバイダーによって提供されるユーザーの固有 ID。

ユーザーが初めてアプリにサインインすると、{{site.data.keyword.appid_short_notm}} はユーザーを検索します。 見つかった場合、ユーザーは割り当てられている ID を継承します。 ユーザーが見つからない場合は、ID プロバイダーによって提供された情報に基づいて新規ユーザーが作成されます。

**ユーザーを追加するには、以下のようにします。**

1. IBM Cloud にログインします。
  ```
  ibmcloud login
  ```
  {: codeblock}

2. 以下のコマンドを実行して、IAM トークンを見つけます。
  ```
  ibmcloud iam oauth-tokens
  ```
  {: codeblock}

3. JSON オブジェクトとして設定するユーザーと属性の記述を含めた POST 要求を `/users` エンドポイントに対して行います。

  ヘッダー:
  ```
  POST {management-url}/management/v4/{tenantId}/users
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: codeblock}

  本体:
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes": {
             "mealPreference":"vegeterian"
           }
       }
   }
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="アイデア・アイコン"/> 構成要素について</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>idp</em></code></td>
        <td>ユーザーが認証に使用する ID プロバイダー。 オプションとして、`saml`、`cloud_directory`、`facebook`、`google`、`appid_custom`、`ibmid` があります。</td>
      </tr>
      <tr>
        <td><code><em>idp-identity</em></code></td>
        <td>ID プロバイダーによって提供される固有 ID。</td>
      </tr>
      <tr>
        <td><code><em>profile</em></code></td>
        <td>カスタム属性 JSON マッピングを格納するユーザーのプロファイル。</td>
      </tr>
    </tbody>
  </table>

  要求例:
  ```
  $ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
  ```
  {: screen}

3. 以下のいずれかの方法で、登録が成功したことを確認します。
  * 応答内でユーザー ID を見つけます。
    ```
    {
        "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
    }
    ```
    {: screen}
  * 作成されたユーザー・プロファイルを見つけます。

ユーザーの事前定義属性は最初の認証が行われるまで空になっていますが、その意図や目的に関係なく、このユーザーは完全に認証されたユーザーであることに注目してください。 その固有 ID は、既にサインインしているユーザーの場合と同様に使用できます。 例えば、そのプロファイルを変更、検索、または削除することができます。

これでユーザーが特定の属性に関連付けられましたので、[属性へのアクセスまたは属性の更新](/docs/services/appid?topic=appid-profiles)を試してみてください。


</br>
