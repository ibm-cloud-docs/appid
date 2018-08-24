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

# 將您的應用程式加上品牌
{: #branding}

您可以顯示自己的自訂畫面，並充分運用 {{site.data.keyword.appid_full}} 的鑑別及授權功能。使用「雲端目錄」作為身分提供者，使用者就可以在您提供較少協助的情況下，與您的應用程式互動。他們可以登入、註冊、變更其密碼及其他作業，而不需要要求協助。
{: shortdesc}

當您使用自己的畫面時，[資源擁有者密碼認證流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)即可用來提供存取及身分記號。


## 使用 iOS Swift SDK 將應用程式加上品牌
{: #branded-ui-ios-swift}

啟用「雲端目錄」之後，即可使用 iOS Swift SDK 來呼叫您自己的品牌畫面。
{: shortdesc}

</br>
**登入**

1. 在 GUI 的身分提供者標籤中，將「雲端目錄」設為**開啟**。
2. 呼叫登入小組件來啟動登入流程。當使用者嘗試使用其使用者名稱或電子郵件及密碼來登入時，即會取得存取及身分記號。
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: pre}

</br>

**註冊**

1. 在 GUI 的身分提供者標籤中，將「雲端目錄」設為**開啟**。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 呼叫登入小組件來啟動註冊流程。
  ```swift
class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
       if accessToken == nil && identityToken == nil {
        //email verification is required
        return
       }
     //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Sign up canceled by the user
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: pre}

</br>

**忘記密碼**

1. 在 GUI 的身分提供者標籤中，將「雲端目錄」設為**開啟**。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 呼叫登入小組件來啟動忘記密碼流程。
  ```swift
class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
        //forgot password finished, in this case accessToken and identityToken will be null.
     }

     public func onAuthorizationCanceled() {
         //forgot password canceled by the user
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: pre}

</br>

**變更詳細資料**

1. 在 GUI 的身分提供者標籤中，將「雲端目錄」設為**開啟**。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 呼叫登入小組件來啟動變更詳細資料流程。
  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //changed details canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>

**變更密碼**

1. 在 GUI 的身分提供者標籤中，將「雲端目錄」設為**開啟**。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 呼叫登入小組件來啟動變更詳細資料流程。
  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //change password canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
           //Exception occurred
      }
  }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}

</br>


## 使用 Android SDK 將應用程式加上品牌
{: #branded-ui-android}

啟用雲端目錄之後，即可使用 Android SDK 來呼叫自訂的畫面。您可以選擇您要使用者可與之互動的畫面組合。<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">如需詳細範例，請參閱此部落格 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>！
{: shortdesc}

</br>

**登入**

1. 以身分提供者身分，將**雲端目錄**設為**開啟**。
2. 提供一般使用者的使用者名稱及密碼，來取得存取、身分及重新整理記號。
3. 呼叫登入小組件來啟動登入流程。
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }
  @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //User authenticated
        }
      });
  ```
  {: pre}

</br>

**註冊**

1. 以身分提供者身分，將**雲端目錄**設為**開啟**。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 呼叫登入小組件來啟動註冊流程。
  ```java
 LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }
  @Override
        public void onAuthorizationCanceled () {
          //Sign up canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            if (accessToken != null && identityToken != null) {
				     //User authenticated
          } else {
              //email verification is required
          }
      }
  });
  ```
  {: pre}

</br>


**忘記密碼**

1. 以身分提供者身分，將**雲端目錄**設為**開啟**。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 呼叫登入小組件來啟動忘記密碼流程。
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }
  @Override
        public void onAuthorizationCanceled () {
          // Forogt password canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            // Forgot password finished, in this case accessToken and identityToken will be null.
      }
  });
  ```
  {: pre}

</br>

**變更詳細資料**

1. 以身分提供者身分，將**雲端目錄**設為**開啟**。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 呼叫登入小組件來啟動變更詳細資料流程。
  ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          // Exception occurred
      }

      @Override
        public void onAuthorizationCanceled () {
          // Changed details canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            // User authenticated, and fresh tokens received
      }
  });
  ```
  {: pre}


</br>

**變更密碼**

1. 以身分提供者身分，將**雲端目錄**設為**開啟**。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 呼叫登入小組件來啟動變更密碼流程。
  ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          // Exception occurred
      }

      @Override
        public void onAuthorizationCanceled () {
          // Change password canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            // User authenticated, and fresh tokens received
      }
  });
  ```
  {: pre}

