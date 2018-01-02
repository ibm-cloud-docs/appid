---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Cloud Directory の管理
{: #cd}

Cloud Directory を ID プロバイダーとして使用するように、{{site.data.keyword.appid_short_notm}} を構成することができます。ユーザーは、E メールとパスワードを使用してサインインすると、ディレクトリーに追加されます。サービス GUI で、それらのユーザーを管理することができます。
{: shortdesc}

<!--- What is a cloud directory? --->

## ディレクトリー設定の管理

アプリでの通知とユーザー制御レベルを構成することができます。GUI の**「ディレクトリー設定 (Directory Settings)」**タブで、各ユーザーが実行できるセルフサービスの程度を決定します。

1. E メールを使用した登録をユーザーに許可するには、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定する必要があります。**「オフ (Off)」**に設定されている場合でもコンソールでユーザーを追加できますが、そうするのは開発目的に限られます。
2. 送信者の詳細を構成します。メッセージを送信する E メール、送信者の表示名、ユーザーの返信先を指定してください。
  **注**: アクション URL を構成するときには、ユーザーにリンクをクリックしてもらうのに十分な時間を設定してください。ユーザーは、特定のオプション (パスワードのリセットを要求する機能など) を利用する際に、E メールを検証する必要があります。
3. ユーザーが受信する E メールのタイプと、送信者情報を決定します。



## メッセージの管理

テンプレートとは、ユーザーに送信する E メール・メッセージのサンプルです。テンプレートは、メッセージの内容やレイアウトを更新してカスタマイズできます。それらのメッセージは、「ディレクトリー設定 (Directory Settings)」タブで**「オン (On)」**または**「オフ (Off)」**に設定できます。

1. **「メッセージ・タイプ (Message type)」**を選択します。
2. メッセージの内容やデザインを変更して、メッセージをカスタマイズします。パラメーターを使用して、メッセージをパーソナライズすることができます。変更後は必ず保存してください。

### メッセージのタイプ

<dl>
  <dt> ようこそ</dt>
    <dd>ユーザーが登録されたら、アプリケーションのウェルカム・メッセージを E メールで送信できます。ユーザーを歓迎して長く使ってもらうために、できるだけ人を引きつけるメッセージになるようにします。
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> すべてのメッセージ・タイプで使用可能なパラメーター</th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> ログイン・ウィジェットのために構成したイメージを表示します。</td>
        </tr>
	 <tr>
          <td> %{display.headerColor} </td>
          <td> ログイン・ウィジェットのために構成したヘッダーの色を表示します。</td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> アプリとやり取りするときに使用する、ユーザーが選択した画面名を表示します。</td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> ユーザーが登録した E メール・アドレスを表示します。</td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> ユーザーが指定した名を表示します。</td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> ユーザーのフルネームを表示します。</td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> ユーザーが指定した姓を表示します。</td>
        </tr>
      </tbody>
    </table>

    **注**: ユーザーによって設定されていない情報が、パラメーターによってプルされた場合は、ブランクとして表示されます。</dd>
  <dt> パスワードを忘れた場合</dt>
    <dd> ユーザーは、パスワードを忘れるか、または何らかの理由でパスワードを更新する必要がある場合に、パスワードのリセットを要求することができます。その要求に対する E メール応答をカスタマイズすることができます。ユーザーが変更を要求しても、ユーザーがこのメール内のリンクをクリックするまではパスワードが変更されません。

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> パスワード変更パラメーター</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> リンクが有効な時間数を表示します。</td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> リンクが有効な分数を表示します。</td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> URL の一部としてワンタイム・パスコードを表示します。ユーザーごとに異なるコードになります。例: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> パスワードをリセットするためにユーザーがクリックするリンクを表示します。</td>
        </tr>
       </tbody>
    </table></dd>
  <dt> 検証</dt>
    <dd> E メールによってアカウントを検証するようユーザーに要求することができます。検証を要求することで、アプリに登録されるおそれのある偽アカウントの数を抑制します。ユーザーが E メールを検証するまでアプリへのアクセスを制限したり、プロファイルを作成する対象ユーザーを管理する手段として利用したりできます。
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 検証メッセージ・パラメーター</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> リンクが有効な時間数を表示します。</td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> リンクが有効な分数を表示します。</td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> ワンタイム検証 URL を表示します。</td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> 設定で指定したアクション URL を表示します。</td>
        </tr>
      </tbody>
    </table></dd>
  <dt> パスワード変更</dt>
    <dd> パスワードが更新されたときにユーザーに通知することができます。これは、ユーザーがパスワードの変更を要求しなかった場合に役立ちます。ユーザーは適切な手順に沿って、アカウントを再びセキュアにすることができます。

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> パスワード変更パラメーター</th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> 新規パスワードが有効になった時刻を表示します。</td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> パスワード変更の要求元となった IP アドレスを表示します。</td>
        </tr>
      </tbody>
    </table></dd>
</dl>



## Android SDK による Cloud Directory の管理
{: #managing-android}

以下の API を使用する場合は、**「Cloud Directory ID プロバイダー (Cloud Directory identity provider)」**を必ず**「オン (ON)」**に設定してください。

### リソース所有者パスワードを使用したログイン
エンド・ユーザーのユーザー名とパスワードを指定して、アクセス・トークンと ID トークンを取得することができます。

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

### 登録

Cloud Directory の設定で、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を必ず**「オン (ON)」**に設定してください。

 LoginWidget クラスを使用して登録フローを開始します。
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
			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
				 if (accessToken != null && identityToken != null) {
				     //ユーザーの認証
				 } else {
				     //E メール検証が必要
				 }

			 }
		 });
 ```
 {: codeblock}

### パスワードを忘れた場合
Cloud Directory の設定で**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**と**「パスワード忘れ E メール (Forgot password email)」**を必ず**「オン (ON)」**に設定してください。

LoginWidget クラスを使用して、パスワード忘れフローを開始します。
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
 			 public void onAuthorizationFailure (AuthorizationException exception) {
 				 //例外の発生
 			 }

 			 @Override
 			 public void onAuthorizationCanceled () {
 				 //ユーザーによるパスワード忘れ処理キャンセル
 			 }

 			 @Override
 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
 				 //パスワード忘れ処理の終了。この場合 accessToken と identityToken はヌル。

 			 }
 		 });
  ```
  {: codeblock}

