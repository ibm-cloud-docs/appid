---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-13"

keywords: authentication, authorization, identity, app security, secure, access, platform, management, permissions

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


# サービス・アクセスの管理
{: #service-access-management}

{{site.data.keyword.appid_full}} と {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) を使用すると、アカウント所有者は自分のアカウント内でユーザー・アクセスを管理できます。
{: shortdesc}

アカウント所有者は、アカウント内にポリシーを設定して、さまざまなユーザー用にさまざまなレベルのアクセス権限を作成できます。 例えば、特定のユーザーに対して、あるインスタンスについては**「読み取り専用」**アクセス権限を付与し、別のインスタンスについては**「書き込み」**アクセス権限を付与することができます。 どのユーザーに、{{site.data.keyword.appid_short_notm}} のインスタンスの作成、更新、削除を許可するかを決定することができます。

IAM について詳しくは、[IAM のアクセス権限](/docs/iam?topic=iam-userroles)を参照してください。

## ユーザー役割
{: #iam-roles}

アクセス・ポリシーの有効範囲は、ユーザーに割り当てられた役割に基づいています。
{: shortdesc}

ポリシーにより、アクセス権限をさまざまなレベルで付与することができます。 オプションには以下のものがあります。
<ul><ul>
  <li>自分のアカウント内のサービスのすべてのインスタンスにわたるアクセス</li>
  <li>自分のアカウント内の個別のサービス・インスタンスへのアクセス</li>
  <li>インスタンス内の特定のリソースへのアクセス</li>
  <li>自分のアカウント内のすべての IAM 対応のサービスへのアクセス</li>
</ul></ul>

### プラットフォーム役割
{: #iam-platform-roles}

ユーザーは、プラットフォーム管理役割を使用して、プラットフォーム・レベルでサービス・リソースに対するタスクを実行できます。 例えば、役割を割り当てることにより、ID の作成や削除、インスタンスの作成、アプリへのインスタンスのバインドを実行できるユーザーを決定できます。 以下の表は、プラットフォーム管理役割と相関するアクションについて詳しく示しています。

<table>
  <tr>
    <th>プラットフォーム役割</th>
    <th>許可</th>
    <th>アクションの例</th>
  </tr>
  <tr>
    <td><i>ビューアー</i></td>
    <td>{{site.data.keyword.appid_short_notm}} インスタンスを表示します。</td>
    <td>Cloud Directory ユーザーのデータや ID プロバイダーの構成を表示できます。</td>
  </tr>
  <tr>
    <td><i>エディター</i></td>
    <td>{{site.data.keyword.appid_short_notm}} インスタンスを表示およびバインドできます。</td>
    <td>アプリケーションを {{site.data.keyword.appid_short_notm}} のインスタンスにバインドできます。</td>
  </tr>
  <tr>
    <td><i>オペレーター</i></td>
    <td>{{site.data.keyword.appid_short_notm}} インスタンスを作成、削除、編集、一時停止、再開、表示、またはバインドすることができます。</td>
    <td>カタログから {{site.data.keyword.appid_short_notm}} インスタンスを作成または削除することができます。</td>
  </tr>
  <tr>
    <td><i>管理者</i></td>
    <td>アカウント内のすべてのサービスに対するすべての管理アクション。</td>
    <td>すべてのオペレーター・アクション、および他のユーザーにポリシーを割り当てる機能を実行できます。</td>
  </tr>
</table>

### サービス・アクセスの役割
{: #iam-service-roles}
次の表は、サービス・アクセス役割にマップされたアクションについて詳しく示しています。 ユーザーは、サービス・アクセス役割を使用して、{{site.data.keyword.appid_short_notm}} にアクセスしたり、{{site.data.keyword.appid_short_notm}} API を呼び出したりできます。


<table>
  <tr>
    <th>サービス役割</th>
    <th>許可</th>
    <th>アクションの例</th>
  </tr>
  <tr>
    <td><i>リーダー</i></td>
    <td>{{site.data.keyword.appid_short_notm}} インスタンス・データを表示します。</td>
    <td>ユーザー・データや ID プロバイダー情報など、サービス・インスタンスの詳細を表示できます。</td>
  </tr>
  <tr>
    <td> <i>ライターまたは管理者</i></td>
    <td>{{site.data.keyword.appid_short_notm}} インスタンスを表示および変更できます。</td>
    <td>リーダーのすべてのアクション、およびサービス・インスタンスの編集 (ID プロバイダー構成の編集など) を実行できます。 </li></ul></td>
  </tr>
</table>

UI でユーザー役割を割り当てる方法について詳しくは、[IAM アクセス権限の管理](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)を参照してください。


## {{site.data.keyword.appid_short_notm}} アクセス・ポリシー
{: #iam-access}

ご使用のアカウント内の {{site.data.keyword.appid_short_notm}} サービスにアクセスするすべてのユーザーには、IAM ユーザー役割が定義されたアクセス・ポリシーを割り当てる必要があります。 そのポリシーにより、選択したサービスまたはインスタンスのコンテキスト内でユーザーが実行できるアクションを決定します。
{: shortdesc}

アクションは、{{site.data.keyword.cloud_notm}} サービスで実行が許可された操作として、そのサービスでカスタマイズおよび定義されます。 その後、アクションは IAM ユーザー役割にマップされます。 実行したアクションのいくつかは、{{site.data.keyword.cloudaccesstrailshort}} サービスを使用して追跡できます。 以下の表では、{{site.data.keyword.appid_short_notm}} のアクションと必要な許可がマップされています。

<table>
  <tr>
    <th>アクション</th>
    <th>説明</th>
    <th>必要な役割</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>認証後のリダイレクト URL を表示します。</td>
    <td>リーダー、ライター、管理者</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>認証後のリダイレクト URL を追加または更新します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>ID プロバイダー構成を更新します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>ID プロバイダー構成を表示します。</td>
    <td>リーダー、ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>最近の認証イベントをリストとして表示します。</td>
    <td>リーダー、ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>ロゴや色など、ログイン・ウィジェット構成を表示します。</td>
    <td>リーダー、ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>ログイン・ウィジェット構成を更新します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>ユーザー・プロファイル構成を表示します。</td>
    <td>リーダー、ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>ユーザー・プロファイル構成を変更します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>ユーザー・プロファイル構成を表示します。</td>
    <td>リーダー、ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>新しいユーザーをクラウド・ディレクトリーに追加します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>クラウド・ディレクトリー・ユーザーの詳細を更新します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>ユーザーをクラウド・ディレクトリーから削除します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>クラウド・ディレクトリーの E メール・テンプレートを表示します。</td>
    <td>リーダー、ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>独自のコンテンツを使って E メール・テンプレートを更新します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>クラウド・ディレクトリーの E メール・テンプレートを削除します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>クラウド・ディレクトリーの SAML サービス・プロバイダー (SP) メタデータを表示します。</td>
    <td>リーダー、ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>SAML ID プロバイダーのログイン・ウィジェットで、イメージを設定または更新します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>テンプレートに基づいてユーザーに E メールを送信します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>E メールの送信者の詳細を表示します。</td>
    <td>リーダー、ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>送信者の詳細を更新します。</td>
    <td>ライター、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>ユーザー ID を使用して、ユーザーのリフレッシュ・トークンを取り消します。</td>
    <td>ライター、管理者</td>
  </tr>
</table>

</br>

## 例: 別のユーザーに {{site.data.keyword.appid_short_notm}} のインスタンスへのアクセス権限を付与する
{: #iam-example}

このシナリオで、管理者は {{site.data.keyword.appid_short_notm}} のインスタンスを作成し、チームの別のメンバーにビューアー・アクセス権限を付与する必要があります。
{: shortdesc}

開始前に、以下のことを行います。

* [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli) をインストールします。

アクセス許可を更新するために、管理者は以下の手順を実行します。

1. {{site.data.keyword.cloud_notm}} コンソールにログインします。

2. [IAM の資料](/docs/iam?topic=iam-iammanidaccser)に記載された手順に従って、その従業員に表示アクセス権限を付与します。

3. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「サービス資格情報」**タブに移動します。 **「資格情報の表示」**をクリックして、**tentantID** をコピーします。

4. 端末で {{site.data.keyword.cloud_notm}} CLI を使用してサインインします。

    ```
    ibmcloud login -api -a https://api.{region}.cloud.ibm.com
    ```
    {: codeblock}

    <table>
      <tr>
        <th>地域</th>
        <th>エンドポイント</th>
      </tr>
      <tr>
        <td>ダラス</td>
        <td><code>us-south</code></td>
      </tr>
      <tr>
        <td>フランクフルト</td>
        <td><code>eu-de</code></td>
      </tr>
      <tr>
        <td>シドニー</td>
        <td><code>au-syd</code></td>
      </tr>
      <tr>
        <td>ロンドン</td>
        <td><code>eu-gb</code></td>
      </tr>
      <tr>
        <td>東京</td>
        <td><code> jp-tok </code></td>
      </tr>
    </table>

5. IAM トークンを取得して、それをメモします。

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

6. そのチーム・メンバーは変更を行えないことを確認します。

    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/config/idps/facebook'
    ```
    {: codeblock}

    結果は 403 無許可メッセージです。

そのチーム・メンバーが {{site.data.keyword.appid_short_notm}} 構成を CLI から表示するには、以下の手順を実行する必要があります。

1. 端末で {{site.data.keyword.cloud_notm}} CLI を使用して、サインインします。

    ```
    ibmcloud login -a api.<region>.console.cloud.ibm.com
    ```
    {: codeblock}

2. IAM トークンを取得して、それをメモします。

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

3. cURL を使用して、Facebook の ID プロバイダー構成を表示します。

    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/facebook'
    ```
    {: codeblock}

    結果として、ID プロバイダー情報が入った 200 メッセージが得られます。