</br>
</br>


## 使用 Node.js SDK 將應用程式加上品牌
{: #branded-ui-nodejs}

啟用「雲端目錄」之後，即可使用 Node.js SDK 來呼叫自訂的畫面。
{: shortdesc}

**登入**

藉由使用 WebAppStrategy，使用者可以利用其使用者名稱和密碼來登入您的 Web 應用程式。在使用者順利登入您的應用程式之後，只要 HTTP 階段作業保持作用中，他們的存取記號就會持續保存在 HTTP 階段作業中。HTTP 階段作業關閉或過期之後，也會破壞存取記號。

1. 在身分提供者設定中，將「雲端目錄」設為**開啟**，並指定回呼端點。
2. 將張貼路徑新增至可利用使用者名稱及密碼參數所呼叫的應用程式，並使用資源擁有者密碼流程登入。
  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: pre}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 指令參數</th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>在成功鑑別之後，您要將使用者重新導向至其中的 URL。</td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>鑑別失敗時，您要將使用者重新導向至其中的 URL。</td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td>設為 <code>true</code> 時，會從「雲端目錄」服務傳回錯誤訊息。依預設，值會設為 <code>false</code>。</td>
      </tr>
    </tbody>
  </table>

  1. 如果您以 HTML 表單提交要求，則可以使用[主體剖析器](https://www.npmjs.com/package/body-parser)中介軟體。
  2. 若要取得傳回的錯誤訊息，您可以使用 [connect-flash](https://www.npmjs.com/package/connect-flash)。如需相關資訊，請參閱 [Web 應用程式範例](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js)。
  {: tip}

</br>
**註冊**

1. 在身分提供者設定中，將「雲端目錄」設為**開啟**，並指定回呼端點。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 將**容許使用者無需電子郵件驗證即可登入**設為**否**。否則，無法擷取 {{site.data.keyword.appid_short_notm}} 存取及身分記號。
4. 將張貼路徑新增至可利用使用者名稱及密碼參數所呼叫的應用程式，並使用資源擁有者密碼流程登入。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**忘記密碼**

1. 在身分提供者設定中，將「雲端目錄」設為**開啟**，並指定回呼端點。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 將**忘記密碼電子郵件**設為**開啟**。
4. 將 *show* 內容傳遞至 `WebAppStrategy.FORGOT_PASSWORD`，以啟動忘記密碼表單。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**變更詳細資料**

1. 在身分提供者設定中，將「雲端目錄」設為**開啟**，並指定回呼端點。
2. 在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
3. 驗證使用者先前已使用 {{site.data.keyword.appid_short_notm}} 進行鑑別。
4. 將 *show* 內容傳遞至 `WebAppStrategy.CHANGE_DETAILS`，以啟動忘記密碼表單。
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## 使用 API 將應用程式加上品牌
{: #branded-ui-api}

您可以顯示自己的自訂畫面，並充分運用 {{site.data.keyword.appid_short_notm}} 的鑑別及授權功能。使用雲端目錄作為身分提供者，使用者就可以在您提供較少協助的情況下，與您的應用程式互動。他們可以登入、註冊、重設其密碼及其他作業，而不需要要求協助。
{: shortdesc}

為了使此動作可行，{{site.data.keyword.appid_short_notm}} 會公開 REST API。您可以使用 REST API 來建置用於服務 Web 應用程式的後端伺服器，或使用您自己的自訂畫面與行動應用程式互動。

管理 API 是使用 IBM Cloud Identity and Access Management 產生的記號來保護。這表示帳戶擁有者可以指定其團隊成員對每一個服務實例的存取層次。如需 IAM 與 {{site.data.keyword.appid_short_notm}} 如何合作的相關資訊，請參閱[服務存取管理](/docs/services/appid/iam.html)。

在您配置[設定](/docs/services/appid/cloud-directory.html)之後，即可呼叫下列端點來顯示每個畫面。


**註冊**
您可以使用 `/sign_up` 端點，容許使用者自行註冊您的應用程式。
在要求內文中提供下列資料：
  * 您的承租戶 ID。
  * 雲端目錄使用者資料。如需詳細資料，請參閱 [SCIM 完整使用者呈現](https://tools.ietf.org/html/rfc7643#section-8.2)。
    * `password` 屬性。
    * 在 `primary` 屬性設為 `true` 的電子郵件陣列中，您必須至少具有 1 個電子郵件位址。

取決於您的[電子郵件配置](/docs/services/appid/cloud-directory.html)，使用者可能會收到一個驗證要求，或一封在他們註冊您的應用程式時歡迎他們的電子郵件。當使用者註冊您的應用程式時，會觸發這兩種類型的電子郵件。驗證電子郵件包含**驗證**按鈕。在他們按下按鈕並確認其身分之後，{{site.data.keyword.appid_short_notm}} 即會顯示一個畫面，感謝他們進行驗證。  

您可以呈現自己的後置驗證頁面：

1. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的**自訂登入頁面**標籤。
2. 在**自訂電子郵件位址驗證頁面的 URL** 中輸入登入頁面的 URL

當提供此值時，{{site.data.keyword.appid_short_notm}} 會呼叫 URL 以及 `context` 查詢。當您呼叫 `/sign_up/confirmation_result` 端點，並傳遞收到的 `context` 參數時，結果會告知您的使用者是否已驗證其帳戶。如果已驗證，則您可以顯示自訂頁面。

</br>
**忘記密碼**

您可以使用 `/forgot_password` 端點，容許使用者萬一忘記其密碼時可以予以回復。

在要求內文中提供下列資料：
  * 您的承租戶 ID。
  * 雲端目錄使用者的電子郵件。

呼叫端點時，會將重設密碼電子郵件傳送給使用者。此電子郵件包含**重設**按鈕。在他們按下按鈕之後，{{site.data.keyword.appid_short_notm}} 即會顯示一個畫面，容許他們重設其密碼。

您可以呈現自己的後置重設密碼頁面：

1. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的**自訂登入頁面**標籤。
2. 在**自訂重設密碼頁面的 URL** 中輸入登入頁面的 URL  

當提供此值時，{{site.data.keyword.appid_short_notm}} 會呼叫 URL 以及 `context` 查詢。呼叫 `/forgot_password/confirmation_result` 時，會使用 `context` 參數來接收結果。如果結果成功，則您可以顯示自訂頁面。

將隨機字串新增至您的自訂重設密碼頁面，並在提交要求時將它傳遞給您的後端。讓您的處理程式驗證字串，並只在 `/change_password` 端點有效時，才會呼叫它。這樣做可以減少後端重設密碼端點的漏洞。
{: tip}

</br>
**變更密碼**

您可以採用兩種方式來使用 `/change_password` 端點。當使用者提交重設要求時，或當使用者登入您的應用程式，並想要更新其密碼時。

在重設要求之後，於要求內文中提供下列資料來更新其密碼：
  * 您的承租戶 ID。
  * 使用者的新密碼
  * 雲端目錄使用者 UUID。
  * 選用項目：從中執行密碼重設的 IP 位址。如果您選擇傳遞 IP 位址，則位置保留元 `%{passwordChangeInfo.ipAddress}` 可供變更密碼電子郵件範本使用。

取決於您的配置，當密碼變更時，{{site.data.keyword.appid_short_notm}} 可能會傳送電子郵件給使用者，讓他們知道發生變更。

</br>
若要容許使用者在登入您的應用程式時變更其密碼，請執行下列動作：

在要求內文中提供下列資料：
  * 您的承租戶 ID。
  * 使用者的新密碼
  * 雲端目錄使用者 UUID。

您的變更密碼頁面應該會提示使用者輸入其現行密碼及其新密碼。
{: tip}

您的後端會使用 ROP API 來驗證使用者的現行密碼，如果有效，則會使用新密碼來呼叫端點。取決於您的配置，當密碼變更時，{{site.data.keyword.appid_short_notm}} 可能會傳送電子郵件給使用者，讓他們知道發生變更。

</br>
**重新傳送**

當使用者因某種原因而未接收到電子郵件時，您可以使用 `/resend/{templateName}` 來重新傳送電子郵件。

在要求內文中提供下列資料：
  * 承租戶 ID。
  * 範本名稱
  * 雲端目錄使用者 UUID。


**變更詳細資料**

當使用者登入您的應用程式時，他們可以更新其部分資訊。您可以使用 `/Users/{userId}` 來取得及更新其資訊。

更新使用者詳細資料時，端點會以 [SCIM 格式](https://tools.ietf.org/html/rfc7643#section-8.2)取得要求內文中更新的使用者資料。請確定您只變更相關的詳細資料。

無法變更其電子郵件位址。
{: tip}
