---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 管理 Cloud Directory
{: #cd}

您可以配置 {{site.data.keyword.appid_short_notm}}，以将 Cloud Directory 用作身份提供者。当用户使用电子邮件登录时，他们将添加到您的目录中，然后您便可以从服务 GUI 管理这些用户。
{: shortdesc}

<!--- What is a cloud directory? --->

## 管理目录设置

您可以配置通知以及用户对应用程序的控制级别。在 GUI 的**目录设置**标签中，您可以决定用户可执行的自助服务。

1. 要允许用户使用电子邮件注册，必须将**允许用户注册并重置密码**设置为**开启**。当其设置为**关闭**时，您仍可通过控制台添加用户，但仅适用于开发目的。
2. 配置发件人详细信息。指定将发送消息的电子邮件、显示谁为发件人以及用户可回复的对象。
  **注**：确保在配置操作 URL 时，为用户提供足够用于单击链接的时间。用户必须验证其电子邮件中包含特定选项，例如，请求重置其密码的功能。
3. 确定用户将接收的电子邮件类型以及发件人信息。



## 管理消息

模板是您可发送给用户的电子邮件示例。您可以通过更新消息的内容和布局来定制模板。在目录设置标签中，可将这些消息设置为**开启**或**关闭**。

1. 选择**消息类型**。
2. 通过更改消息的内容和设计，对消息进行定制。可以使用参数对消息进行个性化操作。切记保存更改！

### 消息的类型

<dl>
  <dt> 欢迎</dt>
    <dd>在用户注册后，您可以通过电子邮件欢迎用户使用您的应用程序。要欢迎用户加入并留住用户，尽可能让消息充满吸引力。
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 任何消息类型中均可使用的参数</th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> 显示为登录窗口小部件配置的图像。</td>
        </tr>
	 <tr>
          <td> %{display.headerColor} </td>
          <td> 显示为登录窗口小部件配置的标题颜色。</td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> 显示用户所选在与应用程序交互时要使用的屏幕名称。</td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> 显示用户的注册电子邮件地址。</td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> 显示用户的指定名字。</td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> 显示用户的全名。</td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> 显示用户的指定姓氏。</td>
        </tr>
      </tbody>
    </table>

    **注**：如果用户未提供参数拉出的信息，将显示为空。</dd>
  <dt> 忘记密码</dt>
    <dd> 用户在忘记密码或出于任何原因需要更新密码时，可要求重置密码。您可以定制对这些请求的电子邮件响应。当用户请求更改时，在他们单击此电子邮件中的链接之前，其密码仍保持未更改状态。

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 密码更改参数</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 显示链接保持有效的时数。</td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 显示链接保持有效的分钟数。</td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> 在 URL 中，显示一次性密码作为其中一部分。这意味着每个人都会收到不同的代码。示例：<code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> 显示用户单击以重置密码的链接。</td>
        </tr>
       </tbody>
    </table></dd>
  <dt> 验证</dt>
    <dd> 您可以请求用户通过电子邮件验证其帐户。通过请求验证，您可以限制可注册应用程序的伪帐户数。您可以限制为当用户已验证电子邮件后才可访问应用程序，或用于管理您将为哪些用户创建概要文件。<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 验证消息参数</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 显示链接保持有效的时数。</td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 显示链接保持有效的分钟数。</td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> 显示一次性验证 URL。</td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> 显示在设置中指定的操作 URL。</td>
        </tr>
      </tbody>
    </table></dd>
  <dt> 密码更改</dt>
    <dd> 您可以在用户密码进行更新后告知用户。如果用户并未请求更改密码，这将很有用。他们可以采取适当步骤来重新保护帐户的安全。

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 密码更改参数</th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> 显示新密码生效的时间。</td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> 显示请求更改密码的 IP 地址。</td>
        </tr>
      </tbody>
    </table></dd>
</dl>



## 使用 Android SDK 管理 Cloud Directory
{: #managing-android}

使用以下 API 时，确保将 **Cloud Directory 身份提供者**设置为**开启**。

### 使用资源所有者密码进行登录
通过提供最终用户的用户名和密码，可获取访问和标识令牌。

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

### 注册

确保在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。

 使用 LoginWidget 类启动注册流程。
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
			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
				 if (accessToken != null && identityToken != null) {
				     //User authenticated
				 } else {
				     //email verification is required
				 }

			 }
		 });
 ```
 {: codeblock}

### 忘记密码
确保在 Cloud Directory 的设置中，将**允许用户注册并重置密码**和**忘记密码电子邮件**设置为**开启**。

使用 LoginWidget 类启动忘记密码流程。
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
 			 public void onAuthorizationFailure (AuthorizationException exception) {
 				 //Exception occurred
		}
	@Override
        public void onAuthorizationCanceled () {
          //forogt password canceled by the user
 			 }

 			 @Override
 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
 				 //forgot password finished, in this case accessToken and identityToken will be null.

 			 }
 		 });
  ```
  {: codeblock}

