---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: Authentication, authorization, identity, app security, secure, compliance, high availability, ha, disaster recover, dr, protocols, oauth, oidc

subcollection: appid

---

{:external: target="_blank" .external}
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
{: shortdesc}



## サービスを使用する理由
{: #about-reasons}

開発者は {{site.data.keyword.appid_short_notm}} を利用すると、少ない行数のコードで Web アプリやモバイル・アプリに認証を簡単に追加し、{{site.data.keyword.cloud_notm}} 上のクラウド・ネイティブのアプリケーションとサービスを保護することができます。 ユーザーにアプリへのサインインを要求することで、アプリの設定や公開されているソーシャル・プロファイル情報などのユーザー・データを保管し、そのデータを利用してアプリ内の操作環境をユーザーごとにカスタマイズできます。 {{site.data.keyword.appid_short_notm}} では、ログイン・フレームワークが提供されますが、独自のブランド・マークが付いた画面を Cloud Directory で使用することもできます。
{: shortdesc}

Cloud Directory はどのようなことができますか? このビデオでサービスのさまざまな利用方法の詳細を確認した後、その他のシナリオについて次の表で追加の情報をお読みください。

<iframe class="embed-responsive-item" id="about-appid" title="{{site.data.keyword.appid_short_notm}} の概要" type="text/html" width="640" height="390" src="//www.youtube.com/embed/XlrCjHdK43Q?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<table>
  <tr>
    <th>シナリオ</th>
    <th>ソリューション</th>
  </tr>
  <tr>
    <td>モバイル・アプリや Web アプリに[許可と認証](/docs/services/appid?topic=appid-key-concepts)を追加する必要があるが、セキュリティーに関する背景知識がない。</td>
    <td>{{site.data.keyword.appid_short_notm}} を使用すれば、アプリに認証ステップを簡単に追加できます。 API、SDK、事前構築された UI、または独自のブランド・マークが付いた UI を使用する、E メールまたはユーザー名によるサインイン、ソーシャル・サインイン、またはエンタープライズ・サインインをアプリに追加することができます。</td>
  </tr>
  <tr>
    <td>アプリケーションやバックエンド・リソースへのアクセスを制限したい。</td>
    <td>{{site.data.keyword.appid_short_notm}} によって提供される標準ベースの認証を使用すれば、アプリ、バックエンド・リソース、API を簡単に保護できます。</td>
  </tr>
  <tr>
    <td>ユーザーのために個人別設定の可能なアプリケーション操作環境を構築したい。</td>
    <td>{{site.data.keyword.appid_short_notm}} を使用すれば、アプリの設定や公開されているソーシャル・プロファイル情報などの[ユーザー・データを保管](/docs/services/appid?topic=appid-profiles)し、そのデータを利用してアプリの操作環境を個別にカスタマイズできます。</td>
  </tr>
  <tr>
    <td>スケーラブルな方法でユーザーを管理したい。</td>
    <td> {{site.data.keyword.appid_short_notm}} では、[Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) を作成できます。これにより、ユーザー登録とサインインをアプリに追加できます。 Cloud Directory は、ユーザー・ベースに合わせて拡張可能なユーザー・レジストリーを維持するためのフレームワークを提供します。 事前構築されたセルフサービスの機能 (E メールの検証やパスワードのリセットなど) を利用することで、アプリはユーザーを安全に認証できるようになります。</td>
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
    <strong>Cloud Directory</strong>: ユーザーは自分の E メールとパスワードを使用してサービスに登録できます。 その後、UI を使用してユーザーをリスト表示で管理できます。 Cloud Directory を使用すれば、{{site.data.keyword.appid_short_notm}} は ID プロバイダーとして機能します。</dd>
  <dt>外部 (サード・パーティー)</dt>
    <dd><strong>ソーシャル ID プロバイダーとエンタープライズ ID プロバイダー</strong>: {{site.data.keyword.appid_short_notm}} は、Facebook、Google+、SAML 2.0 フェデレーションを ID プロバイダー・オプションとしてサポートしています。 このサービスは、ID プロバイダーへのリダイレクトを調整し、返された認証トークンを検証します。 トークンが有効であれば、サービスは、実際のパスフレーズに一度もアクセスせずに、アプリにアクセス権限を付与します。</dd>
</dl>


## 統合
{: #about-integrations}

{{site.data.keyword.appid_short_notm}} を他の {{site.data.keyword.cloud_notm}} オファリングと一緒に使用することができます。
{:shortdesc}

<dl>
  <dt>{{site.data.keyword.containershort_notm}}</dt>
    <dd>標準クラスター内に Ingress を構成することにより、クラスター・レベルでアプリを保護できます。 始めに <a href="/docs/containers?topic=containers-ingress_annotation#appid-auth">{{site.data.keyword.appid_short_notm}} 認証 Ingress アノテーション</a>または <a href="https://www.ibm.com/cloud/blog/announcing-app-id-integration-ibm-cloud-kubernetes-service">Announcing {{site.data.keyword.appid_short_notm}} integration to {{site.data.keyword.containerlong_notm}} <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> ブログ投稿を確認してください。</dd>
  <dt>{{site.data.keyword.openwhisk_short}} および {site.data.keyword.apiconnect_short}}</dt>
    <dd>[{{site.data.keyword.openwhisk_short}}](/docs/openwhisk?topic=cloud-functions-getting-started) と [API Connect](/docs/services/apiconnect?topic=apiconnect-getting-started) を使用して API を作成すると、アプリ・コードではなくゲートウェイでアプリケーションを保護できます。 実際の統合を確認するには、<a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAuth with API Connect and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> をご覧ください。</dd>
  <dt>Cloud Foundry</dt>
    <dd>提供されているサンプル Cloud Foundry アプリのいずれかを試してみて、アプリに {{site.data.keyword.appid_short_notm}} を組み込む方法を確認してください。</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>[{{site.data.keyword.cloudaccesstrailshort}} の資料](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started)を使用し、{{site.data.keyword.appid_short_notm}} で行われた管理アクティビティー (ダッシュボード構成の変更など) をモニターできます。</dd>
  <dt>iOS プログラミング・ガイド</dt>
    <dd>Apple 対応アプリを開発しますか? {{site.data.keyword.cloud_notm}} を使用する既存の iOS アプリの学習、実験、拡張を行うには、[iOS プログラミング・ガイド](/docs/swift?topic=swift-getting-started)を実際に使ってみてください。</dd>
  <dt>Node.js プログラミング・ガイド</dt>
    <dd>Node.js でアプリを開発しますか? {{site.data.keyword.cloud_notm}} を使用する既存の Node.js アプリの学習、実験、拡張を行うには、[Node.js プログラミング・ガイド](/docs/node?topic=nodejs-getting-started)を実際に使ってみてください。</dd>
</dl>


## コンプライアンスと標準
{: #about-compliance}

{{site.data.keyword.appid_short_notm}} は、いくつもの認定、監査、および標準に合格しています。 
{: shortdesc}

{{site.data.keyword.appid_short_notm}} は、企業向けのアプリケーションと消費者向けのアプリケーションの両方で広く使用されている既知の業界標準プロトコルと仕様のセットである OAuth 2.0 Authorization Framework、および Open ID Connect に基づいています。 OAuth 2.0 は、保護リソースにアクセスするための許可の取得と検証のために使用されています。 それに加えて、Open ID Connect により、認証と ID 保護のレイヤーがアプリケーションに追加されています。

[認定](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=BF31C8008D7C11E59F9AD7336D7D0FFB){: external}の詳細なリストを確認するには、{{site.data.keyword.appid_short_notm}} ソフトウェア製品互換性レポートのセクション 5.4 を参照してください。 認定に加えて、{{site.data.keyword.appid_short_notm}} は、OAuth 2.0、OpenID Connect、JSON Web Token (JWT)、JSON Web Signature (JWS)、System for Cross-domain Identity Management (SCIM) の仕様にも準拠しています。 


## 地域的高可用性
{: #ha-dr}

{{site.data.keyword.appid_short_notm}} は、複数のゾーンで稼働する高可用性地域サービスです。
{: shortdesc}

サポートされるそれぞれの複数ゾーン地域の中のどのゾーンにも、いくつかのワーカー・ノードが存在する独自の {{site.data.keyword.containerlong_notm}} クラスターがあります。 各ワーカー・ノードでは {{site.data.keyword.appid_short_notm}} コンポーネントの複数のインスタンスが実行されます。 各地域に対して、グローバル・ロード・バランサーと Web アプリケーション・ファイアウォールが置かれています。

{{site.data.keyword.appid_short_notm}} に保管されるデータは暗号化され、複数のアベイラビリティー・ゾーンにわたって広がるデータベース・クラスターで保持されます。 データは別個の暗号化されたオブジェクト・ストレージでもバックアップされます。

{{site.data.keyword.appid_short_notm}} は地域サービスであるため、自動地域間フェイルオーバーや地域間災害復旧は提供しません。 ただし、{{site.data.keyword.appid_short_notm}} には、[多種多様な API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external} が用意されているので、開発者は API を使用してサービス構成を {{site.data.keyword.appid_short_notm}} の別のインスタンスと手動で同期することができます。

