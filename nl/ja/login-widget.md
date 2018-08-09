---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# サインイン操作環境の管理

{{site.data.keyword.appid_full}} に用意されているログイン・ウィジェットを使用して、ユーザーに機密保護機能のあるサインイン・オプションを提供できます。
{: shortdesc}

ID プロバイダーを使用するようにアプリが構成されている場合、アプリへの訪問者はログイン・ウィジェットによってサインイン画面に誘導されます。デフォルトでは、1 つのプロバイダーのみがオンに設定されている場合、訪問者はその ID プロバイダーの認証画面にリダイレクトされます。ログイン・ウィジェットを使用してデフォルトのサインイン画面を表示することができます。あるいは、クラウド・ディレクトリーを使用して既存の UI を再利用することができます。

サインイン・フローは、ソース・コードを変更せずにいつでも更新することができます。
{: tip}

このサービスは OAuth 2 付与タイプを使用して許可プロセスをマップします。Facebook などのソーシャル ID プロバイダーを構成した場合は、[Oauth2 許可付与フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)によってログイン・ウィジェットが呼び出されます。独自の UI 画面を表示する場合は、[リソース所有者のパスワード資格情報フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)を使用してログインし、アクセス・トークンと識別トークンを取得できます。


## デフォルトのサインイン画面のカスタマイズ
{: #login-widget}

自分で選択したロゴや色が表示されるように、事前構成されたサインイン画面をカスタマイズすることができます。
{: shortdesc}

画面をカスタマイズするには、以下のようにします。

1. {{site.data.keyword.appid_short_notm}} サービス・ダッシュボードを開きます。
2. **「ログインのカスタマイズ」**セクションを選択します。ログイン・ウィジェットの外観を企業のブランドに合うように変更できます。
3. ローカル・システムにある PNG ファイルまたは JPG ファイルを選択し、企業のロゴをアップロードします。 推奨される画像サイズは 320 x 320 ピクセルです。 ファイルの最大サイズは 100 KB です。
4. ウィジェットのヘッダー・カラーをカラー・ピッカーから選択するか、または別のカラーの 16 進コードを入力します。
5. プレビュー・ペインでカスタマイズを検査し、問題がなければ**「変更を保存」**をクリックします。 確認メッセージが表示されます。
6. ブラウザーでログイン・ページを最新表示し、変更内容を確認します。


## デフォルト画面の表示
{: #default}

{{site.data.keyword.appid_short_notm}} にはデフォルトのログイン画面が用意されており、表示する独自の UI 画面がない場合に呼び出すことができます。
{: shortdesc}

表示できる画面は、ID プロバイダーの構成によって異なります。このサービスでは、ソーシャル ID プロバイダーの拡張機能は提供していません。ユーザー・アカウント情報へのアクセス権限がないためです。ユーザーが情報を管理する場合は、自分で ID プロバイダーにアクセスする必要があります。例えば、Facebook のパスワードを変更する場合は、www.facebook.com にアクセスする必要があります。

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


以下の画像の中から選択した言語をクリックし、コードの実装を開始します。

<img usemap="#default-options-map" border="0" class="image" id="options" src="images/default-options.png" width="750" alt="アプリでクラウド・ディレクトリーを開始するには、SDK 言語のアイコンをクリックします。" style="width:750px;" />
<map name="default-options-map" id="default-options-map">
<area href="login-widget.html#android" alt="Android SDK によるサインイン操作環境の管理" shape="rect" coords="113, 8, 224, 123" />
<area href="login-widget.html#ios-swift" alt="iOS Swift SDK によるサインイン操作環境の管理" shape="rect" coords="251, 12, 362, 127" />
<area href="login-widget.html#nodejs" alt="Node.js SDK によるサインイン操作環境の管理" shape="rect" coords="387, 10, 498, 125" />
<area href="login-widget.html#swift" alt="Swift SDK によるサインイン操作環境の管理" shape="rect" coords="525, 10, 636, 125" />
</map>
</br>

### Android SDK を使用したデフォルト画面の表示
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

### iOS Swift SDK を使用したデフォルト画面の表示
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

### Node.js SDK を使用したデフォルト画面の表示
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
    `WebAppStrategy` により、ユーザーはユーザー名とパスワードを使用して Web アプリにサインインできます。ログインに成功すると、ユーザーのアクセス・トークンは HTTP セッションに保管され、セッション中に使用できるようになります。HTTP セッションが破棄されるか期限切れになると、トークンは無効になります。
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
### Swift SDK を使用したデフォルト UI の表示
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


### Android SDK を使用してカスタマイズした画面の表示
{: #branded-ui-android}

クラウド・ディレクトリーを有効にした場合は、Android SDK を使用してカスタマイズした画面を呼び出せます。 ユーザーの対話に使用できるようにする画面の組み合わせを選択できます。詳しい例については、<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">このブログ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"> を確認してください</a>。
{: shortdesc}

</br>
**サインイン**

1. ID プロバイダーとして**「クラウド・ディレクトリー (Cloud Directory)」**を**「オン (On)」**に設定します。
2. 以下のコマンドをコードに挿入します。
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
             //例外の発生
        }

          @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //ユーザーの認証
        }
         });
  ```
  {: pre}

</br>
</br>

### iOS Swift SDK を使用してカスタマイズした画面の表示
{: #branded-ui-ios-swift}

クラウド・ディレクトリーを有効にした場合は、iOS Swift SDK を使用してカスタマイズ画面を呼び出せます。
{: shortdesc}

</br>
**サインイン**

1. GUI の ID プロバイダーのタブで、クラウド・ディレクトリーを**「オン (On)」**に設定します。
2. リソース所有者のパスワードを使用してログインします。 ユーザーがユーザー名とパスワードを使用してログインしようとすると、アクセス・トークンと識別トークンが取得されます。
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //ユーザーの認証
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //例外の発生
      }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: pre}
</br>
</br>

### Node.js SDK を使用してカスタマイズした画面の表示
{: #branded-ui-nodejs}

クラウド・ディレクトリーを有効にした場合は、Node.js SDK を使用してカスタマイズした画面を呼び出せます。 ユーザーの対話に使用できるようにする画面の組み合わせを選択できます。 Node.js バックエンドを選択すると、{{site.data.keyword.appid_short_notm}} Node.js SDK (リンク) にあるセルフサービス・モジュールを使用できます。
{: shortdesc}

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
    `WebAppStrategy` により、ユーザーはユーザー名とパスワードを使用して Web アプリにサインインできます。ログインに成功すると、ユーザーのアクセス・トークンは HTTP セッションに保管され、セッション中に使用できるようになります。HTTP セッションが破棄されるか期限切れになると、トークンは無効になります。
    {: tip}

</br>
</br>

## API を使用したカスタマイズ画面の表示
{: #branding}

独自のカスタマイズ画面を表示して、{{site.data.keyword.appid_short_notm}} の認証機能と許可機能を利用することができます。クラウド・ディレクトリーを ID プロバイダーとして使用する場合、ユーザーとアプリの対話が簡単になります。 サインイン、登録、パスワードのリセットなどを、支援を頼まずに各自で行うことができます。
{: shortdesc}

これを可能にするために、{{site.data.keyword.appid_short_notm}} は REST API を公開しています。REST API を使用して、Web アプリにサービスを提供するバックエンド・サーバーを構築したり、独自のカスタム画面を使用してモバイル・アプリと対話したりできます。

管理 API は、IBM Cloud Identity and Access Management で生成されたトークンにより保護されます。つまり、アカウント所有者は、各サービス・インスタンスに対して自分のチームの誰がどのレベルのアクセス権限を持つかを指定できます。IAM と {{site.data.keyword.appid_short_notm}} の連動方法について詳しくは、[サービス・アクセス管理](/docs/services/appid/iam.html)を参照してください。

あるユーザーがカスタマイズ画面で「サインイン」をクリックすると、[リソース所有者のパスワード資格情報フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)を使用して、Web アプリまたはモバイル・アプリからアクセス・トークンと識別トークンを直接取得できます。

[設定](/docs/services/appid/cloud-directory.html)の構成が完了したら、以下のようにします。


**登録**
`/sign_up` エンドポイントを使用して、各ユーザーが自分でアプリに登録できるようにします。
要求本体に以下のデータを指定します。
  * tenantID。
  * クラウド・ディレクトリーのユーザー・データ。詳しくは、[SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) を参照してください。
    * `password` 属性。
    * `true` に設定された `primary` 属性のある email 配列に、少なくとも 1 つの E メール・アドレスが必要です。

[E メール構成](/docs/services/appid/cloud-directory.html)に応じて、ユーザーは確認の要求を受け取るか、アプリへの登録時に歓迎の E メールを受け取ります。両方のタイプの E メールは、ユーザーがアプリに登録したときにトリガーされます。確認 E メールには**「確認 (Verify)」**ボタンがあります。ユーザーがボタンを押して ID を確認すると、確認を感謝する画面が {{site.data.keyword.appid_short_notm}} によって表示されます。  

独自に用意した確認後のページを表示するには、以下のようにします。

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「カスタム・ランディング・ページ (Custom Landing Pages)」**タブに移動します。
2. 独自のランディング・ページの URL を**「カスタム E メール・アドレス確認ページの URL (URL for your custom email address verification page)」**に入力します。

この値を指定した場合、{{site.data.keyword.appid_short_notm}} はその URL を `context` 照会で呼び出します。`/sign_up/confirmation_result` エンドポイントを呼び出し、受け取った `context` パラメーターを渡すと、その結果から、各ユーザーが自分のアカウントを確認したかどうかが分かります。確認が済んでいる場合は、独自のカスタム・ページを表示できます。

</br>
**パスワードを忘れた場合**

`/forgot_password` エンドポイントを使用して、ユーザーがパスワードを忘れた場合に自分でパスワードを取り戻せるようにします。

要求本体に以下のデータを指定します。
  * tenantID。
  * クラウド・ディレクトリー・ユーザーの E メール。

このエンドポイントが呼び出されると、パスワード・リセット E メールがユーザーに送信されます。この E メールには**「リセット (Reset)」**ボタンがあります。ユーザーがボタンを押すと、パスワードをリセットできる画面が {{site.data.keyword.appid_short_notm}} によって表示されます。

独自に用意したパスワード・リセット後のページを表示するには、以下のようにします。

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「カスタム・ランディング・ページ (Custom Landing Pages)」**タブに移動します。
2. 独自のランディング・ページの URL を**「カスタム・パスワード・リセット・ページの URL (URL for your custom reset password page)」**に入力します。  

この値を指定した場合、{{site.data.keyword.appid_short_notm}} はその URL を `context` 照会で呼び出します。`/forgot_password/confirmation_result` を呼び出すと、この `context` パラメーターを使用して結果を受け取ることができます。正常な結果が得られた場合は、独自のカスタム・ページを表示できます。

ランダムなストリングをカスタム・パスワード・リセット・ページに追加し、要求の送信時にそれをバックエンドに渡すようにしてください。そのストリングをハンドラーで検証し、それが有効である場合のみ `/change_password` エンドポイントを呼び出すようにします。そうすることで、バックエンドのパスワード・リセット・エンドポイントの脆弱性を減らすことができます。
{: tip}

</br>
**パスワードの変更**

`/change_password` エンドポイントには、2 種類の使用方法があります。ユーザーがリセット要求を送信する場合と、ユーザーがアプリにサインインしてパスワードの更新を要求する場合です。

リセット要求後にパスワードを更新するには、以下のようにします。

要求本体に以下のデータを指定します。
  * tenantID。
  * ユーザーの新規パスワード
  * クラウド・ディレクトリー・ユーザーの UUID。
  * オプション: パスワード・リセットの実行元となる IP アドレス。IP アドレスを渡す場合は、パスワード変更 E メールのテンプレートでプレースホルダー `%{passwordChangeInfo.ipAddress}` を使用できます。

構成によっては、パスワードが変更されると、変更があったことを該当ユーザーに通知する E メールを {{site.data.keyword.appid_short_notm}} で送信することもできます。

</br>
ユーザーがアプリへのサインイン中に自分でパスワードを変更できるようにするには、以下のようにします。

要求本体に以下のデータを指定します。
  * tenantID。
  * ユーザーの新規パスワード
  * クラウド・ディレクトリー・ユーザーの UUID。

パスワード変更ページでは、ユーザーに対して現在のパスワードと新規パスワードを入力するように求める必要があります。
{: tip}

バックエンドで ROP API を使用してユーザーの現在のパスワードが検証され、それが有効であった場合は、新規パスワードを使用してこのエンドポイントが呼び出されます。構成によっては、パスワードが変更されると、変更があったことを該当ユーザーに通知する E メールを {{site.data.keyword.appid_short_notm}} で送信することもできます。

</br>
**再送**

`/resend/{templateName}` を使用して、何らかの理由でユーザーが E メールを受信しなかった場合に、それを再送することができます。

要求本体に以下のデータを指定します。
  * tenantID。
  * テンプレート名
  * クラウド・ディレクトリー・ユーザーの UUID。


**変更の詳細**

ユーザーは、アプリにサインインしているときに、ユーザー情報の一部を自分で更新することができます。そのような情報は、`/Users/{userId}` で取得して更新できます。

ユーザー詳細が更新されると、このエンドポイントは、更新されたユーザー・データを [SCIM 形式](https://tools.ietf.org/html/rfc7643#section-8.2)で要求本体から取得します。関連する詳細のみを変更するようにしてください。

ユーザーの E メール・アドレスは変更できません。
{: tip}
