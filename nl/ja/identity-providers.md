---

copyright:
  years: 2017
lastupdated: "2017-06-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# ID プロバイダーの構成
{: #setting-up-idp}

ユーザーのシングル・サインオン・エクスペリエンスをセットアップするために、Facebook、Google、IBM ID、またはこの 3 つの組み合わせを構成できます。ID プロバイダーを使用すると、ユーザーは使い慣れた資格情報でサインインできるようになります。
{:shortdesc}


## Facebook 認証の構成
{: #facebook}

Facebook を ID プロバイダーとして使用するように {{site.data.keyword.appid_short}} サービスを構成します。


### Facebook からアプリ ID とアプリ・シークレットを取得する
{: #getting-facebook-appid}

モバイル・アプリや Web アプリで Facebook を ID プロバイダーとして使用するには、Facebook アプリケーションで Web サイトのプラットフォームを追加して構成する必要があります。

1. <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for Developers サイト<img src="../../icons/launch-glyph.svg" alt="アイコン・アイコン"></a>で自分のアカウントにログインします。
2. Facebook のアプリ ID とアプリ・シークレットをメモします。サービスのダッシュボードで Web プロジェクトの認証を構成するときに、これらの値が必要になります。
3. Web プラットフォームを追加して、サイト URL を入力します。
4. 製品リストから、**「Facebook ログイン」**を選択します。
5. 「有効な OAuth リダイレクト URL」フィールドに、許可サーバーのコールバック・エンドポイント URL を入力します。サービス・インスタンスを構成した後、この値を追加できます。
6. **「変更の保存」**をクリックします。

### Facebook 認証用の {{site.data.keyword.appid_short_notm}} の構成
{: #configuring-facebook-appid}

Facebook のアプリ ID とアプリ・シークレットを取得し、Web クライアントを処理できるように Facebook for Developers アプリを構成すると、サービスのダッシュボードで Facebook 認証を編集できます。

1. サービスのダッシュボードの**「管理」**タブで、**「Facebook」**を選択して**「編集」**をクリックします。
2. Facebook for Developers Web サイトから取得した Facebook のアプリ ID とアプリ・シークレットを入力します。
3. **「Facebook for Developers のリダイレクト URI (Redirect URI for Facebook for Developers)」**フィールドにある URI をコピーします。この URI を Facebook Developers ポータルの**「Facebook ログイン (Facebook Login)」**セクションの**「有効な OAuth リダイレクト URI (Valid OAuth redirect URIs)」**フィールドに貼り付けます。
4. **「保存」**をクリックします。
5. オプション: Web アプリの場合は、リダイレクト URL を**「Web アプリケーションのリダイレクト URL (Web Application Redirect URLs)」**フィールドに入力します。この値は、開発者が決定する値であり、許可プロセスの完了後にリダイレクト URL にアクセスするために使用されます。


## Google 認証の構成
{: #google}

Google を ID プロバイダーとして使用するように {{site.data.keyword.appid_short_notm}} サービスを構成します。


### Google からクライアント ID とシークレットを取得する
{: #google-client-id}

Google を ID プロバイダーとして使用するには、Google のクライアント ID とシークレットを取得して Google Developer Console でプロジェクトを作成します。

1. <a href="https://console.developers.google.com/apis/library" target="_blank">Google Developer Console<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> で Google アプリケーションを開きます。
2. Google+ API を追加します。
3. OAuth を使用して資格情報を作成します。**「アプリケーションの種類」**フィールドで、**「ウェブ アプリケーション」**を選択します。**「承認済みのリダイレクト URI (Authorized redirect URIs)」**フィールドに、{{site.data.keyword.appid_short_notm}} リダイレクト URI を入力します。{{site.data.keyword.appid_short_notm}} のリダイレクト許可 URI は、サービスのダッシュボードの Google 構成画面から取得できます。
4. Google のクライアント ID とシークレットをメモし、変更を保存します。



### Google 認証用の {{site.data.keyword.appid_short_notm}} の構成
{: #google-client-appid}

Google のクライアントとシークレットを取得し、Web クライアントを処理できるように Google Developers コンソールを構成すると、サービスのダッシュボードで Google 認証を編集できます。

1. サービスのダッシュボードの**「管理」**タブで、**「Google」**を選択して**「編集」**をクリックします。
3. Google Developers コンソールから取得した Google のクライアント ID とシークレットを入力します。
4. **「Google for Developers のリダイレクト URI (Redirect URI for Google for Developers)」**フィールドにある URI をコピーします。この URI を、Google Developers ポータルの**「Web アプリケーションのクライアント ID (Client ID for web application)」**セクションの**「制限事項 (Restrictions)」**の下にある**「承認済みのリダイレクト URI (Authorized redirect URIs)」** フィールドに貼り付けます。
5. **「保存」**をクリックします。
6. オプション: Web アプリの場合、リダイレクト URI を**「Web アプリケーションのリダイレクト URI (Web Application Redirect URIs)」**フィールドに入力します。この値は、開発者が決定する値であり、許可プロセスの完了後にリダイレクト URI にアクセスするために使用されます。


## IBM ID 認証の構成

IBM ID を ID プロバイダーとして使用する場合は、<a href="https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide" target="_blank">IBMid-Federation-Guide <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用します。既に BlueID アプリを使用している場合は、BlueID クライアント ID とシークレットを取得します。


### IBM ID からクライアント ID とシークレットを取得する

クライアント ID とシークレットを取得するには、以下の手順を使用します。

1. <a href="https://w3.innovate.ibm.com/tools/sso/home.html" target="_blank">SSO Self-Service Provisioner <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> で、BlueID アカウントにログインします。
2. BlueID アプリを登録します。ID プロバイダーには、必ず**「実動前 (preproduction)」**または**「実動 (production)」**を選択してください。
3. **「クライアントの詳細 (Client Details)」**に、App ID リダイレクト URL を入力します。リダイレクト許可 URI は、サービス・ダッシュボードの IBM ID 構成画面から取得できます。
4. 必ず**「許可コード」**を選択してください。
5. BlueID クライアント ID、シークレット、およびアカウント ID プロバイダー・タイプをメモします。**「続行」&「完了」**をクリックします。

### IBM ID 認証用の App ID の構成

BlueID クライアント ID とシークレットを取得し、BlueID アプリに正しいリダイレクト URI を構成すれば、サービス・ダッシュボードの BlueID 認証セクションを編集できます。

1. サービスのダッシュボードの**「管理」**タブで、**「IBM ID」**を選択して**「編集」**をクリックします。
2. BlueID クライアント ID とシークレットを入力します。
3. **「IBMid for Developers のリダイレクト URI (Redirect URI for IBMid for Developers)」** フィールドにある URI をコピーして、**「リダイレクト URI (Redirect URIs)」**に貼り付けます。
4. ID プロバイダーに**「実動前 (preproduction)」**または**「実動 (production)」**を選択し、**「保存」**をクリックします。
5. オプション: Web アプリの場合は、リダイレクト URI を**「Web アプリケーションのリダイレクト URI (Web Application Redirect URIs)」**フィールドに入力します。この値は、開発者が決定する値であり、許可後にリダイレクト URI にアクセスするために使用されます。
