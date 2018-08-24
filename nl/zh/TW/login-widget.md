---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="blank"}
{:shortdesc: .shortdesc}


# 顯示預設畫面
{: #default}

{{site.data.keyword.appid_full}} 提供登入小組件，可讓您提供使用者安全的登入選項。
{: shortdesc}

將您的應用程式配置為使用身分提供者時，登入小組件即會將您應用程式的訪客導向至登入畫面。作為預設值，只有在將一個提供者設為**開啟**時，才會將訪客重新導向至該身分提供者鑑別畫面。使用登入小組件，您可以顯示預設登入畫面，或使用雲端目錄，您可以重複使用現有的使用者介面。而且，附加價值是您可以隨時更新登入流程，而無需以任何方式變更您的原始碼！


服務會使用 OAuth 2 授權類型來對映授權處理程序。當您配置社交身分提供者（例如 Facebook）時，[Oauth2 授權授與流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)是用來呼叫登入小組件。

想要建立您應用程式特有的體驗嗎？您可以[帶入自己的畫面](/docs/services/appid/branded.html)！
{: tip}


## 自訂預設登入畫面
{: #login-widget}

您可以自訂預先配置的登入畫面，以顯示您選擇的標誌及顏色。
{: shortdesc}

若要自訂畫面，請執行下列動作：

1. 開啟 {{site.data.keyword.appid_short_notm}} 服務儀表板。
2. 選取**登入自訂作業**區段。您可以修改登入小組件的外觀，以符合公司品牌。
3. 選取本端系統中的 PNG 或 JPG 檔案，以上傳公司的標誌。建議的影像大小是 320 x 320 像素。檔案大小上限是 100 KB。
4. 從顏色選取器中選取小組件的標頭顏色，或輸入另一個顏色的十六進位碼。
5. 檢查預覽窗格，然後在滿意自訂時按一下**儲存變更**。即會顯示一則確認訊息。
6. 在瀏覽器中，重新整理登入頁面，以驗證您的變更。


## 規劃要顯示的畫面
{: #plan}

{{site.data.keyword.appid_short_notm}} 提供您可以呼叫的預設登入畫面（如果您沒有自己的使用者介面畫面可顯示）。
{: shortdesc}

取決於您的身分提供者配置，您可以顯示的畫面會有所不同。此服務不會提供社交身分提供者的進階功能，因為我們永遠無權存取使用者帳戶資訊。使用者必須移至身分提供者來管理其資訊。例如，如果他們想要變更其 Facebook 密碼，則他們需要移至 www.facebook.com。

請參閱下表，以查看您可以對每一種類型的身分提供者顯示的畫面。

<table>
  <thead>
    <tr>
      <th>顯示畫面</th>
      <th>社交身分提供者</th>
      <th>企業身分提供者</th>
      <th>雲端目錄</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>登入</td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>註冊</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>忘記密碼</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>變更密碼</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>帳戶詳細資料</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用特性" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

在您配置了[社交身分提供者](/docs/services/appid/identity-providers.html)及[雲端目錄](/docs/services/appid/cloud-directory.html)的設定之後，請按一下下列影像中您選擇的語言來開始實作程式碼。


按一下映像檔，以使用其中一個提供的 SDK 或 API。請不要忘記，您也可以搭配使用 App ID 與其他語言。藉由使用我們的 API，您可以在任何應用程式中設定雲端目錄。如需映像檔中未列出之語言的協助，請查看<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">我們的部落格 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{: shortdesc}

</br>

## 使用 Android SDK 顯示預設畫面
{: #android}

您可以使用 Android SDK 來呼叫預先配置的畫面。
{: shortdesc}

</br>

**登入**
1. 在您的程式碼中放置下列指令。
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        

          @Override
        public void onAuthorizationCanceled () {
          //Authentication canceled by the user
        }

        

@Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
            //User authenticated
        }
      });
    ```
  {: pre}

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
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 if (accessToken != null && identityToken != null) {
				     } else {
  			 }

  		 }
  	 });
  ```
  {: pre}

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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
    ```
    {: pre}

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
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 }
  		 });
   ```
   {: pre}

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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
   ```
   {: pre}
</br>
</br>

## 使用 iOS Swift SDK 顯示預設畫面
{: #ios-swift}

您可以使用 iOS Swift SDK 來呼叫預先配置的畫面。
{: shortdesc}

</br>
**登入**

1. 在您的程式碼中放置下列指令。
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}


</br>
**註冊**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 呼叫 LoginWidget 來啟動註冊流程。
  ```swift
class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
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

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**及**忘記密碼電子郵件**設為**開啟**。
2. 呼叫 LoginWidget 來啟動忘記密碼流程。
  ```swift
class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
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
**帳戶詳細資料**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 呼叫 LoginWidget 來啟動變更詳細資料流程。
  ```swift

class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>
**變更密碼**

1. 在雲端目錄的設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。
2. 呼叫 LoginWidget 來啟動變更密碼流程。
  ```swift
class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}
</br>
</br>

## 使用 Node.js SDK 顯示預設畫面
{: #nodejs}

您可以使用 Node.js SDK 來呼叫預先配置的畫面。
{: shortdesc}

</br>
**登入**

1. 在身分提供者設定中，將雲端目錄設為**開啟**，並指定回呼端點。
2. 將張貼路徑新增至可利用使用者名稱及密碼參數所呼叫的應用程式，並使用資源擁有者密碼登入。
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
    {: pre}
    `WebAppStrategy` 可讓使用者利用使用者名稱和密碼登入您的 Web 應用程式。登入成功之後，使用者的存取記號會儲存在 HTTP 階段作業中，並且可在階段作業期間使用。只要 HTTP 階段作業遭到破壞或過期，記號即會無效。
    {: tip}

</br>
**註冊**

1. 在雲端目錄設定中，將**容許使用者註冊及重設其密碼**設為**開啟**。如果設為否，則處理程序會結束，而不會擷取存取及身分記號。
2. 傳遞 WebAppStrategy `show` 內容，並將其設為 `WebAppStrategy.SIGN_UP`。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**忘記密碼**

1. 在雲端目錄設定中，將**容許使用者註冊及重設其密碼**及**忘記密碼電子郵件**設為**開啟**。如果設為否，則處理程序會結束，而不會擷取存取及身分記號。
2. 傳遞 WebAppStrategy `show` 內容，並將其設為 `WebAppStrategy.FORGOT_PASSWORD`。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

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
  {: pre}

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
  {: pre}

</br>
</br>

## 使用 Swift SDK 顯示預設畫面
{: #swift}

啟用社交身分提供者之後，即可使用 Swift SDK 呼叫預先配置的登入畫面。
{: shortdesc}

1. 下列程式碼示範如何在 Kitura 應用程式中使用 WebAppKituraCredentialsPlugin 來保護 `/protected` 端點。

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // The following URLs will be used for AppID OAuth flows
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Setup Kitura to use session middleware
  // Must be configured with proper session storage for production
  // environments. See https://github.com/IBM-Swift/Kitura-Session for
  // additional documentation
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)

  let options = [
  	"clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)

  // Explicit login endpoint
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback to finish the authorization process. Will retrieve access and identity tokens from AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Logout endpoint. Clears authentication information from session
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Protected area
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
      let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]

      guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
          response.status(.unauthorized)
          return next()
      }

      response.send(json: identityTokenPayload!)
      next()
			})
  var port = 3000
  if let portString = ProcessInfo.processInfo.environment["PORT"]{
      port = Int(portString)!
  }
  print("Starting on \(port)")

  // Add an HTTP server and connect it to the router
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start the Kitura runloop (this call never returns)
  Kitura.run()
  ```
  {: codeblock}
</br>
</br>



