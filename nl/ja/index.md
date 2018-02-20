---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 概説チュートリアル
{: #gettingstarted}

{{site.data.keyword.appid_full}} は、モバイル・アプリや Web アプリに認証を追加するのに役立ち、バックエンド・リソースを保護します。
{: shortdesc}

## サービス・インスタンスの作成
{: #create}

始めに {{site.data.keyword.appid_short_notm}} のインスタンスを作成します。{: shortdesc}

1. {{site.data.keyword.Bluemix}} カタログで、{{site.data.keyword.appid_short_notm}} を選択します。 サービス構成画面が開きます。
2. サービス・インスタンスに名前を付けます。または、事前設定された名前を使用します。
3. インスタンスをバインドするには、**「接続」**メニューからアプリを選択します。 **「アンバインドのまま」**を選択した場合、後でサービス・インスタンスをバインドすることができます。
4. 料金プランを選択し、**「作成」**をクリックします。

## サンプル・アプリの構成
{: #sample-app}

事前構成されたサンプル・アプリの 1 つを使用して、サービスの機能について学ぶことができます。
{: shortdesc}

すぐに使用可能なサンプル・アプリには 2 つの ID プロバイダーが構成されています。これを使用して認証について学習できます。また、ログイン・ウィジェット機能を使用してサインイン・ページをカスタマイズし、加えた更新がすぐにアプリに表示されることも確認できます。

GUI からサンプル・アプリを構成するには、以下のようにします。

1. サービスのインスタンスを作成した後に、使用しやすい言語のサンプル・アプリを選択できます。iOS Swift、Android、Node.js、および Java から選択できます。SDK を使用しないことも可能です。<a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">{{site.data.keyword.appid_short_notm}} を Python などの他の言語で使用する方法 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> についてのブログを参照してください。
2. GUI の手順に従い、サンプル・アプリを**ビルドして実行します**。言語ごとに構成方法が若干異なるので、必ず、ダウンロードしたアプリの言語をドロップダウンから選択してください。アプリが構成された後に、それをブラウザーで開き、資格情報を使用してログインすることができます。
  **注**: 使用する言語の前提条件がインストールされていることを確認してください。
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 以上 </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools バージョン 25.0.2 </li></ul></dd>
    <dt> iOS Swift</dt>
      <dd><ul><li> CocoaPods (バージョン 1.1.0 以上) </li><li> iOS 9 以上 </li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> Cloud Foundry CLI </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> Cloud Foundry CLI </li><li> Maven </li></ul></dd>
  </dl>
3. **「アクティビティーの確認」**をクリックして、発生した認証イベントを表示します。自分がログインしているので、イベントは少なくとも 1 つ表示されます。
4. ログイン操作環境をカスタマイズします。ロゴなどの画像やヘッダーの色を選択できます。色の選択肢の中から選択することも、16 進値を入力することもできます。プレビューを確認したら、**「変更を保存」**をクリックします。次の図は、サンプルのサインイン操作環境の例を示しています。
5. ブラウザーで、ログイン・ページを最新表示します。前の手順で加えた変更が既に表示されています。
