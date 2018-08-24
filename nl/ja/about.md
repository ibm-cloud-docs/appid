---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 概要
{: #about}

アプリケーション・セキュリティーは複雑過ぎて手に負えなくなることもあります。 これはほとんどの開発者にとって、アプリ作成における難題の一つとなっています。 確実にユーザー情報を保護するにはどうすればよいでしょうか? アプリに {{site.data.keyword.appid_full}} を統合することによって、セキュリティーに関する経験があまりなくても、リソースを保護し、認証を追加することができます。
{:shortdesc}


## サービスを使用する理由
{: #reasons}

開発者は {{site.data.keyword.appid_short_notm}} を利用すると、少ない行数のコードで Web アプリやモバイル・アプリに認証を簡単に追加し、{{site.data.keyword.Bluemix_notm}} 上のクラウド・ネイティブのアプリケーションとサービスを保護することができます。ユーザーにアプリへのサインインを要求することで、アプリの設定や公開されているソーシャル・プロファイル情報などのユーザー・データを保管し、そのデータを利用してアプリ内の操作環境をユーザーごとにカスタマイズできます。{{site.data.keyword.appid_short_notm}} により手軽なログイン・フレームワークが提供されますが、クラウド・ディレクトリーと共に使用される、独自のブランド・マークが付いたサインイン画面を表示することもできます。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} を使用したいと思うのはなぜでしょうか。 以下にいくつかのシナリオを取り上げます。当てはまるシナリオがあるかどうか、ご確認ください。

<table>
  <tr>
    <th>シナリオ</th>
    <th>ソリューション</th>
  </tr>
  <tr>
    <td>モバイル・アプリや Web アプリに[許可と認証](/docs/services/appid/authorization.html)を追加する必要があるが、セキュリティーに関する背景知識がない。</td>
    <td>{{site.data.keyword.appid_short_notm}} を使用すれば、アプリに認証ステップを簡単に追加できます。 API、SDK、事前構築された UI、または独自のブランド・マークが付いた UI を使用する、E メールまたはユーザー名によるサインイン、ソーシャル・サインイン、またはエンタープライズ・サインインをアプリに追加することができます。</td>
  </tr>
  <tr>
    <td>アプリケーションやバックエンド・リソースへのアクセスを制限したい。</td>
    <td>{{site.data.keyword.appid_short_notm}} によって提供される標準ベースの認証を使用すれば、アプリ、バックエンド・リソース、API を簡単に保護できます。</td>
  </tr>
  <tr>
    <td>ユーザーのために個人別設定の可能なアプリケーション操作環境を構築したい。</td>
    <td>{{site.data.keyword.appid_short_notm}} を使用すれば、アプリの設定や公開されているソーシャル・プロファイル情報などの[ユーザー・データを保管](/docs/services/appid/user-profile.html)し、そのデータを利用してアプリの操作環境を個別にカスタマイズできます。</td>
  </tr>
  <tr>
    <td>スケーラブルな方法でユーザーを管理したい。</td>
    <td> {{site.data.keyword.appid_short_notm}} では、[Cloud Directory](/docs/services/appid/cloud-directory.html)を作成できます。これにより、ユーザー登録とサインインをアプリに追加できます。 Cloud Directory は、ユーザー・ベースに合わせて拡張可能なユーザー・レジストリーを維持するためのフレームワークを提供します。 事前構築されたセルフサービスの機能 (E メールの検証やパスワードのリセットなど) を利用することで、アプリはユーザーを安全に認証できるようになります。</td>
  </tr>
</table>


## 統合
{: #integrations}

{{site.data.keyword.appid_short_notm}} を他の {{site.data.keyword.Bluemix_notm}} オファリングと一緒に使用することができます。
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>標準クラスター内に入口を構成することにより、クラスター・レベルでアプリを保護できます。 始めに <a href="/docs/containers/cs_annotations.html#appid-auth">{{site.data.keyword.appid_short_notm}} 認証 Ingress アノテーション</a>または <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Announcing App ID integration to IBM Cloud Kubernetes Service <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> ブログ投稿を確認してください。</dd>
  <dt>{{site.data.keyword.openwhisk}} と API Connect</dt>
    <dd>[{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) と [API Connect](/docs/apis/management/manage_apis.html) を使用して API を作成すると、アプリ・コードではなくゲートウェイでアプリケーションを保護できます。 実際の統合を確認するには、<a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> をご覧ください。</dd>
  <dt>Cloud Foundry</dt>
    <dd>提供されているサンプル Cloud Foundry アプリのいずれかを試してみて、アプリに {{site.data.keyword.appid_short_notm}} を組み込む方法を確認してください。</dd>
  <dt>iOS プログラミング・ガイド</dt>
    <dd>Apple 対応アプリを開発しますか? {{site.data.keyword.Bluemix_notm}} を使用する既存の iOS アプリの学習、実験、拡張を行うには、<a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS プログラミング・ガイド <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を実際に使ってみてください。</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>[{{site.data.keyword.cloudaccesstrailshort}} サービス](/docs/services/cloud-activity-tracker/index.html)を使用すると、{{site.data.keyword.appid_short_notm}} で行われた管理アクティビティー (ダッシュボード構成の変更など) をモニターできます。</dd>
  <dt>Node.js プログラミング・ガイド</dt>
    <dd>Node.js でアプリを開発しますか? {{site.data.keyword.Bluemix_notm}} を使用する既存の Node.js アプリの学習、実験、拡張を行うには、<a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Node.js プログラミング・ガイド <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を実際に使ってみてください。</dd>
</dl>


## アーキテクチャー
{: #architecture}

{{site.data.keyword.appid_short_notm}} を使用すれば、ユーザーにサインインを要求することによって、アプリのセキュリティー・レベルを強化できます。 さらに Server SDK または API を使用してバックエンド・リソースを保護することも可能です。
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} アーキテクチャーの図](/images/appid_architecture1.png)

<dl>
  <dt>アプリケーション</dt>
    <dd><strong>Server SDK</strong>: Server SDK を使用して、{{site.data.keyword.Bluemix_notm}} でホストされているバックエンド・リソースや、Web アプリを保護できます。 Server SDK は、要求からアクセス・トークンを抽出し、{{site.data.keyword.appid_short_notm}} で検証します。 </br>
    <strong>Client SDK</strong>: Android または iOS の Client SDK を使用して、モバイル・アプリを保護できます。 Client SDK は、許可チャレンジを検出すると、クラウド・リソースと通信して認証プロセスを開始します。</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: 認証が成功すると、{{site.data.keyword.appid_short_notm}} からアクセス・トークンと識別トークンがアプリに返されます。</br>
    <strong>クラウド・ディレクトリー</strong>: ユーザーは自分の E メールとパスワードを使用してサービスに登録できます。 その後、UI を使用してユーザーをリスト表示で管理できます。 クラウド・ディレクトリーを使用すれば、{{site.data.keyword.appid_short_notm}} は ID プロバイダーとして機能します。</dd>
  <dt>外部 (サード・パーティー)</dt>
    <dd><strong>ソーシャル ID プロバイダーとエンタープライズ ID プロバイダー</strong>: {{site.data.keyword.appid_short_notm}} は、Facebook、Google+、SAML 2.0 フェデレーションを ID プロバイダー・オプションとしてサポートしています。このサービスは、ID プロバイダーへのリダイレクトを調整し、返された認証トークンを検証します。 トークンが有効であれば、サービスは、実際のパスフレーズに一度もアクセスせずに、アプリにアクセス権限を付与します。</dd>
</dl>


## 要求フロー
{: #request}

要求フローはアプリケーション構成に応じて異なる場合はありますが、App ID を利用する際に扱う可能性のある主なフローは 3 つあります。モバイル・アプリ・フローを作成するか、Web アプリ・フローを作成するか、別のフローによってリソースを保護することができます。いくつかのフロー例を調べて、アプリを構成するときに開始点として使用できないか確認してください。
{: shortdesc}

### Web アプリ要求フロー
{: #web-flow}

![{{site.data.keyword.appid_short_notm}} 要求フロー](/images/web_flow1.png)

1. ユーザーが、ブラウザーを使用して、App ID SDK への要求をトリガーするアクションを実行します。
2. ユーザーに許可が与えられなかった場合、App ID へのリダイレクトが開始します。
3. App ID はログイン・ウィジェットを起動し、それをブラウザーに送信します。
4. ユーザーは、認証を行うための ID プロバイダーを選択し、サインイン・プロセスを実行します。
5. ID プロバイダーは、元の App ID SDK にリダイレクトし、識別トークンを渡します。
6. App ID SDK は、App ID サービスからアクセス・トークンを取得します。
7. それらのトークンが App ID SDK によって保存され、リダイレクトが実行されます。
8. ユーザーはアプリケーションへのアクセス権限を付与されます。

### モバイル要求フロー
{: #mobile-flow}

![{{site.data.keyword.appid_short_notm}} 要求フロー](/images/mobile_flow.png)

1. ユーザーが、クライアント・アプリケーションによる App ID SDK への要求をトリガーするアクションを実行します。
2. ユーザーが有効なアクセス・トークンを持っていない場合、App ID SDK は許可プロセスを開始します。
3. ログイン・ウィジェットがユーザーに表示されます。
4. 構成されている ID プロバイダーのいずれかを使用して、ユーザーの認証が行われます。
5. ユーザーに識別トークンが付与されると、SDK は App ID サービスからアクセス・トークンを取得します。
6. 両方のトークンを使用して、SDK は要求を再実行します。
7. 両方のトークンが有効であれば、ユーザーはアプリケーションへのアクセス権限を付与されます。

### 保護リソース要求フロー
{: #pr-flow}

![{{site.data.keyword.appid_short_notm}} 要求フロー](/images/pr_flow.png)

1. リソースへの要求を行うためには、その前にクライアント・アプリケーションで一式の公開鍵を取得しておくことが必要です。
2. クライアント・アプリケーションが公開鍵を使用して要求を行います。
3. 有効なアクセス・トークンがない場合、アプリケーションはエラーを受け取ります。
4. 有効なトークンを取得したら、クライアント・アプリは要求を再び実行できます。今回はトークンを含めます。
5. アクセス・トークンによって付与される許可をアプリケーションで検証できた場合、そのアプリケーションに保護リソースへのアクセス権限が付与されます。
