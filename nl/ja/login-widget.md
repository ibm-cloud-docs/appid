---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# ログイン操作環境の管理
ログイン・ウィジェットを使用して、サインインの流れを数分間で準備できます。サインイン・ソース・コードの追加、削除、変更を行わずに、いつでもウィジェットまたはテーマを更新できます。
{: shortdesc}



## ログイン・ウィジェットのカスタマイズ
{: #login-widget}

自分で選択したロゴや色が表示されるように、ログイン・ウィジェットを構成することができます。
{: shortdesc}

{{site.data.keyword.appid_short}} サービスに 2 つ以上の ID プロバイダーを構成した場合、ユーザーはログイン・ウィジェットで ID プロバイダーを選択できます。 ログイン・ウィジェットをカスタマイズする手順は、次のとおりです。

1. {{site.data.keyword.appid_short_notm}} サービス・ダッシュボードを開きます。
2. **「ログインのカスタマイズ (Login Customization)」**セクションを選択します。ここで、ログイン・ウィジェットの外観を企業のブランドに合うように変更できます。
3. ローカル・システムにある PNG ファイルまたは JPG ファイルを選択し、企業のロゴをアップロードします。 推奨される画像サイズは 320 x 320 ピクセルです。 ファイルの最大サイズは 100 KB です。
4. ウィジェットのヘッダー・カラーをカラー・ピッカーから選択するか、または別のカラーの 16 進コードを入力します。
5. プレビュー・ペインでカスタマイズを検査し、問題がなければ**「変更を保存」**をクリックします。 確認メッセージが表示されます。

**注**: アプリケーションを再ビルドする必要はありません。 画像が {{site.data.keyword.appid_short}} データベースに保管され、次回のログイン時に表示されます。

## Android SDK を使用したログイン・ウィジェットの実行
{: #authenticate-android}

複数の ID プロバイダーを構成している場合、ユーザーには、アプリへのアクセス時にログイン・ウィジェットが表示されます。1 つしか構成していない場合、デフォルトでは、ユーザーは構成済みの ID プロバイダー認証画面にリダイレクトされます。


{{site.data.keyword.appid_short_notm}} Client SDK が初期化されたら、ログイン・ウィジェットを実行してユーザーを認証できるようになります。

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //例外の発生
        }

        @Override
        public void onAuthorizationCanceled () {
          //ユーザーによる認証の取り消し
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //ユーザーの認証
        }
      });
  ```
  {: codeblock}

## iOS SDK を使用したログイン・ウィジェットの実行
{: #authenticate-ios}

複数の ID プロバイダーを構成している場合、ユーザーには、アプリへのアクセス時にログイン・ウィジェットが表示されます。1 つしか構成していない場合、デフォルトでは、ユーザーは構成済みの ID プロバイダー認証画面にリダイレクトされます。


1. SDK を使用するファイルに以下のインポートを追加します。

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. 以下のコマンドを実行してウィジェットを起動します。

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //ユーザーの認証
      }

      public func onAuthorizationCanceled() {
          //ユーザーによる認証の取り消し
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //例外の発生
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

## Node.js SDK を使用したログイン・ウィジェットの実行
{: #authenticate-nodejs}

`WebAppStrategy` を使用して Web アプリケーション・リソースを保護できます。

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {: codeblock}


## Swift SDK を使用したログイン・ウィジェットの実行
{: #authenticate-swift}

WebAppKituraCredentialsPlugin は、OAuth2 の authorization_code 認可フローに基づくものであり、ブラウザーを使用する Web アプリケーションで使用する必要があります。 このプラグインには、認証フローと許可フローを実装するためのツールが用意されています。 プラグインはまた、保護リソースに対する非認証のアクセス試行を検出し、ユーザーのブラウザーを認証ページに自動的にリダイレクトするメカニズムも備えています。 認証に成功すると、ユーザーは Web アプリケーションのコールバック URL に送られ、この URL がプラグインを使用して {{site.data.keyword.appid_short_notm}} からアクセス・トークンと識別トークンを取得します。 それらのトークンを取得すると、プラグインはそれらを WebAppKituraCredentialsPlugin.AuthContext の下の HTTP セッションに保管します。

以下のコードは、WebAppKituraCredentialsPlugin を Kitura アプリケーションで使用して `/protected` エンドポイントを保護する方法を示しています。

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // The following URLs will be used for AppID OAuth flows
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Setup Kitura to use session middleware
  // Must be configured with proper session storage for production
  // environments. See https://github.com/IBM-Swift/Kitura-Session for
  // additional documentation
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)

  let options = [
  	"clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)

  // Explicit login endpoint
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback to finish the authorization process. Will retrieve access and identity tokens from AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Logout endpoint. Clears authentication information from session
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Protected area
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
  var port = 3000
  if let portString = ProcessInfo.processInfo.environment["PORT"]{
      port = Int(portString)!
  }
  print("Starting on \(port)")

  // Add an HTTP server and connect it to the router
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start the Kitura runloop (this call never returns)
  Kitura.run()
  ```
  {: codeblock}
