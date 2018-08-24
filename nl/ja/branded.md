---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# アプリのブランド設定
{: #branding}

独自のカスタマイズ画面を表示して、{{site.data.keyword.appid_full}} の認証機能と許可機能を利用することができます。 Cloud Directory を ID プロバイダーとして使用する場合、ユーザーとアプリの対話が簡単になります。 サインイン、登録、パスワードの変更などを、支援を頼まずに各自で行うことができます。
{: shortdesc}

独自の画面を使用する場合は、[リソース所有者のパスワード資格情報フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)を使用してアクセス・トークンと識別トークンを提供します。


## iOS Swift SDK によるアプリのブランド設定
{: #branded-ui-ios-swift}

Cloud Directory を有効にした場合は、iOS Swift SDK を使用して独自のブランド・マークがついた画面を呼び出せます。
{: shortdesc}

</br>
**サインイン**

1. GUI の ID プロバイダーのタブで、Cloud Directory を**「オン (On)」**に設定します。
2. ログイン・ウィジェットを呼び出してサインイン・フローを開始します。 ユーザーがユーザー名または E メールとパスワードを使用してログインしようとすると、アクセス・トークンと識別トークンが取得されます。
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

**登録**

1. GUI の ID プロバイダーのタブで、Cloud Directory を**「オン (On)」**に設定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. ログイン・ウィジェットを呼び出して登録フローを開始します。
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
  {: pre}

</br>

**パスワードを忘れた場合**

1. GUI の ID プロバイダーのタブで、Cloud Directory を**「オン (On)」**に設定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. ログイン・ウィジェットを呼び出してパスワード忘れフローを開始します。
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
  {: pre}

</br>

**変更の詳細**

1. GUI の ID プロバイダーのタブで、Cloud Directory を**「オン (On)」**に設定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
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
  {: pre}

</br>

**パスワードの変更**

1. GUI の ID プロバイダーのタブで、Cloud Directory を**「オン (On)」**に設定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. ログイン・ウィジェットを呼び出して詳細変更フローを開始します。
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
  {: pre}

</br>


## Android SDK によるアプリのブランド設定
{: #branded-ui-android}

クラウド・ディレクトリーを有効にした場合は、Android SDK を使用してカスタマイズした画面を呼び出せます。 ユーザーの対話に使用できるようにする画面の組み合わせを選択できます。詳しい例については、<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">このブログ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"> を確認してください</a>。
{: shortdesc}

</br>

**サインイン**

1. ID プロバイダーとして**「クラウド・ディレクトリー (Cloud Directory)」**を**「オン (On)」**に設定します。
2. エンド・ユーザーのユーザー名とパスワードを指定して、アクセス・トークン、識別トークン、リフレッシュ・トークンを取得します。
3. ログイン・ウィジェットを呼び出してサインイン・フローを開始します。
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //例外の発生
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //ユーザーの認証
        }
  });
  ```
  {: pre}

</br>

**登録**

1. ID プロバイダーとして**「クラウド・ディレクトリー (Cloud Directory)」**を**「オン (On)」**に設定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. ログイン・ウィジェットを呼び出して登録フローを開始します。
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


**パスワードを忘れた場合**

1. ID プロバイダーとして**「クラウド・ディレクトリー (Cloud Directory)」**を**「オン (On)」**に設定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. ログイン・ウィジェットを呼び出してパスワード忘れフローを開始します。
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
  {: pre}

</br>

**変更の詳細**

1. ID プロバイダーとして**「クラウド・ディレクトリー (Cloud Directory)」**を**「オン (On)」**に設定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. ログイン・ウィジェットを呼び出して詳細変更フローを開始します。
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //例外の発生
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
  {: pre}


</br>

**パスワードの変更**

1. ID プロバイダーとして**「クラウド・ディレクトリー (Cloud Directory)」**を**「オン (On)」**に設定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. ログイン・ウィジェットを呼び出してパスワード変更フローを開始します。
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //例外の発生
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
  {: pre}

</br>
</br>


## Node.js SDK によるアプリのブランド設定
{: #branded-ui-nodejs}

Cloud Directory を有効にした場合は、Node.js SDK を使用してカスタマイズした画面を呼び出せます。
{: shortdesc}

**サインイン**

WebAppStrategy を使用すると、ユーザーはユーザー名とパスワードで Web アプリにサインインできます。ユーザーがアプリに正常にサインインすると、アクセス・トークンは、HTTP セッションが存続している限り、そのセッションで持続します。HTTP セッションが閉じられるか期限切れになると、アクセス・トークンも破棄されます。

1. ID プロバイダー設定で Cloud Directory を**「オン (On)」**に設定して、コールバック・エンドポイントを指定します。
2. ユーザー名とパスワードのパラメーターを使用して呼び出せる post ルートをアプリに追加し、リソース所有者のパスワード・フローを使用してサインインします。
  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // フラッシュ・メッセージの許可
  }));
  ```
  {: pre}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> コマンド・パラメーター </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td>認証に成功した後にユーザーのリダイレクト先となる URL。</td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td>認証に失敗した場合にユーザーのリダイレクト先となる URL。</td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td><code>true</code> に設定した場合、Cloud Directory サービスからエラー・メッセージが返されます。デフォルトでは、値は <code>false</code> に設定されています。</td>
      </tr>
    </tbody>
  </table>

  1. HTML 形式で要求を送信する場合、[body parser](https://www.npmjs.com/package/body-parser) ミドルウェアを使用することができます。
  2. 返されたエラー・メッセージを取得するためには、[connect-flash](https://www.npmjs.com/package/connect-flash) を使用できます。詳しくは、[Web アプリのサンプル](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js)を参照してください。
  {: tip}

</br>
**登録**

1. ID プロバイダー設定で Cloud Directory を**「オン (On)」**に設定して、コールバック・エンドポイントを指定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. **「E メール検証なしのサインインをユーザーに許可する (Allow users to sign-in without email verification)」**を**「いいえ (No)」**に設定します。そのように設定しない場合、{{site.data.keyword.appid_short_notm}} のアクセス・トークンと識別トークンを取得できません。
4. ユーザー名とパスワードのパラメーターを使用して呼び出せる post ルートをアプリに追加し、リソース所有者のパスワード・フローを使用してサインインします。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**パスワードを忘れた場合**

1. ID プロバイダー設定で Cloud Directory を**「オン (On)」**に設定して、コールバック・エンドポイントを指定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. **「パスワードを忘れた場合の E メール (Forgot password email)」**を**「オン (ON)」**に設定します。
4. *show* プロパティーを `WebAppStrategy.FORGOT_PASSWORD` に渡して、パスワード忘れフォームを起動します。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**変更の詳細**

1. ID プロバイダー設定で Cloud Directory を**「オン (On)」**に設定して、コールバック・エンドポイントを指定します。
2. Cloud Directory の設定で、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (ON)」**に設定します。
3. ユーザーが {{site.data.keyword.appid_short_notm}} を使用して以前に認証されていることを確認します。
4. *show* プロパティーを `WebAppStrategy.CHANGE_DETAILS` に渡して、パスワード忘れフォームを起動します。
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## API によるアプリのブランド設定
{: #branded-ui-api}

独自のカスタマイズ画面を表示して、{{site.data.keyword.appid_short_notm}} の認証機能と許可機能を利用することができます。 クラウド・ディレクトリーを ID プロバイダーとして使用する場合、ユーザーとアプリの対話が簡単になります。 サインイン、登録、パスワードのリセットなどを、支援を頼まずに各自で行うことができます。
{: shortdesc}

これを可能にするために、{{site.data.keyword.appid_short_notm}} は REST API を公開しています。 REST API を使用して、Web アプリにサービスを提供するバックエンド・サーバーを構築したり、独自のカスタム画面を使用してモバイル・アプリと対話したりできます。

管理 API は、IBM Cloud Identity and Access Management で生成されたトークンにより保護されます。 つまり、アカウント所有者は、各サービス・インスタンスに対して自分のチームの誰がどのレベルのアクセス権限を持つかを指定できます。 IAM と {{site.data.keyword.appid_short_notm}} の連動方法について詳しくは、[サービス・アクセス管理](/docs/services/appid/iam.html)を参照してください。

[設定](/docs/services/appid/cloud-directory.html)の構成が完了したら、以下のエンドポイントを呼び出して各スクリーンを表示することができます。


**登録**
`/sign_up` エンドポイントを使用して、各ユーザーが自分でアプリに登録できるようにします。
要求本体に以下のデータを指定します。
  * tenantID。
  * クラウド・ディレクトリーのユーザー・データ。 詳しくは、[SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) を参照してください。
    * `password` 属性。
    * `true` に設定された `primary` 属性のある email 配列に、少なくとも 1 つの E メール・アドレスが必要です。

[E メール構成](/docs/services/appid/cloud-directory.html)に応じて、ユーザーは確認の要求を受け取るか、アプリへの登録時に歓迎の E メールを受け取ります。 どちらのタイプの E メールも、ユーザーがアプリに登録したときにトリガーされます。 確認 E メールには**「確認 (Verify)」**ボタンがあります。 ユーザーがボタンを押して ID を確認すると、確認を感謝する画面が {{site.data.keyword.appid_short_notm}} によって表示されます。  

独自に用意した確認後のページを表示するには、以下のようにします。

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「カスタム・ランディング・ページ (Custom Landing Pages)」**タブに移動します。
2. 独自のランディング・ページの URL を**「カスタム E メール・アドレス確認ページの URL (URL for your custom email address verification page)」**に入力します。

この値を指定した場合、{{site.data.keyword.appid_short_notm}} はその URL を `context` 照会とともに呼び出します。 `/sign_up/confirmation_result` エンドポイントを呼び出し、受け取った `context` パラメーターを渡すと、その結果から、各ユーザーが自分のアカウントを確認したかどうかが分かります。 確認が済んでいる場合は、独自のカスタム・ページを表示できます。

</br>
**パスワードを忘れた場合**

`/forgot_password` エンドポイントを使用して、ユーザーがパスワードを忘れた場合に自分でパスワードを回復できるようにします。

要求本体に以下のデータを指定します。
  * tenantID。
  * クラウド・ディレクトリー・ユーザーの E メール。

このエンドポイントが呼び出されると、パスワード・リセット E メールがユーザーに送信されます。 この E メールには**「リセット (Reset)」**ボタンがあります。 ユーザーがボタンを押すと、パスワードをリセットできる画面が {{site.data.keyword.appid_short_notm}} によって表示されます。

独自に用意したパスワード・リセット後のページを表示するには、以下のようにします。

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「カスタム・ランディング・ページ (Custom Landing Pages)」**タブに移動します。
2. 独自のランディング・ページの URL を**「カスタム・パスワード・リセット・ページの URL (URL for your custom reset password page)」**に入力します。  

この値を指定した場合、{{site.data.keyword.appid_short_notm}} はその URL を `context` 照会とともに呼び出します。 `/forgot_password/confirmation_result` を呼び出すと、この `context` パラメーターを使用して結果を受け取ることができます。 正常な結果が得られた場合は、独自のカスタム・ページを表示できます。

ランダムなストリングをカスタム・パスワード・リセット・ページに追加し、要求の送信時にそれをバックエンドに渡すようにしてください。 そのストリングをハンドラーで検証し、それが有効である場合のみ `/change_password` エンドポイントを呼び出すようにします。 そうすることで、バックエンドのパスワード・リセット・エンドポイントの脆弱性を減らすことができます。
{: tip}

</br>
**パスワードの変更**

`/change_password` エンドポイントには、2 種類の使用方法があります。 ユーザーがリセット要求を送信する場合と、ユーザーがアプリにサインインしてパスワードの更新を要求する場合です。

リセット要求後にパスワードを更新するには、要求本体に以下のデータを指定します。
  * tenantID。
  * ユーザーの新規パスワード
  * クラウド・ディレクトリー・ユーザーの UUID。
  * オプション: パスワード・リセットの実行元となる IP アドレス。 IP アドレスを渡す場合は、パスワード変更 E メールのテンプレートでプレースホルダー `%{passwordChangeInfo.ipAddress}` を使用できます。

構成によっては、パスワードが変更されると、変更があったことを該当ユーザーに通知する E メールを {{site.data.keyword.appid_short_notm}} で送信することもできます。

</br>
ユーザーがアプリへのサインイン中に自分でパスワードを変更できるようにするには、以下のようにします。

要求本体に以下のデータを指定します。
  * tenantID。
  * ユーザーの新規パスワード
  * クラウド・ディレクトリー・ユーザーの UUID。

パスワード変更ページでは、ユーザーに対して現在のパスワードと新規パスワードを入力するように求める必要があります。
{: tip}

バックエンドで ROP API を使用してユーザーの現在のパスワードが検証され、それが有効であった場合は、新規パスワードを使用してこのエンドポイントが呼び出されます。 構成によっては、パスワードが変更されると、変更があったことを該当ユーザーに通知する E メールを {{site.data.keyword.appid_short_notm}} で送信することもできます。

</br>
**再送**

`/resend/{templateName}` を使用して、何らかの理由でユーザーが E メールを受信しなかった場合に、それを再送することができます。

要求本体に以下のデータを指定します。
  * tenantID。
  * テンプレート名
  * クラウド・ディレクトリー・ユーザーの UUID。


**変更の詳細**

ユーザーは、アプリにサインインしているときに、ユーザー情報の一部を自分で更新することができます。 そのような情報は、`/Users/{userId}` で取得して更新できます。

ユーザー詳細が更新されると、このエンドポイントは、更新されたユーザー・データを [SCIM 形式](https://tools.ietf.org/html/rfc7643#section-8.2)で要求本体から取得します。 関連する詳細のみを変更するようにしてください。

ユーザーの E メール・アドレスは変更できません。
{: tip}
