---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 既存のアプリへの {{site.data.keyword.appid_short_notm}} の追加

既存のアプリケーションで {{site.data.keyword.appid_full}} を使用して、認証を行い、ユーザーに関するプロファイル情報を保管できます。


## 前提条件

* 既存の iOS Swift、Android、Node.js、または Swift アプリケーション。
* {{site.data.keyword.appid_short_notm}} の既存のインスタンス。


## 既存の Android アプリへの {{site.data.keyword.appid_short_notm}} の追加

既存の Android アプリケーションに App ID サービスを追加できます。

1. JitPack リポジトリーをルートの build.gradle ファイルに追加します。

  ```gradle
  allprojects {
      		repositories {
		    ...
         	 maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: pre}

2. アプリケーションの build.gradle ファイルを開き、ファイルの従属関係セクションを見つけて、{{site.data.keyword.appid_short_notm}} Client SDK 用のコンパイル従属関係を追加します。

  ```gradle
dependencies { 
compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: pre}

3. defaultConfig セクションを見つけて、以下のコード行を追加します。

  ```gradle
defaultConfig {
...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. プロジェクトを Gradle と同期化します。
5. context、tenant ID、region パラメーターを initialize メソッドに渡して、Client SDK を初期化します。初期化コードの配置場所として一般的な (必須ではありません) 場所は、Android アプリケーションのメイン・アクティビティーの onCreate メソッド内です。

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> 表 1. コマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント</th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> この値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。</td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> 地域は UI に示されています。オプションは、`AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、または `AppID.REGION_Sydney` です。</td>
    </tr>
  </table>

6. {{site.data.keyword.appid_short_notm}} Client SDK が初期化されたら、ログイン・ウィジェットを実行してユーザーを認証できるようになります。

  ```Java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

          @Override
          public void onAuthorizationCanceled () {
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
        });
  ```
  {: pre}

  <table>
  <caption> 表 2. コマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント</th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> 例外が発生しました。</td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> 認証プロセスは、ユーザーによって取り消されました。</td>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> ユーザーは認証されました。</td>
    </tr>
  </table>

## 既存の iOS アプリへの {{site.data.keyword.appid_short_notm}} の追加

1. プロジェクトのディレクトリー内の podfile を開きます。
2. プロジェクトのターゲットの下に、「BluemixAppID」Pod の従属関係を追加します。必ず、`use_frameworks!` コマンドもターゲットの下に置いてください。
3. `BluemixAppID` の従属関係をダウンロードするには、以下のコマンドを実行します。

  ```
  pod install --repo-update
  ```
  {: pre}

