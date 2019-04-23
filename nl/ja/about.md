---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-08"

keywords: authentication, authorization, identity, app security, secure, compliance, high availability

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

# {{site.data.keyword.appid_short_notm}} の概要
{: #about}

アプリケーション・セキュリティーは複雑過ぎて手に負えなくなることもあります。 これはほとんどの開発者にとって、アプリ作成における難題の一つとなっています。 確実にユーザー情報を保護するにはどうすればよいでしょうか? アプリに {{site.data.keyword.appid_full}} を統合することによって、セキュリティーに関する経験があまりなくても、リソースを保護し、認証を追加することができます。
{:shortdesc}



## サービスを使用する理由
{: #about-reasons}

開発者は {{site.data.keyword.appid_short_notm}} を利用すると、少ない行数のコードで Web アプリやモバイル・アプリに認証を簡単に追加し、{{site.data.keyword.cloud_notm}} 上のクラウド・ネイティブのアプリケーションとサービスを保護することができます。 ユーザーにアプリへのサインインを要求することで、アプリの設定や公開されているソーシャル・プロファイル情報などのユーザー・データを保管し、そのデータを利用してアプリ内の操作環境をユーザーごとにカスタマイズできます。 {{site.data.keyword.appid_short_notm}} では、ログイン・フレームワークが提供されますが、独自のブランド・マークが付いた画面を Cloud Directory で使用することもできます。
{: shortdesc}

Cloud Directory はどのようなことができますか? このビデオでサービスのさまざまな利用方法の詳細を確認した後、その他のシナリオについて次の表で追加の情報をお読みください。

<iframe class="embed-responsive-item" id="youtubeplayer" title="App ID の概要" type="text/html" width="640" height="390" src="//www.youtube.com/embed/XlrCjHdK43Q?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<table>
  <tr>
    <th>シナリオ</th>
    <th>ソリューション</th>
  </tr>
  <tr>
    <td>モバイル・アプリや Web アプリに[許可と認証](/docs/services/appid?topic=appid-key-concepts#key-concepts)を追加する必要があるが、セキュリティーに関する背景知識がない。</td>
    <td>{{site.data.keyword.appid_short_notm}} を使用すれば、アプリに認証ステップを簡単に追加できます。 API、SDK、事前構築された UI、または独自のブランド・マークが付いた UI を使用する、E メールまたはユーザー名によるサインイン、ソーシャル・サインイン、またはエンタープライズ・サインインをアプリに追加することができます。</td>
  </tr>
  <tr>
    <td>アプリケーションやバックエンド・リソースへのアクセスを制限したい。</td>
    <td>{{site.data.keyword.appid_short_notm}} によって提供される標準ベースの認証を使用すれば、アプリ、バックエンド・リソース、API を簡単に保護できます。</td>
  </tr>
  <tr>
    <td>ユーザーのために個人別設定の可能なアプリケーション操作環境を構築したい。</td>
    <td>{{site.data.keyword.appid_short_notm}} を使用すれば、アプリの設定や公開されているソーシャル・プロファイル情報などの[ユーザー・データを保管](/docs/services/appid?topic=appid-user-profile#user-profile)し、そのデータを利用してアプリの操作環境を個別にカスタマイズできます。</td>
  </tr>
  <tr>
    <td>スケーラブルな方法でユーザーを管理したい。</td>
    <td> {{site.data.keyword.appid_short_notm}} では、[Cloud Directory](/docs/services/appid?topic=appid-cloud-directory#cloud-directory) を作成できます。これにより、ユーザー登録とサインインをアプリに追加できます。Cloud Directory は、ユーザー・ベースに合わせて拡張可能なユーザー・レジストリーを維持するためのフレームワークを提供します。 事前構築されたセルフサービスの機能 (E メールの検証やパスワードのリセットなど) を利用することで、アプリはユーザーを安全に認証できるようになります。</td>
  </tr>
</table>


## 動作の仕組み
{: #about-how-it-works}

{{site.data.keyword.appid_short_notm}} を使用すれば、ユーザーにサインインを要求することによって、アプリのセキュリティー・レベルを強化できます。 さらに Server SDK または API を使用してバックエンド・リソースを保護することも可能です。
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} アーキテクチャーの図](images/appid_architecture1.png)

<dl>
  <dt>アプリケーション</dt>
    <dd><strong>Server SDK</strong>: Server SDK を使用して、{{site.data.keyword.cloud_notm}} でホストされているバックエンド・リソースや、Web アプリを保護できます。 Server SDK は、要求からアクセス・トークンを抽出し、{{site.data.keyword.appid_short_notm}} で検証します。 </br>
    <strong>Client SDK</strong>: Android または iOS の Client SDK を使用して、モバイル・アプリを保護できます。 Client SDK は、許可チャレンジを検出すると、クラウド・リソースと通信して認証プロセスを開始します。</dd>
  <dt>{{site.data.keyword.cloud_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: 認証が成功すると、{{site.data.keyword.appid_short_notm}} からアクセス・トークンと識別トークンがアプリに返されます。</br>
    <strong>Cloud Directory</strong>: ユーザーは自分の E メールとパスワードを使用してサービスに登録できます。その後、UI を使用してユーザーをリスト表示で管理できます。 Cloud Directory を使用すれば、{{site.data.keyword.appid_short_notm}} は ID プロバイダーとして機能します。</dd>
  <dt>外部 (サード・パーティー)</dt>
    <dd><strong>ソーシャル ID プロバイダーとエンタープライズ ID プロバイダー</strong>: {{site.data.keyword.appid_short_notm}} は、Facebook、Google+、SAML 2.0 フェデレーションを ID プロバイダー・オプションとしてサポートしています。 このサービスは、ID プロバイダーへのリダイレクトを調整し、返された認証トークンを検証します。 トークンが有効であれば、サービスは、実際のパスフレーズに一度もアクセスせずに、アプリにアクセス権限を付与します。</dd>
</dl>


## 統合
{: #about-integrations}

{{site.data.keyword.appid_short_notm}} を他の {{site.data.keyword.cloud_notm}} オファリングと一緒に使用することができます。
{:shortdesc}

<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>標準クラスター内に Ingress を構成することにより、クラスター・レベルでアプリを保護できます。 始めに <a href="/docs/containers?topic=containers-ingress_annotation#appid-auth">{{site.data.keyword.appid_short_notm}} 認証 Ingress アノテーション</a>または <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Announcing {{site.data.keyword.appid_short_notm}} integration to {{site.data.keyword.containerlong_notm}} <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> ブログ投稿を確認してください。</dd>
  <dt>{{site.data.keyword.openwhisk}} と API Connect</dt>
    <dd>[{{site.data.keyword.openwhisk_short}}](/docs/openwhisk?topic=cloud-functions-getting_started#getting_started) と [API Connect](/docs/services/apiconnect?topic=apiconnect-index#index) を使用して API を作成すると、アプリ・コードではなくゲートウェイでアプリケーションを保護できます。 実際の統合を確認するには、<a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAauth with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> をご覧ください。</dd>
  <dt>Cloud Foundry</dt>
    <dd>提供されているサンプル Cloud Foundry アプリのいずれかを試してみて、アプリに {{site.data.keyword.appid_short_notm}} を組み込む方法を確認してください。</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>[{{site.data.keyword.cloudaccesstrailshort}} サービス](/docs/services/cloud-activity-tracker/reference?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla)を使用すると、{{site.data.keyword.appid_short_notm}} で行われる管理アクティビティー (ダッシュボード構成の変更など) をモニターできます。</dd>
  <dt>iOS プログラミング・ガイド</dt>
    <dd>Apple 対応アプリを開発しますか? {{site.data.keyword.cloud_notm}} を使用する既存の iOS アプリの学習、実験、拡張を行うには、[iOS プログラミング・ガイド](/docs/swift/authenticate?topic=swift-getting_started_swift#getting_started_swift)を実際に使ってみてください。</dd>
  <dt>Node.js プログラミング・ガイド</dt>
    <dd>Node.js でアプリを開発しますか? {{site.data.keyword.cloud_notm}} を使用する既存の Node.js アプリの学習、実験、拡張を行うには、[Node.js プログラミング・ガイド](/docs/node?topic=nodejs-node-getting-started#node-getting-started)を実際に使ってみてください。</dd>
</dl>


## コンプライアンスと標準
{: #about-compliance}

{{site.data.keyword.appid_short_notm}} は、いくつもの認定取得、監査、標準準拠を既に完了しています。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} は、企業と利用者の両方に接続するアプリケーションである OAuth 2.0 Authorization Framework、および Open ID Connect でよく見られる既知の業界標準プロトコルと業界標準仕様のセットに基づいています。OAuth 2.0 は、保護リソースにアクセスするための許可の取得と検証に使用されます。その上で、Open ID Connect は、認証と ID の保護のレイヤーをアプリケーションに追加します。

[認定](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=BF31C8008D7C11E59F9AD7336D7D0FFB)の詳細なリストを確認するには、{{site.data.keyword.appid_short_notm}} ソフトウェア製品互換性レポートのセクション 5.4 を参照してください。認定に加えて、{{site.data.keyword.appid_short_notm}} は、Oauth 2.0、OpenID Connect、JSON Web Token (JWT)、JSON Web Signature (JWS)、System for Cross-domain Identity Management (SCIM) の仕様においても準拠しています。 


## 地域的高可用性
{: #ha-dr}

{{site.data.keyword.appid_short_notm}} は、複数のゾーンで稼働する高可用性地域サービスです。
{: shortdesc}

サポートされる複数ゾーン地域のそれぞれで、どのゾーンにも、いくつかのワーカー・ノードが存在する独自の {{site.data.keyword.containerlong_notm}} クラスターがあります。各ワーカー・ノードは {{site.data.keyword.appid_short_notm}} コンポーネントのいくつかのインスタンスを実行します。各地域に面して、グローバル・ロード・バランサーと Web アプリケーション・ファイアウォールが置かれています。

{{site.data.keyword.appid_short_notm}} に保管されるデータは暗号化され、複数のアベイラビリティー・ゾーンにわたって広がるデータベース・クラスターで保持されます。データは別個の暗号化オブジェクト・ストレージでもバックアップされます。

{{site.data.keyword.appid_short_notm}} は地域サービスであるため、自動地域間フェイルオーバーや地域間災害復旧は提供しません。ただし、{{site.data.keyword.appid_short_notm}} には、<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">広範囲 API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> が用意されています。開発者はこれを使用して、サービス構成を {{site.data.keyword.appid_short_notm}} の別のインスタンス (複数可) と手動で同期を取ることができます。
