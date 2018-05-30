---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# サービス・アクセスの管理
{: #service-access-management}

{{site.data.keyword.appid_full}} と {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) を使用すると、アカウント所有者は自分のアカウントに属するユーザー・アクセスを管理できます。
{: shortdesc}

アカウント所有者は、アカウント内にポリシーを設定して、さまざまなユーザー用にさまざまなレベルのアクセス権限を作成できます。例えば、特定のユーザーに対して、あるインスタンスについては**「読み取り専用」**アクセス権限を付与し、別のインスタンスについては**「書き込み」**アクセス権限を付与することができます。どのユーザーに、{{site.data.keyword.appid_short_notm}} のインスタンスの作成、更新、削除を許可するかを決定することができます。

IAM について詳しくは、[IAM のアクセス権限](/docs/iam/users_roles.html)を参照してください。

## ユーザー役割
{: #roles}

アクセス・ポリシーの有効範囲は、ユーザーに割り当てられた役割に基づいています。
{: shortdesc}

ポリシーにより、アクセス権限をさまざまなレベルで付与することができます。オプションには以下のものがあります。
<ul><ul>
  <li>自分のアカウントに属するサービスのすべてのインスタンス間でのアクセス</li>
  <li>自分のアカウントに属する個別のサービス・インスタンスへのアクセス</li>
  <li>インスタンス内の特定のリソースへのアクセス</li>
  <li>自分のアカウントに属するすべての IAM 対応のサービスへのアクセス</li>
</ul></ul>

ユーザーは、プラットフォーム管理役割を使用して、プラットフォーム・レベルでサービス・リソースに対するタスクを実行できます。例えば、役割を割り当てることにより、ID の作成や削除、インスタンスの作成、アプリへのインスタンスのバインドを実行できるユーザーを決定できます。以下の表は、プラットフォーム管理役割と相関するアクションについて詳しく示しています。

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
    <td>アカウントに属するすべてのサービスに対するすべての管理アクション。</td>
    <td>すべてのオペレーター・アクション、および他のユーザーにポリシーを割り当てる機能を実行できます。</td>
  </tr>
</table>

</br>
</br>
次の表は、サービス・アクセス役割にマップされたアクションについて詳しく示しています。ユーザーは、サービス・アクセス役割を使用して、{{site.data.keyword.appid_short_notm}} にアクセスしたり、{{site.data.keyword.appid_short_notm}} API を呼び出したりできます。


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
    <td>リーダーのすべてのアクション、およびサービス・インスタンスの編集 (ID プロバイダー構成の編集など) を実行できます。</li></ul></td>
  </tr>
</table>

UI でユーザー役割を割り当てる方法について詳しくは、[IAM アクセス権限の管理](/docs/iam/mngiam.html#iammanidaccser)を参照してください。

## {{site.data.keyword.appid_short_notm}} アクセス・ポリシー
{: #access}

ご使用のアカウントに属する {{site.data.keyword.appid_short_notm}} サービスにアクセスするすべてのユーザーには、IAM ユーザー役割が定義されたアクセス・ポリシーを割り当てる必要があります。そのポリシーにより、選択したサービスまたはインスタンスのコンテキスト内でユーザーが実行できるアクションを決定します。
{: shortdesc}

アクションは、{{site.data.keyword.Bluemix_notm}} サービスで実行が許可された操作として、そのサービスでカスタマイズおよび定義されます。その後、アクションは IAM ユーザー役割にマップされます。{{site.data.keyword.appid_short_notm}} の場合、以下のアクションが存在します。

<table>
  <tr>
    <th>コマンド</th>
    <th>説明</th>
    <th>役割</th>
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
</table>




## 例: 別のユーザーに {{site.data.keyword.appid_short_notm}} のインスタンスへのアクセス権限を付与する
{: #example}

このシナリオで、管理者は {{site.data.keyword.appid_short_notm}} のインスタンスを作成し、チームの別のメンバーにビューアー・アクセス権限を付与する必要があります。
{: shortdesc}

開始前に、以下のことを行います。
* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html) をインストールします。

アクセス許可を更新するために、管理者は以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。
2. [IAM の資料](/docs/iam/iamusermanage.html#iamusermanage)に記載された手順に従って、その従業員に表示アクセス権限を付与します。
3. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「サービス資格情報」**タブに移動します。**「資格情報の表示」**をクリックして、**tentantID** をコピーします。
4. 端末で {{site.data.keyword.Bluemix_notm}} CLI を使用してサインインします。
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. IAM トークンを取得して、それをメモします。
    ```
    bx iam oauth-tokens
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
    'https://appid-management.stage1.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    結果は 403 無許可メッセージです。

そのチーム・メンバーが {{site.data.keyword.appid_short_notm}} 構成を CLI から表示するには、以下の手順を実行する必要があります。

1. 端末で {{site.data.keyword.Bluemix_notm}} CLI を使用して、サインインします。
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. IAM トークンを取得して、それをメモします。
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. cURL を使用して、Facebook の ID プロバイダー構成を表示します。
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    結果として、ID プロバイダー情報が入った 200 メッセージが得られます。
