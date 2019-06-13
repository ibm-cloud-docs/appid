---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-06"

keywords: Authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

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


# ログイン・ウィジェットの使用
{: #login-widget}

{{site.data.keyword.appid_full}} では、ログイン・ウィジェットというデフォルト UI を使用して、サインインに使用する ID プロバイダーをアプリケーション・ユーザーに選択させることができます。クラウド・ディレクトリーを使用する場合は、登録、パスワードを忘れた場合の処理、多要素認証などの他の機能のための追加の UI もログイン・ウィジェットで利用できます。
{: shortdesc}


## ログイン・ウィジェットについて
{: #widget-understanding}

ログイン・ウィジェットの利点の 1 つは、独自の認証 UI を一切実装せずに、{{site.data.keyword.appid_short_notm}} の使用を開始できることです。これにより、開発者のオンボーディング・エクスペリエンスがはるかに簡単になります。

### ログイン・ウィジェットのデフォルトの動作
{: #widget-default}

デフォルトでは、ログイン・ウィジェットは Facebook、Google、クラウド・ディレクトリーを使用できるように設定されます。この動作は、オプションとして構成する ID プロバイダーを選択して、いつでも変更できます。複数の ID プロバイダーを有効にすると、ID プロバイダーをユーザーが選択できる画面がログイン・ウィジェットに表示されます。一方、プロバイダーを 1 つだけ有効にした場合、そのような選択画面はユーザーに表示されません。ユーザーはすぐに ID プロバイダーに転送され、サインイン・プロセスを開始します。

例えば、デフォルトの Facebook、Google、およびクラウド・ディレクトリーを使用している場合は、ユーザーに選択画面が表示されます。Facebook のみを有効にした場合は、ユーザーは認証のためにすぐに Facebook に転送されます。



### 各プロバイダーで表示できる画面はどれですか?
{: #widget-options}

クラウド・ディレクトリーを使用する場合は、{{site.data.keyword.appid_short_notm}} で利用できるユーザー管理機能が拡張されます。機能の拡張は、ログイン・ウィジェットの機能にも当てはまります。クラウド・ディレクトリーに保管されているユーザーは、登録やパスワードのリセットなどの機能をログイン・ウィジェットで直接利用できます。以下の表を参照して、ID プロバイダーのタイプごとに表示できる画面を確認してください。

<table>
  <thead>
    <tr>
      <th>ログイン・ウィジェット画面</th>
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


## ログイン・ウィジェットのカスタマイズ
{: #widget-customize}

ログイン・ウィジェットは動的です。外観や ID プロバイダー構成をカスタマイズでき、変更はすぐに適用されます。アプリケーション・コードを更新したりアプリを再デプロイしたりする必要はありません。
{: shortdesc}

ログイン・ウィジェットに用意されている以上のカスタマイズが必要ですか? ユーザーのサインイン、登録、パスワードのリセットなどのフローのために全面的にカスタマイズした独自の UI を実装して、アプリ固有のエクスペリエンスを構築できます。まずは、[アプリのブランド設定](/docs/services/appid?topic=appid-branded)を参照してください。
{: tip}

画面をカスタマイズするには、以下のようにします。

1. {{site.data.keyword.appid_short_notm}} サービス・ダッシュボードを開きます。
2. **「ログインのカスタマイズ」**セクションを選択します。 ログイン・ウィジェットの外観を自社のブランドに合うように変更できます。
3. ローカル・システムにある PNG ファイルまたは JPG ファイルを選択し、自社のロゴをアップロードします。 推奨される画像サイズは 320 x 320 ピクセルです。 ファイルの最大サイズは 100 KB です。
4. ウィジェットのヘッダー・カラーをカラー・ピッカーから選択するか、または別のカラーの 16 進コードを入力します。
5. プレビュー・ペインでカスタマイズを検査し、問題がなければ**「変更を保存」**をクリックします。 確認メッセージが表示されます。
6. ブラウザーでログイン・ページを最新表示し、変更内容を確認します。


## Android SDK を使用したログイン・ウィジェットの表示
{: #widget-display-android}

[Android クライアント SDK](https://github.com/ibm-cloud-security/appid-clientsdk-android) を使用して、事前構成された画面を呼び出すことができます。
{: shortdesc}

以下のコマンドをコードに挿入します。

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
{: codeblock}

</br>

### 登録
{: #widget-android-signup}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションにサインアップできるようにする」**と**「ユーザーがアプリケーションからアカウントを管理できるようにする」**の両方を**「オン」**に設定する必要があります。
2. アプリに以下のコードを追加します。 ユーザーがカスタム画面からアプリに登録すると、登録フローが開始します。 以下の呼び出しは、ユーザーを登録できるだけではなく、クラウド・ディレクトリーの構成によっては、登録を完了するための確認 E メールを送信することもできます。

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //例外の発生
      }

      @Override
        public void onAuthorizationCanceled () {
          //ユーザーによる登録キャンセル
			 }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              //ユーザーの認証
				 } else {
              //E メール検証が必要
				 }
      }
  });
  ```
  {: codeblock}

</br>

### パスワードを忘れた場合
{: #widget-android-forgot-password}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションからアカウントを管理できるようにする」**を**「オン」**に設定する必要があります。
2. サービス・ダッシュボードの**「パスワードの再設定」**タブで、**「パスワード再設定の E メール」**が**「オン」**に設定されていることを確認します。
3. アプリに以下のコードを追加します。 ユーザーがアプリケーションで「パスワードを忘れた場合」をクリックすると、SDK は forgot_password API を呼び出して、パスワードを再設定できるようにするための E メールをユーザーに送信します。

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //例外の発生
      }

      @Override
        public void onAuthorizationCanceled () {
          // ユーザーによるパスワード忘れ処理キャンセル
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // パスワード忘れ処理の終了。この場合 accessToken と identityToken はヌル。
      }
  });
  ```
  {: codeblock}

</br>

### 変更の詳細
{: #widget-android-change-details}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションにサインアップできるようにする」**と**「ユーザーがアプリケーションからアカウントを管理できるようにする」**の両方を**「オン」**に設定する必要があります。
2. サービス・ダッシュボードの**「パスワード変更済み」**タブで、**「パスワード変更通知 E メール」**を次のように設定します。
3. ログイン・ウィジェットを呼び出して詳細変更フローを開始します。

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          // 例外の発生
      }

      @Override
        public void onAuthorizationCanceled () {
          // ユーザーによる詳細変更キャンセル
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //ユーザーの認証と、新しいトークンの受信
   			 }
  });
  ```
  {: codeblock}

</br>

### パスワードの変更
{: #widget-android-change-password}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションにサインアップできるようにする」**と**「ユーザーがアプリケーションからアカウントを管理できるようにする」**の両方を**「オン」**に設定する必要があります。
2. 以下のコードをアプリに配置して、パスワード変更フローを開始します。

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          // 例外の発生
      }

      @Override
        public void onAuthorizationCanceled () {
          // ユーザーによるパスワード変更キャンセル
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //ユーザーの認証と、新しいトークンの受信
   			 }
  });
  ```
  {: codeblock}



## iOS Swift SDK を使用したログイン・ウィジェットの表示
{: #widget-display-ios-swift}

[iOS Swift クライアント SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift) を使用して、事前構成された画面を呼び出すことができます。
{: shortdesc}

以下のコマンドをコードに挿入します。

  ```swift
  import IBMCloudAppID
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
  {: codeblock}

</br>

### 登録
{: #widget-ios-signup}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションにサインアップできるようにする」**と**「ユーザーがアプリケーションからアカウントを管理できるようにする」**の両方を**「オン」**に設定する必要があります。
2. 以下のコードをアプリケーションに挿入します。 ユーザーがアプリケーションに登録しようとすると、ログイン・ウィジェットが呼び出され、カスタム登録ページが表示されます。

  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

### パスワードを忘れた場合
{: #widget-ios-forgot-password}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションからアカウントを管理できるようにする」**を**「オン」**に設定する必要があります。
2. サービス・ダッシュボードの**「パスワードの再設定」**タブで、**「パスワード再設定の E メール」**が**「オン」**に設定されていることを確認します。
3. 以下のコードをアプリケーションに挿入します。 いずれかのアプリ・ユーザーがパスワードの更新を要求すると、ログイン・ウィジェットが呼び出され、プロセスが開始します。

  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

### 変更の詳細
{: #widget-ios-change-details}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションにサインアップできるようにする」**と**「ユーザーがアプリケーションからアカウントを管理できるようにする」**の両方を**「オン」**に設定する必要があります。
2. サービス・ダッシュボードの**「パスワード変更済み」**タブで、**「パスワード変更通知 E メール」**を次のように設定します。
3. ログイン・ウィジェットを呼び出して詳細変更フローを開始します。

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         //ユーザーの認証と、新しいトークンの受信
       }

       public func onAuthorizationCanceled() {
          //ユーザーによる詳細変更キャンセル
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
          //例外の発生
      }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>

### パスワードの変更
{: #widget-ios-change-password}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションにサインアップできるようにする」**と**「ユーザーがアプリケーションからアカウントを管理できるようにする」**の両方を**「オン」**に設定する必要があります。
2. 以下のコードをアプリに配置して、パスワード変更フローを開始します。

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          //ユーザーの認証と、新しいトークンの受信
       }

       public func onAuthorizationCanceled() {
          //ユーザーによるパスワード変更キャンセル
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
           //例外の発生
      }
   }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}


## Node.js SDK を使用したログイン・ウィジェットの表示
{: #widget-display-nodejs}

[Node.js サーバー SDK](https://github.com/ibm-cloud-security/appid-serversdk-nodejs) を使用して、事前構成された画面を呼び出すことができます。
{: shortdesc}

ユーザー名とパスワードのパラメーターを使用して呼び出せる post ルートをアプリに追加し、リソース所有者のパスワードを使用してログインします。

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // フラッシュ・メッセージの許可
  }));
  ```
  {: codeblock}

`WebAppStrategy` により、ユーザーはユーザー名とパスワードを使用して Web アプリにサインインできます。 ログインに成功すると、ユーザーのアクセス・トークンは HTTP セッションに保管され、セッション中に使用できるようになります。 HTTP セッションが破棄されるか期限切れになると、トークンは無効になります。
{: tip}

</br>

### 登録
{: #widget-nodejs-signup}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションにサインアップできるようにする」**と**「ユーザーがアプリケーションからアカウントを管理できるようにする」**の両方を**「オン」**に設定する必要があります。
2. 以下のコードをアプリケーションに挿入します。 ユーザーがアプリケーションに登録しようとすると、ログイン・ウィジェットが呼び出され、カスタム登録ページが表示されます。

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

### パスワードを忘れた場合
{: #widget-nodejs-forgot-password}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションからアカウントを管理できるようにする」**を**「オン」**に設定する必要があります。
2. サービス・ダッシュボードの**「パスワードの再設定」**タブで、**「パスワード再設定の E メール」**が**「オン」**に設定されていることを確認します。
3. 以下のコードをアプリケーションに配置して、*show* プロパティーを `WebAppStrategy.FORGOT_PASSWORD` に渡します。 ユーザーがアプリへのパスワードの更新を要求すると、ログイン・ウィジェットが呼び出され、プロセスが開始します。

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

### 変更の詳細
{: #widget-nodejs-change-details}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションにサインアップできるようにする」**と**「ユーザーがアプリケーションからアカウントを管理できるようにする」**の両方を**「オン」**に設定する必要があります。
2. サービス・ダッシュボードの**「パスワード変更済み」**タブで、**「パスワード変更通知 E メール」**を次のように設定します。
3. 以下のコードをアプリケーションに配置して、*show* プロパティーを `WebAppStrategy.FORGOT_PASSWORD` に渡し、詳細変更フォームを起動します。

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

### パスワードの変更
{: #widget-nodejs-change-password}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションにサインアップできるようにする」**と**「ユーザーがアプリケーションからアカウントを管理できるようにする」**の両方を**「オン」**に設定する必要があります。
2. サービス・ダッシュボードの**「パスワード変更済み」**タブで、**「パスワード変更通知 E メール」**を次のように設定します。
3. 以下のコードをアプリケーションに配置して、*show* プロパティーを `WebAppStrategy.FORGOT_PASSWORD` に渡し、詳細変更フォームを起動します。

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