### 詳細の変更
Cloud Directory の設定で、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を必ず**「オン (ON)」**に設定してください。LoginWidget クラスを使用して、詳細変更フローを開始します。この API は、ユーザーが Cloud Directory を ID プロバイダーとして使用することでログインする場合にのみ使用できます。
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  				 //例外の発生
  			 }

  			 @Override
  			 public void onAuthorizationCanceled () {
  				 //ユーザーによる詳細変更キャンセル
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  				 //ユーザーの認証と、新しいトークンの受信
  			 }
  		 });
   ```
   {: codeblock}

### パスワード変更
Cloud Directory の設定で、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を必ず**「オン (ON)」**に設定してください。

LoginWidget クラスを使用して、パスワード変更フローを開始します。この API は、ユーザーが Cloud Directory を ID プロバイダーとして使用することでログインした場合にのみ使用できます。

   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   				 //例外の発生
   			 }

   			 @Override
   			 public void onAuthorizationCanceled () {
   				 //ユーザーによるパスワード変更キャンセル
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   				   //ユーザーの認証と、新しいトークンの受信
   			 }
   		 });
   ```
   {: codeblock}

## iOS Swift SDK による Cloud Directory の管理


### リソース所有者パスワードを使用したログイン

エンド・ユーザーのユーザー名とパスワードを指定して、アクセス・トークンと ID トークンを取得することができます。
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

### 登録

Cloud Directory の設定で、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を必ず**「オン (ON)」**に設定してください。

LoginWidget クラスを使用して登録フローを開始します。
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

### パスワードを忘れた場合
Cloud Directory の設定で**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**と**「パスワード忘れ E メール (Forgot password email)」**を必ず**「オン (ON)」**に設定してください。

LoginWidget クラスを使用して、パスワード忘れフローを開始します。
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

### 詳細の変更

Cloud Directory の設定で、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を必ず**「オン (ON)」**に設定してください。

LoginWidget クラスを使用して、詳細変更フローを開始します。この API は、ユーザーが Cloud Directory を ID プロバイダーとして使用することでログインする場合にのみ使用できます。
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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

### パスワード変更

