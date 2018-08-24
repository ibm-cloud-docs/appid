---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="blank"}
{:shortdesc: .shortdesc}


# デフォルト画面の表示
{: #default}

{{site.data.keyword.appid_full}} に用意されているログイン・ウィジェットを使用して、ユーザーに機密保護機能のあるサインイン・オプションを提供できます。
{: shortdesc}

ID プロバイダーを使用するようにアプリが構成されている場合、アプリへの訪問者はログイン・ウィジェットによってサインイン画面に誘導されます。 デフォルトでは、1 つのプロバイダーのみが**オン**に設定されている場合、訪問者はその ID プロバイダーの認証画面にリダイレクトされます。 ログイン・ウィジェットを使用してデフォルトのサインイン画面を表示することができます。あるいは、クラウド・ディレクトリーを使用して既存の UI を再利用することができます。 そして、さらに、サインイン・フローは、ソース・コードを変更せずにいつでも更新することができます。


このサービスは OAuth 2 付与タイプを使用して許可プロセスをマップします。 Facebook などのソーシャル ID プロバイダーを構成した場合は、[Oauth2 許可付与フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)によってログイン・ウィジェットが呼び出されます。

アプリに固有の操作環境を作成しますか? [自分の画面を起動](/docs/services/appid/branded.html)できます。
{: tip}


## デフォルトのサインイン画面のカスタマイズ
{: #login-widget}

自分で選択したロゴや色が表示されるように、事前構成されたサインイン画面をカスタマイズすることができます。
{: shortdesc}

画面をカスタマイズするには、以下のようにします。

1. {{site.data.keyword.appid_short_notm}} サービス・ダッシュボードを開きます。
2. **「ログインのカスタマイズ」**セクションを選択します。 ログイン・ウィジェットの外観を自社のブランドに合うように変更できます。
3. ローカル・システムにある PNG ファイルまたは JPG ファイルを選択し、自社のロゴをアップロードします。 推奨される画像サイズは 320 x 320 ピクセルです。 ファイルの最大サイズは 100 KB です。
4. ウィジェットのヘッダー・カラーをカラー・ピッカーから選択するか、または別のカラーの 16 進コードを入力します。
5. プレビュー・ペインでカスタマイズを検査し、問題がなければ**「変更を保存」**をクリックします。 確認メッセージが表示されます。
6. ブラウザーでログイン・ページを最新表示し、変更内容を確認します。


## 表示する画面の計画
{: #plan}

{{site.data.keyword.appid_short_notm}} にはデフォルトのログイン画面が用意されており、表示する独自の UI 画面がない場合に呼び出すことができます。
{: shortdesc}

表示できる画面は、ID プロバイダーの構成によって異なります。 このサービスでは、ソーシャル ID プロバイダーの拡張機能は提供していません。ユーザー・アカウント情報へのアクセス権限がないためです。 ユーザーが情報を管理する場合は、自分で ID プロバイダーにアクセスする必要があります。 例えば、Facebook のパスワードを変更する場合は、www.facebook.com にアクセスする必要があります。

以下の表を参照して、ID プロバイダーのタイプごとに表示できる画面を確認してください。

<table>
  <thead>
    <tr>
      <th>表示画面</th>
      <th>ソーシャル ID プロバイダー</th>
      <th>エンタープライズ ID プロバイダー</th>
      <th>クラウド・ディレクトリー</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>サインイン</td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>登録</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>パスワードを忘れた場合</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>パスワードの変更</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>アカウントの詳細</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="フィーチャーを使用可能" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

[ソーシャル ID プロバイダー](/docs/services/appid/identity-providers.html)および[クラウド・ディレクトリー](/docs/services/appid/cloud-directory.html)の設定を構成したら、以下の画像の中から選択した言語をクリックし、コードの実装を開始します。


提供されている SDK または API の 1 つを使用するには、そのイメージをクリックします。App ID の利点は他の言語でも活用できることを忘れないでください。これらの API を使用すると、任意のアプリにクラウド・ディレクトリーをセットアップできます。イメージ内にリストされていない言語に関するヘルプは、<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">ブログ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
{: shortdesc}

</br>

## Android SDK を使用したデフォルト画面の表示
{: #android}

Android SDK を使用して、事前構成された画面を呼び出すことができます。
{: shortdesc}

</br>

**サインイン**
1. 以下のコマンドをコードに挿入します。
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
            //ユーザーの認証
        }
        });
    ```
  {: pre}

</br>
**登録**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。
2. LoginWidget を呼び出して登録フローを開始します。
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
  		 @Override
  		 public void onAuthorizationFailure (AuthorizationException exception) {
  		 }

  		 @Override
  		 public void onAuthorizationCanceled () {
  		 }

  		 @Override
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: pre}

</br>
**パスワードを忘れた場合**

1. クラウド・ディレクトリーの設定で**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**と**「パスワードを忘れた場合の E メール (Forgot password email)」**を必ず**「オン (On)」**に設定します。
2. LoginWidget を呼び出してパスワード忘れフローを開始します。
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
   			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
        public void onAuthorizationCanceled () {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
    ```
    {: pre}

</br>
**アカウントの詳細**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。
2. LoginWidget を呼び出して詳細変更フローを開始します。
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  			 }

  			 @Override
  			 public void onAuthorizationCanceled () {
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 }
  		 });
   ```
   {: pre}

</br>
**パスワードの変更**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定してください。
2. LoginWidget を呼び出してパスワード変更フローを開始します。
   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
   			 public void onAuthorizationCanceled () {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
   ```
   {: pre}
