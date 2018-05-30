---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# 管理登录体验

{{site.data.keyword.appid_full}} 提供了一个登录窗口小部件，使您能够为用户提供安全登录选项。
{: shortdesc}

当您的应用程序配置为使用身份提供者时，登录窗口小部件会将应用程序的访问者定向到登录屏幕。缺省情况下，仅一个提供者设置为开启，访问者会重定向到该身份提供者的认证屏幕。借助登录窗口小部件，可以显示缺省的登录屏幕，或者可以通过 Cloud Directory 复用现有 UI。

您可以随时更新登录流程，而无需以任何方式更改源代码！
{: tip}

此服务使用 OAuth 2 授权类型映射授权过程。在配置社交身份提供者（如 Facebook）时，会使用 [Oauth2 授权流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)来调用登录窗口小部件。当您显示自己的 UI 屏幕时，[资源所有者密码凭证流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)可用于登录以及获取访问和身份令牌。


## 定制缺省登录屏幕
{: #login-widget}

您可以定制预配置的登录屏幕以显示您选择的徽标和颜色。
{: shortdesc}

要定制屏幕：

1. 打开 {{site.data.keyword.appid_short_notm}} 服务仪表板。
2. 选择**登录定制**部分。您可以修改登录窗口小部件的外观，使其与贵公司的品牌保持一致。
3. 通过从本地系统中选择 PNG 或 JPG 文件来上传您公司的徽标。建议的图像大小为 320 x 320 像素。最大文件大小为 100 Kb。
4. 从颜色选取器中选择窗口小部件的标题颜色，或者输入其他颜色的十六进制代码。
5. 检查预览窗格，对定制满意后，单击**保存更改**。此时将显示确认消息。
6. 在浏览器中，刷新登录页面以验证您的更改。


## 显示缺省屏幕
{: #default}

{{site.data.keyword.appid_short_notm}} 提供了缺省登录屏幕，如果您没有自己的 UI 屏幕需要显示，那么可以进行调用。
{: shortdesc}

根据您的身份提供者配置，可以显示不同屏幕。此服务不提供社交身份提供者的高级功能，因为我们从不具有用户帐户信息的访问权。用户必须转至身份提供者来管理其信息。例如，如果他们希望更改其 Facebook 密码，那么他们需要转至 www.facebook.com。

查看下表，了解对于各种身份提供者可以显示哪些屏幕。

<table>
  <thead>
    <tr>
      <th>显示屏幕</th>
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

在针对[社交身份提供者](/docs/services/appid/identity-providers.html)和 [Cloud Directory](/docs/services/appid/cloud-directory.html) 配置完您的设置后，单击下图中所选语言，开始实现代码。


单击下图中您所选的语言，以开始实现代码。

<img usemap="#default-options-map" border="0" class="image" id="options" src="images/default-options.png" width="750" alt="单击 SDK 语言，开始在您的应用程序中使用 Cloud Directory。" style="width:750px;" />
<map name="default-options-map" id="default-options-map">
<area href="login-widget.html#android" alt="使用 Android SDK 管理登录体验。" shape="rect" coords="113, 8, 224, 123" />
<area href="login-widget.html#ios-swift" alt="使用 iOS Swift SDK 管理登录体验。" shape="rect" coords="251, 12, 362, 127" />
<area href="login-widget.html#nodejs" alt="使用 Node.js SDK 管理登录体验。" shape="rect" coords="387, 10, 498, 125" />
<area href="login-widget.html#swift" alt="使用 Swift SDK 管理登录体验。" shape="rect" coords="525, 10, 636, 125" />
</map>
</br>

### 使用 Android SDK 显示缺省屏幕
{: #android}

您可以使用 Android SDK 调用预先配置的屏幕。
{: shortdesc}

</br>

**登录**
1. 将以下命令放在代码中。
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
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 if (accessToken != null && identityToken != null) {
				     } else {
  			 }

  		 }
  	 });
  ```
  {: pre}

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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
    ```
    {: pre}

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
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 }
  		 });
   ```
   {: pre}

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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
   ```
   {: pre}
</br>
</br>

