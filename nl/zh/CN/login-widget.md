---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# 显示登录窗口小部件
{: #login-widget}

{{site.data.keyword.appid_full}} 提供了一个登录窗口小部件，使您能够为用户提供安全登录选项。
{: shortdesc}

应用程序配置为使用身份提供者时，登录窗口小部件会将应用程序的访问者定向到登录屏幕。使用登录窗口小部件，可以显示登录流程的预配置屏幕。使用登录窗口小部件的另一个额外优点是，您可以随时更新登录流程，而无需以任何方式更改源代码！


要创建您的应用程序所特有的体验吗？您可以[自带屏幕](/docs/services/appid/branded.html)！
{: tip}

## 了解登录窗口小部件
{: #understanding}

即使您没有自己的 UI 屏幕，也可以通过显示登录窗口小部件来利用 {{site.data.keyword.appid_short_notm}}。
{: shortdesc}

**缺省设置是什么？**

配置了多个身份提供者时，会在用户尝试登录到应用程序时将其重定向到登录窗口小部件。通过使用登录窗口小部件，用户可以选择要用于验证自己身份的提供者。但是，只有一个提供者设置为**开启**时，访问者会重定向到该身份提供者的认证屏幕。

**{{site.data.keyword.appid_short_notm}} 会从身份提供者那里获取多少信息？**

使用社交或企业身份提供者时，{{site.data.keyword.appid_short_notm}} 对用户帐户信息具有读访问权。服务使用身份提供者返回的令牌和断言来验证用户的身份是否与其声明的一致。由于服务从不具有对信息的写访问权，因此用户必须通过其所选身份提供者来执行操作，如重置其密码。例如，如果用户使用 Facebook 登录到应用程序，然后希望更改自己的密码，那么他们必须转至 www.facebook.com 来执行此操作。

使用 [Cloud Directory](/docs/services/appid/cloud-directory.html) 时，{{site.data.keyword.appid_short_notm}} 是身份提供者。该服务会使用注册表来验证用户身份。由于 {{site.data.keyword.appid_short_notm}} 是提供者，因此用户可以直接利用应用程序中的高级功能（例如，重置其密码）。

**对于每种类型的提供者，可以显示哪种类型的屏幕？**

查看下表，了解对于各种身份提供者可以显示哪些屏幕。

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

</br>
</br>

## 定制登录窗口小部件
{: #customize}

{{site.data.keyword.appid_short_notm}} 提供了缺省登录屏幕，如果您没有自己的 UI 屏幕需要显示，那么可以进行调用。
您可以定制屏幕以显示您选择的徽标和颜色。
{: shortdesc}

要定制屏幕：

1. 打开 {{site.data.keyword.appid_short_notm}} 服务仪表板。
2. 选择**登录定制**部分。可以修改登录窗口小部件的外观，使其与您公司的品牌保持一致。
3. 通过从本地系统中选择 PNG 或 JPG 文件来上传您公司的徽标。建议的图像大小为 320 x 320 像素。最大文件大小为 100 Kb。
4. 从颜色选取器中选择窗口小部件的标题颜色，或者输入其他颜色的十六进制代码。
5. 检查预览窗格，对定制满意后，单击**保存更改**。此时将显示确认消息。
6. 在浏览器中，刷新登录页面以验证您的更改。

请牢记！您还可以利用其他语言版本的 {{site.data.keyword.appid_short_notm}}。如果看不到针对所用语言的 SDK，您始终可以使用 API。请查看<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">我们的博客 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
{: tip}


## 使用 Android SDK 显示登录窗口小部件
{: #android}

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

**注册**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
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
  {: pre}

</br>

**忘记密码**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户通过应用程序管理自己的帐户**必须设置为**开启**。
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

**更改详细信息**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
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

**更改密码**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
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


</br>
</br>

## 使用 iOS Swift SDK 显示登录窗口小部件
{: #ios-swift}

您可以使用 [iOS Swift 客户端 SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift) 来调用预先配置的屏幕。
{: shortdesc}

将以下命令放在代码中。

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
  {: codeblock}

</br>

**注册**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
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

**忘记密码**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户通过应用程序管理自己的帐户**必须设置为**开启**。
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

**更改详细信息**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
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

**更改密码**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
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

</br>
</br>

## 使用 Node.js SDK 显示登录窗口小部件
{: #nodejs}

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

**注册**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 将以下代码放入应用程序中。用户尝试向应用程序注册时，会调用登录窗口小部件并显示定制注册页面。

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

**忘记密码**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户通过应用程序管理自己的帐户**必须设置为**开启**。
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

**更改详细信息**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
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

**更改密码**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户向应用程序注册**和**允许用户通过应用程序管理自己的帐户**都必须设置为**开启**。
2. 在服务仪表板的**密码已更改**选项卡中，将**密码已更改电子邮件**设置为“开启”。
3. 将以下代码放入应用程序中，以便将 *show* 属性传递到 `WebAppStrategy.FORGOT_PASSWORD` 来启动更改详细信息表单。

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

</br>
