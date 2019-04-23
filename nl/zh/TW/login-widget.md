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


# 顯示登入小組件
{: #login-widget}

{{site.data.keyword.appid_full}} 提供「登入小組件」，可讓您提供使用者安全的登入選項。
{: shortdesc}

將您的應用程式配置為使用身分提供者時，「登入小組件」即會將您應用程式的訪客導向至登入畫面。使用「登入小組件」，您可以顯示登入流程的預先配置畫面。附加價值是您可以隨時更新登入流程，而無需以任何方式變更您的原始碼！

想要建立您應用程式特有的體驗嗎？您可以[帶入自己的畫面](/docs/services/appid?topic=appid-branded)！
{: tip}

## 瞭解登入小組件
{: #widget-understanding}

即使沒有自己的使用者介面畫面，您也可以顯示「登入小組件」來充分運用 {{site.data.keyword.appid_short_notm}}。
{: shortdesc}

### 何謂預設值？
{: #widget-default}

配置多個身分提供者時，若使用者嘗試登入您的應用程式，會將他們重新導向至「登入小組件」。使用「登入小組件」，使用者可以選擇要用來驗證其身分的提供者。但是，只有一個提供者設為**開啟**時，會將訪客重新導向至該身分提供者鑑別畫面。

### {{site.data.keyword.appid_short_notm}} 從身分提供者取得多少資訊？
{: #widget-obtain-info}

當您使用社交或企業身分提供者時，{{site.data.keyword.appid_short_notm}} 具有使用者帳戶資訊的讀取權。此服務會使用記號以及身分提供者所傳回的主張，來驗證使用者的身分。因為此服務永不具有資訊的寫入權，所以使用者必須透過其選擇的身分提供者執行動作，例如重設其密碼。例如，如果使用者使用 Facebook 來登入您的應用程式，然後想要變更其密碼，他們必須移至 www.facebook.com 才能執行此動作。

當您使用[雲端目錄](/docs/services/appid?topic=appid-cloud-directory)時，{{site.data.keyword.appid_short_notm}} 是身分提供者。此服務會使用您的登錄來驗證您的使用者身分。因為 {{site.data.keyword.appid_short_notm}} 是提供者，所以使用者可以直接在您的應用程式中充分運用進階功能，例如重設其密碼。


### 可對每一個提供者顯示哪些畫面？
{: #widget-options}

請參閱下表，以查看您可以對每一種類型的身分提供者顯示的畫面。

<table>
  <thead>
    <tr>
      <th>登入小組件畫面</th>
      <th>社交身分提供者</th>
      <th>企業身分提供者</th>
      <th>Cloud Directory</th>
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

</br>
</br>

## 自訂登入小組件
{: #widget-customize}

{{site.data.keyword.appid_short_notm}} 提供您可以呼叫的預設登入畫面（如果您沒有自己的使用者介面畫面可顯示）。
您可以自訂畫面，以顯示您選擇的標誌及顏色。
{: shortdesc}

若要自訂畫面，請執行下列動作：

1. 開啟 {{site.data.keyword.appid_short_notm}} 服務儀表板。
2. 選取**登入自訂作業**區段。您可以修改「登入小組件」的外觀，以符合公司品牌。
3. 選取本端系統中的 PNG 或 JPG 檔案，以上傳公司的標誌。建議的影像大小是 320 x 320 像素。檔案大小上限是 100 KB。
4. 從顏色選取器中選取小組件的標頭顏色，或輸入另一個顏色的十六進位碼。
5. 檢查預覽窗格，然後在滿意自訂時按一下**儲存變更**。即會顯示一則確認訊息。
6. 在瀏覽器中，重新整理登入頁面，以驗證您的變更。

切記！您也可以充分運用其他語言的 {{site.data.keyword.appid_short_notm}}。如果您看不到所使用語言的 SDK，則可以一律使用 API。請參閱<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">我們的部落格 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{: tip}


## 使用 Android SDK 顯示登入小組件
{: #widget-display-android}

您可以使用 [Android 用戶端 SDK](https://github.com/ibm-cloud-security/appid-clientsdk-android) 來呼叫預先配置的畫面。
{: shortdesc}

在您的程式碼中放置下列指令。

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
{: codeblock}

</br>

### 註冊
{: #widget-android-signup}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者註冊至您的應用程式**及**容許使用者從您的應用程式管理其帳戶**兩者必須都設為**開啟**。
2. 將下列程式碼新增至您的應用程式。當使用者從您的自訂畫面註冊您的應用程式時，會啟動註冊流程。下列呼叫不僅會登錄使用者，還可以傳送驗證電子郵件來完成登錄，視您的「雲端目錄」配置而定。

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

### 忘記密碼
{: #widget-android-forgot-password}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者從您的應用程式管理其帳戶**必須設為**開啟**。
2. 在服務儀表板的**重設密碼**標籤中，請確定**忘記密碼電子郵件**已設為**開啟**。
3. 將下列程式碼新增至您的應用程式。當使用者在您的應用程式中按一下「忘記密碼」時，SDK 會呼叫 forgot_password API，以將電子郵件傳送給使用者，容許他們重設其密碼。

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
  {: codeblock}

</br>

### 變更詳細資料
{: #widget-android-change-details}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者註冊至您的應用程式**及**容許使用者從您的應用程式管理其帳戶**兩者必須都設為**開啟**。
2. 在服務儀表板的**密碼變更**標籤中，將**密碼變更電子郵件**設為「開啟」。
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
  {: codeblock}

</br>

### 變更密碼
{: #widget-android-change-password}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者註冊至您的應用程式**及**容許使用者從您的應用程式管理其帳戶**兩者必須都設為**開啟**。
2. 將下列程式碼放在您的應用程式中，以啟動變更密碼流程。

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
  {: codeblock}



## 使用 iOS Swift SDK 顯示登入小組件
{: #widget-display-ios-swift}

您可以使用 [iOS Swift 用戶端 SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift) 來呼叫預先配置的畫面。
{: shortdesc}

在您的程式碼中放置下列指令。

  ```swift
  import IBMCloudAppID
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
  {: codeblock}

</br>

### 註冊
{: #widget-ios-signup}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者註冊至您的應用程式**及**容許使用者從您的應用程式管理其帳戶**兩者必須都設為**開啟**。
2. 將下列程式碼放在您的應用程式中。當使用者嘗試註冊您的應用程式時，就會呼叫登入小組件，並顯示您的自訂註冊頁面。

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
          }}

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: codeblock}

</br>

### 忘記密碼
{: #widget-ios-forgot-password}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者從您的應用程式管理其帳戶**必須設為**開啟**。
2. 在服務儀表板的**重設密碼**標籤中，請確定**忘記密碼電子郵件**已設為**開啟**。
3. 將下列程式碼放在您的應用程式中。當您的其中一個應用程式使用者要求更新其密碼時，就會呼叫登入小組件，並啟動處理程序。

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
          }}

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: codeblock}

</br>

### 變更詳細資料
{: #widget-ios-change-details}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者註冊至您的應用程式**及**容許使用者從您的應用程式管理其帳戶**兩者必須都設為**開啟**。
2. 在服務儀表板的**密碼變更**標籤中，將**密碼變更電子郵件**設為「開啟」。
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
  {: codeblock}

</br>

### 變更密碼
{: #widget-ios-change-password}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者註冊至您的應用程式**及**容許使用者從您的應用程式管理其帳戶**兩者必須都設為**開啟**。
2. 將下列程式碼放在您的應用程式中，以啟動變更密碼流程。

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
  {: codeblock}


## 使用 Node.js SDK 顯示登入小組件
{: #widget-display-nodejs}

您可以使用 [Node.js 伺服器 SDK](https://github.com/ibm-cloud-security/appid-serversdk-nodejs) 來呼叫預先配置的畫面。
{: shortdesc}

將張貼路徑新增至可利用使用者名稱及密碼參數所呼叫的應用程式，並使用資源擁有者密碼登入。
    

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

`WebAppStrategy` 可讓使用者利用使用者名稱和密碼登入您的 Web 應用程式。登入成功之後，使用者的存取記號會儲存在 HTTP 階段作業中，並且可在階段作業期間使用。在 HTTP 階段作業損毀或過期之後，記號即無效。
{: tip}

</br>

### 註冊
{: #widget-nodejs-signup}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者註冊至您的應用程式**及**容許使用者從您的應用程式管理其帳戶**兩者必須都設為**開啟**。
2. 將下列程式碼放在您的應用程式中。當使用者嘗試註冊您的應用程式時，就會呼叫登入小組件，並顯示您的自訂註冊頁面。

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

### 忘記密碼
{: #widget-nodejs-forgot-password}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者從您的應用程式管理其帳戶**必須設為**開啟**。
2. 在服務儀表板的**重設密碼**標籤中，請確定**忘記密碼電子郵件**已設為**開啟**。
3. 將下列程式碼放在您的應用程式中，以將 *show* 內容傳遞至 `WebAppStrategy.FORGOT_PASSWORD`。當使用者要求更新其登入您應用程式的密碼時，就會呼叫登入小組件，並啟動處理程序。

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

### 變更詳細資料
{: #widget-nodejs-change-details}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者註冊至您的應用程式**及**容許使用者從您的應用程式管理其帳戶**兩者必須都設為**開啟**。
2. 在服務儀表板的**密碼變更**標籤中，將**密碼變更電子郵件**設為「開啟」。
3. 將下列程式碼放在您的應用程式中，以將 *show* 內容傳遞至 `WebAppStrategy.FORGOT_PASSWORD`，來啟動變更詳細資料表單。

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

### 變更密碼
{: #widget-nodejs-change-password}

1. 在 GUI 中配置「雲端目錄」[設定](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**容許使用者註冊至您的應用程式**及**容許使用者從您的應用程式管理其帳戶**兩者必須都設為**開啟**。
2. 在服務儀表板的**密碼變更**標籤中，將**密碼變更電子郵件**設為「開啟」。
3. 將下列程式碼放在您的應用程式中，以將 *show* 內容傳遞至 `WebAppStrategy.FORGOT_PASSWORD`，來啟動變更詳細資料表單。

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
