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

# サインイン操作環境のブランド化
{: #branding}

{{site.data.keyword.appid_full}} の認証機能と許可機能を利用しながら、カスタマイズした独自の UI を表示することができます。クラウド・ディレクトリーを ID プロバイダーとして使用する場合、ユーザーとアプリの対話が簡単になります。ユーザーは、サインイン、登録、パスワードの変更などを、支援を頼まずに自分で行うことができます。
{: shortdesc}

クラウド・ディレクトリーを ID プロバイダーとして使用する場合は、[リソース所有者のパスワード資格情報フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)によってアクセス・トークンと識別トークンを取得できます。

**注**: カスタマイズしたサインイン・ページを使用できるのは、クラウド・ディレクトリーだけをオプションとして構成した場合のみです。他の ID プロバイダーを **on** に設定した場合は、事前構成されたサインイン画面が表示されます。

## Android SDK を使用してカスタマイズした画面の表示
{: #branded-ui-android}

クラウド・ディレクトリーを有効にした場合は、Android SDK を使用してカスタマイズした画面を呼び出せます。ユーザーの対話に使用できるようにする画面の組み合わせを選択できます。<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">ブログを参照してください。<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>
{: shortdesc}

</br>
**サインイン**

1. ID プロバイダーとして**「クラウド・ディレクトリー (Cloud Directory)」**を**「オン (On)」**に設定します。
2. 以下のコマンドをコードに挿入します。
  ```java
  AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
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
  {: codeblock}

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
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: codeblock}

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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   			 }
   		 });
    ```
    {: codeblock}

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
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  			 }
  		 });
   ```
   {: codeblock}

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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   			 }
   		 });
   ```
   {: codeblock}

</br>
</br>

## iOS Swift SDK を使用してカスタマイズした画面の表示
{: #branded-ui-ios-swift}

クラウド・ディレクトリーを有効にした場合は、ios Swift SDK を使用してカスタマイズした画面を呼び出せます。ユーザーの対話に使用できるようにする画面の組み合わせを選択できます。{: shortdesc}

</br>
**サインイン**

1. GUI の ID プロバイダーのタブで、クラウド・ディレクトリーを**「オン (On)」**に設定します。
2. リソース所有者のパスワードを使用してログインします。エンド・ユーザーのユーザー名とパスワードを指定して、アクセス・トークンと ID トークンを取得することができます。
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //ユーザーの認証
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //例外の発生
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}

</br>
**登録**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定してください。
2. LoginWidget を呼び出して登録フローを開始します。
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

</br>
**パスワードを忘れた場合**

1. クラウド・ディレクトリーの設定で**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**と**「パスワードを忘れた場合の E メール (Forgot password email)」**を必ず**「オン (On)」**に設定します。
2. LoginWidget を呼び出してパスワード忘れフローを開始します。
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

</br>
**アカウントの詳細**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。
2. LoginWidget を呼び出して詳細変更フローを開始します。
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>
**パスワードの変更**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。
2. LoginWidget を呼び出してパスワード変更フローを開始します。
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}

</br>

## Node.js SDK を使用してカスタマイズした画面の表示
{: #branded-ui-nodejs}

クラウド・ディレクトリーを有効にした場合は、Node.js SDK を使用してカスタマイズした画面を呼び出せます。ユーザーの対話に使用できるようにする画面の組み合わせを選択できます。{: shortdesc}

**サインイン**
1. ID プロバイダー設定でクラウド・ディレクトリーを**「オン (On)」**に設定して、コールバック・エンドポイントを指定します。
2. ユーザー名とパスワードのパラメーターを使用して呼び出せる post ルートをアプリに追加し、リソース所有者のパスワードを使用してログインします。
    **注**: `WebAppStrategy` により、ユーザーはユーザー名とパスワードを使用して Web アプリにログインできます。ログインに成功すると、ユーザーのアクセス・トークンは HTTP セッションに保管され、セッションの期間中、使用可能です。HTTP セッションが破棄されるか期限切れになると、トークンは無効になります。
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // フラッシュ・メッセージの許可
  }));
    ```
    {: codeblock}

</br>
**登録**

1. クラウド・ディレクトリーの設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。これを「いいえ (no)」に設定した場合、プロセスはアクセス・トークンと識別トークンを取得せずに終了します。
2. WebAppStrategy に `show` プロパティーを渡し、それを `WebAppStrategy.SIGN_UP` に設定します。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>
**パスワードを忘れた場合**

1. クラウド・ディレクトリーの設定で**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**と**「パスワードを忘れた場合の E メール (Forgot password email)」**を**「オン (ON)」**に設定します。これを「いいえ (no)」に設定した場合、プロセスはアクセス・トークンと識別トークンを取得せずに終了します。
2. WebAppStrategy に `show` プロパティーを渡し、それを `WebAppStrategy.FORGOT_PASSWORD` に設定します。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

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
  {: codeblock}

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
  {: codeblock}
