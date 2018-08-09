---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# サインイン操作環境のブランド設定
{: #branding}

独自のカスタマイズ画面を表示して、{{site.data.keyword.appid_full}} の認証機能と許可機能を利用することができます。クラウド・ディレクトリーを ID プロバイダーとして使用する場合、ユーザーとアプリの対話が簡単になります。 ユーザーは、支援を求めずにサインインできます。
{: shortdesc}

独自の画面を使用する場合は、[リソース所有者のパスワード資格情報フロー](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)を使用してアクセス・トークンと識別トークンを提供します。


## Android SDK を使用してカスタマイズした画面の表示
{: #branded-ui-android}

クラウド・ディレクトリーを有効にした場合は、Android SDK を使用してカスタマイズした画面を呼び出せます。  <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">このブログを参照してください。<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //ユーザーの認証
        }
         });
  ```
  {: pre}

</br>
</br>

## iOS Swift SDK を使用してカスタマイズした画面の表示
{: #branded-ui-ios-swift}

クラウド・ディレクトリーを有効にした場合は、iOS Swift SDK を使用してカスタマイズ画面を呼び出せます。
{: shortdesc}

</br>
**サインイン**

1. GUI の ID プロバイダーのタブで、クラウド・ディレクトリーを**「オン (On)」**に設定します。
2. リソース所有者のパスワードを使用してログインします。 ユーザーがユーザー名とパスワードを使用してログインしようとすると、アクセス・トークンと識別トークンが取得されます。
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
      //ユーザーの認証
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //例外の発生
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: pre}


</br>
</br>

## Node.js SDK を使用してカスタマイズした画面の表示
{: #branded-ui-nodejs}

クラウド・ディレクトリーを有効にした場合は、Node.js SDK を使用してカスタマイズした画面を呼び出せます。
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

