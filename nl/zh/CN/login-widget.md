---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

subcollection: appid

---

{:external: target="_blank" .external}
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


# 使用登录窗口小部件
{: #login-widget}

通过 {{site.data.keyword.appid_full}}，您可以使用缺省 UI（称为“登录窗口小部件”）来允许应用程序用户选择要用于进行登录的身份提供者。如果使用的是 Cloud Directory，那么登录窗口小部件还会提供其他 UI 以给出额外功能，例如注册、忘记密码、多因子认证等。
{: shortdesc}


## 了解登录窗口小部件
{: #widget-understanding}

登录窗口小部件的其中一大优点是，您无需实施自己的任何认证 UI 就能开始使用 {{site.data.keyword.appid_short_notm}}，这使开发者的上线体验轻松得多。

### 缺省登录窗口小部件行为是什么？
{: #widget-default}

缺省情况下，允许登录窗口小部件使用 Facebook、Google 和 Cloud Directory。您可以随时通过选择要配置为选项的身份提供者来更改此行为。启用了多个身份提供者时，登录窗口小部件会显示一个屏幕，在其中用户可以选择自己的身份提供者。但是，如果只启用了一个提供者，那么用户不会看到上述选择屏幕。系统会将用户直接转至该身份提供者以开始登录过程。

例如，如果使用缺省设置（Facebook、Google 和 Cloud Directory），那么用户将看到该屏幕。如果仅启用 Facebook，那么系统会将用户直接转至 Facebook 进行认证。



### 对于每个提供者，可以显示哪些屏幕？
{: #widget-options}

使用 Cloud Directory 时，{{site.data.keyword.appid_short_notm}} 能够为您提供扩展的用户管理功能。扩展功能还会应用于登录窗口小部件功能。存储在 Cloud Directory 中的用户可以直接在登录窗口小部件中利用注册或重置其密码等功能。查看下表，了解对于各种身份提供者可以显示哪些屏幕。

<table>
  <thead>
    <tr>
      <th>登录窗口小部件屏幕</th>
      <th>社交身份提供者</th>
      <th>企业身份提供者</th>
      <th>Cloud Directory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>登录</td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>注册</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>忘记密码</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>更改密码</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>帐户详细信息</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>


## 定制登录窗口小部件
{: #widget-customize}

登录窗口小部件是动态的。可以定制外观或身份提供者配置，并且这些更改会立即应用。无需以任何方式更新应用程序代码或重新部署应用程序！
{: shortdesc}

除了登录窗口小部件提供的定制外，还需要更多定制吗？您可以实施自己的完全定制的 UI，用于用户登录、注册、重置密码和其他流程，以创建应用程序的独特体验。首先，请查看[为应用程序添加品牌形象](/docs/services/appid?topic=appid-branded)。
{: tip}

要定制屏幕：

1. 打开 {{site.data.keyword.appid_short_notm}} 服务仪表板。
2. 选择**登录定制**部分。可以修改登录窗口小部件的外观，使其与您公司的品牌保持一致。
3. 通过从本地系统中选择 PNG 或 JPG 文件来上传您公司的徽标。建议的图像大小为 320 x 320 像素。最大文件大小为 100 Kb。
4. 从颜色选取器中选择窗口小部件的标题颜色，或者输入其他颜色的十六进制代码。
5. 检查预览窗格，对定制满意后，单击**保存更改**。此时将显示确认消息。
6. 在浏览器中，刷新登录页面以验证您的更改。


## 使用 Android SDK 显示登录窗口小部件
{: #widget-display-android}

您可以使用 [Android 客户端 SDK](https://github.com/ibm-cloud-security/appid-clientsdk-android) 来调用预先配置的屏幕。
{: shortdesc}

将以下命令放在代码中。

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

### 注册
{: #widget-android-signup}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 将以下代码添加到应用程序。用户在定制屏幕中向应用程序注册时，会启动注册流程。以下调用不仅会注册用户，还可以发送验证电子邮件以完成注册，具体取决于 Cloud Directory 配置。

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
  {: codeblock}

</br>

### 忘记密码
{: #widget-android-forgot-password}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户通过应用程序管理自己的帐户**必须设置为**开启**。
2. 在服务仪表板的**重置密码**选项卡中，确保将**忘记密码电子邮件**设置为**开启**。
3. 将以下代码添加到应用程序。用户在应用程序中单击“忘记密码”时，SDK 会调用 forgot_password API 向用户发送电子邮件，以允许用户重置其密码。

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

### 更改详细信息
{: #widget-android-change-details}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 在服务仪表板的**密码已更改**选项卡中，将**密码已更改电子邮件**设置为“开启”。
3. 调用“登录”窗口小部件以开始更改详细信息流程。

  ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
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

### 更改密码
{: #widget-android-change-password}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 将以下代码放入应用程序中以启动更改密码流程。

  ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
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



## 使用 iOS Swift SDK 显示登录窗口小部件
{: #widget-display-ios-swift}

您可以使用 [iOS Swift 客户端 SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift) 来调用预先配置的屏幕。
{: shortdesc}

将以下命令放在代码中。

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

### 注册
{: #widget-ios-signup}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 将以下代码放入应用程序中。用户尝试向应用程序注册时，会调用登录窗口小部件并显示定制注册页面。

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
  {: codeblock}

</br>

### 忘记密码
{: #widget-ios-forgot-password}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户通过应用程序管理自己的帐户**必须设置为**开启**。
2. 在服务仪表板的**重置密码**选项卡中，确保将**忘记密码电子邮件**设置为**开启**。
3. 将以下代码放入应用程序中。当某个应用程序用户请求更新其密码时，会调用登录窗口小部件并启动该流程。

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
  {: codeblock}

</br>

### 更改详细信息
{: #widget-ios-change-details}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 在服务仪表板的**密码已更改**选项卡中，将**密码已更改电子邮件**设置为“开启”。
3. 调用“登录”窗口小部件以开始更改详细信息流程。

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

### 更改密码
{: #widget-ios-change-password}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 将以下代码放入应用程序中以启动更改密码流程。

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


## 使用 Node.js SDK 显示登录窗口小部件
{: #widget-display-nodejs}

您可以使用 [Node.js 服务器 SDK](https://github.com/ibm-cloud-security/appid-serversdk-nodejs) 来调用预先配置的屏幕。
{: shortdesc}

为应用程序添加发布路径（可以使用用户名和密码参数来调用该路径），然后使用资源所有者密码登录。


  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

利用 `WebAppStrategy`，用户可以使用用户名和密码登录 Web 应用程序。成功登录后，用户的访问令牌会存储在 HTTP 会话中，并在整个会话过程中可用。当 HTTP 会话销毁或到期后，令牌会失效。
{: tip}

</br>

### 注册
{: #widget-nodejs-signup}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 将以下代码放入应用程序中。用户尝试向应用程序注册时，会调用登录窗口小部件并显示定制注册页面。

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

### 忘记密码
{: #widget-nodejs-forgot-password}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户通过应用程序管理自己的帐户**必须设置为**开启**。
2. 在服务仪表板的**重置密码**选项卡中，确保将**忘记密码电子邮件**设置为**开启**。
3. 将以下代码放入应用程序中，以便将 *show* 属性传递到 `WebAppStrategy.FORGOT_PASSWORD`。用户请求更新其用于应用程序的密码时，会调用登录窗口小部件并启动该流程。

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

### 更改详细信息
{: #widget-nodejs-change-details}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 在服务仪表板的**密码已更改**选项卡中，将**密码已更改电子邮件**设置为“开启”。
3. 将以下代码放入应用程序中，以便将 *show* 属性传递到 `WebAppStrategy.FORGOT_PASSWORD` 来启动更改详细信息表单。

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

### 更改密码
{: #widget-nodejs-change-password}

1. 在 GUI 中配置 Cloud Directory [设置](/docs/services/appid?topic=appid-cloud-directory#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 在服务仪表板的**密码已更改**选项卡中，将**密码已更改电子邮件**设置为“开启”。
3. 将以下代码放入应用程序中，以便将 *show* 属性传递到 `WebAppStrategy.FORGOT_PASSWORD` 来启动更改详细信息表单。

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
