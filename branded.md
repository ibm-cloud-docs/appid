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

# Branding the sign in experience
{: #branding}

You can display your own customized UI's while taking advantage of the authentication and authorization capabilities of {{site.data.keyword.appid_full}}. With cloud directory as your identity provider, your users are able to interact with your app with less help from you. They're able to sign in, sign up, change their password, and more without asking for help.
{: shortdesc}

With cloud directory as your identity provider, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) is used to provide access and identity tokens.

**Note**: You are only able to bring customized sign in pages when cloud directory is the only option configured. If you have any other identity providers set to **on**, then the preconfigured sign in screen displays.

## Displaying customized screens with the Android SDK
With cloud directory enabled, you can call customized screens with the Android SDK. You can choose the combination of the screens that you'd like your users to be able to interact with. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Check out our blog! <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
{: shortdesc}

</br>
**Sign in**

1. Set **Cloud Directory** to **On** as an identity provider.
2. Place the following command in your code.
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
**Sign up**

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the sign up flow.
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
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: codeblock}

</br>
**Forgot password**

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the forgot password flow.
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
**Account details**

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the change details flow.
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
**Change password**

1. Set **Allow users to sign up and reset their password** to **ON**, in the settings for cloud directory.
2. Call the LoginWidget to start the change password flow.
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

## Displaying customized screens with the iOS Swift SDK

With cloud directory enabled, you can call customized screens with the ios Swift SDK. You can choose the combination of the screens that you'd like your users to be able to interact with.
{: shortdesc}

</br>
**Sign in**

1. In the identity provider tab on the GUI, set cloud directory to **On**.
2. Log in by using the resource owner password. You can obtain an access and ID token by supplying the end user's username and password.
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
**Sign up**

1. Set **Allow users to sign up and reset their password** to **On**, in the settings for cloud directory.
2. Call the LoginWidget to start the sign up flow.
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
**Forgot password**

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the forgot password flow.
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
**Account details**

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the change details flow.
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
**Change password**

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the change password flow.
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
## Displaying customized screens with the Node.js SDK
{: #branded-ui-nodejs}

With cloud directory enabled, you can call customized screens with the Node.js SDK. You can choose the combination of the screens that you'd like your users to be able to interact with.
{: shortdesc}

**Sign in**
1. Set cloud directory to **On** in your identity provider settings and specify a callback endpoint.
2. Add a post route to your app that can be called with the username and password parameters and log in by using the resource owner password.
    **Note**: `WebAppStrategy` allows users to log in to your web apps with a username and password. After successful login, a user's access token is stored in the HTTP session and is available for the duration of the session. Once the HTTP session is destroyed or has expired, the token is no longer valid.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // allow flash messages
    }));
    ```
    {: codeblock}

</br>
**Sign up**

1. Set **Allow users to sign up and reset their password** to **On** in the cloud directory settings. If this is set to no, the process ends without retreiving access and identity tokens.
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>
**Forgot password**

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **ON** in the cloud directory settings. If this is set to no, the process ends without retrieving access and identity tokens.
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>
**Account details**
1. Set **Allow users to sign up and reset their password** to **On** in the cloud directory settings
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>
**Change password**
1. Set **Allow users to sign up and reset their password** to **On** in the cloud directory settings.
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
