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

# 將登入體驗加上品牌
{: #branding}

您可以顯示自己的自訂使用者介面，同時利用 {{site.data.keyword.appid_full}} 的鑑別及授權功能。使用雲端目錄作為身分提供者，使用者就可以在您提供較少協助的情況下，與您的應用程式互動。他們可以登入、註冊、變更其密碼及其他作業，而不需要要求協助。
{: shortdesc}

使用雲端目錄作為身分提供者，會使用[資源擁有者密碼認證流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)來提供存取及身分記號。

**附註**：雲端目錄是唯一配置的選項時，您只可以啟動自訂登入頁面。如果您有任何其他身分提供者設為**開啟**，則會顯示預先配置的登入畫面。

## 使用 Android SDK 顯示自訂的畫面
{: #branded-ui-android}

啟用雲端目錄之後，即可使用 Android SDK 來呼叫自訂的畫面。您可以選擇您要使用者可與之互動的畫面組合。<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">請查看我們的部落格！<img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>
{: shortdesc}

</br>
**登入**

1. 以身分提供者身分，將**雲端目錄**設為**開啟**。
2. 在您的程式碼中放置下列指令。
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

</br>
**註冊**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 呼叫 LoginWidget 來啟動註冊流程。
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
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			if (accessToken != null && identityToken != null) {
				     } else {
  			 }

  		 }
  	 });
  ```
  {: codeblock}

</br>
**忘記密碼**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**及**忘記密碼電子郵件**設為**開啟**。
2. 呼叫 LoginWidget 來啟動忘記密碼流程。
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
**帳戶詳細資料**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 呼叫 LoginWidget 來啟動變更詳細資料流程。
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
**變更密碼**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 呼叫 LoginWidget 來啟動變更密碼流程。
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

## 使用 iOS Swift SDK 顯示自訂的畫面
{: #branded-ui-ios-swift}

啟用雲端目錄之後，即可使用 iOS Swift SDK 來呼叫自訂的畫面。您可以選擇您要使用者可與之互動的畫面組合。
{: shortdesc}

</br>
**登入**

1. 在 GUI 的身分提供者標籤中，將雲端目錄設為**開啟**。
2. 使用資源擁有者密碼登入。您可以藉由提供一般使用者的使用者名稱及密碼來取得存取及 ID 記號。
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

</br>
**註冊**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 呼叫 LoginWidget 來啟動註冊流程。
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

</br>
**忘記密碼**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**及**忘記密碼電子郵件**設為**開啟**。
2. 呼叫 LoginWidget 來啟動忘記密碼流程。
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

</br>
**帳戶詳細資料**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 呼叫 LoginWidget 來啟動變更詳細資料流程。
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
**變更密碼**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 呼叫 LoginWidget 來啟動變更密碼流程。
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

## 使用 Node.js SDK 顯示自訂的畫面
{: #branded-ui-nodejs}

啟用雲端目錄之後，即可使用 Node.js SDK 來呼叫自訂的畫面。您可以選擇您要使用者可與之互動的畫面組合。
{: shortdesc}

**登入**
1. 在身分提供者設定中，將雲端目錄設為**開啟**，並指定回呼端點。
2. 將張貼路徑新增至可利用使用者名稱及密碼參數所呼叫的應用程式，並使用資源擁有者密碼登入。
    **附註**：`WebAppStrategy` 可讓使用者利用使用者名稱及密碼登入 Web 應用程式。登入成功之後，使用者的存取記號會儲存在 HTTP 階段作業中，並且可以在階段作業持續時間內使用。只要 HTTP 階段作業遭到破壞或過期，記號就不再有效。
    ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
    {: codeblock}

</br>
**註冊**

1. 在雲端目錄設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。如果這設為否，則處理程序會結束，而不會擷取存取及身分記號。
2. 傳遞 WebAppStrategy `show` 內容，並將其設為 `WebAppStrategy.SIGN_UP`。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>
**忘記密碼**

1. 在雲端目錄設定中，將**容許使用者註冊及重設其密碼**及**忘記密碼電子郵件**設為**開啟**。如果這設為否，則處理程序會結束，而不會擷取存取及身分記號。
2. 傳遞 WebAppStrategy `show` 內容，並將其設為 `WebAppStrategy.FORGOT_PASSWORD`。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>
**帳戶詳細資料**
1. 在雲端目錄設定中，將**容許使用者註冊及重設其密碼**設為**開啟**
2. 傳遞 WebAppStrategy `show` 內容，並將其設為 `WebAppStrategy.CHANGE_DETAILS`。
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>
**變更密碼**
1. 在雲端目錄設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 傳遞 WebAppStrategy `show` 內容，並將其設為 `WebAppStrategy.CHANGE_PASSWORD`。
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
