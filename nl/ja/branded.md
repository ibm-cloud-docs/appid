---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, customizing apps, directory, registry, 

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

# アプリのブランド設定
{: #branded}

独自のカスタマイズ画面を表示し、独自のフローを使用し、{{site.data.keyword.appid_full}} の認証機能と許可機能を利用することができます。 クラウド・ディレクトリーを ID プロバイダーとして使用すると、ユーザーとアプリの対話が簡単になります。 サインイン、登録、パスワードの変更などを、支援を頼まずに各自で行うことができます。
{: shortdesc}


## 画面の再利用について
{: #branded-understand}

既にある独自の UI をアプリで再利用すると、統一性のあるサインイン・フローを作成できます。 同じ画像、色、ブランド設定を使用するなら、ユーザーはアプリと直接対話していないときでさえ、ブランドを認識しやすくなります。

### 独自の画面を使用するにあたって何か条件はありますか?
{: #branded-requirements}


独自の UI を表示するには、ID プロバイダーとして [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) を使用する必要があります。クラウド・ディレクトリーを[構成](/docs/services/appid?topic=appid-cloud-directory)する方法はいくつかあります。 送信するメッセージのタイプを決定し、コンテンツとデザインをカスタマイズすることができます。 どんなメッセージを使用すればよいでしょうか? 問題ありません。 GUI には、使用できるメッセージの例があります。


英語以外の[言語](/docs/services/appid?topic=appid-cd-messages#cd-languages)を使用する必要がありますか? <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization" target="_blank">言語管理 API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して別の言語を選択し、翻訳された独自のコンテンツを表示することができます。
{: tip}


### 独自の画面のいくつかとデフォルトの画面のいくつかを使用することはできますか?
{: #branded-hybrid}

はい。 独自の画面のいくつかとデフォルトの画面のいくつかを使用するハイブリッド・フローを作成できます。ただし、使用できる選択肢は、1 つのフローにつき 1 つだけです。例として、独自のサインイン画面を使用するとともに、デフォルトの登録画面を使用することもできます。ただし、デフォルトの登録画面を使用することを選択した場合は、登録の検証を含め、登録フロー全体を通してデフォルトを使い続ける必要があります。

### 各フローは技術的にどのように異なっていますか?
{: #branded-technically}

このサービスでは、OAuth 2.0 付与フローを使用して許可プロセスをマップします。 Facebook などのソーシャル ID プロバイダーを構成する場合は、<a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html" target="_blank">許可付与フロー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用してログイン・ウィジェットが呼び出されます。 独自の画面を使用する場合は、<a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html" target="_blank">リソース所有者のパスワード資格情報フロー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して、アクセス・トークンと識別トークンを提供して画面の呼び出しを可能にします。



### 例
{: #branded-examples}

はい。 以下のいずれかのサンプルを参照して、クラウド・ディレクトリーが機能する様子を確認してください。

* <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="_blank">Use your own branded UI for user sign-in with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/use-ui-flows-user-sign-sign-app-id/" target="_blank">Use your own UI and Flows for User Sign-Up and Sign-in with with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/custom-login-page-app-id-integration/" target="_blank">Use a custom login page with  {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>


## Android SDK によるアプリのブランド設定
{: #branded-ui-android}

クラウド・ディレクトリーを有効にした場合は、Android SDK を使用してカスタマイズした画面を呼び出せます。 ユーザーの対話に使用できるようにする画面の組み合わせを選択できます。詳しい例については、<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">このブログ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"> を確認してください</a>。
{: shortdesc}



### サインイン
{: #branded-android-sign-in}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。
2. 以下のコードをアプリケーションに追加します。 ユーザーがカスタム画面でサインインをクリックすると、サインイン・フローがトリガーされます。 エンド・ユーザーのユーザー名とパスワードを指定して、アクセス・トークン、識別トークン、リフレッシュ・トークンを取得します。

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
</br>

## iOS Swift SDK によるアプリのブランド設定
{: #branded-ui-ios-swift}

クラウド・ディレクトリーを有効にした場合は、[iOS Swift SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift) を使用して独自のブランド・マークがついた画面を呼び出せます。
{: shortdesc}

</br>

### サインイン
{: #branded-ios-sign-in}

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。
2. 以下のコードをアプリケーションに挿入します。 ユーザーがサインインしようとすると、カスタマイズされた画面が呼び出され、カスタマイズされたサインイン・ページで許可および認証のプロセスが開始します。

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
  {: codeblock}


## Node.js SDK によるアプリのブランド設定
{: #branding-ui-nodejs}

Cloud Directory を有効にした場合は、Node.js SDK を使用してカスタマイズした画面を呼び出せます。
{: shortdesc}

### サインイン
{: #branded-node-sign-in}

`WebAppStrategy` を使用すると、ユーザーはユーザー名とパスワードで Web アプリにサインインできます。 ユーザーがアプリに正常にサインインすると、アクセス・トークンは、HTTP セッションが存続している限り、そのセッションで持続します。 HTTP セッションが閉じられるか期限切れになると、アクセス・トークンも破棄されます。


1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。
2. 以下のコードをアプリケーションに挿入します。 ユーザーがサインインしようとすると、カスタマイズされた画面が呼び出され、許可および認証のプロセスが開始します。

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
        <td><code>true</code> に設定した場合、Cloud Directory サービスからエラー・メッセージが返されます。 デフォルトでは、値は <code>false</code> に設定されています。</td>
      </tr>
    </tbody>
  </table>

**注**: HTML で要求を送信する場合、<a href="https://www.npmjs.com/package/body-parser" target="blank">body parser <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> ミドルウェアを使用することができます。 返されたエラー・メッセージを参照するには、<a href="https://www.npmjs.com/package/connect-flash" target="blank">connect-flash <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用することができます。 実際に機能する様子を確認するには、<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js" target="blank">web app sample <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。


## API によるアプリのブランド設定
{: #branded-ui-api}

独自のカスタマイズ画面を表示して、{{site.data.keyword.appid_short_notm}} の認証機能と許可機能を利用することができます。 Cloud Directory を ID プロバイダーとして使用する場合、ユーザーとアプリの対話が簡単になります。 サインイン、登録、パスワードのリセットなどを、支援を頼まずに各自で行うことができます。
{: shortdesc}

これを可能にするために、{{site.data.keyword.appid_short_notm}} は REST API を公開しています。 REST API を使用して、Web アプリにサービスを提供するバックエンド・サーバーを構築したり、独自のカスタム画面を使用してモバイル・アプリと対話したりできます。

管理 API は、IBM Cloud Identity and Access Management で生成されたトークンで保護されます。これは、各サービス・インスタンスに対してチームの誰がどのレベルのアクセス権限を持つかをアカウント所有者が指定できるということを意味します。IAM と {{site.data.keyword.appid_short_notm}} の連動方法について詳しくは、[サービス・アクセス管理](/docs/services/appid?topic=appid-service-access-management#service-access-management)を参照してください。

[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成したら、以下のエンドポイントを呼び出して各画面を表示できます。

### 登録
{: #branded-api-signup}

`/sign_up` エンドポイントを使用して、各ユーザーが自分でアプリに登録できるようにします。
要求本体に以下のデータを指定します。
  * tenantID。
  * クラウド・ディレクトリーのユーザー・データ。 詳しくは、[SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) を参照してください。
    * `password` 属性。
    * `true` に設定された `primary` 属性のある email 配列に、少なくとも 1 つの E メール・アドレスが必要です。

[E メール構成](/docs/services/appid?topic=appid-cd-messages#cd-messages)に応じて、ユーザーは確認の要求を受け取るか、アプリへの登録時のウェルカム・メールを受け取るか、その両方を受け取ります。 どちらのタイプの E メールも、ユーザーがアプリに登録したときにトリガーされます。 確認メールには、ユーザーがクリックすることによって同一性を確認できるリンクが用意されています。クリックすると、確認操作に対する感謝、または確認の完了を伝える画面が表示されます。  

独自に用意した確認後のページを表示するには、以下のようにします。

1. {site.data.keyword.appid_short_notm}} ダッシュボードでクラウド・ディレクトリー ID プロバイダーにナビゲートします。
2. **「E メールの検証」**タブをクリックします。
3. **「カスタム検証ページの URL」**に、独自のランディング・ページの URL を入力します。

この値を指定した場合、{{site.data.keyword.appid_short_notm}} はその URL を `context` 照会とともに呼び出します。 `/sign_up/confirmation_result` エンドポイントを呼び出し、受け取った `context` パラメーターを渡すと、その結果から、各ユーザーが自分のアカウントを確認したかどうかが分かります。 確認が済んでいる場合は、独自のカスタム・ページを表示できます。


### パスワードを忘れた場合
{: #branded-api-forgot-password}

`/forgot_password` エンドポイントを使用して、ユーザーがパスワードを忘れた場合に自分でパスワードを回復できるようにします。

要求本体に以下のデータを指定します。
  * tenantID。
  * クラウド・ディレクトリー・ユーザーの E メール。

このエンドポイントが呼び出されると、パスワード・リセット E メールがユーザーに送信されます。 この E メールには**「リセット (Reset)」**ボタンがあります。 このボタンをユーザーが押すと、パスワードを再設定できる画面が {{site.data.keyword.appid_short_notm}} によって表示されます。

独自に用意したパスワード・リセット後のページを表示するには、以下のようにします。

1. GUI でクラウド・ディレクトリーの[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)を構成します。 **「ユーザーがアプリケーションからアカウントを管理できるようにする」**を**「オン」**に設定する必要があります。
2. サービス・ダッシュボードの**「パスワードの再設定」**タブで、**「パスワード再設定の E メール」**が**「オン」**に設定されていることを確認します。
3. 独自のランディング・ページの URL を**「カスタム・パスワード・リセット・ページの URL (URL for your custom reset password page)」**に入力します。  

この値を指定した場合、{{site.data.keyword.appid_short_notm}} はその URL を `context` 照会とともに呼び出します。 `/forgot_password/confirmation_result` を呼び出すと、この `context` パラメーターを使用して結果を受け取ることができます。 正常な結果が得られた場合は、独自のカスタム・ページを表示できます。

ランダムなストリングをカスタム・パスワード・リセット・ページに追加し、要求の送信時にそれをバックエンドに渡すようにしてください。 そのストリングをハンドラーで検証し、それが有効である場合のみ `/change_password` エンドポイントを呼び出すようにします。 そうすることで、バックエンドのパスワード・リセット・エンドポイントの脆弱性を減らすことができます。
{: tip}


### パスワードの変更
{: #branded-api-change-password}

`/change_password` エンドポイントには、2 種類の使用方法があります。 ユーザーがリセット要求を送信する場合と、ユーザーがアプリにサインインしてパスワードの更新を要求する場合です。

リセット要求後にパスワードを更新するには、要求本体に以下のデータを指定します。
  * tenantID。
  * ユーザーの新規パスワード
  * クラウド・ディレクトリー・ユーザーの UUID。
  * オプション: パスワード・リセットの実行元となる IP アドレス。 IP アドレスを渡す場合は、パスワード変更 E メールのテンプレートでプレースホルダー `%{passwordChangeInfo.ipAddress}` を使用できます。

構成によっては、パスワードが変更されると、{{site.data.keyword.appid_short_notm}} は、変更が行われたことを通知する E メールを該当ユーザーに送信します。


ユーザーがアプリへのサインイン中に自分でパスワードを変更できるようにするには、以下のようにします。

要求本体に以下のデータを指定します。
  * tenantID。
  * ユーザーの新規パスワード
  * クラウド・ディレクトリー・ユーザーの UUID。

パスワード変更ページでは、ユーザーに対して現在のパスワードと新規パスワードを入力するように求める必要があります。
{: tip}

バックエンドで ROP API を使用してユーザーの現在のパスワードが検証され、それが有効であった場合は、新規パスワードを使用してこのエンドポイントが呼び出されます。 構成によっては、パスワードが変更されると、変更があったことを該当ユーザーに通知する E メールを {{site.data.keyword.appid_short_notm}} で送信することもできます。


### 再送
{: #branded-api-resend}

`/resend/{templateName}` を使用して、何らかの理由でユーザーが E メールを受信しなかった場合に、それを再送することができます。

要求本体に以下のデータを指定します。
  * tenantID。
  * テンプレート名
  * クラウド・ディレクトリー・ユーザーの UUID。

### 変更の詳細
{: #branded-api-change-details}

ユーザーは、アプリにサインインしているときに、ユーザー情報の一部を自分で更新することができます。 そのような情報は、`/Users/{userId}` で取得して更新できます。

ユーザー詳細が更新されると、このエンドポイントは、更新されたユーザー・データを [SCIM 形式](https://tools.ietf.org/html/rfc7643#section-8.2)で要求本体から取得します。 関連する詳細のみを変更するようにしてください。

ユーザーの E メール・アドレスは変更できません。
{: tip}
