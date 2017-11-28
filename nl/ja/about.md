---

copyright:
  years: 2017
lastupdated: "2017-11-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 概要
{: #about}

{{site.data.keyword.appid_full}} には、アプリケーションへのアクセスを管理するための使いやすい機能が用意されています。
{:shortdesc}


## サービスを使用する理由
{: #reasons}

{{site.data.keyword.appid_short_notm}} を使用したいと思うのはなぜでしょうか。以下にいくつかのシナリオを取り上げます。当てはまるシナリオがあるかどうか、ご確認ください。
{: shortdesc}

<table>
  <tr>
    <th> シナリオ</th>
    <th> 理由</th>
  </tr>
  <tr>
    <td> モバイル・アプリケーションや Web アプリケーションにセキュリティーを追加したい。</td>
    <td> {{site.data.keyword.appid_short_notm}} を使用すれば、アプリケーションに認証ステップを簡単に追加できます。サービスを使用することによって、ID プロバイダーと通信しながらアプリケーションへのアクセスを管理できます。</td>
  </tr>
  <tr>
    <td> アプリケーションやバックエンド・リソースへのアクセスを制限したい。</td>
    <td> サービスを使用すれば、認証ユーザーと匿名ユーザーの両方のリソースを保護できます。</td>
  </tr>
  <tr>
    <td> ユーザーのために個人別設定の可能なアプリケーション操作環境を構築したい。</td>
    <td> {{site.data.keyword.appid_short_notm}} では、ユーザー・データ (アプリケーションの設定や公開用のソーシャル・プロファイルの情報など) を保管できます。そのデータに基づいて、ユーザーごとにカスタマイズした操作環境を提供できます。</td>
  </tr>
</table>

**注**: 実装されているプロトコルは、OpenID Connect (OIDC) に完全に準拠しています。


## アーキテクチャー
{: #architecture}

{{site.data.keyword.appid_short_notm}} を使用すれば、ユーザーにサインインを要求することによって、アプリケーションのセキュリティー・レベルを強化できます。Server SDK を使用してバックエンド・リソースを保護することも可能です。

{{site.data.keyword.appid_short_notm}} サービスの仕組みの概要を以下の図に示します。


![{{site.data.keyword.appid_short_notm}} アーキテクチャーの図](/images/appid_architecture2.png)

図 1. {{site.data.keyword.appid_short_notm}} アーキテクチャーの図



<dl>
  <dt> アプリケーション</dt>
    <dd> Client SDK には、クラウド・リソースと通信するための要求クラスが用意されています。Client SDK は、許可チャレンジを検出すると、認証プロセスを自動的に開始します。</dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd>  サーバー SDK は、要求からアクセス・トークンを抽出し、{{site.data.keyword.appid_short_notm}} で検証します。認証が成功すると、{{site.data.keyword.appid_short_notm}} からアクセス・トークンと識別トークンがアプリケーションに返されます。</dd>
  <dt> ID プロバイダー</dt>
    <dd> サービスが ID プロバイダーへのリダイレクトを調整し、認証情報を確認してアプリケーションへのアクセスを許可します。{{site.data.keyword.appid_short_notm}} は、実際のパスフレーズにアクセスしないで資格情報を確認します。</dd>
</dl>


## 要求フロー
{: #request}

以下の図は、要求が Client SDK からバックエンド・アプリケーションおよび ID プロバイダーへどのように流れていくのかを説明したものです。

![{{site.data.keyword.appid_short_notm}} 要求フロー](/images/appidrequestflow.png)

図 2. {{site.data.keyword.appid_short_notm}} の要求フロー


* {{site.data.keyword.appid_short_notm}} Client SDK が、{{site.data.keyword.appid_short_notm}} Server SDK によって保護されているバックエンド・リソースへの要求を実行します。
* {{site.data.keyword.appid_short_notm}} Server SDK は、無許可の要求を検出し、HTTP 401 と許可スコープを返します。
* Client SDK は自動的に HTTP 401 を検出し、認証プロセスを開始します。
* 複数の ID プロバイダーが構成されている場合、Client SDK がサービスに連絡を取ると、Server SDK はログイン・ウィジェットを返します。{{site.data.keyword.appid_short_notm}} は、ID プロバイダーを呼び出してそのプロバイダーのログイン・フォームを提示するか、ID プロバイダーが構成されていない場合には認証のための権限付与コードを返します。
* {{site.data.keyword.appid_short_notm}} は、認証チャレンジを提供することによって、認証を行うようにクライアント・アプリに要求します。
* ID プロバイダーが構成されていると、ユーザーのログイン時に、該当する OAuth フローによって認証が処理されます。
* 認証が同じ権限付与コードで終了する場合、そのコードがトークン・エンドポイントに送信されます。エンドポイントは、アクセス・トークンと識別トークンという 2 つのトークンを返します。この時点以降、Client SDK で行われたすべての要求は、新しく入手した許可ヘッダーを含むようになります。
* Client SDK は、認証フローをトリガーしたオリジナルの要求を自動的に再送します。
* Server SDK は、要求から許可ヘッダーを抽出し、サービスを使用してそのヘッダーを検証し、バックエンド・リソースへのアクセスを認可します。


## コンポーネント
{: #components}

サービスは、以下のコンポーネントで構成されています。

<dl>
  <dt> ダッシュボード</dt>
    <dd> サービス・ダッシュボードで、研修用のサンプルをダウンロードしたり、アクティビティー・ログを確認したり、認証と ID プロバイダーを構成したりできます。</dd>
  <dt> Client SDK</dt>
    <dd> モバイル・アプリケーションや Web アプリケーションで Client SDK を使用して、ユーザー認証を実装できます。</br></br>
    Android の場合の前提条件:
    <ul><ul><li> API 25 以上</li>
    <li> Java 8.x </li>
    <li> Android SDK Tools 25.2.5 以上</li>
    <li> Android SDK Platform Tools 25.0.3 以上</li>
    <li> Android Build Tools バージョン 25.0.2 以上</li></ul></ul></br>
    iOS の場合の前提条件:
    </br>
    <ul><ul><li> iOS9 以上</li>
    <li> MacOS 10.11.5 </li>
    <li>Xcode 8.2 </li></ul></ul></dd>
  <dt> Server SDK</dt>
    <dd> {{site.data.keyword.Bluemix_notm}} でホストされているバックエンド・リソースを保護できます。</br>
    サポートされているランタイム:
    <ul><ul><li> Node.js</li>
    <li> Liberty for Java </li>
    <li> Swift

</li></ul></ul></dd>
</dl>