Cloud Directory の設定で、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を必ず**「オン (ON)」**に設定してください。

LoginWidget クラスを使用して、パスワード変更フローを開始します。この API は、ユーザーが Cloud Directory を ID プロバイダーとして使用することでログインする場合にのみ使用できます。
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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


## Node.js SDK による Cloud Directory の管理
Cloud Directory ID プロバイダーが**「オン (ON)」**に設定され、コールバック・エンドポイントを含んでいることを確認してください。

### リソース所有者パスワード・フローを使用したログイン
WebAppStrategy を使用すると、各ユーザーはユーザー名とパスワードを使用して Web アプリケーションにログインできます。
ログインに成功すると、そのユーザーのアクセス・トークンは HTTP セッションで持続し、HTTP セッションが存続している限り有効です。HTTP セッションが破棄されるか期限切れになると、トークンも破棄されます。

ユーザー名とパスワードを使用したログインをユーザーに許可するには、ユーザー名とパスワードのパラメーターを指定して呼び出す post 経路をアプリに追加します。

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // フラッシュ・メッセージの許可
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> このコマンドの構成要素について</th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> この値を、認証に成功した場合にユーザーのリダイレクト先となる URL に設定します。デフォルトは元の要求 URL です。例: <code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td> この値を、認証に失敗した場合にユーザーのリダイレクト先となる URL に設定します。デフォルトは元の要求 URL です。</td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td> Cloud Directory から返されたエラー・メッセージを受信する場合、この値を <code>true</code> に設定します。デフォルト値は false です。</td>
      </tr>
     </tbody>
  </table>


**注**:
  * HTML フォームを使用して要求を送信する場合、[body-parser](https://www.npmjs.com/package/body-parser) ミドルウェアを使用します。
  * 返されるエラー・メッセージを取得するには、[connect-flash](https://www.npmjs.com/package/connect-flash) を使用します。`web-app-sample-server.js` を参照してください。

### 登録
{{site.data.keyword.appid_short_notm}} 登録フォームを起動するには、WebAppStrategy に「show」プロパティーを渡し、それを `WebAppStrategy.SIGN_UP` に設定します。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

    **注**:
    * Cloud Directory 設定で**「ユーザーによる E メール検証なしのサインインを許可 (Allow users to sign-in without email verification)」**が**「いいえ (No)」**に設定されている場合は、{{site.data.keyword.appid_short_notm}} アクセス・トークンと ID トークンを取得せずに処理が終了します。
    * Cloud Directory 設定で、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を必ず**「オン (ON)」**に設定してください。


### パスワードを忘れた場合
{{site.data.keyword.appid_short_notm}} パスワード忘れフォームを起動するには、WebAppStrategy に `show` プロパティーを渡し、それを `WebAppStrategy.FORGOT_PASSWORD` に設定します。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

**注**:
* Cloud Directory 設定で**「ユーザーによる E メール検証なしのサインインを許可 (Allow users to sign-in without email verification)」**が**「いいえ (No)」**に設定されている場合は、{{site.data.keyword.appid_short_notm}} アクセス・トークンと ID トークンを取得せずに処理が終了します。
* Cloud Directory 設定で**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**と**「パスワード忘れ E メール (Forgot password email)」**を必ず**「オン (ON)」**に設定してください。

### 詳細の変更
{{site.data.keyword.appid_short_notm}} 詳細変更フォームを起動するには、WebAppStrategy に `show` プロパティーを渡し、それを `WebAppStrategy.CHANGE_DETAILS` に設定します。
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

**注**:
* Cloud Directory を ID プロバイダーとして使用することによってユーザーを認証する必要があります。
* Cloud Directory 設定で、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を必ず**「オン (ON)」**に設定してください。


### パスワード変更
{{site.data.keyword.appid_short_notm}} パスワード変更フォームを起動するには、WebAppStrategy に `show` プロパティーを渡し、それを `WebAppStrategy.CHANGE_PASSWORD` に設定します。
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

**注**:
* Cloud Directory を ID プロバイダーとして使用することによってユーザーを認証する必要があります。
* Cloud Directory 設定で、**「ユーザーによる登録とパスワード・リセットの許可 (Allow users to sign up and reset their password)」**を必ず**「オン (ON)」**に設定してください。
