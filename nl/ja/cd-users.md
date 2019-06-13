---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# ユーザーの管理
{: #cd-users}

クラウド・ディレクトリーでは、セキュリティーとセルフサービスを強化する作成済みの機能を使用して、スケーラブルなレジストリーでユーザーを管理できます。
{: shortdesc}

Cloud Directory ユーザーは {{site.data.keyword.appid_short_notm}} ユーザーと同じではありません。 管理者が構成したさまざまな ID プロバイダー・オプションを使用してユーザーがアプリに登録することも、管理者が独自のディレクトリーにユーザーを追加することもできます。このトピックに出てくるユーザーは、ID プロバイダーであるクラウド・ディレクトリーに関連付けられているユーザーです。
{: note}

## ユーザー情報の表示
{: #cd-user-info}

API またはダッシュボードを使用して、すべてのクラウド・ディレクトリー・ユーザーのすべての既知の情報を JSON オブジェクトとして表示できます。
{: shortdesc}


### GUI を使用する場合

{{site.data.keyword.appid_short_notm}} ダッシュボードを使用して、アプリ・ユーザーについての詳細を表示できます。 

1. {{site.data.keyword.appid_short_notm}} インスタンスの**「クラウド・ディレクトリー」>「ユーザー」**タブにナビゲートします。

2. テーブルに目を通すか E メール・アドレスで検索して、情報を表示するユーザーを見つけます。

3. ユーザーの行のオーバーフロー・メニューで、**「ユーザーの詳細の表示 (View user details)」**をクリックします。ユーザーの情報を含むページが開きます。表示される情報について、次の表に記載します。

<table>
  <tr>
    <th colspan="2">ユーザーの詳細</th>
  </tr>
  <tr>
    <td>ユーザー ID (User identitifier)</td>
    <td>ユーザー ID は、構成したユーザー登録のタイプによって異なります。E メールとパスワードのフローを構成した場合、ID はユーザーの E メールです。ユーザー名とパスワードのフローを使用する場合、ID は登録時に指定されたユーザー名です。</td>
  </tr>
  <tr>
    <td>E メール</td>
    <td>ユーザーに関連付けられた 1 次 E メール・アドレス。</td>
  </tr>
    <tr>
    <td>氏名 (First and last name)</td>
    <td>登録プロセスでユーザーが指定した氏名。</td>
  </tr>
  <tr>
    <td>最後のログイン</td>
    <td>ユーザーがアプリケーションに最後にログインしたときのタイム・スタンプ。注: ダッシュボードでユーザーを追加した場合、ユーザー自身がアプリにサインインするまでログインはブランクです。サインインが行われると、ユーザーは App ID ユーザーにもなります。</td>
  </tr>
  <tr>
    <td>ID</td>
    <td>{{site.data.keyword.appid_short_notm}} によってユーザーに割り当てられた ID。UI には表示されませんが、値をコピーしてテキスト・エディターに貼り付けると値を確認できます。</td>
  </tr>
  <tr>
    <td>事前定義された属性</td>
    <td>事前定義された属性は、SCIM に基づく既知のユーザー情報です。</td>
  </tr>
  <tr>
    <td>カスタム属性</td>
    <td>カスタム属性は、ユーザーのプロファイルに追加された追加情報、または、ユーザーとアプリケーションの対話の中で収集された追加情報です。</td>
  </tr>
  <tr>
    <td>サマリー</td>
    <td>すべての属性が集められ、クラウド・ディレクトリー・ユーザーの完全な概要を示す 1 つのプロファイルが形成されます。詳しくは、[ユーザー・プロファイル](/docs/services/appid?topic=appid-profiles)を参照してください。</td>
  </tr>
</table>

</br>

### API を使用する場合

{{site.data.keyword.appid_short_notm}} API を使用して、アプリ・ユーザーについての詳細を表示できます。 

1. サービスのインスタンスからテナント ID を取得します。

2. E メール・アドレスなどの識別照会を使用して App ID ユーザーを検索し、ユーザー ID を見つけます。

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users?query={identifying-search-query}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  例:

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@email.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. 前のステップで取得した ID を使用して、`cloud_directory/users` エンドポイントに対して GET 要求を行い、完全なユーザー・プロファイルを表示します。

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-ID}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  応答例:

  ```
  {
    sub: "c155c0ff-337a-46d3-a22a-a8f2cca08995",
    name: "Test User",
    email: "testuser@test.com",
    identities: [
      {
        provider: "cloud_directory",
        id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
        idpUserInfo: {
          displayName: "Test User",
          active: true,
          mfaContext: {},
          emails: [
            {
              value: "testuser@test.com",
              primary: true
            }
          ],
          meta: {
            lastLogin: "2019-05-20T16:33:20.699Z",
            created: "2019-05-20T16:25:13.019Z",
            location: "/v1/6b8ab644-1d4a-4b3e-bcd9-777ba8430a51/Users/f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            lastModified: "2019-05-20T16:33:20.707Z",
            resourceType: "User"
          },
          scemas: [
            "urn:ietf:params:scim:schemas:core:2.0:User"
          ],
          name: {
            givenName: "Test",
            familyName: "User",
            formatted: "Test User"
            },
          id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
          status: "CONFIRMED",
          idpType: "cloud_directory"
        }
      }
    ]
  }
  ```
  {: screen}

  {{site.data.keyword.appid_short_notm}} がサポートするユーザー・データ・セットの詳細を確認するには、[SCIM コア・スキーマ](https://tools.ietf.org/html/rfc7643#section-8.2)を参照してください。
  {: tip}


## ユーザーの追加と削除
{: #add-delete-users}

Cloud Directory ユーザーの管理は、{{site.data.keyword.appid_short_notm}} ダッシュボードまたは API を使用して行えます。
{: shortdesc}

ユーザーがアプリケーションに登録する場合は、ユーザーがセルフサービス・ワークフローを介して登録を行います。そのワークフローによって、ウェルカムや検証要求などの E メールが自動的にトリガーされます。管理者がユーザーをアプリに追加する場合は、セルフサービス・ワークフローは開始されません。つまり、ユーザーはアプリケーションから E メールを受信しません。この場合にも追加されたということをユーザーに通知するには、[App ID 管理 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher) を使用してメッセージング・フローをトリガーします。


### ユーザーの追加
{: #add-users}

アプリケーションに登録したユーザーは、ユーザーとして追加されます。テストのために、{{site.data.keyword.appid_short_notm}} ダッシュボードまたは API を使用してユーザーを追加できます。

セルフサービス登録を無効にした場合や、本人の代わりにユーザーを追加した場合、ユーザーは追加されてもウェルカム E メールや検証 E メールを受信しません。
{: tip}



**GUI を使用して新規ユーザーを追加するには、以下のようにします。**

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「Cloud Directory」>「ユーザー」**タブにナビゲートします。

2. **「ユーザーの追加」**をクリックします。 フォームが表示されます。

3. **名**、**姓**、**E メール**、**パスワード**を入力します。 登録しようとしている E メールが別のユーザーによってまだ取得されていないことを確認してください。 パスワードを正しく入力したことの確認のために、**「パスワードの再入力」**フィールドにパスワードを入力します。

4. **「保存」**をクリックします。 Cloud Directory ユーザーが作成されます。

</br>


**API を使用して新規ユーザーを追加するには、以下のようにします。**

以下のフローは、E メールとパスワードを使用してユーザーを追加する方法を示しています。ユーザー名とパスワードのフローを使用することもできます。

1. アプリケーションまたはサービスの資格情報から `tenantID` を取得します。

2. {{site.data.keyword.cloud_notm}} IAM トークンを取得します。

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. ステップ 2 で取得したトークンを使用して、`cloud-directory/users` エンドポイントに POST 要求を行います。この例では、E メール/パスワードのフローを使用していることに注意してください。ユーザー名/パスワードのフローを使用することもできます。

  ```
  curl --X POST "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users"
  -H "accept: application/json"
  -H "content-type: application/json"
  -H "authorization: Bearer {token}"
  -d {
    "displayName": "Test User",
    "password": "{App-ID-Cloud-Directory-User-Password}",
    "active": true,
    "emails": [
      {
        "value": "{App-ID-Cloud-Directory-User-Email}",
        "primary": true
      }
    ]
  }
  ```
  {: codeblock}

</br>


### ユーザーの削除
{: #delete-users}

ディレクトリーからユーザーを削除するには、GUI または API を使用して、ユーザーを削除します。
{: shortdesc}

**GUI を使用してユーザーを削除するには、以下のようにします。**

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「Cloud Directory」>「ユーザー」**タブにナビゲートします。

2. 削除するユーザーの横にあるチェック・ボックスをクリックします。 ボックスが表示されます。

3. ボックスで、**「削除」**をクリックします。 画面が表示されます。

4. ユーザーの削除は元に戻せないということを理解した上で、**「削除」**をクリックして確定します。 間違って削除した場合、ディレクトリーにユーザーを再度追加できますが、そのユーザーに関する情報はすべてなくなっています。

</br>

**API を使用してユーザーを削除するには、以下のようにします。**

1. テナント ID を取得します。

2. ユーザーに関連付けられている E メールを使用し、ディレクトリーを検索してユーザーの ID を見つけます。

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users?email={user-email}" -H "accept: application/json"
  ```
  {: codeblock}

3. ユーザーを削除します。

  ```
  curl --X DELETE "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-GUID}"
  -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}



## ユーザーのマイグレーション
{: #user-migration}

{{site.data.keyword.appid_short_notm}} の新規インスタンスをセットアップする必要が生じることがあります。 クラウド・ディレクトリーを使用している場合、ユーザーを新規インスタンスにマイグレーションすることが必要になります。 マイグレーションに役立つ管理 API を使用することができます。
{: shortdesc}


{{site.data.keyword.appid_short_notm}} の両方のインスタンスで、`Manager` という [IAM 役割](/docs/iam?topic=iam-getstarted#getstarted)が割り当てられている必要があります。
{: note}


### エクスポート
{: cd-export}

ユーザーを新規インスタンスに追加するには、その前にそれらのユーザーを現行インスタンスからエクスポートする必要があります。 これを行うには、<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">エクスポート管理 API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用できます。

cURL コマンド例:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>変数</th>
    <th>説明</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>ハッシュ処理されたユーザー・パスワードの暗号化と復号のために使用するカスタム・ストリング。</td>
  </tr>
  <tr>
    <td><code>tenantID</code></td>
    <td>サービスのテナント ID はサービス資格情報の中にあります。 サービス資格情報は、{{site.data.keyword.appid_short_notm}} ダッシュボードで確認できます。</td>
  </tr>
</table>

クラウド・ディレクトリーのユーザーとそれらのユーザーのプロファイルのみが返されます。 他の ID プロバイダーのユーザーは返されません。
{: note}


### インポート
{: #cd-import}

ユーザーの準備ができたので、これからユーザーの情報を新規インスタンスにインポートすることができます。 これを行うには、<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">インポート管理 API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用できます。


cURL コマンド例:

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}



### マイグレーション・スクリプト
{: cd-migration-script}

{{site.data.keyword.appid_short_notm}} には、マイグレーション・プロセスの高速化に役立つ、CLI で使用可能なマイグレーション・スクリプトが用意されています。

開始する前に、以下のパラメーター情報を用意してください。

<table>
  <tr>
    <th>パラメーター</th>
    <th>説明</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>ユーザーのエクスポート元となる、{{site.data.keyword.appid_short_notm}} のインスタンスのテナント ID。</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>ユーザーのインポート先となる、{{site.data.keyword.appid_short_notm}} のインスタンスのテナント ID。</td>
  </tr>
  <tr>
    <td>地域</td>
    <td>地域オプションとしては、<code>au-syd</code>、<code>eu-de</code>、<code>eu-gb</code>、<code>jp-tok</code>、<code>us-south</code> があります。</td>
  </tr>
  <tr>
    <td>IAM トークン</td>
    <td>トークンを取得する前に、<code>manager</code> 許可があることを確認してください。 IAM トークンの取得については、<a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">資料 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。</td>
  </tr>
</table>

このスクリプトを実行するには、次のようにします。

1. <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">リポジトリー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を複製します。
2. 端末を開き、リポジトリーの複製先のフォルダーにナビゲートします。
3. 以下のコマンドを実行します。

  ```
  npm install
  ```
  {: codeblock}

4. パラメーターを指定して、以下のコマンドを実行します。

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  コマンド例:

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}
