---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 管理雲端目錄
{: #cd}

您可以將 {{site.data.keyword.appid_short_notm}} 配置為使用「雲端目錄」作為身分提供者。當使用者藉由其電子郵件及密碼登入時，他們會新增您的目錄，而且您可以從服務 GUI 管理您的使用者。
{: shortdesc}

<!--- What is a cloud directory? --->

## 管理目錄設定

您可以針對應用程式配置通知及使用者控制層次。在 GUI 的**目錄設定**標籤中，您可以決定您的使用者將能夠執行多少自我服務。

1. 若要容許使用者使用電子郵件來註冊，您必須將**容許使用者註冊及重設其密碼**設為**開啟**。當設為**關閉**時，您仍然可以透過主控台新增使用者，但僅基於開發目的。
2. 配置寄件者詳細資料。請指定將傳送訊息的電子郵件、誰將以寄件者身分出現，以及您的使用者可以回覆給誰。**附註**：當配置動作 URL，請確定您提供足夠時間，可讓使用者按一下鏈結。使用者必須驗證其電子郵件具有特定選項，例如能夠要求重設其密碼。
3. 判斷使用者接收的電子郵件類型及寄件者資訊。



## 管理訊息

範本是您可以傳送至使用者之電子郵件訊息的範例。您可以更新訊息的內容及佈置來自訂範本。您可以在目錄設定標籤中將這些訊息設為**開啟**或**關閉**。

1. 選取**訊息類型**。
2. 變更訊息的內容及設計來自訂訊息。您可以使用參數來個人化訊息。請不要忘記儲存您的變更！

### 訊息類型

<dl>
  <dt> 歡迎使用</dt>
    <dd>在使用者完成登錄之後，您可以歡迎使用者使用您的應用程式。若要歡迎並留住您的使用者，請讓您的訊息儘可能吸引人。<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/>可在任何類型之訊息中使用的參數</th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> 顯示您已針對登入小組件配置的影像。</td>
        </tr>
	 <tr>
          <td> %{display.headerColor} </td>
          <td> 顯示您已針對登入小組件配置的標頭顏色。</td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> 顯示使用者已選擇要在與應用程式互動時使用的畫面名稱。</td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> 顯示使用者的已登錄電子郵件位址。</td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> 顯示使用者的指定名字。</td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> 顯示使用者的完整名稱。</td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> 顯示使用者的指定姓氏。</td>
        </tr>
      </tbody>
    </table>

    **附註**：如果使用者未提供參數所取回的資訊，則它會出現空白。</dd>
  <dt> 忘記密碼</dt>
    <dd> 如果使用者忘記或基於任何原因而需要更新其密碼，使用者可以要求重設該密碼。您可以自訂對其要求的電子郵件回應。當使用者要求變更時，其密碼會保持不變，直到他們按一下此電子郵件中的鏈結。

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 密碼變更參數</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 顯示鏈結有效的時數。</td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 顯示鏈結有效的分鐘數。</td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> 將一次性通行碼顯示為 URL 的一部分。這將表示每一個人員都將具有不同的通行碼。範例：<code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> 顯示使用者按一下即可重設其密碼的鏈結。</td>
        </tr>
       </tbody>
    </table></dd>
  <dt> 驗證</dt>
    <dd> 您可以透過電子郵件要求使用者驗證其帳戶。藉由要求驗證，您可以限制可以登入您應用程式之偽造帳戶的數目。您可以限制應用程式的存取，直到使用者已驗證其電子郵件，或使用它作為管理您可以為哪些使用者建立設定檔的方法。<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 驗證訊息參數</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 顯示鏈結有效的時數。</td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 顯示鏈結有效的分鐘數。</td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> 顯示一次性驗證 URL。</td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> 顯示您已在設定中指定的動作 URL。</td>
        </tr>
      </tbody>
    </table></dd>
  <dt> 密碼變更</dt>
    <dd> 您可以讓使用者知道其密碼何時已更新。如果他們並未要求變更其密碼，此舉很有用。他們可以採取適當的步驟來重新保護其帳戶的安全。

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 密碼變更參數</th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> 顯示新密碼生效的時間。</td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> 顯示從中要求密碼變更的 IP 位址。</td>
        </tr>
      </tbody>
    </table></dd>
</dl>



## 使用 Android SDK 管理雲端目錄
{: #managing-android}

使用下列 API 時，務必將**雲端目錄身分提供者**設為**開啟**。

### 使用資源擁有者密碼登入
您可以藉由提供一般使用者的使用者名稱及密碼來取得存取及 ID 記號。

 ```java
 AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }
  @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //User authenticated
        }
      });
 ```
 {: codeblock}

### 註冊

確定在「雲端目錄」的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。

 使用 LoginWidget 類別來啟動註冊流程。
 ```java
 LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
      }
  @Override
        public void onAuthorizationCanceled () {
          //Sign up canceled by the user
			 }

			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			if (accessToken != null && identityToken != null) {
				     //User authenticated
				 } else {
				     //email verification is required
				 }

			 }
		 });
 ```
 {: codeblock}

### 忘記密碼
務必在「雲端目錄」的設定中，將**容許使用者註冊及重設其密碼**及**忘記密碼電子郵件**設為**開啟**。

使用 LoginWidget 類別來啟動忘記密碼流程。
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
      }
  @Override
        public void onAuthorizationCanceled () {
          //forogt password canceled by the user
 			 }

 			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//forgot password finished, in this case accessToken and identityToken will be null.

 			 }
 		 });
  ```
  {: codeblock}

### 變更詳細資料
務必在「雲端目錄」的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。請使用 LoginWidget 類別來啟動變更詳細資料流程。僅在使用者使用「雲端目錄」作為其身分提供者登入時，才能使用此 API。
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
      }
  @Override
        public void onAuthorizationCanceled () {
          //changed details canceled by the user
  			 }

  			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//User authenticated, and fresh tokens received
  			 }
  		 });
   ```
   {: codeblock}