### 使用 iOS Swift SDK 显示缺省屏幕
{: #ios-swift}

您可以使用 iOS Swift SDK 调用预先配置的屏幕。
{: shortdesc}

</br>
**登录**

1. 将以下命令放在代码中。
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
**注册**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 调用 LoginWidget 以开始注册流程。
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
**忘记密码**
1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**和**忘记密码电子邮件**设置为**开启**。
2. 调用 LoginWidget 以开始忘记密码流程。
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
**帐户详细信息**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 调用 LoginWidget 以开始更改详细信息流程。
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
**更改密码**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。
2. 调用 LoginWidget 以开始更改密码流程。
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

### 使用 Node.js SDK 显示缺省屏幕
{: #nodejs}

您可以使用 Node.js SDK 来调用预先配置的屏幕。
{: shortdesc}

</br>
**登录**

1. 在身份提供者设置中，将 Cloud Directory 设置为**开启**，然后指定回调端点。
2. 为应用程序添加发布路径（可以使用用户名和密码参数来调用该路径），然后使用资源所有者密码登录。

    ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
    {: pre}
    利用 `WebAppStrategy`，用户可以使用用户名和密码登录 Web 应用程序。成功登录后，用户的访问令牌会存储在 HTTP 会话中，并在整个会话过程中可用。当 HTTP 会话销毁或到期后，令牌会失效。
    {: tip}

</br>
**注册**

1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**设置为**开启**。如果设置为“否”，那么到该流程结束也不会检索访问令牌和身份令牌。
2. 传递 WebAppStrategy `show` 属性并将其设置为 `WebAppStrategy.SIGN_UP`。
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**忘记密码**
1. 在 Cloud Directory 的设置中，将**允许用户注册并重置密码**和**忘记密码电子邮件**设置为**开启**。如果设置为“否”，那么到该流程结束也不会检索访问令牌和身份令牌。
2. 传递 WebAppStrategy `show` 属性并将其设置为 `WebAppStrategy.FORGOT_PASSWORD`。
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

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
  {: pre}

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
  {: pre}

</br>
</br>
### 使用 Swift SDK 显示缺省 UI
{: #swift}

在启用社交身份提供者的情况下，可以使用 Swift SDK 来调用预配置的登录屏幕。
{: shortdesc}

1. 以下代码演示了如何在 Kitura 应用程序中使用 WebAppKituraCredentialsPlugin 来保护 `/protected` 端点。

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


### 使用 Android SDK 显示定制屏幕
{: #branded-ui-android}

在启用 Cloud Directory 的情况下，可以使用 Android SDK 来调用定制屏幕。您可以选择希望用户能够与其进行交互的屏幕组合。<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">查看此博客 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 以获取详细示例！
{: shortdesc}

</br>
**登录**

1. 将 **Cloud Directory** 作为身份提供者设置为**开启**。
2. 将以下命令放在代码中。
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
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
  {: pre}

</br>
</br>

### 使用 iOS Swift SDK 显示定制屏幕
{: #branded-ui-ios-swift}

在启用 Cloud Directory 的情况下，可以使用 iOS Swift SDK 来调用定制屏幕。
{: shortdesc}

</br>
**登录**

1. 在 GUI 上的身份提供者选项卡中，将 Cloud Directory 设置为**开启**。
2. 使用资源所有者密码登录。当用户尝试使用其用户名和密码登录时，会获取访问令牌和身份令牌。
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
</br>

### 使用 Node.js SDK 显示定制屏幕
{: #branded-ui-nodejs}

在启用 Cloud Directory 的情况下，可以使用 Node.js SDK 来调用定制屏幕。您想让用户能跟哪些屏幕交互？可以选择将这些屏幕组合起来。如果选择 Node.js 后端，那么您可以使用 {{site.data.keyword.appid_short_notm}}Node.js SDK（链接）中的自助服务模块。
{: shortdesc}

**登录**
1. 在身份提供者设置中，将 Cloud Directory 设置为**开启**，然后指定回调端点。
2. 为应用程序添加发布路径（可以使用用户名和密码参数来调用该路径），然后使用资源所有者密码登录。

    ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
    {: pre}
    利用 `WebAppStrategy`，用户可以使用用户名和密码登录 Web 应用程序。成功登录后，用户的访问令牌会存储在 HTTP 会话中，并在整个会话过程中可用。当 HTTP 会话销毁或到期后，令牌也会失效。
    {: tip}

</br>
</br>

## 使用 API 显示定制屏幕
{: #branding}

您可以显示自己的定制屏幕，并利用 {{site.data.keyword.appid_short_notm}} 的认证和授权功能。利用 Cloud Directory 作为身份提供者，用户不需要多少帮助就可以与应用程序进行交互。用户无需寻求帮助就可以完成登录、注册、重置密码等操作。
{: shortdesc}

为了实现此目标，{{site.data.keyword.appid_short_notm}} 公开了 REST API。您可使用该 REST API 构建为 Web 应用程序提供服务的后端服务器，或使用自己的定制屏幕与移动应用程序进行交互。

管理 API 通过 IBM Cloud Identity and Access Management 生成的令牌进行保护。这意味着帐户所有者可以指定团队成员对每个服务实例的访问级别。有关 IAM 和 {{site.data.keyword.appid_short_notm}} 如何协作的更多信息，请参阅[服务访问管理](/docs/services/appid/iam.html)。

当用户从定制屏幕单击登录时，[资源所有者密码凭证流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)可用于从您的 Web 或移动应用程序直接获取访问和身份令牌。

在您配置完[设置](/docs/services/appid/cloud-directory.html)之后，


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

要在重置请求后更新其密码：

在请求主体中提供以下数据：
  * 您的租户标识。
  * 用户新密码
  * Cloud Directory 用户 UUID。
  * 可选：执行密码重置的 IP 地址。如果您选择传递 IP 地址，那么占位符 `%{passwordChangeInfo.ipAddress}`  可用于更改密码电子邮件模板。

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
