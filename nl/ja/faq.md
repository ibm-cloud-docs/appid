---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# FAQ

この FAQ には、{{site.data.keyword.appid_full}} サービスに関する一般的な質問に対する答えがあります。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} の料金はどのように計算しますか?
{: #pricing}

{{site.data.keyword.appid_short_notm}} では、使用するリソースが増えるにつれて、支払いは少なくなります。
{: shortdesc}

累進階層方式のプランは、認証イベントの数と許可ユーザーの数の 2 つの部分で構成されています。 この 2 つの部分の合計に基づいて、毎月課金されます。 合計額は、数量にその階層の単価を乗算して計算する、各レベルの使用量の累積料金です。

### 認証イベント

認証イベントは、新しい {{site.data.keyword.appid_short_notm}} トークンの発行時に発生します。 識別されたユーザーの場合、新しいトークンはそれぞれ 1 時間有効になります。 匿名ユーザーの場合、トークンは 1 カ月有効になります。 トークンの期限が切れた後に保護リソースにアクセスするには、新しいトークンを作成する必要があります。 アプリ ID を使用してモバイル認証を行う場合、ユーザー・トークンは `key-store/key-chain` に保管され、以後のすべての要求に追加されます。 {{site.data.keyword.appid_short_notm}} の Android または iOS の Swift SDK を使用してトークンにアクセスできます。 このサービスを使用して Web 認証を行う場合、セッション Cookie に<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">ユーザー・トークンを保管 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> します。

### 許可ユーザー

許可ユーザーとは、直接的または間接的にサービスにログインする固有のユーザーのことです。 各 ID プロバイダーから 1 人の新しいユーザー (匿名ユーザーを含む) がログインするたびに、1 人分の許可ユーザー料金が課金されます。 例えば、あるユーザーが Facebook でログインし、その後 Google を使用してログインした場合には、それらは 2 つの別個の許可ユーザーと見なされます。

累進階層方式の価格設定について詳しくは、[{{site.data.keyword.Bluemix_notm}} の価格設定の資料](/docs/billing-usage/how_charged.html#services)を参照してください。

</br>

## どのようなタイプのアクティビティーが App ID によってモニターされますか?
{: #activity-monitor}

サービス・インスタンスにバインドされたアプリ内で生成されたアクティビティーを追跡できます。また、Activity Tracker サービスを使用して、App ID 内で行われた管理アクティビティーもモニターできます。

アプリによって生成されたアクティビティーを参照するには、以下のようにします。

1. ご自分の IBM Cloud アカウントにログインします。
2. ダッシュボードから、App ID のインスタンスを選択します。
3. **「概要」**タブをクリックします。
4. **「アクティビティー・ログ」**にリストされたアクティビティーを参照します。

</br>
管理アクティビティーをモニターするには、以下のようにします。

1. ご自分の IBM Cloud アカウントにログインします。App ID のインスタンスがプロビジョンされている組織とスペースに移動します。
2. カタログから、Activity Tracker サービスのインスタンスをプロビジョンします。App ID のインスタンスと同じスペース内にいることを確認してください。
3. Activity Tracker ダッシュボードで、**「管理」**タブをクリックします。
4. ドロップダウン・リストで以下の構成を選択して、App ID によって生成されたイベントを検索します。
<table>
  <tr>
    <th> フィールド</th>
    <th> 構成</th>
  </tr>
  <tr>
    <td><i>ログの表示</i></td>
    <td><b>スペース・ログ</b></td>
  </tr>
  <tr>
    <td><i>Search</i></td>
    <td><b>target.name</b></td>
  </tr>
  <tr>
    <td>フィルター</td>
    <td>appid</td>
  </tr>
</table>
5. **「フィルター」**をクリックします。

このサービスの機能について詳しくは、[Activity Tracker の資料](/docs/services/cloud-activity-tracker/index.html)を参照してください。
