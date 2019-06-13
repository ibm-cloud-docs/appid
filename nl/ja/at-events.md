---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-01"

keywords: authentication, authorization, identity, app security, secure, application identity, app to app, access token, activity

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


# {{site.data.keyword.cloudaccesstrailshort}} イベント
{: #at-events}

{{site.data.keyword.cloudaccesstrailshort}} サービスを使用すると、{{site.data.keyword.appid_full}} サービス・インスタンスで行われたユーザー開始アクティビティーを表示、管理、および分析することができます。
{: shortdesc}





サービスの動作について詳しくは、[{{site.data.keyword.cloudaccesstrailshort}} の資料](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)を参照してください。






## 管理イベントの表示
{: #at-monitor-admin}

{{site.data.keyword.at_short}} サービスを使用すると、{{site.data.keyword.appid_short_notm}} インスタンスで行われた構成アクティビティーを表示、管理、および分析することができます。
{: shortdesc}

管理アクティビティーをモニターするには、以下のようにします。

1. 自分の {{site.data.keyword.cloud_notm}} アカウントにログインします。
2. カタログから、{{site.data.keyword.appid_short_notm}} インスタンスと同じアカウントに {{site.data.keyword.cloudaccesstrailshort}} サービスのインスタンスをプロビジョンします。
3. {{site.data.keyword.cloudaccesstrailshort}} ダッシュボードで、**「管理」**タブをクリックします。
4. ドロップダウン・リストから以下の構成を行って、{{site.data.keyword.appid_short_notm}} によって生成されたイベントを検索します。
    * **「ログの表示」**で、**「アカウント・ログ」**を選択します。
    * **「検索」**で、**target.Management** を選択します。
    * **「フィルター」**で、`appid` と入力します。
5. **「フィルター」**をクリックします。

</br>

## 管理イベントのリスト
{: #at-events-admin}

{{site.data.cloudaccesstrailshort}} に送信されるイベントのリストについては、以下の表を参照してください。

<table>
  <tr>
    <th>アクション</th>
    <th>説明</th>
    <th>UI の場所</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>最近のアクティビティーを表示します。</td>
    <td><strong>「概要」</strong>タブの<strong>「アクティビティー・ログ」</strong>ボックスにあります。</td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>ID プロバイダー構成を表示します。</td>
    <td><strong>「ID プロバイダー」>「管理」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>ID プロバイダー構成を更新します。</td>
    <td><strong>「ID プロバイダー」>「管理」</strong>タブで更新できます。</td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>トークン有効期限構成を表示します。</td>
    <td><strong>「ID プロバイダー」>「トークン有効期限」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>ユーザー・プロファイル・ストレージ構成を表示します。</td>
    <td><strong>「概要」</strong>タブの<strong>「アクティビティー・ログ」</strong>にあります。</td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>ユーザー・プロファイル・ストレージ構成を更新します。</td>
    <td><strong>「プロファイル」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>ログイン・ウィジェット・ヘッダーのテーマ・カラーを表示します。</td>
    <td><strong>「ログインのカスタマイズ」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>ログイン・ウィジェット・ヘッダーのテーマ・カラーを更新します。</td>
    <td><strong>「ログインのカスタマイズ」</strong>タブで更新できます。</td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>ログイン・ウィジェットに表示されるイメージを表示します。</td>
    <td><strong>「ログインのカスタマイズ」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>ログイン・ウィジェットに表示されるイメージを更新します。</td>
    <td><strong>「ログインのカスタマイズ」</strong>タブで更新できます。</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>ヘッダーのカラーとイメージを含むログイン・ウィジェット UI 構成を表示します。</td>
    <td><strong>「ログインのカスタマイズ」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>サポート対象言語のリストを表示します。</td>
    <td>API から表示されなければなりません。</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>サポート対象言語を更新します。</td>
    <td>API を介して更新されなければなりません。</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>{{site.data.keyword.appid_short_notm}} SAML メタデータを表示します。</td>
    <td><strong>「ID プロバイダー」>「SAML 2.0 フェデレーション」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>Cloud Directory ユーザーを表示します。</td>
    <td><strong>「ユーザー」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>Cloud Directory ユーザーを更新します。</td>
    <td><strong>「ユーザー」</strong>タブで更新できます。</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>Cloud Directory ユーザーを削除します。</td>
    <td><strong>「ユーザー」</strong>タブで削除できます。</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>Cloud Directory ユーザーのリストを表示します。</td>
    <td><strong>「ユーザー」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>Cloud Directory ユーザーのリストを更新します。</td>
    <td><strong>「ユーザー」</strong>タブで更新できます。</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>Cloud Directory ユーザーのリストを削除します。</td>
    <td><strong>「ユーザー」</strong>タブで削除できます。</td>
  </tr>
  <tr>
    <td><code>read.emailTemplate</code></td>
    <td>E メール・テンプレートを表示します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「テンプレート」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.emailTemplate</code></td>
    <td>E メール・テンプレートを更新します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「テンプレート」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>delete.emailTemplate</code></td>
    <td>E メール・テンプレートを削除して、デフォルトにリセットします。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「テンプレート」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>read.senderDetails</code></td>
    <td>送信者の詳細を表示します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「設定」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.senderDetails</code></td>
    <td>送信者の詳細を更新します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「設定」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.resendNotification</code></td>
    <td>ユーザー通知を再送します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「設定」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>パスワード忘れプロセスを更新します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「設定」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>パスワード忘れの確認結果を表示します。</td>
    <td>API を介して実行されなければなりません。</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>登録プロセスを更新します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「設定」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>登録の結果確認を表示します。</td>
    <td>API を介して実行されなければなりません。</td>
  </tr>
  <tr>
    <td><code>read.action_url</code></td>
    <td>アクションの実行時に呼び出されるカスタム URL を表示します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「カスタムのランディング・ページ」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>アクションの実行時に呼び出されるカスタム URL を更新します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「設定」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.changePassword</code></td>
    <td>Cloud Directory ユーザー・パスワードを変更します。</td>
    <td><strong>「ID プロバイダー」>「クラウド・ディレクトリー」>「設定」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>read.loginWidgetConfig</code></td>
    <td>ログイン・ウィジェット構成を表示します。</td>
    <td><strong>「ログインのカスタマイズ」</strong>タブにあります。</td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>ログイン・ウィジェット構成を更新します。</td>
    <td><strong>「ログインのカスタマイズ」</strong>タブで更新できます。</td>
  </tr>
</table>



