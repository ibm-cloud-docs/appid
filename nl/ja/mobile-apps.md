---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-27"

keywords: authentication, authorization, identity, app security, secure, development, mobile, android, iOS

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

# モバイル・アプリ
{: #mobile-apps}

{{site.data.keyword.appid_full}} を使用すると、ネイティブまたはハイブリッドのモバイル・アプリ用に認証レイヤーを素早く構成できます。
{: shortdesc}

## フローについて
{: #understanding-mobile}

モバイル・フローは、ユーザーのデバイス (ネイティブ・アプリケーション) にインストールされるアプリを開発する際に役立ちます。 このフローを使用すると、アプリ上でユーザーを安全に認証できるので、各デバイスで個別設定されたユーザー・エクスペリエンスを提供できます。

### このフローの技術基盤
{: #mobile-technical-flow}

ネイティブ・アプリケーションはユーザーのデバイスに直接インストールされるため、サード・パーティーは、プライベート・ユーザー情報とアプリケーション資格情報を比較的に容易に抽出できます。 デフォルトでは、これらのタイプのアプリケーションは、グローバル資格情報やユーザー・リフレッシュ・トークンを保管できないため、信頼できないクライアントと呼ばれます。 その結果、信頼できないクライアントでは、アクセス・トークンの有効期限が切れるたびにユーザーが資格情報を入力する必要があります。

アプリケーションを信頼できるクライアントに変換するために、{{site.data.keyword.appid_short}} は[動的クライアント登録](https://tools.ietf.org/html/rfc7591)を利用します。 アプリケーション・インスタンスは、ユーザーの認証を開始する前に、まず OAuth2 クライアントとして {{site.data.keyword.appid_short}} に登録します。 クライアント登録の結果、アプリケーションはインストール済み環境に固有のクライアント ID を受け取ります。これにデジタル署名して使用することによって、{{site.data.keyword.appid_short}} に要求を許可してもらうことができます。 {{site.data.keyword.appid_short}} はアプリケーションの対応する公開鍵を保管しているので、要求署名を検証できます。これにより、アプリケーションを機密クライアントとして扱うことが可能になります。 このプロセスにより、アプリケーションが資格情報を無期限に公開するリスクが最小限に抑えられます。また、トークンの自動リフレッシュが可能になるので、ユーザー・エクスペリエンスが大幅に向上します。

登録の後に、ユーザーを認証するための OAuth2 の `authorization code` または `resource owner password` [許可付与](https://tools.ietf.org/html/rfc6749#section-1.3)フローを使用して、ユーザーの認証が行われます。


### 動的クライアント登録
{: #mobile-dynamic}

1. ユーザーが、クライアント・アプリケーションによる {{site.data.keyword.appid_short}} SDK への要求をトリガーするアクションを実行します。
2. アプリがまだモバイル・クライアントとして登録されていない場合、SDK は動的登録フローを開始します。
3. 登録が成功すると、{{site.data.keyword.appid_short}} はインストール済み環境に固有のクライアント ID を返します。

### 許可フロー
{: #mobile-auth-flow}

![{{site.data.keyword.appid_short_notm}} アプリからアプリへのフロー](images/mobile-flow.png)

1. {{site.data.keyword.appid_short}} SDK は、{{site.data.keyword.appid_short_notm}}`/authorization` エンドポイントを使用して許可プロセスを開始します。
2. ログイン・ウィジェットがユーザーに表示されます。
3. 構成されている ID プロバイダーのいずれかを使用して、ユーザーの認証が行われます。
4. {{site.data.keyword.appid_short}} は許可付与を返します。
5. 許可付与は、{{site.data.keyword.appid_short_notm}}`/token` エンドポイントからのアクセス・トークン、識別トークン、およびリフレッシュ・トークンに交換されます。


## {{site.data.keyword.appid_short}} SDK を使用したモバイル・アプリの構成
{: #configuring-mobile}

SDK を使用して {{site.data.keyword.appid_short}} を開始します。
{: shortdesc}

**始める前に**

以下の情報が必要です。

* {{site.data.keyword.appid_short_notm}} インスタンス

* インスタンスのテナント ID。 これは、サービス・ダッシュボードの**「サービス資格情報」**タブにあります。

* インスタンスのデプロイメント {{site.data.keyword.cloud_notm}} 地域。 地域はコンソールに表示されています。

  <table><caption> 表 1. {{site.data.keyword.cloud_notm}} 地域と対応する SDK 値</caption>
  <tr>
    <th>{{site.data.keyword.cloud_notm}} 地域</th>
    <th>SDK 値</th>
  </tr>
  <tr>
    <td>米国南部</td>
    <td><code>AppID.REGION_US_SOUTH</code> </td>
  </tr>
  <tr>
    <td>シドニー</td>
    <td><code>AppID.REGION_SYDNEY</code></td>
  </tr>
  <tr>
    <td>英国</td>
    <td><code>AppID.REGION_UK</code></td>
  </tr>
  <tr>
    <td>ドイツ</td>
    <td><code>AppID.REGION_GERMANY</code></td>
  </tr>
</table>

## Android SDK を使用した認証
{: #mobile-android}

**始める前に**

開始する前に、以下の前提条件を満たしている必要があります。

  * API 27 以上
  * Java 8.x
  * Android SDK Tools 26.1.1+
  * Android SDK Platform Tools 27.0.1+
  * Android Build Tools バージョン 27.0.0+


### SDK のインストール
{: #mobile-android-install}

1. Android Studio プロジェクトを作成するか、既存のプロジェクトを開きます。

2. JitPack リポジトリーをルートの `build.gradle` ファイルに追加します。

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. アプリケーションの `build.gradle` ファイルを見つけます。 **注**: プロジェクトの `build.gradle` ファイルではなくアプリのファイルを開いてください。

  1. {{site.data.keyword.appid_short_notm}} クライアント SDK を dependencies セクションに追加します。

    ```gradle
    dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
    ```
    {: codeblock}

  2. `defaultConfig` セクションで、リダイレクト・スキームを構成します。

    ```gradle
    defaultConfig {
      ...
      manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
    ```
    {: codeblock}

6. プロジェクトを Gradle と同期化します。 **「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**とクリックします。

</br>

### SDK の初期化
{: #mobile-android-initialize}


1. context、tenant ID、region パラメーターを initialize メソッドに渡して、SDK を構成します。

    初期化コードを入れる一般的な場所 (ただし、必須ではない) は、Android アプリケーション内のメイン・アクティビティーの `onCreate` メソッド内です。
    {: tip}

    ```java
    AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <region>);
    ```
    {: codeblock}

</br>
</br>

## iOS Swift SDK を使用した認証
{: #mobile-ios}

{{site.data.keyword.appid_short}} Client SDK を使用してモバイル・アプリケーションを保護します。
{:shortdesc}

</br>
**始める前に**

開始する前に、以下の前提条件を満たしている必要があります。

  * Xcode 9.0 以上
  * CocoaPods 1.1.0 以上
  * iOS 10.0 以上

</br>

### SDK のインストール
{: #mobile-ios-install}

{{site.data.keyword.appid_short_notm}} Client SDK には、Swift プロジェクトと Objective-C Cocoa プロジェクト用の従属関係マネージャーである CocoaPods が付属しています。 CocoaPods は成果物をダウンロードし、プロジェクトで使用できるようにします。

1. Xcode プロジェクトを作成するか、既存のプロジェクトを開きます。

2. プロジェクトのディレクトリー内に `Podfile` を新規作成するか、または既存のものを開きます。

3. `IBMCloudAppID` ポッドと `use_frameworks!` コマンドをターゲットの従属関係に追加します

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. プロジェクト・ディレクトリー内のコマンド・ラインから従属関係をインストールします。

  ```swift
  $ pod install --repo-update
  ```
  {: codeblock}

5. インストールの後に、Xcode プロジェクトおよびリンクされた従属関係を格納する `<your app>.xcworkspace` ファイルを開きます

6. Xcode プロジェクトのキーチェーン共有を有効にします。 **「Project Settings」>「Capabilities」>「Keychain Sharing」**に移動し、**「Enable keychain sharing」**を選択します。

7. **「Project Settings」>「Info」>「URL Types」**を開き、**「URL Type」**を追加します。 **「Identifier」**と**「URL Scheme」**の両方のテキスト・ボックスに以下の値を入力します。

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

</br>

### SDK の初期化
{: #mobile-ios-initialize}

1. tenant ID パラメーターと region パラメーターを initialize メソッドに渡すことによって、Client SDK を初期化します。

  ```swift
    AppID.sharedInstance.initialize(tenantId: <tenantId>, region: <region>)
  ```
  {: codeblock}

  初期化コードの一般的な配置場所 (必須の場所ではない) は、Swift アプリケーションの AppDelegate ファイルの `application:didFinishLaunchingWithOptions` メソッド内です。
  {: tip}

2. {{site.data.keyword.appid_short}} SDK を `AppDelegate` ファイルにインポートします。

  ```swift
  import IBMCloudAppID
  ```
  {: codeblock}

3. {{site.data.keyword.appid_short}} を介したリダイレクトを処理するようにアプリケーションを構成します。

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
      return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}


## 保護 API へのアクセス
{: #mobile-accessing-apis}

ログイン・フローが成功した後に、アクセス・トークンと ID トークンを使用して、任意の SDK やネットワーキング・ライブラリーを使用する保護バックエンド・リソースを呼び出すことができます。

</br>

### Swift SDK を使用する場合
{: #mobile-access-api-swift}

1.  保護リソース要求を呼び出すファイルに、以下のインポートを追加します。

  ```swift
  import BMSCore
  import IBMCloudAppID
  ```
  {: codeblock}

2. 保護リソースを呼び出します

   ```swift
  BMSClient.sharedInstance.initialize(region: <region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)

  let request =  Request(url: "<your protected resource url>")

  request.send { (response: Response?, error: Error?) in

      guard let response = response, error == null else {
          print("An error occurred invoking a protected resources", error?.localizedDescription ?? "No response was received")
          return;
      }
      // use your response object
  })
  ```
  {: codeblock}

</br>

### Android SDK を使用する場合
{: #mobile-access-api-android}

1. 保護リソース要求を呼び出すファイルに、以下のインポートを追加します。

  ```java
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
  import com.ibm.cloud.appid.android.api.AppIDAuthorizationManager;
  ```

2. 保護リソースを呼び出します

   ```java
   BMSClient bmsClient = BMSClient.getInstance();
   bmsClient.initialize(getApplicationContext(), <region>);

   AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

   Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {

   @Override
   public void onSuccess (Response response) {
       Log.d("My app", "onSuccess :: " + response.getResponseText());
   }

   @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
       if (null != t) {
           Log.d("My app", "onFailure :: " + t.getMessage());
       } else if (null != extendedInfo) {
           Log.d("My app", "onFailure :: " + extendedInfo.toString());
       } else {
           Log.d("My app", "onFailure :: " + response.getResponseText());
           }
       }
   });
  ```
  {: codeblock}

</br>

### SDK を使用しない場合
{: #mobile-access-api-nosdk}

任意のライブラリーを使用して、`Authorization` 要求ヘッダーが `Bearer` 認証スキームを使用してアクセス・トークンを送信するように設定します。
要求フォーマットの例:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer <access token> <optional identity token>
  ```
  {: screen}

</br>
</br>

## 次のステップ
{: #mobile-next}

{{site.data.keyword.appid_short}} がアプリケーションにインストールされたので、ユーザーの認証を開始する準備がほぼ整いました。 次に、以下のいずれかの作業を行ってください。

* [ID プロバイダー](/docs/services/appid?topic=appid-social) の構成
* [ログイン・ウィジェット](/docs/services/appid?topic=appid-login-widget) のカスタマイズと構成
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android SDK<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> について学習します
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">iOS SDK<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> について学習します
