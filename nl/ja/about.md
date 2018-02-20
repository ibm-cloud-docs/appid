---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 概要
{: #about}

{{site.data.keyword.appid_full}} を使用して、アプリに認証を追加したり、バックエンド・リソースを保護したりできます。
{:shortdesc}

## サービスを使用する理由
{: #reasons}

{{site.data.keyword.appid_short_notm}} を使用したいと思うのはなぜでしょうか。 以下にいくつかのシナリオを取り上げます。当てはまるシナリオがあるかどうか、ご確認ください。
{: shortdesc}

<table>
  <tr>
    <th> シナリオ </th>
    <th> 理由 </th>
  </tr>
  <tr>
    <td> モバイル・アプリや Web アプリに[許可と認証](/docs/services/appid/authorization.html)を追加する必要があるが、セキュリティーに関する背景知識がない。 </td>
    <td> {{site.data.keyword.appid_short_notm}} を使用すれば、アプリに認証ステップを簡単に追加できます。 サービスを使用することによって、アプリへのアクセスを管理するために [ID プロバイダー](/docs/services/appid/identity-providers.html)と通信できます。 </td>
  </tr>
  <tr>
    <td> アプリケーションやバックエンド・リソースへのアクセスを制限したい。 </td>
    <td> このサービスを使用すれば、認証ユーザーと匿名ユーザーの両方を対象に、[自分のリソースを保護](/docs/services/appid/protecting-resources.html)できます。 </td>
  </tr>
  <tr>
    <td> ユーザーのために個人別設定の可能なアプリケーション操作環境を構築したい。 </td>
    <td> {{site.data.keyword.appid_short_notm}} を使用すれば、アプリの設定や公開されているソーシャル・プロファイル情報などの[ユーザー・データを保管](/docs/services/appid/user-profile.html)し、そのデータを利用してアプリの操作環境を個別にカスタマイズできます。</td>
  </tr>
  <tr>
    <td> ユーザーが自分の E メールとパスワードを使用してアプリにアクセスできるようにしたい。</td>
    <td> {{site.data.keyword.appid_short_notm}} は、[クラウド・ディレクトリー](/docs/services/appid/cloud-directory.html)を作成する機能を提供します。これにより、ユーザー登録およびサインインをモバイル・アプリと Web アプリに追加できます。クラウド・ディレクトリーは、ユーザー・ベースに合わせて拡張可能なユーザー・レジストリーを維持するためのフレームワークを提供します。事前構築されたセルフサービスの機能 (E メールの検証やパスワードのリセットなど) を利用することで、アプリはユーザーを安全に認証できるようになります。</td>
  </tr>
</table>


## アーキテクチャー
{: #architecture}

{{site.data.keyword.appid_short_notm}} を使用すれば、ユーザーにサインインを要求することによって、アプリのセキュリティー・レベルを強化できます。 さらに Server SDK を使用してバックエンド・リソースを保護することも可能です。{: shortdesc}

![{{site.data.keyword.appid_short_notm}} アーキテクチャーの図](/images/appid_architecture.png)

<dl>
  <dt> アプリケーション </dt>
    <dd> Server SDK: Server SDK を使用して、{{site.data.keyword.Bluemix_notm}} でホストされているバックエンド・リソースや、Web アプリを保護できます。 Server SDK は、要求からアクセス・トークンを抽出し、{{site.data.keyword.appid_short_notm}} で検証します。 </br>
    Client SDK: Android または iOS の Client SDK を使用して、モバイル・アプリを保護できます。 Client SDK は、許可チャレンジを検出すると、クラウド・リソースと通信して認証プロセスを開始します。</dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd> App ID: 認証が成功すると、{{site.data.keyword.appid_short_notm}} からアクセス・トークンと識別トークンがアプリに返されます。</br>
    Cloud Directory: ユーザーは自分の E メールとパスワードを使用してサービスに登録できます。 その後、UI を使用してユーザーをリスト表示で管理できます。 </dd>
  <dt> 外部 (サード・パーティー) </dt>
    <dd>  {{site.data.keyword.appid_short_notm}} は、Facebook と Google+ の 2 つのソーシャル ID プロバイダーをサポートしています。 このサービスは、ID プロバイダーへのリダイレクトを調整し、認証情報の検証後にアプリへのアクセス権限を付与します。 {{site.data.keyword.appid_short_notm}} は、実際のパスフレーズにアクセスしないで資格情報を確認します。 </dd>
</dl>


## 要求フロー
{: #request}

以下の図は、要求が Client SDK からバックエンド・リソースと ID プロバイダーへどのように流れていくのかを説明したものです。{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 要求フロー](/images/appidrequestflow.png)


* {{site.data.keyword.appid_short_notm}} Client SDK が、{{site.data.keyword.appid_short_notm}} Server SDK によって保護されているバックエンド・リソースへの要求を実行します。
* {{site.data.keyword.appid_short_notm}} Server SDK は、無許可の要求を検出し、HTTP 401 と許可スコープを返します。
* Client SDK は自動的に HTTP 401 を検出し、認証プロセスを開始します。
* 複数の ID プロバイダーが構成されている場合、Client SDK がサービスに連絡を取ると、Server SDK はログイン・ウィジェットを返します。 {{site.data.keyword.appid_short_notm}} は、ID プロバイダーを呼び出してそのプロバイダーのログイン・フォームを提示するか、ID プロバイダーが構成されていない場合には認証のための権限付与コードを返します。
* {{site.data.keyword.appid_short_notm}} は、認証チャレンジを提供することによって、認証を行うようにクライアント・アプリに要求します。
* ID プロバイダーが構成されていると、ユーザーのログイン時に、該当する OAuth フローによって認証が処理されます。
* 認証が同じ権限付与コードで終了する場合、そのコードがトークン・エンドポイントに送信されます。 エンドポイントは、アクセス・トークンと識別トークンという 2 つのトークンを返します。 この時点以降、Client SDK で行われたすべての要求は、新しく入手した許可ヘッダーを含むようになります。
* Client SDK は、認証フローをトリガーしたオリジナルの要求を自動的に再送します。
* Server SDK は、要求から許可ヘッダーを抽出し、サービスを使用してそのヘッダーを検証し、バックエンド・リソースへのアクセスを認可します。

**注**: 実装されているプロトコルは、OpenID Connect (OIDC) に完全に準拠しています。
