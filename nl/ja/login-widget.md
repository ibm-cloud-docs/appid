---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

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


# ログイン・ウィジェットの表示
{: #login-widget}

{{site.data.keyword.appid_full}} に用意されているログイン・ウィジェットを使用して、ユーザーに機密保護機能のあるサインイン・オプションを提供できます。
{: shortdesc}

ID プロバイダーを使用するようにアプリが構成されている場合、アプリへの訪問者はログイン・ウィジェットによってサインイン画面に誘導されます。 ログイン・ウィジェットを使用して、サインイン・フロー用に事前構成された画面を表示できます。 さらに、サインイン・フローは、ソース・コードを変更せずにいつでも更新することができます。

アプリに固有の操作環境を作成しますか? [自分の画面を起動](/docs/services/appid?topic=appid-branded)できます。
{: tip}

## ログイン・ウィジェットについて
{: #widget-understanding}

ログイン・ウィジェットを表示することで、独自の UI 画面がなくても {{site.data.keyword.appid_short_notm}} を利用できます。
{: shortdesc}

### デフォルトとは何ですか?
{: #widget-default}

複数の ID プロバイダーが構成されている場合、ユーザーは、アプリケーションにサインインしようとすると、ログイン・ウィジェットにリダイレクトされます。 ログイン・ウィジェットを使用することにより、ユーザーは同一性を検証するプロバイダーを選択できます。 ただし、1 つのプロバイダーのみが**「オン」**に設定されている場合、訪問者はその ID プロバイダーの認証画面にリダイレクトされます。

### {{site.data.keyword.appid_short_notm}} は ID プロバイダーからどれほどの量の情報を取得しますか?
{: #widget-obtain-info}

ソーシャル ID プロバイダーまたはエンタープライズ ID プロバイダーを使用する場合、{{site.data.keyword.appid_short_notm}} にはユーザー・アカウント情報への読み取り権限があります。 このサービスは、ID プロバイダーから返されるトークンとアサーションを使用して、ユーザーが本人であることを検証します。 このサービスには情報への書き込み権限がないため、ユーザーは選択した ID プロバイダーを使用して、パスワードのリセットなどのアクションを実行する必要があります。 例えば、ユーザーが Facebook を使用してアプリにサインインした後にパスワードを変更する場合は、www.facebook.com にアクセスしてそれを行う必要があります。

[クラウド・ディレクトリー](/docs/services/appid?topic=appid-cloud-directory)を使用する場合、{{site.data.keyword.appid_short_notm}} が ID プロバイダーになります。 このサービスは、レジストリーを使用してユーザー ID を検証します。 {{site.data.keyword.appid_short_notm}} はプロバイダーであるため、ユーザーは、パスワードのリセットなどの拡張機能をアプリ内で直接利用できます。


### プロバイダーごとにどの画面を表示できますか?
{: #widget-options}

以下の表を参照して、ID プロバイダーのタイプごとに表示できる画面を確認してください。

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

</br>
</br>

## ログイン・ウィジェットのカスタマイズ
{: #widget-customize}

{{site.data.keyword.appid_short_notm}} にはデフォルトのログイン画面が用意されており、表示する独自の UI 画面がない場合に呼び出すことができます。 自分で選択したロゴや色が表示されるように、画面をカスタマイズすることができます。
{: shortdesc}

画面をカスタマイズするには、以下のようにします。

1. {{site.data.keyword.appid_short_notm}} サービス・ダッシュボードを開きます。
2. **「ログインのカスタマイズ」**セクションを選択します。 ログイン・ウィジェットの外観を自社のブランドに合うように変更できます。
3. ローカル・システムにある PNG ファイルまたは JPG ファイルを選択し、自社のロゴをアップロードします。 推奨される画像サイズは 320 x 320 ピクセルです。 ファイルの最大サイズは 100 KB です。
4. ウィジェットのヘッダー・カラーをカラー・ピッカーから選択するか、または別のカラーの 16 進コードを入力します。
5. プレビュー・ペインでカスタマイズを検査し、問題がなければ**「変更を保存」**をクリックします。 確認メッセージが表示されます。
6. ブラウザーでログイン・ページを最新表示し、変更内容を確認します。

注意: {{site.data.keyword.appid_short_notm}} は他の言語でも利用できます。 作業中の言語の SDK が表示されない場合は、常に API を使用できます。 <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">ブログ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
{: tip}


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
  {: pre}

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
