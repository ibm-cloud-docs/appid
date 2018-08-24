---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{: tip: .tip}

# ソーシャル ID プロバイダーの構成
{: #setting-up-idp}

ID プロバイダーによって、モバイル・アプリケーションや Web アプリケーションに認証レベルを追加できます。 {{site.data.keyword.appid_full}} では、1 つ以上の ID プロバイダーを構成して、アプリのシングル・サインオンをセットアップできます。
{: shortdesc}

## デフォルト構成
{: #default}

{{site.data.keyword.appid_short_notm}} には、ID プロバイダーの初期セットアップに役立つデフォルト構成が用意されています。
{: shortdesc}

デフォルトの資格情報のセットアップは、Facebook と Google を対象にしています。 資格情報の使用は、1 インスタンスあたり毎日 100 回に制限されています。 これらは IBM の資格情報なので、これを使用するのは開発モードの時だけにしてください。 アプリを公開する前に、自分の資格情報になるように構成を更新してください。

## リダイレクト URL のホワイトリスト設定
{: #redirect}

リダイレクト URL は、アプリのコールバック・エンドポイントです。 フィッシング攻撃を防ぐために、App ID はリダイレクト URL のホワイトリストに照らして URL を検証します。 フィッシングが発生すると、攻撃者はユーザー・トークンへのアクセス権を取得してしまう恐れがあります。

URL をホワイトリストに追加するには、以下のようにします。

1. **「ID プロバイダー」>「管理」**に移動します。
2. **「Web リダイレクト URL の追加」**フィールドに URL を入力し、**「+」**をクリックします。

URL には照会パラメーターは含めないでください。 それらは検証プロセスで無視されます。 URL 例: `http://host:[port]/path`
{: tip}


## Facebook の構成
{: #facebook}

Facebook を ID プロバイダーとして使用するように {{site.data.keyword.appid_short}} サービスを構成できます。
{: shortdesc}

### Facebook からアプリ ID とアプリ・シークレットを取得する

Facebook を ID プロバイダーとして使用するには、Facebook アプリケーションで Web サイトのプラットフォームを追加して構成する必要があります。

1. <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for developers サイト<img src="../../icons/launch-glyph.svg" alt="アイコン・アイコン"></a>で自分のアカウントにログインします。
2. Facebook のアプリ ID とアプリ・シークレットをメモします。 サービスのダッシュボードで Web プロジェクトの認証を構成するときに、これらの値が必要になります。
3. Web プラットフォームを追加して、サイト URL を入力します。
4. 製品リストから、**「Facebook ログイン」**を選択します。
5. 「有効な OAuth リダイレクト URL」フィールドに、許可サーバーのコールバック・エンドポイント URL を入力します。
6. **「変更の保存」**をクリックします。


### Facebook 認証用の {{site.data.keyword.appid_short_notm}} の構成

Facebook のアプリ ID とアプリ・シークレットを取得し、Web クライアントを処理できるように Facebook for Developers アプリを構成すると、サービスのダッシュボードで Facebook 認証を編集できます。

1. サービスのダッシュボードの**「管理」**タブで、**「Facebook」**を選択して**「編集」**をクリックします。
2. Facebook for Developers Web サイトから取得した Facebook のアプリ ID とアプリ・シークレットを入力します。
3. **「Facebook for Developers のリダイレクト URI (Redirect URI for Facebook for Developers)」**フィールドにある URI をコピーします。 この URI を Facebook Developers ポータルの**「Facebook ログイン (Facebook Login)」**セクションの**「有効な OAuth リダイレクト URI (Valid OAuth redirect URIs)」**フィールドに貼り付けます。
4. **「保存」**をクリックします。
5. オプション: Web アプリの場合は、リダイレクト URL を**「Web アプリケーションのリダイレクト URL (Web Application Redirect URLs)」**フィールドに入力します。 この値は、開発者が決定する値であり、許可プロセスの完了後にリダイレクト URL にアクセスするために使用されます。 URL は `http` または `https` スキームに従う必要があります。高水準のセキュリティーを実現するには、`https` スキームを使用します。


## Google の構成
{: #google}

Google を ID プロバイダーとして使用するように {{site.data.keyword.appid_short}} サービスを構成できます。
{: shortdesc}

### Google からクライアント ID とシークレットを取得する

<a href="https://developers.google.com/" target="_blank">Google Developers Console <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> でプロジェクトを作成し、Web クライアントに対応できるようにプロジェクトを構成し、クライアント ID とシークレットを取得します。

1. プロジェクトを作成します。
2. Google プロジェクトに Google+ API を追加します。
3. Google+ API に資格情報を追加します。
    1. API のタイプとして Google+ API を選択します。
    2. API を呼び出す場所として**「Web ブラウザー」**を選択します。
    3. **「ユーザー・データ」**を選択します。
    4. 必須フィールドに値を入力して、クライアント ID を作成します。 同時にシークレットも作成されます。
4. Google のクライアント ID とシークレットをメモします。 資格情報のタブで、作成した ID を選択し、シークレットとクライアント ID を取得します。

### Google 認証用の {{site.data.keyword.appid_short}} の構成

Google プロジェクトを構成してクライアント ID とシークレットを取得したら、Google 認証のためにサービス・ダッシュボードを編集します。

1. サービスのダッシュボードの**「管理」**タブで、**「Google」**を選択して**「編集」**をクリックします。
2. Google Developers Console コンソールから取得したクライアント ID とシークレットを入力します。
3. {{site.data.keyword.appid_short}} の URL を許可します。
    1. Google ID プロバイダーの詳細情報から **Google Developer Console のリダイレクト URL** をコピーします。
    2. Google プロジェクトの資格情報のタブで、この統合のために作成したクライアント ID を選択します。
    3. {{site.data.keyword.appid_short}} の URL を**「許可されたリダイレクト URI」**フィールドに貼り付けて、**「保存」**をクリックします。
4. **「保存」**をクリックして、{{site.data.keyword.appid_short}} の Google 構成を更新します。
5. Web アプリの場合は、**「管理」**タブにリダイレクト URL を入力します。 許可プロセスが完了すると、ユーザーがその URL に送信されます。 URL は `http` または `https` スキームに従う必要があります。高水準のセキュリティーを実現するには、`https` スキームを使用します。
