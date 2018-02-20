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

# 有品牌形象的登录体验
{: #branding}

在利用 {{site.data.keyword.appid_full}} 认证和授权功能的同时，也可以显示自己的定制 UI。利用 Cloud Directory 作为身份提供者，用户不需要多少帮助就可以与应用程序进行交互。用户无需寻求帮助就可以完成登录、注册、更改密码等操作。
{: shortdesc}

利用 Cloud Directory 作为身份提供者，会使用[资源所有者密码凭证流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)来提供访问令牌和身份令牌。

**注**：只有将 Cloud Directory 配置为唯一选项，才能显示定制登录页面。如果将其他身份提供者设置为**开启**，那么会显示预配置的登录屏幕。

## 使用 Android SDK 显示定制屏幕
{: #branded-ui-android}

在启用 Cloud Directory 的情况下，可以使用 Android SDK 来调用定制屏幕。您想让用户能跟哪些屏幕交互？可以选择将这些屏幕组合起来。<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">查看博客！ <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>
{: shortdesc}

</br>
**登录**

1. 将 **Cloud Directory** 作为身份提供者设置为**开启**。
2. 将以下命令放在代码中。
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
**注册**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 调用 LoginWidget 以开始注册流程。
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
**忘记密码**
1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**和**忘记密码电子邮件**设置为**开启**。
2. 调用 LoginWidget 以开始忘记密码流程。
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
**帐户详细信息**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 调用 LoginWidget 以开始更改详细信息流程。
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
**更改密码**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 调用 LoginWidget 以开始更改密码流程。
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

## 使用 iOS Swift SDK 显示定制屏幕
{: #branded-ui-ios-swift}

在启用 Cloud Directory 的情况下，可以使用 ios Swift SDK 来调用定制屏幕。您想让用户能跟哪些屏幕交互？可以选择将这些屏幕组合起来。
{: shortdesc}

</br>
**登录**

1. 在 GUI 上的身份提供者选项卡中，将 Cloud Directory 设置为**开启**。
2. 使用资源所有者密码登录。通过提供最终用户的用户名和密码，可获取访问和标识令牌。
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
**注册**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 调用 LoginWidget 以开始注册流程。
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
**忘记密码**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**和**忘记密码电子邮件**设置为**开启**。
2. 调用 LoginWidget 以开始忘记密码流程。
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
**帐户详细信息**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 调用 LoginWidget 以开始更改详细信息流程。
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
**更改密码**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 调用 LoginWidget 以开始更改密码流程。
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

## 使用 Node.js SDK 显示定制屏幕
{: #branded-ui-nodejs}

在启用 Cloud Directory 的情况下，可以使用 Node.js SDK 来调用定制屏幕。您想让用户能跟哪些屏幕交互？可以选择将这些屏幕组合起来。
{: shortdesc}

**登录**
1. 在身份提供者设置中，将 Cloud Directory 设置为**开启**，然后指定回调端点。
2. 为应用程序添加发布路径（可以使用用户名和密码参数来调用该路径），然后使用资源所有者密码登录。
**注**：利用 `WebAppStrategy`，用户可以使用用户名和密码登录 Web 应用程序。成功登录后，用户的访问令牌会存储在 HTTP 会话中，并在整个会话过程中可用。当 HTTP 会话销毁或到期后，令牌不再有效。
    ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
    {: codeblock}

</br>
**注册**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。如果设置为“否”，那么到该进程结束也不会检索访问令牌和身份令牌。
2. 传递 WebAppStrategy `show` 属性并将其设置为 `WebAppStrategy.SIGN_UP`。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>
**忘记密码**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**和**忘记密码电子邮件**设置为**开启**。如果设置为“否”，那么到该进程结束也不会检索访问令牌和身份令牌。
2. 传递 WebAppStrategy `show` 属性并将其设置为 `WebAppStrategy.FORGOT_PASSWORD`。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>
**帐户详细信息**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 传递 WebAppStrategy `show` 属性并将其设置为 `WebAppStrategy.CHANGE_DETAILS`。
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>
**更改密码**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 传递 WebAppStrategy `show` 属性并将其设置为 `WebAppStrategy.CHANGE_PASSWORD`。
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
