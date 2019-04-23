---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-08"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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


# チュートリアル: ユーザーの役割の設定
{: #tutorial-roles}

アプリケーションのコーディング時に、適切な人が、適切な時に、適切なアクセス権を持っていることを確認するのは困難な場合があります。このプロセスで助けが必要な場合は、{{site.data.keyword.appid_full}} を使用し、`role` などのカスタム属性を定義して、さまざまなタイプのユーザーを割り当てることができます。それから、アプリケーションを使用して、ユーザーのタイプごとに各種レベルの許可を実施できます。以下のステップバイステップ・ガイドを使用すると、{{site.data.keyword.appid_short_notm}} API を使用することにより、ユーザー属性を設定して更新してからトークン内に挿入する方法を学習できます。
{: shortdesc}

API を使用するのは初めてですか? [この Postman コレクション](https://github.com/ibm-cloud-security/appid-postman)を使用して試してください。
{: tip}

## シナリオ
{: #roles-scenario}

架空のテーマパークの開発者を想定します。[Web アプリケーション](/docs/services/appid?topic=appid-web-apps)のアクセスを管理する仕事を課されており、この仕事を行う最も簡単な方法はユーザーのタイプごとに役割を設定することであると思っています。テーマパークのスタッフや訪問客などの複数の異なるタイプの役割があり、それぞれ異なるレベルの許可が必要になります。このプロセスを合理化し、ユーザーが初めてアプリケーションにサインインした時点から正しい役割を割り当てられるようにしようとしています。  
{: shortdesc}

問題ありません。 {{site.data.keyword.appid_short_notm}} の [カスタム属性フィーチャー](/docs/services/appid?topic=appid-custom-attributes)を使用して、いずれのタイプのユーザー関連情報も保管できます。ここでは、役割ベースのアクセス制御を処理しているので、`role` と呼ばれる属性を作成して異なる値を割り当て、役割のタイプを指定できます。例えば、テーマパークに `visitors` や `staff` があり、それぞれ `role` 属性の値が異なるとします。この場合、割り当てたアクセス・ポリシーと特権をアプリケーション・コードで実施することができます。

このチュートリアルは特に Web アプリと Cloud Directory を念頭に置いて書かれていますが、もっと広い意味で属性を使用できます。カスタム属性は、どんなものにでもすることができます。属性の数が 100k 未満で、それらの形式が平文の JSON オブジェクトであれば、あらゆるタイプの情報を保管できます。
{: note}


## 開始する前に
{: #roles-before}

準備はよろしいですか? では、開始しましょう。

開始する前に、以下の前提条件が揃っていることを確認してください。
- {{site.data.keyword.appid_short_notm}} サービスのインスタンス
- サービス資格情報のセット
- アクセスおよび検証できる E メール・アドレス


## ステップ 1: {{site.data.keyword.appid_short_notm}} インスタンスの構成
{: #roles-configure-app}

クラウド・ランドのユーザーに関する属性の追加を開始する前に、{{site.data.keyword.appid_short_notm}} のインスタンスを構成する必要があります。
{: shortdesc}

1. サービス・ダッシュボードの**「ID プロバイダー」**タブで、**「Cloud Directory」**を有効にします。このチュートリアルでは [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) を使用していますが、[SAML](/docs/services/appid?topic=appid-enterprise)、[Facebook](/docs/services/appid?topic=appid-social#facebook)、[Google](/docs/services/appid?topic=appid-social#google)、または[カスタム・プロバイダー](/docs/services/appid?topic=appid-custom-identity)など、他の IdP を選択することもできます。

2. **「Cloud Directory」>「E メールの検証 (Email Verification)」**タブで、検証を有効にして、**「最初にユーザーの E メール・アドレスを検証せずに、ユーザーがアプリケーションにサインインできるようにする」**を**「いいえ」**に設定します。カスタム属性を使用して許可関連の役割を設定する際には、設定する属性をユーザーが担う前にそのユーザーの ID を検証しなければならないことを確認してください。

3. **「プロファイル」**タブで、**「アプリからのカスタム属性の変更 (Change custom attributes from the app)」**を**「無効」**に設定します。

  デフォルトでは、アクセス・トークンを持っていれば誰でもカスタム属性を変更できます。アプリケーション・セキュリティーを確保するには、管理者またはアプリの所有者だけがカスタム属性を変更できるように {{site.data.keyword.appid_short_notm}} を構成しなければなりません。このように構成すると、ユーザーが自分のカスタム属性を変更したり、自分が持ってはならない許可を自身に付与したりするのを回避できます。
  {: important}

順調です! ダッシュボードが構成され、役割の設定を開始する準備ができました。


## ステップ 2: サインイン前に別のユーザーのために役割を設定する
{: #roles-set-before}

クラウド・ランドに新しいスタッフ・メンバーが加わりました。メンバーの情報はすべてわかっていますが、数日間は始動しません。{{site.data.keyword.appid_short_notm}} ユーザーと、`staff` 役割などの属性が含まれるプロファイルを作成して、彼らを[事前登録](/docs/services/appid?topic=appid-preregister)できます。
{: shortdesc}

このプロセスでは Cloud Directory 登録は終了しません。引き続き、ユーザーがアプリに申し込みを行い、作成するプロファイル内の属性を継承しなければなりません。
{: tip}

1. CLI を使用して {{site.data.keyword.cloud_notm}} にログインします。

  ```
  ibmcloud login
  ```
  {: pre}

2. IAM アクセス・トークンを入手します。

  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. POST 要求を行い、新しいユーザー用に `staff` 属性が含まれるユーザー・プロファイルを作成します。使用している E メール・アドレスにアクセスして検証できることを確認してください。

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": “user@email.com“,
    "profile": {
      "attributes": {
        “role”: “staff”
      }
    }
  }'
  ```
  {: pre}

  正常な応答出力は次のとおりです。

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. `staff` 役割のあるプロファイルが作成されたことを確認します。

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

  正常な応答本体は次のとおりです。

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

お疲れさまでした。アプリケーション用にユーザーを事前登録しました。この時点で、事前登録に使用した ID でアプリにサインインすると、Cloud Directory ユーザーが作成され、{{site.data.keyword.appid_short_notm}} ユーザー・プロファイルを継承することになります。次に、属性を更新する方法を学びます。


## ステップ 3: ユーザー属性の更新
{: #roles-update-attributes}

クラウド・ランドは成長しています! この成長と歩調を合わせるために、会社は新人を雇おうとしています。ステップ 2 の `staff` ユーザーは今やマネージャーになります。[新しい役割を割り当てて](/docs/services/appid?topic=appid-custom-attributes)、このユーザーのプロファイルを更新できます。
{: shortdesc}

1. プロファイルを更新します。

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
        “role”: “manager”
      }
    }
  }'
  ```
  {: pre}

3. プロファイルを表示して、正しく更新されたことを検証します。

  ```
  curl --request POST \
  GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

  正常な応答出力は次のとおりです。

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

お疲れさまでした。


## ステップ 4: 属性をトークン内に挿入する
{: #roles-map-claims}

テーマパークはさらに有名になって成長を続けています。新しい訪問客やスタッフがとても多いので、行われる要求を制限しようとしています。パフォーマンスが向上するように、ユーザー・プロファイルの属性をアクセス・トークンと識別トークンのクレームにマップできます。カスタム・クレームをマップすると、トークン自体にカスタム属性を保管できます。
{: shortdesc}

[トークン構成](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)はグローバルです。つまり、実際に割り当てられている役割にかかわらず、`role` 属性のあるすべてのユーザーに適用されます。
{: tip}


1. トークン構成エンドポイントに対して要求を行います。

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
          "expires_in": 3601
      },
  "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: pre}

  <table>
    <tr>
      <th>変数</th>
      <th>説明</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td>
      <td>テナント ID は、要求内で {{site.data.keyword.appid_short_notm}} のインスタンスを識別する手段です。ID は、ダッシュボードの<em>「サービス資格情報」</em>タブにあります。セットがない場合は、GUI 内のステップに従って資格情報を作成できます。</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td><code>accessTokenClaim</code> と <code>idTokenClaims</code> の両方について、ソースを <code>attribute</code> に設定します。</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td><code>accessTokenClaim</code> と <code>idTokenClaims</code> の両方について、ソース・クレームを <code>role</code> に設定します。</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>この値は、各トークン・タイプに適用され、各要求内で設定しなければなりません。以前にこの値を GUI 内で設定してからこの要求を実行する場合、以前に設定した値は要求内の値によりオーバーライドされます。有効期限を構成にとって正しい値に設定していることを確認してください。</td>
    </tr>
  </table>

  正常な応答出力は次のとおりです。

  ```
  {
      "access": {
          "expires_in": 3601
      },
  "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## ステップ 5: アクセス・トークンを表示する
{: #roles-view-token}

オプションで、アクセス・トークンを表示して、ステップ 4 が正常に行われたことを検証できます。
{: shortdesc}

1. テストの目的で、{{site.data.keyword.appid_short_notm}} GUI を使用して Cloud Directory ユーザーを作成します。

  1. **「ユーザー」**タブで、**「ユーザーの追加」**をクリックします。フォームが表示されます。
  2. 姓、名、E メール、パスワードを入力します。
  3. **「保存」**をクリックします。

2. クライアント ID とシークレットをエンコードします。

  1. {{site.data.keyword.appid_short_notm}} GUI の**「サービス資格情報」**タブで、クライアント ID とシークレットをコピーします。
  2. Base64 エンコーダーを使用して、許可情報をエンコードします。
  3. 出力をコピーして以下のコマンドで使用します。

4. API を使用してサインインし、アクセス・トークン情報を入手します。戻されるトークンはエンコードされています。

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: pre}

5. アクセス・トークンをデコードします。
  1. 前述のコマンドからの応答出力内のトークンをコピーします。
  2. ブラウザーで、https://jwt.io/ にナビゲートします。
  3. **「エンコード (Encoded)」**というラベルのボックス内にトークンを貼り付けます。

6. **「デコード (Decoded)」**セクションで、役割が表示されることを確認します。

  ```
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
    "role": "manager"
  }
  ```
  {: screen}



## 次のステップ
{: #roles-next}

お疲れさまでした。チュートリアルは完了しました。次に、[多要素認証](/docs/services/appid?topic=appid-cd-mfa)の構成か[独自ブランドの GUI](/docs/services/appid?topic=appid-branded) のセットアップを試行できます。
