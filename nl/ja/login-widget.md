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

# サインイン操作環境の管理

ログイン・ウィジェットによって、ソース・コードの追加、削除、変更を行わずに、いつでもサインイン・フローを更新できます。サンプル・アプリとして用意されているコードを使用して、数分で稼働させることができます。
{: shortdesc}

**注**: Facebook などのソーシャル ID プロバイダーを構成した場合は、[Oauth2 許可付与フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)によってログイン・ウィジェットが呼び出されます。

</br>

## サンプル・アプリのコードのカスタマイズ
{: #login-widget}

自分で選択したロゴや色が表示されるように、事前構成されたサインイン画面をカスタマイズすることができます。独自にブランド化した UI を表示する場合は、[クラウド・ディレクトリー](/docs/services/appid/cloud-directory.html)を参照してください。
{: shortdesc}

![カスタマイズしたサインイン操作環境の例](/images/customize.gif)

画面をカスタマイズするには、以下のようにします。

1. {{site.data.keyword.appid_short_notm}} サービス・ダッシュボードを開きます。
2. **「ログインのカスタマイズ (Login Customization)」**セクションを選択します。ここで、ログイン・ウィジェットの外観を企業のブランドに合うように変更できます。
3. ローカル・システムにある PNG ファイルまたは JPG ファイルを選択し、企業のロゴをアップロードします。 推奨される画像サイズは 320 x 320 ピクセルです。 ファイルの最大サイズは 100 KB です。
4. ウィジェットのヘッダー・カラーをカラー・ピッカーから選択するか、または別のカラーの 16 進コードを入力します。
5. プレビュー・ペインでカスタマイズを検査し、問題がなければ**「変更を保存」**をクリックします。 確認メッセージが表示されます。
6. アプリにアクセスして、変更内容を確認します。アプリを再ビルドする必要はありません。画像は {{site.data.keyword.appid_short}} データベースに保管されて、ログイン・ウィジェットが次に呼び出されたときに表示されます。


</br>

## Android SDK を使用したログイン・ウィジェットの呼び出し
{: #android}

ソーシャル ID プロバイダーを有効にした場合は、事前構成されたサインイン画面を Android SDK で呼び出せます。
{: shortdesc}

1. ID プロバイダーを構成します。
2. 以下のコマンドをコードに挿入します。
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


</br>

## iOS Swift SDK を使用したログイン・ウィジェットの呼び出し
{: ios-swift}

ソーシャル ID プロバイダーを有効にした場合は、事前構成されたサインイン画面を iOS Swift SDK で呼び出せます。
{: shortdesc}

1. ID プロバイダーを構成します。
2. アプリのコードに以下のコマンドを追加します。
  ```swift
  import BluemixAppID
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


</br>

## Node.js SDK を使用したログイン・ウィジェットの呼び出し
{: #nodejs}

ソーシャル ID プロバイダーを有効にした場合は、事前構成されたサインイン画面を Node.js SDK で呼び出せます。
{: shortdesc}

1. ID プロバイダーを構成します。
2. 以下のコマンドをコードに追加します。
    ```JavaScript

    var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
    ```
    {: codeblock}


</br>

## Swift SDK でログイン・ウィジェットを呼び出しています。
{: #swift}

ソーシャル ID プロバイダーを有効にした場合は、事前構成されたサインイン画面を Swift SDK で呼び出せます。
{: shortdesc}

WebAppKituraCredentialsPlugin は、OAuth2 の許可コードの認可フローに基づくものであり、ブラウザーを使用する Web アプリケーションで使用する必要があります。このプラグインには、認証フローと許可フローを実装するためのツールが用意されています。 プラグインはまた、保護リソースに対する非認証のアクセス試行を検出し、ユーザーのブラウザーを認証ページに自動的にリダイレクトするメカニズムも備えています。 認証に成功すると、ユーザーは Web アプリケーションのコールバック URL に送られ、この URL がプラグインを使用して {{site.data.keyword.appid_short_notm}} からアクセス・トークンと識別トークンを取得します。それらのトークンを取得すると、プラグインは HTTP セッションの WebAppKituraCredentialsPlugin.AuthContext の下に保管します。

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
