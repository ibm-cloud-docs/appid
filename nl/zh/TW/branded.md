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

# 將登入體驗加上特有風格
{: #branding}

您可以顯示自己的自訂畫面，並充分運用 {{site.data.keyword.appid_full}} 的鑑別及授權功能。使用雲端目錄作為身分提供者，使用者就可以在您提供較少協助的情況下，與您的應用程式互動。他們可以在未要求協助的情況下登入。
{: shortdesc}

當您使用自己的畫面時，[資源擁有者密碼認證流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)即可用來提供存取及身分記號。


## 使用 Android SDK 顯示自訂的畫面
{: #branded-ui-android}

啟用雲端目錄之後，即可使用 Android SDK 來呼叫自訂的畫面。<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">請查看此部落格！<img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //User authenticated
        }
      });
  ```
  {: pre}

</br>
</br>

## 使用 iOS Swift SDK 顯示自訂的畫面
{: #branded-ui-ios-swift}

啟用雲端目錄之後，即可使用 iOS Swift SDK 來呼叫自訂的畫面。
{: shortdesc}

</br>
**登入**

1. 在 GUI 的身分提供者標籤中，將雲端目錄設為**開啟**。
2. 使用資源擁有者密碼登入。當使用者嘗試使用其使用者名稱和密碼來登入時，即會取得存取及身分記號。
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: pre}


</br>
</br>

## 使用 Node.js SDK 顯示自訂的畫面
{: #branded-ui-nodejs}

啟用雲端目錄之後，即可使用 Node.js SDK 來呼叫自訂的畫面。
{: shortdesc}

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

