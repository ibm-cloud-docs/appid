---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# アプリへの {{site.data.keyword.appid_short}} の追加
{: #configuring}

このサービスをアプリケーション内にセットアップして {{site.data.keyword.appid_short}} の使用を開始します。
{: shortdesc}


## Android SDK のセットアップ
{: #android-setup}

{{site.data.keyword.appid_short}} Client SDK を使用して Android アプリを構築し、SDK を初期化し、ユーザーを認証し、保護リソースや無保護リソースへの要求を実行します。
{:shortdesc}


### 開始する前に
{: #before-android}

以下の情報が必要です。
  * {{site.data.keyword.appid_short_notm}} サービスのインスタンス。
  * テナント ID。 テナント ID は、アプリの初期化に使用される固有 ID であり、サービス・ダッシュボードの**「サービス資格情報」 ** タブで見つかります。
  * {{site.data.keyword.Bluemix}} 地域。 地域は UI に表示されています。 その値をアプリの初期化に使用します。
    <table><caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地域と対応する SDK 値</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 地域</th>
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

  * Gradle と連動して機能するようにセットアップされた <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio プロジェクト<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>。

### SDK のインストール
{: #install-android}

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

3. `build.gradle` ファイルの従属関係セクションを見つけて、{{site.data.keyword.appid_short_notm}} Client SDK 用のコンパイル従属関係を追加します。 **注**: プロジェクトの `build.gradle` ファイルではなくアプリのファイルを開いてください。

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
  ```
  {: codeblock}

5. `defaultConfig` セクションを見つけて、以下のコード行を追加します。

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. プロジェクトを Gradle と同期化します。 **「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**とクリックします。

### SDK の初期化
{: #initialize-android}

context、tenant ID、region パラメーターを initialize メソッドに渡して、Client SDK を初期化します。 初期化コードの配置場所として一般的な (必須ではありません) 場所は、Android アプリケーションのメイン・アクティビティーの onCreate メソッド内です。

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> 表. コマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> この値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。 </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> 地域は UI に示されています。 オプションは、`AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、 `AppID.REGION_Sydney`、または `AppID.REGION_Germany` です。 </td>
    </tr>
  </table>

これで、ID プロバイダーを構成し、ユーザーの認証を開始できるようになりました。詳細については、<a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub リポジトリー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。


</br>

## iOS Swift SDK のセットアップ
{: #ios-setup}

{{site.data.keyword.appid_short}} Client SDK を使用して Swift アプリケーションを構築し、SDK を初期化し、ユーザーを認証し、保護リソースや無保護リソースへの要求を実行します。
{:shortdesc}


### 開始する前に
{: #before-ios}

以下の情報が必要です。
  * {{site.data.keyword.appid_short_notm}} のインスタンス。
  * テナント ID。 テナント ID は、アプリの初期化に使用される固有 ID であり、サービス・ダッシュボードの**「サービス資格情報」 ** タブで見つかります。
  * {{site.data.keyword.Bluemix_notm}} 地域。
  地域は UI に表示されています。 その値をアプリの初期化に使用します。
  <table> <caption> 表. {{site.data.keyword.Bluemix_notm}} 地域と対応する SDK 値</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 地域</th>
      <th>SDK 値</th>
    </tr>
    <tr>
      <td>米国南部</td>
      <td><code>AppID.REGION_US_SOUTH </code></td>
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

  * Xcode プロジェクト (バージョン 9.0.1 以上)。
  * CocoaPods (バージョン 1.1.0 以上)。


### SDK のインストール
{: #install-ios}

{{site.data.keyword.appid_short_notm}} Client SDK には、Swift プロジェクトと Objective-C Cocoa プロジェクト用の従属関係マネージャーである CocoaPods が付属しています。 CocoaPods は成果物をダウンロードし、プロジェクトで使用できるようにします。

1. Xcode プロジェクトを作成するか、既存のプロジェクトを開きます。
2. プロジェクトのディレクトリー内の podfile を開くか、このディレクトリー内に podfile を作成します。
3. プロジェクトのターゲットに続いて、「IBMCloudAppID」ポッドおよび `use_frameworks!` コマンドの従属関係を追加します。

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. 「IBMCloudAppID」の従属関係をダウンロードします。

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Xcode プロジェクトのキーチェーン共有を有効にします。 **「Project Settings」>「Capabilities」>「Keychain Sharing」**に移動し、**「Enable keychain sharing」**を選択します。
7. **「Project Settings」>「Info」>「URL Types」**を開き、**「URL Type」**を追加します。 **「Identifier」**と**「URL Scheme」**の両方のテキスト・ボックスに以下の値を入力します。
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### SDK の初期化
{: #initialize-ios}

1. tenant ID パラメーターと region パラメーターを initialize メソッドに渡すことによって、Client SDK を初期化します。 初期化コードの配置場所として一般的な (必須ではありません) 場所は、Swift アプリケーションの AppDelegate の `application:didFinishLaunchingWithOptions` メソッド内です。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, region: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> 表. コマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> この値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。 </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> 地域は UI に示されています。 オプションは、`AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、 `AppID.REGION_Sydney`、または `AppID.REGION_Germany` です。</td>
    </tr>
  </table>

2. `AppDelegate` ファイルに以下のインポートを追加します。

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. 以下のコードを AppDelegate ファイルに追加します。

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

これで、ID プロバイダーを構成し、ユーザーの認証を開始できるようになりました。iOS SDK の詳細については、<a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub リポジトリー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。

</br>

## Node.js SDK のセットアップ
{: #nodejs-setup}

### 開始する前に
{: #before-nodejs}

以下の前提条件が整っていることを確認します。
1. [IBM Cloud CLI](../cli/index.html) をインストールします。
2. <a href="http://expressjs.com/" target="_blank">Express フレームワーク <img src="../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>を使用して Node.js サーバーを実装します。 Express フレームワークをインストールするには、コマンド・ラインを使用して、Node.js アプリのディレクトリーを開き、以下のコマンドを実行します。
  ```
  npm install --save express
  ```
  {: codeblock}
3. Passport をインストールする。 コマンド・ラインを使用して、Node.js アプリのディレクトリーを開き、以下のコマンドを実行します。
  ```
  npm install --save passport
  ```
  {: codeblock}

**注**: その他のフレームワークは `Express` フレームワーク (LoopBack など) を使用します。 {{site.data.keyword.appid_short_notm}} Server SDK は、それらのどのフレームワークでも使用できます。


### SDK のインストール
{: #install-nodejs}

1. コマンド・ラインを使用して、Node.js アプリのディレクトリーを開いてください。
2. {{site.data.keyword.appid_short_notm}} サービスをインストールします。
  ```
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### SDK の初期化
{: #initialize}

1. `server.js` ファイルに以下の `require` 定義を追加します。
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. express-session ミドルウェアを使用するように Express アプリをセットアップする。 **注**: ミドルウェアには、実稼働環境用の適切なセッション・ストレージを構成する必要があります。 詳細については、<a href="https://github.com/expressjs/session" target="_blank">expressjs の資料 <img src="../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
    ```
    const app = express();
    app.use(session({
        secret: "123456",
        resave: true,
        saveUninitialized: true
        }));
    app.use(passport.initialize());
    app.use(passport.session());
    ```
    {: codeblock}

3. テナント ID と資格情報を渡して、SDK を初期化します。
    ```
    passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
    ```
    {: codeblock}

 <table summary="コマンド・コンポーネント: Node.js アプリ">
  <caption>Node.js アプリのコマンドのコンポーネント</caption>
    <tr>
      <th>コンポーネント</th>
      <th>説明</th>
    </tr>
    <tr>
      <td><i> tenantID </i></td>
      <td>テナント ID は、アプリの初期化に使用される固有 ID です。 **「サービス資格情報」**タブで**「資格情報の表示」**をクリックして、{{site.data.keyword.appid_short_notm}} サービス・ダッシュボードで値を見つけることができます。</td>
    </tr>
    <tr>
      <td><i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td>これらの値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。</td>
    </tr>
    <tr><td><i>redirectUri</i></td>
    <td>redirectUri 値は、以下の 3 つの方法で指定できます。</br>
        1. 新しい WebAppStrategy({redirectUri: "...."}) 内に手動で</br>
        2. `redirectUri` という名前の環境変数として</br>
        3. 上記のいずれも指定されなかった場合、App ID SDK は IBM Cloud で稼働しているアプリケーションの application_uri の取得を試行して、デフォルトのサフィックス「/ibm/cloud/appid/callback」を追加します</td>
    </tr>
    <tr>
      <td><i> CALLBACK_URL </i></td>
      <td>ログイン後にユーザーに表示されるページの URL。</td>
    </tr>
  </table>

4. passport にシリアライゼーションとデシリアライゼーションを構成する。 この構成手順は、複数の HTTP 要求にわたって認証済みセッション・パーシスタンスを維持するために必要です。 詳細については、<a href="http://passportjs.org/docs" target="_blank">passport の資料 <img src="../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。

  ```
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. `server.js` ファイルに以下のコードを追加して、サービス・リダイレクトを発行します。
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get('/protected', passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **注**: サービスは、以下の順序でリダイレクトされます。
    1. `WebAppStrategy.ORIGINAL_URL` キーの下の HTTP セッションに永続する、認証プロセスを起動した要求の元の URL。
    2. 正常に実行されたリダイレクト (`passport.authenticate(name, {successRedirect: "...."})` で指定)。
    3. アプリケーションのルート (「/」)

6. アプリケーションを再デプロイします。

詳細については、<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}}Node.js GitHub リポジトリー <img src="../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。

## Swift SDK のセットアップ
{: #swift-setup}

{{site.data.keyword.appid_short}} サーバー SDK を使用して、バックエンドと API を保護します。
{:shortdesc}


### 開始する前に
{: #before-swift}

Swift SDK の作業を行う前に、以下の前提条件を満たす必要があります。

* MacOS または Linux のいずれか
* Linux では OpenSSL 1.0.2
* Swift 3.0.2 をインストールします
* Kitura 1.6 をインストールします


### SDK のインストール
{: #install-swift}

1. Swift アプリのディレクトリーにある `Package.swift` ファイルを開き、`appid-serversdk-swift` 従属関係を追加します。

  ```swift
  let package = Package(
      name: “myApp",
      dependencies: [
          .package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", .upToNextMinor(from: “4.0.0")),
      ],
      targets: [
          .target(
              name: "myApp",
              dependencies: ["IBMCloudAppID"]),
      ]
  )
  ```
  {: codeblock}

2. MacOS の場合: コマンド・ラインでビルドする場合、すべてのパッケージに次のフラグが含まれている必要があります。
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. Xcode プロジェクトを作成する場合は、次のコマンドを使用します。
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  openssl.xcconfig は <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> からコピーできます。
  {: tip}

4. 次の目的で、Swift アプリケーションに以下のコードを追加します。
    * session ミドルウェアを使用するように Kitura をセットアップする。 **注**: Kitura には、実稼働環境用の適切なセッション・ストレージを構成する必要があります。 詳細については、<a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura の資料 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
    * コールバック URL で GET コマンドを実行して、{{site.data.keyword.appid_short_notm}} サービスからアクセス・トークンと識別トークンを取得する。

    ```swift
    import Foundation
    import Kitura
    import KituraSession
    import Credentials
    import SwiftyJSON
    import IBMCloudAppID
    let router = Router()
    let session = Session(secret: "Some secret")
    router.all(middleware: session)
    let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()
    let kituraCredentials = Credentials()
    kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
    router.get(CALLBACK_URL,
      handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
        successRedirect: LANDING_PAGE_URL,
        failureRedirect: LANDING_PAGE_URL
        ))
    router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
    let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]
    guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
        response.status(.unauthorized)
          return next()
      }
      response.send(json: identityTokenPayload!)
      next()
      })
    ```
    {: codeblock}

5. アプリケーションを再デプロイします。

</br>

## Liberty for Java SDK のセットアップ
{: #lfj-setup}

{{site.data.keyword.appid_short_notm}} で、Liberty for Java Web アプリケーションを操作するための構成を行います。
{:shortdesc}

1. <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect 機能 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を `server.xml` に追加します。

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. Open ID Connect Client 機能で以下のプレースホルダーを定義します。 プレースホルダーの値は、後で {{site.data.keyword.Bluemix_notm}} によって自動的に設定されます。 インスタンス名の変数は、{{site.data.keyword.appid_short_notm}} インスタンスの名前と一致していなければなりません。

  ```
  clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
  clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
  authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
  tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
  jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
  issuerIdentifier='appid-oauth.ng.bluemix.net'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  ```
  {: codeblock}

  **注**: issuerIdentifier 変数は、地域によって変わります。 以下のいずれかの変数になります。
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. 保護リソースを指定するための許可フィルターを定義します。 フィルターを<a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">定義 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> しない場合は、サービスによってすべてのリソースが保護されます。
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

4. `server.xml` ファイルで、特殊対象タイプを ALL_AUTHENTICATED_USERS として定義します。

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample"
  location="${server.config.dir}/apps/libertySample-1.0.0.war">
    <application-bnd>
        <security-role name="myrole">
        <special-subject type="ALL_AUTHENTICATED_USERS"/>
        </security-role>
            </application-bnd>
        </application>
  ```
  {: codeblock}

5. `<application-bnd>` 要素で、Web アプリケーションの `web.xml` のとおりに<a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">役割を定義します <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>。

  ```xml
  <security-role>
  <role-name>myrole</role-name>
  </security-role>

  <security-constraint>
  <web-resource-collection>
  <web-resource-name>ProtectedServlet</web-resource-name>
  <url-pattern>/ProtectedServlet/*</url-pattern>
  <http-method>GET</http-method>
  <http-method>PUT</http-method>
  <http-method>POST</http-method>
  <http-method>DELETE</http-method>
  </web-resource-collection>

  <auth-constraint>
  <role-name>myrole</role-name>
  </auth-constraint>
  <user-data-constraint>
  <transport-guarantee>NONE</transport-guarantee>
  </user-data-constraint>
  </security-constraint>
  ```
  {: codeblock}

6. 証明書を取得します。

    a. {{site.data.keyword.appid_short_notm}} ダッシュボードで「サービス資格情報」をクリックします。

    b. **「資格情報の表示」**をクリックして、`oauthServerUrl` をコピーします。

    c. URL に `/token` を追加します。 Firefox で出力の URL を参照して、証明書を取得します。 例えば、以下のような URL を使用できます。

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Firefox のアドレス・バーで、錠のアイコン > **右矢印** > **「詳細を表示」** > **「証明書を表示」**をクリックします。

    e. **「セキュリティー」**タブで**「証明書を表示」** > **「詳細」**をクリックします。

    f. 証明書をエクスポートして、ローカル・ドライブに PEM ファイルとして保存します。

7. 証明書を Liberty for Java の truststore.jks ファイルに追加します。そのために、<a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用し、証明書別名への参照を OIDC 要素に追加してください。 `.jks ファイル`は、サーバー・ディレクトリー (**resources** > **security** > **<i>トラストストア・ファイル名</i>** > **`.jks ファイル`**) にあります。 以下のいずれかのオプションを使用して、証明書をファイルに追加できます。

    * 端末で Liberty for Java セキュリティー・フォルダー (wlp > usr > servers > <i>サーバー名</i> > resources > security) に移動し、以下のコマンドを使用して証明書を追加します。

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **注**: `~/Documents/[certificatename].cer` は、ご使用のローカル・ドライブ上のファイルの場所です。

    * <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して証明書を追加します。 KeyStore Explorer を開いて、**「Open an existing KeyStore」**を選択します。

    **注**: 証明書が期限切れまたは変更になっている可能性があります。この場合、新しい証明書によってトラストストアを更新する必要があります。

8. `manifest.yml` ファイルで {{site.data.keyword.appid_short_notm}} インスタンスを定義します。

  ```yml
  services:
  - <appid service name>

  Manifest.yml file example:
  applications:
  - name: LibertyExampl
  buildpack: liberty-for-java
  instances: 1
  random-route: true
  memory: 512M
  disk_quota: 1024M
  timeout: 180
  services:
  - AppID-Instance-Name
  ```
  {: codeblock}

    {{site.data.keyword.appid_short_notm}} に合わせて構成した `server.xml` ファイルのサンプルを以下に示します。

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <server description="sample server">
      <featureManager>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>  
      </featureManager>
      <openidConnectClient id="MyDefaultRP"
         clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
         clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
         authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
         tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
         jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
         issuerIdentifier='${cloud.services.AppID-Instance-Name.credentials.appid-oauth.ng.bluemix.net}'
         tokenEndpointAuthMethod="basic"
         signatureAlgorithm="RS256"
         authFilterid="myAuthFilter"/>
      <authFilter id="myAuthFilter">
               <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
      </authFilter>
      <application type="war" id="ProtectedServlet" context-root="/appidSample" location="${server.config.dir}/apps/libertySample-1.0.0.war">
          <application-bnd>
              <security-role name="myrole">
                  <special-subject type="ALL_AUTHENTICATED_USERS" />
              </security-role>
          </application-bnd>
      </application>
   <applicationManager autoExpand="true"/>
  <keyStore id="defaultKeyStore" password="Password"/>
  <keyStore id="defaulttrustore" password="Liberty" location="<FileContainingCertificated>.jks"/>
  <ssl id="defaultSSLSettings" keyStoreRef="defaultKeyStore" trustStoreRef="defaulttrustore"/>
  <sslDefault sslRef="defaultSSLSettings"/>
      <httpEndpoint id="defaultHttpEndpoint" httpPort="9080" host="*" httpsPort="9443" />
      <applicationManager autoExpand="true"/>
  </server>
  ```
  {: codeblock}



</br>

## {{site.data.keyword.Bluemix_notm}} 上で実行されない既存のアプリケーションへの {{site.data.keyword.appid_short_notm}} の追加
{: #existing}

{{site.data.keyword.appid_short_notm}} を、{{site.data.keyword.Bluemix_notm}} 上で稼働しないアプリケーションに追加できます。 このトピックにはいくつかの例が示されていますが、これらの例にある言語だけがこのサービスを使用できるということではありません。

</br>

**Node.js**

Node.js アプリでは、`passport.use(new WebAppStrategy());` を以下のコードに置き換えます。

  ```
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: codeblock}

  <table>
  <caption> 表. Node.js アプリのコマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> これらの値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。 </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>アプリケーションの URL。</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> ログイン後にユーザーに表示されるページの URL。 </td>
    </tr>
  </table>

</br>

**Swift**

Swift アプリでは、`let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` を以下のコードに置き換えます。

  ```swift
  let options = [
        "clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
    let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  ```
  {: codeblock}

  <table>
  <caption>表. Swift アプリのコマンドのコンポーネントの説明</caption>
    <tr>
      <th> コンポーネント </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> これらの値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。 </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>アプリケーションの URL。</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> ログイン後にユーザーに表示されるページの URL。 </td>
    </tr>
  </table>


</br>

**Liberty for Java**

Liberty for Java アプリで、[Liberty for Java SDK のセットアップ](#lfj-setup)の手順を実行します。ただし、OIDC クライアント要素変数を以下のコードに置き換えてください。

  ```
  clientId='App ID client_ID'
  clientSecret='App Id Secret'      
  authorizationEndpointUrl='oauthServerUrl/authorization'       
  tokenEndpointUrl='oauthServerUrl/token'
  jwkEndpointUrl='oauthServerUrl/publickeys'
  issuerIdentifier='Changed according to the region'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  trustAliasName="my.bluemix.certificate"
  ```
  {: codeblock}

  <table>
  <caption>表. Liberty for Java アプリケーションの OIDC 要素変数</caption>
    <tr>
      <th> コンポーネント </th>
      <th> 説明 </th>
    </tr>
    <tr>
    <td><code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
    <td>これらの値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td>
      <td> oauthServerURL の最後に `/authorization` を追加します。</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td>
      <td>oauthServerURL の最後に `/token` を追加します。</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td>
      <td>oauthServerURL の最後に `/publickeys` を追加します。</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td>
      <td>地域によって変わります。 以下の値のいずれかです。 </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td>
      <td>"basic" を指定します。</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td>
      <td>"RS256" を指定します。</td>
    </tr>
    <tr>
      <td><code> authFilterid </code></td>
      <td>保護するリソースのリスト。</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td>
      <td>トラストストア内の証明書の名前。</td>
    </tr>
  </table>