</br>
</br>

## iOS Swift SDK を使用したデフォルト画面の表示
{: #ios-swift}

iOS Swift SDK を使用して、事前構成された画面を呼び出すことができます。
{: shortdesc}

</br>
**サインイン**

1. 以下のコマンドをコードに挿入します。
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
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
  {: pre}


</br>
**登録**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定してください。
2. LoginWidget を呼び出して登録フローを開始します。
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       if accessToken == nil && identityToken == nil {
        //E メール検証が必要
        return
       }
     //ユーザーの認証
      }

      public func onAuthorizationCanceled() {
        //ユーザーによる登録キャンセル
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //例外の発生
      }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: pre}

</br>
**パスワードを忘れた場合**

1. クラウド・ディレクトリーの設定で**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**と**「パスワードを忘れた場合の E メール (Forgot password email)」**を必ず**「オン (On)」**に設定します。
2. LoginWidget を呼び出してパスワード忘れフローを開始します。
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
        //パスワード忘れ処理の終了。この場合 accessToken と identityToken はヌル。
     }

     public func onAuthorizationCanceled() {
         //ユーザーによるパスワード忘れ処理キャンセル
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //例外の発生
      }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: pre}

</br>
**アカウントの詳細**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。
2. LoginWidget を呼び出して詳細変更フローを開始します。
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>
**パスワードの変更**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。
2. LoginWidget を呼び出してパスワード変更フローを開始します。
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}
</br>
</br>

## Node.js SDK を使用したデフォルト画面の表示
{: #nodejs}

Node.js SDK を使用して、事前構成された画面を呼び出すことができます。
{: shortdesc}

</br>
**サインイン**
1. ID プロバイダー設定でクラウド・ディレクトリーを**「オン (On)」**に設定して、コールバック・エンドポイントを指定します。
2. ユーザー名とパスワードのパラメーターを使用して呼び出せる post ルートをアプリに追加し、リソース所有者のパスワードを使用してログインします。
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // フラッシュ・メッセージの許可
  }));
    ```
    {: pre}
    `WebAppStrategy` により、ユーザーはユーザー名とパスワードを使用して Web アプリにサインインできます。 ログインに成功すると、ユーザーのアクセス・トークンは HTTP セッションに保管され、セッション中に使用できるようになります。 HTTP セッションが破棄されるか期限切れになると、トークンは無効になります。
    {: tip}

</br>
**登録**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。 「いいえ (no)」に設定した場合、プロセスはアクセス・トークンと識別トークンを取得せずに終了します。
2. WebAppStrategy に `show` プロパティーを渡し、それを `WebAppStrategy.SIGN_UP` に設定します。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**パスワードを忘れた場合**

1. クラウド・ディレクトリーの設定で**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**と**「パスワードを忘れた場合の E メール (Forgot password email)」**を**「オン (ON)」**に設定します。 「いいえ (no)」に設定した場合、プロセスはアクセス・トークンと識別トークンを取得せずに終了します。
2. WebAppStrategy に `show` プロパティーを渡し、それを `WebAppStrategy.FORGOT_PASSWORD` に設定します。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>
**アカウントの詳細**
1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。
2. WebAppStrategy に `show` プロパティーを渡し、それを `WebAppStrategy.CHANGE_DETAILS` に設定します。
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>
**パスワードの変更**
1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。
2. WebAppStrategy に `show` プロパティーを渡し、それを `WebAppStrategy.CHANGE_PASSWORD` に設定します。
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: pre}

</br>
</br>

## Swift SDK を使用したデフォルト画面の表示
{: #swift}

ソーシャル ID プロバイダーを有効にした場合は、事前構成されたサインイン画面を Swift SDK で呼び出せます。
{: shortdesc}

1. 以下のコードは、WebAppKituraCredentialsPlugin を Kitura アプリで使用して `/protected` エンドポイントを保護する方法を示しています。

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
</br>
</br>



