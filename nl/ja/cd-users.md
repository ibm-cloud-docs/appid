---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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

クラウド・ディレクトリーを有効にすると、ユーザーは E メールまたはユーザー名とパスワードを使用してアプリケーションに登録できるようになります。
{: shortdesc}


Cloud Directory ユーザーは {{site.data.keyword.appid_short_notm}} ユーザーと同じではありません。ユーザーは、構成されたさまざまな ID プロバイダー・オプションを使用して、アプリに登録できます。このトピックでいうユーザーは、アプリへの登録時に Cloud Directory オプションを使用することを選択したユーザーのことです。
{: note}


## ユーザーの追加と削除
{: #add-delete-users}

Cloud Directory ユーザーの管理は、{{site.data.keyword.appid_short_notm}} ダッシュボードまたは API を使用して行えます。
{: shortdesc}

特定のユーザーの全データを調べるには、Cloud Directory ユーザーの情報を JSON オブジェクトとして返す API を使用します。{{site.data.keyword.appid_short_notm}} がサポートするユーザー・データ・セットの詳細を確認するには、[SCIM コア・スキーマ](https://tools.ietf.org/html/rfc7643#section-8.2)を参照してください。

### ユーザーの追加
{: #add-users}

以下の手順を使用して、{{site.data.keyword.appid_short_notm}} ダッシュボードでユーザーを追加できます。

テストが目的の場合は、{{site.data.keyword.appid_short_notm}} ダッシュボードでユーザーを追加できます。

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「Cloud Directory」>「ユーザー」**タブにナビゲートします。

2. **「ユーザーの追加」**をクリックします。フォームが表示されます。

3. **名**、**姓**、**E メール**、**パスワード**を入力します。登録しようとしている E メールが別のユーザーによってまだ取得されていないことを確認してください。パスワードを正しく入力したことを確実にするために、**「パスワードの再入力」**フィールドにパスワードを入力することで確定します。

4. **「保存」**をクリックします。 Cloud Directory ユーザーが作成されます。


### ユーザーの削除
{: #delete-users}

ディレクトリーからユーザーを削除するには、GUI からユーザーを削除します。

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「Cloud Directory」>「ユーザー」**タブにナビゲートします。

2. 削除するユーザーの横にあるチェック・ボックスをクリックします。ボックスが表示されます。

3. ボックスで、**「削除」**をクリックします。 画面が表示されます。

4. ユーザーの削除は元に戻せないということを理解した上で、**「削除」**をクリックして確定します。操作が間違いだった場合、ディレクトリーにユーザーを再度追加できますが、そのユーザーに関する情報はすべて使用できなくなります。


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
    <td>トークンを取得する前に、<code>manager</code> 許可があることを確認してください。 IAM トークンの取得については、<a href="https://cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">資料 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。</td>
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
