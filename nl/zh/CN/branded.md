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

# 为应用程序添加品牌形象
{: #branding}

您可以显示自己的定制屏幕，并利用 {{site.data.keyword.appid_full}} 的认证和授权功能。利用 Cloud Directory 作为身份提供者，用户不需要多少帮助就可以与应用程序进行交互。用户无需寻求帮助就可以完成登录、注册、更改密码等操作。
{: shortdesc}

当您使用自己的屏幕时，[资源所有者密码凭证流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)可用于提供访问令牌和身份令牌。


## 使用 iOS Swift SDK 来为应用程序添加品牌形象
{: #branded-ui-ios-swift}

在启用 Cloud Directory 的情况下，可以使用 iOS Swift SDK 来调用自己的品牌屏幕。
{: shortdesc}

</br>
**登录**

1. 在 GUI 的身份提供者选项卡中，将 Cloud Directory 设置为**开启**。
2. 调用“登录”窗口小部件以开始登录流程。当用户尝试使用其用户名或电子邮件和密码登录时，会获取访问令牌和身份令牌。
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

**注册**

1. 在 GUI 上的身份提供者选项卡中，将 Cloud Directory 设置为**开启**。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
3. 调用“登录”窗口小部件以开始注册流程。
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

**忘记密码**

1. 在 GUI 上的身份提供者选项卡中，将 Cloud Directory 设置为**开启**。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
3. 调用“登录”窗口小部件以开始忘记密码流程。
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

**更改详细信息**

1. 在 GUI 上的身份提供者选项卡中，将 Cloud Directory 设置为**开启**。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
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
  {: pre}

</br>

**更改密码**

1. 在 GUI 上的身份提供者选项卡中，将 Cloud Directory 设置为**开启**。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
3. 调用“登录”窗口小部件以开始更改详细信息流程。
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


## 使用 Android SDK 来为应用程序添加品牌形象
{: #branded-ui-android}

在启用 Cloud Directory 的情况下，可以使用 Android SDK 来调用定制屏幕。您可以选择希望用户能够与其进行交互的屏幕组合。<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">查看此博客 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 以获取详细示例！
{: shortdesc}

</br>

**登录**

1. 将 **Cloud Directory** 作为身份提供者设置为**开启**。
2. 通过提供最终用户的用户名和密码，获取访问、身份和刷新令牌。
3. 调用“登录”窗口小部件以开始登录流程。
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

**注册**

1. 将 **Cloud Directory** 作为身份提供者设置为**开启**。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
3. 调用“登录”窗口小部件以开始注册流程。
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

1. 将 **Cloud Directory** 作为身份提供者设置为**开启**。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
3. 调用“登录”窗口小部件以开始忘记密码流程。
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

**更改详细信息**

1. 将 **Cloud Directory** 作为身份提供者设置为**开启**。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
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
  {: pre}


</br>

**更改密码**

1. 将 **Cloud Directory** 作为身份提供者设置为**开启**。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
3. 调用“登录”窗口小部件以开始更改密码流程。
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
  {: pre}

</br>
</br>


## 使用 Node.js SDK 为应用程序添加品牌形象
{: #branded-ui-nodejs}

在启用 Cloud Directory 的情况下，可以使用 Node.js SDK 来调用定制屏幕。
{: shortdesc}

**登录**

通过使用 WebAppStrategy，用户可以使用其用户名和密码登录 Web 应用程序。用户成功登录到应用程序后，只要其访问令牌保持有效，就会在 HTTP 会话中持久存储其访问令牌。在 HTTP 会话关闭或到期后，访问令牌也将销毁。

1. 在身份提供者设置中，将 Cloud Directory 设置为**开启**，然后指定回调端点。
2. 为应用程序添加发布路径（可以使用用户名和密码参数来调用该路径），然后使用资源所有者密码流程登录。

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
      <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 命令参数</th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>要在成功认证后将用户重定向到的 URL。</td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>要在认证失败时将用户重定向到的 URL。</td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td>设置为 <code>true</code> 时，将从 Cloud Directory 服务返回一条错误消息。缺省情况下，此值设置为 <code>false</code>。</td>
      </tr>
    </tbody>
  </table>

  1. 如果以 HTML 形式提交请求，那么可以使用 [body parser](https://www.npmjs.com/package/body-parser) 中间件。
  2. 要获取返回的错误消息，那么可以使用 [connect-flash](https://www.npmjs.com/package/connect-flash)。有关更多信息，请参阅 [Web 应用程序样本](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js)。{: tip}

</br>
**注册**

1. 在身份提供者设置中，将 Cloud Directory 设置为**开启**，然后指定回调端点。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
3. 将**允许用户无需电子邮件验证即可登录**设置为**开启**。如果未设置，那么无法检索 {{site.data.keyword.appid_short_notm}} 访问和身份令牌。
4. 为应用程序添加发布路径（可以使用用户名和密码参数来调用该路径），然后使用资源所有者密码流程登录。

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**忘记密码**

1. 在身份提供者设置中，将 Cloud Directory 设置为**开启**，然后指定回调端点。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
3. 将**忘记密码电子邮件**设置为**开启**。
4. 将 *show* 属性传递到 `WebAppStrategy.FORGOT_PASSWORD` 以启动忘记密码表单。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**更改详细信息**

1. 在身份提供者设置中，将 Cloud Directory 设置为**开启**，然后指定回调端点。
2. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
3. 验证用户先前是否已向 {{site.data.keyword.appid_short_notm}} 进行认证。
4. 将 *show* 属性传递到 `WebAppStrategy.CHANGE_DETAILS` 以启动忘记密码表单。
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## 使用 API 为应用程序添加品牌形象
{: #branded-ui-api}

您可以显示自己的定制屏幕，并利用 {{site.data.keyword.appid_short_notm}} 的认证和授权功能。利用 Cloud Directory 作为身份提供者，用户不需要多少帮助就可以与应用程序进行交互。用户无需寻求帮助就可以完成登录、注册、重置密码等操作。
{: shortdesc}

为了实现此目标，{{site.data.keyword.appid_short_notm}} 公开了 REST API。您可使用该 REST API 构建为 Web 应用程序提供服务的后端服务器，或使用自己的定制屏幕与移动应用程序进行交互。

管理 API 通过 IBM Cloud Identity and Access Management 生成的令牌进行保护。这意味着帐户所有者可以指定团队成员对每个服务实例的访问级别。有关 IAM 和 {{site.data.keyword.appid_short_notm}} 如何协作的更多信息，请参阅[服务访问管理](/docs/services/appid/iam.html)。

在配置[设置](/docs/services/appid/cloud-directory.html)后，您可以调用以下端点以显示每个屏幕。


**注册**：您可以使用 `/sign_up` 端点来允许用户注册您的应用程序。在请求主体中提供以下数据：
  * 您的租户标识。
  * Cloud Directory 用户数据。请参阅 [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) 以获取更多详细信息。
    * `password` 属性。
    * 在 `primary` 属性设置为 `true` 的电子邮件数组中，必须包含至少 1 个电子邮件地址。

根据您的[电子邮件配置](/docs/services/appid/cloud-directory.html)，用户可能会收到验证请求，或者收到欢迎他们注册应用程序的电子邮件。用户注册您的应用程序时，将触发这两种类型的电子邮件。验证电子邮件包含**验证**按钮。在他们按下按钮并确认其身份后，{{site.data.keyword.appid_short_notm}} 将显示一个感谢他们进行验证屏幕。  

您可以提供您自己的验证后页面：

1. 浏览到 {{site.data.keyword.appid_short_notm}} 仪表板的**定制登录页面**选项卡。
2. 在**定制电子邮件地址验证页面的 URL** 中输入登录页面的 URL。

当提供此值时，{{site.data.keyword.appid_short_notm}} 将调用 URL 和 `context` 查询。当您调用 `/sign_up/confirmation_result` 端点并传递接收到的 `context` 参数时，将显示结果，告知您用户是否已验证其帐户。如果已验证，那么您可以显示定制页面。

</br>
**忘记密码**

您可以使用 `/forgot_password` 端点允许用户在忘记密码时恢复其密码。

在请求主体中提供以下数据：
  * 您的租户标识。
  * Cloud Directory 用户的电子邮件。

调用端点时，系统会向用户发送重置密码的电子邮件。该电子邮件包含**重置**按钮。按下该按钮后，{{site.data.keyword.appid_short_notm}} 将显示一个允许用户重置其密码的屏幕。

您可以提供您自己的重置密码后的页面：

1. 浏览到 {{site.data.keyword.appid_short_notm}} 仪表板的**定制登录页面**选项卡。
2. 在**定制重置密码页面的 URL** 中输入登录页面的 URL  

当提供此值时，{{site.data.keyword.appid_short_notm}} 将调用 URL 和 `context` 查询。`context` 参数用于在调用 `/forgot_password/confirmtion_result` 时接收结果。如果结果成功，那么可以显示定制页面。

向定制重置密码页面添加一个随机字符串，并在提交请求时将其传递到后端。让您的处理程序验证字符串，并仅在其有效时调用 `/change_password` 端点。这样做，您可以降低后端重置密码端点的漏洞。
{: tip}

</br>
**更改密码**

在两种情况下，可以使用 `/change_password` 端点。当用户提交重置请求时，或者用户登录到应用程序并想要更新其密码时。

在请求主体中提供以下数据以在重置请求后更新其密码：
  * 您的租户标识。
  * 用户新密码
  * Cloud Directory 用户 UUID。
  * 可选：执行密码重置的 IP 地址。如果您选择传递 IP 地址，那么占位符 `%{passwordChangeInfo.ipAddress}` 可用于更改密码电子邮件模板。

根据您的配置，当更改密码时，{{site.data.keyword.appid_short_notm}} 可能会向用户发送电子邮件，告知用户发生密码更改。

</br>
要允许用户登录应用程序更改其密码：

在请求主体中提供以下数据：
  * 您的租户标识。
  * 用户新密码
  * Cloud Directory 用户 UUID。

您的更改密码页面应提示用户输入其当前密码及其新密码。
{: tip}

您的后端使用 ROP API 验证用户的当前密码，如果有效，则使用新密码调用端点。根据您的配置，当更改密码时，{{site.data.keyword.appid_short_notm}} 可能会向用户发送电子邮件，告知用户发生密码更改。

</br>
**重新发送**

您可以使用 `/resend/{templateName}` 在用户由于某种原因而未接收到电子邮件时重新发送电子邮件。

在请求主体中提供以下数据：
  * 租户标识。
  * 模板名称
  * Cloud Directory 用户 UUID。


**更改详细信息**

当用户登录到应用程序时，他们可以更新其部分信息。您可以使用 `/Users/{userId}` 来获取和更新其信息。

更新用户详细信息后，端点会以 [SCIM 格式](https://tools.ietf.org/html/rfc7643#section-8.2) 获取请求主体中更新的用户数据。请确保仅更改相关详细信息。

无法更改其电子邮件地址。
{: tip}
