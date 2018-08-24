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


# 显示缺省屏幕
{: #default}

{{site.data.keyword.appid_full}} 提供了一个登录窗口小部件，使您能够为用户提供安全登录选项。
{: shortdesc}

当您的应用程序配置为使用身份提供者时，登录窗口小部件会将应用程序的访问者定向到登录屏幕。缺省情况下，仅一个提供者设置为**开启**，访问者会重定向到该身份提供者的认证屏幕。借助登录窗口小部件，可以显示缺省的登录屏幕，或者可以通过 Cloud Directory 复用现有 UI。而且作为的额外奖励，您可以随时更新登录流程，而无需以任何方式更改源代码！



此服务使用 OAuth 2 授权类型映射授权过程。在配置社交身份提供者（如 Facebook）时，会使用 [Oauth2 授权流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)来调用登录窗口小部件。

要创建您的应用程序所特有的体验吗？您可以[自带屏幕](/docs/services/appid/branded.html)！
{: tip}


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


## 规划要显示的屏幕
{: #plan}

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


单击图像以使用其中一个提供的 SDK 或 API。请勿忘记，您还可以使用其他语言的 App ID。通过使用 API，您可以在任何应用程序中设置 Cloud Directory。有关图像中未列出的语言的帮助，请查看<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">我们的博客<img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
{: shortdesc}

</br>

## 使用 Android SDK 显示缺省屏幕
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

## 使用 iOS Swift SDK 显示缺省屏幕
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

## 使用 Node.js SDK 显示缺省屏幕
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
    利用 `WebAppStrategy`，用户可以使用用户名和密码登录 Web 应用程序。成功登录后，用户的访问令牌会存储在 HTTP 会话中，并在整个会话过程中可用。当 HTTP 会话销毁或到期后，令牌也会失效。
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

## 使用 Swift SDK 显示缺省屏幕
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