### 變更密碼
確定在「雲端目錄」的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。

使用 LoginWidget 類別來啟動變更密碼流程。僅在使用者使用「雲端目錄」作為其身分提供者登入時，才能使用此 API。

   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
      }
  @Override
        public void onAuthorizationCanceled () {
          //change password canceled by the user
   			 }

   			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//User authenticated, and fresh tokens received
   			 }
   		 });
   ```
   {: codeblock}

## 使用 iOS Swift SDK 管理雲端目錄


### 使用資源擁有者密碼登入

您可以藉由提供一般使用者的使用者名稱及密碼來取得存取及 ID 記號。
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}

### 註冊

確定在「雲端目錄」的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。

使用 LoginWidget 類別來啟動註冊流程。
  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

### 忘記密碼
確定在「雲端目錄」的設定中，將**容許使用者註冊及重設其密碼**及**忘記密碼電子郵件**設為**開啟**。

使用 LoginWidget 類別來啟動忘記密碼流程。
  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

### 變更詳細資料

確定在「雲端目錄」的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。

使用 LoginWidget 類別來啟動變更詳細資料流程。僅在使用者使用「雲端目錄」作為其身分提供者登入時，才能使用此 API。
  ```swift

  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

### 變更密碼

確定在「雲端目錄」的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。

使用 LoginWidget 類別來啟動變更密碼流程。僅在使用者使用「雲端目錄」作為身分提供者登入時，才能使用此 API。
  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}


## 使用 Node.js SDK 管理雲端目錄
確定將「雲端目錄」身分提供者設為**開啟**，並包含回呼端點。

### 使用資源擁有者密碼登入流程
WebAppStrategy 容許使用者可以使用其使用者名稱及密碼登入您的 Web 應用程式。
在成功登入之後，使用者的存取記號會持續保存在 HTTP 階段作業中，而且只要 HTTP 階段作業保持作用中，就可以一直使用該存取記號。一旦 HTTP 階段作業遭到破壞或過期，記號也會遭到破壞。

若要容許使用者可以使用其使用者名稱及密碼登入，請在您的應用程式中加入將透過使用者名稱及密碼參數呼叫的公布路徑。

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> 瞭解此指令元件</th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> 將此值設為您想要在成功鑑別之後將使用者重新導向至其中的 URL。預設值為原始要求 URL。範例：<code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td> 將此值設為若其鑑別失敗，您想要將使用者重新導向至其中的 URL。預設值為原始要求 URL。</td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td> 將此值設為 <code>true</code>，來接收從「雲端目錄」傳回的錯誤訊息。預設值為 false。</td>
      </tr>
     </tbody>
  </table>


**附註**：
  * 如果您使用 HTML 表單提交要求，請使用 [body-parser](https://www.npmjs.com/package/body-parser) 中介軟體。
  * 使用 [connect-flash](https://www.npmjs.com/package/connect-flash) 來取得傳回的錯誤訊息。請參閱 `web-app-sample-server.js`。

### 註冊
若要啟動 {{site.data.keyword.appid_short_notm}} 註冊表單，請傳遞 WebAppStrategy "show" 內容，並將其設為 `WebAppStrategy.SIGN_UP`。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

    **附註**：
    * 如果在您的「雲端目錄」設定中，**容許使用者無需電子郵件驗證即可登入**設為**否**，則處理程序會結束，而不會擷取 {{site.data.keyword.appid_short_notm}} 存取及 ID 記號。
    * 務必在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。


### 忘記密碼
若要啟動 {{site.data.keyword.appid_short_notm}} 忘記密碼表單，請傳遞 WebAppStrategy `show` 內容，並將其設為 `WebAppStrategy.FORGOT_PASSWORD`。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

**附註**：
* 如果在您的「雲端目錄」設定中，**容許使用者無需電子郵件驗證即可登入**設為**否**，則處理程序會結束，而不會擷取 {{site.data.keyword.appid_short_notm}} 存取及 ID 記號。
* 務必在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**及**忘記密碼電子郵件**設為**開啟**。

### 變更詳細資料
若要啟動 {{site.data.keyword.appid_short_notm}} 變更詳細資料表單，請傳遞 WebAppStrategy `show` 內容，並將其設為 `WebAppStrategy.CHANGE_DETAILS`。
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

**附註**：
* 必須使用「雲端目錄」作為身分提供者來鑑別使用者。
* 務必在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。


### 變更密碼
若要啟動 {{site.data.keyword.appid_short_notm}} 變更密碼表單，請傳遞 WebAppStrategy `show` 內容，並將其設為 `WebAppStrategy.CHANGE_PASSWORD`。
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

**附註**：
* 必須使用「雲端目錄」作為身分提供者來鑑別使用者。
* 務必在「雲端目錄」設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