### 更改详细信息
确保在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。使用 LoginWidget 类启动更改详细信息流程。仅当用户使用 Cloud Directory 作为其身份提供者登录时，才可使用此 API。
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  				 //Exception occurred
		}
	@Override
        public void onAuthorizationCanceled () {
          //changed details canceled by the user
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  				 //User authenticated, and fresh tokens received
  			 }
  		 });
   ```
   {: codeblock}

### 更改密码
确保在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。

使用 LoginWidget 类启动更改密码流程。仅当用户使用 Cloud Directory 作为其身份提供者登录时，才可使用此 API。

   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   				 //Exception occurred
		}
	@Override
        public void onAuthorizationCanceled () {
          //change password canceled by the user
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   				   //User authenticated, and fresh tokens received
   			 }
   		 });
   ```
   {: codeblock}

## 使用 iOS Swift SDK 管理 Cloud Directory


### 使用资源所有者密码进行登录

通过提供最终用户的用户名和密码，可获取访问和标识令牌。
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

### 注册

确保在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。

使用 LoginWidget 类启动注册流程。
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

### 忘记密码
确保在 Cloud Directory 的设置中，将**允许用户注册并重置密码**和**忘记密码电子邮件**设置为**开启**。

使用 LoginWidget 类启动忘记密码流程。
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

### 更改详细信息

确保在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。

使用 LoginWidget 类启动更改详细信息流程。仅当用户使用 Cloud Directory 作为其身份提供者登录时，才可使用此 API。
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

### 更改密码

确保在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。

使用 LoginWidget 类启动更改密码流程。仅当用户使用 Cloud Directory 作为身份提供者登录时，才可使用此 API。
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


## 使用 Node.js SDK 管理 Cloud Directory
确保 Cloud Directory 身份提供者设置为**开启**，并包含回调端点。

### 使用资源所有者密码流程进行登录
WebAppStrategy 允许用户使用用户名和密码登录到 Web 应用程序。成功登录后，用户的访问令牌会持久存储在 HTTP 会话中，并且只要保持活动状态即可一直可用。当 HTTP 会话销毁或到期后，令牌也将销毁。

要允许用户使用用户名和密码登录，请向应用程序添加将使用用户名和密码参数调用的发布路径。

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
      <th colspan=2><img src="images/idea.png"/> 了解此命令组件</th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> 将此值设置为用户成功认证后，希望将用户重定向的目标位置 URL。缺省值为原始请求 URL。示例：<code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td> 将此值设置为用户认证失败后，希望将用户重定向的目标位置 URL。缺省值为原始请求 URL。</td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td> 将此值设置为 <code>true</code> 以接收从 Cloud Directory 返回的错误消息。缺省值为 false。</td>
      </tr>
     </tbody>
  </table>


**注**：
  * 如果使用 HTML 表单提交请求，请使用 [body-parser](https://www.npmjs.com/package/body-parser) 中间件。
  * 使用 [connect-flash](https://www.npmjs.com/package/connect-flash) 以获取返回的错误消息。请参阅 `web-app-sample-server.js`。

### 注册
要启动 {{site.data.keyword.appid_short_notm}} 注册表单，请传递 WebAppStrategy“show”属性，并将其设置为 `WebAppStrategy.SIGN_UP`。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

    **注**：
    * 如果在 Cloud Directory 设置中，**允许用户无需电子邮件验证即可登录**设置为**否**，那么该进程将结束，而不会检索 {{site.data.keyword.appid_short_notm}} 访问令牌和标识令牌。
    * 确保在 Cloud Directory 设置中，将**允许用户注册并重置密码**设置为**开启**。


### 忘记密码
要启动 {{site.data.keyword.appid_short_notm}} 忘记密码表单，请传递 WebAppStrategy `show` 属性，并将其设置为 `WebAppStrategy.FORGOT_PASSWORD`。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

**注**：
* 如果在 Cloud Directory 设置中，**允许用户无需电子邮件验证即可登录**设置为**否**，那么该进程将结束，而不会检索 {{site.data.keyword.appid_short_notm}} 访问令牌和标识令牌。
* 确保在 Cloud Directory 设置中，将**允许用户注册并重置密码**和**忘记密码电子邮件**设置为**开启**。

### 更改详细信息
要启动 {{site.data.keyword.appid_short_notm}} 更改详细信息表单，请传递 WebAppStrategy `show` 属性，并将其设置为 `WebAppStrategy.CHANGE_DETAILS`。
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

**注**：
* 必须使用 Cloud Directory 作为身份提供者来认证用户。
* 确保在 Cloud Directory 设置中，将**允许用户注册并重置密码**设置为**开启**。


### 更改密码
要启动 {{site.data.keyword.appid_short_notm}} 更改密码表单，请传递 WebAppStrategy `show` 属性，并将其设置为 `WebAppStrategy.CHANGE_PASSWORD`。
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

**注**：
* 必须使用 Cloud Directory 作为身份提供者来认证用户。
* 确保在 Cloud Directory 设置中，将**允许用户注册并重置密码**设置为**开启**。