4. Xcode プロジェクトを開き、キーチェーン共有を使用可能にします。**「Project Settings」**の下で、**「Capabilities」** > **「Keychain Sharing」**をクリックします。
5. **「Project Settings」** > **「Info」** > **「URL Types」**の下で、**「URL Type」**を追加します。**「Identifier」**テキスト・ボックスと**「URL Scheme」**テキスト・ボックスの両方に、以下の値を入力します。

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. AppDelegate.swift ファイルに、以下のインポートを追加します。

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. tenant ID パラメーターと region パラメーターを initialize メソッドに渡して、Client SDK を初期化します。初期化コードを入れる一般的な場所 (ただし、これは必須ではありません) は、アプリケーションの AppDelegate の application:didFinishLaunchingWithOptions: メソッド内です。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> 表 3. コマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント</th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> この値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。</td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> 地域は UI に示されています。オプションは、`AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、または `AppID.REGION_Sydney` です。</td>
    </tr>
  </table>

8. 以下のコードを AppDelegate ファイルに追加します。

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
         	return AppID.sharedInstance.application(application, open: url, options: options)
      }
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
     }

     public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}
  <table>
  <caption> 表 4. コマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント</th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> ユーザーは認証されました。</td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> 認証プロセスは、ユーザーによって取り消されました。</td>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> 例外が発生しました。</td>
    </tr>
  </table>

## 既存の Node.js Web アプリへの {{site.data.keyword.appid_short_notm}} の追加

1. Node.js アプリケーションに `bluemix-appid` モジュールを追加します。

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. まだインストールしていない場合、以下のモジュールをインストールします。

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. 次の目的で、app.js ファイルに以下のコードを追加します。
    * express-session ミドルウェアを使用するように Express アプリをセットアップする。**注**: ミドルウェアには、実稼働環境用の適切なセッション・ストレージを構成する必要があります。詳細については、[expressjs 資料](https://github.com/expressjs/session)を参照してください。
    * passportjs にシリアライゼーションとデシリアライゼーションを構成する。これは、複数の HTTP 要求にわたって認証済みセッション・パーシスタンスを維持するために必要です。詳細については、[passportjs 資料](http://passportjs.org/docs)を参照してください。
    * コールバック URL 上で GET コマンドを実行して、App ID サービスからアクセス・トークンと識別トークンを取得する。

  ```javaScript
  const express = require("express");
  const session = require("express-session");
  const passport = require("passport");
  const WebAppStrategy = require("bluemix-appid").WebAppStrategy;
  const app = express();
  const CALLBACK_URL = "/ibm/bluemix/appid/callback";
  app.use(session({
      secret: "123456",
      resave: true,
      saveUninitialized: true
    }));
  app.use(passport.initialize());
    app.use(passport.session());

    passport.use(new WebAppStrategy());
  passport.serializeUser(function(user, cb) {
      cb(null, user);
    });

    passport.deserializeUser(function(obj, cb) {
      cb(null, obj);
    });
  app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res)
    		res.json(req.user);
    });
  ```
  {: pre}

    **注**: サービスは、以下の順序でリダイレクトされます。
    1. `WebAppStrategy.ORIGINAL_URL` キーの下の HTTP セッションに永続する、認証プロセスを起動した要求の元の URL。
    2. 正常に実行されたリダイレクト (`passport.authenticate(name, {successRedirect: "...."})` で指定)。
    3. アプリケーションのルート (「/」)

4. アプリケーションを再デプロイします。


## 既存の Swift Web アプリケーションへの {{site.data.keyword.appid_short_notm}} の追加

1. Swift アプリのディレクトリーにある `Package.swift` ファイルを開き、`appid-serversdk-swift` 従属関係を追加します。以下に例を示します。

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
    ```
    {: pre}

2. 次の目的で、Swift アプリケーションに以下のコードを追加します。
    * session ミドルウェアを使用するように Kitura をセットアップする。**注**: Kitura には、実稼働環境用の適切なセッション・ストレージを構成する必要があります。詳細については、[Kitura 資料](https://github.com/IBM-Swift/Kitura-Session)を参照してください。
    * コールバック URL 上で GET コマンドを実行して、App ID サービスからアクセス・トークンと識別トークンを取得する。

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID
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
  {: pre}

  <table>
  <caption> 表 6. コマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント</th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> var CALLBACK_URL </i> </td>
      <td> /ibm/bluemix/appid/callback </td>
    </tr>
    <tr>
      <td> <i> var LANDING_PAGE_URL </i> </td>
      <td> /index.html </td>
    </tr>
    </table>

5. アプリケーションを再デプロイします。



## {{site.data.keyword.Bluemix_notm}} 上で実行されない既存のアプリケーションへの {{site.data.keyword.appid_short_notm}} の追加


Bluemix 上で実行されない Node.js または Swift のアプリケーションがある場合、リモート側から作業するように WebAppStrategy または WebAppKituraCredentialsPlugin を構成できます。


Node.js アプリでは、`passport.use(new WebAppStrategy());` を以下のコードに置き換えます。

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
{: pre}

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
  {: pre}

<table>
<caption> 表 7. Swift アプリと Node.js アプリ用のコマンドのコンポーネントの説明 </caption>
  <tr>
    <th> コンポーネント</th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> これらの値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。</td>
  </tr>
  <tr>
    <td> <i> app-url </i> </td>
    <td> アプリケーションの URL。</td>
  </tr>
  <tr>
    <td> <i> CALLBACK_URL </i> </td>
    <td> ログイン後にユーザーに表示されるページの URL。</td>
  </tr>
</table>
