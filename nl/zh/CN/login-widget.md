---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 管理登录体验
使用登录窗口小部件，仅需数分钟即可启动并运行登录流程。您可以随时更新窗口小部件或主题，而不必添加、除去或更改登录源代码。
{: shortdesc}



## 定制登录窗口小部件
{: #login-widget}

您可以配置用于显示徽标和选项颜色的登录窗口小部件。
{: shortdesc}

{{site.data.keyword.appid_short}} 服务配置有两个或更多身份提供者时，用户可以在登录窗口小部件中选择身份提供者。
通过完成以下步骤，可以定制登录窗口小部件：

1. 打开 {{site.data.keyword.appid_short_notm}} 服务仪表板。
2. 选择**登录定制**部分，在其中可以修改登录窗口小部件的外观，使其与您公司的品牌保持一致。
3. 通过从本地系统中选择 PNG 或 JPG 文件来上传您公司的徽标。建议的图像大小为 320 x 320 像素。最大文件大小为 100 Kb。
4. 从颜色选取器中选择窗口小部件的标题颜色，或者输入其他颜色的十六进制代码。
5. 检查预览窗格，对定制满意后，单击**保存更改**。此时将显示确认消息。

**注**：您无需重新构建应用程序。该图像会存储在 {{site.data.keyword.appid_short}} 数据库中，并在下次登录时显示。

## 使用 Android SDK 运行登录窗口小部件
{: #authenticate-android}

如果配置了多个身份提供者，那么在用户访问应用程序时会显示登录窗口小部件。缺省情况下，如果仅配置一个身份提供者，那么用户会重定向到已配置的身份提供者认证屏幕。


初始化 {{site.data.keyword.appid_short_notm}} 客户端 SDK 后，可以通过运行登录窗口小部件来对用户进行认证。

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
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //User authenticated
        }
      });
  ```
  {: codeblock}

## 使用 iOS SDK 运行登录窗口小部件
{: #authenticate-ios}

如果配置了多个身份提供者，那么在用户访问应用程序时会显示登录窗口小部件。缺省情况下，如果仅配置一个身份提供者，那么用户会重定向到已配置的身份提供者认证屏幕。


1. 将以下 import 语句添加到要在其中使用 SDK 的文件中。

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. 运行以下命令来启动该窗口小部件。

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
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

## 使用 Node.js SDK 运行登录窗口小部件
{: #authenticate-nodejs}

可以使用 `WebAppStrategy` 来保护 Web 应用程序资源。

  ```JavaScript

var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {: codeblock}


## 使用 Swift SDK 运行登录窗口小部件
{: #authenticate-swift}

WebAppKituraCredentialsPlugin 基于 OAuth2 authorization_code 授权流程，并且必须用于使用浏览器的 Web 应用程序。此插件提供了用于实施认证和授权流程的工具。此插件还提供了相应机制来检测对受保护资源的未经认证的访问尝试，并自动将用户的浏览器重定向到认证页面。成功认证后，用户会转至 Web 应用程序的回调 URL，该 URL 使用此插件从 {{site.data.keyword.appid_short_notm}} 获取访问令牌和身份令牌。获取这些令牌后，此插件会将其存储在 HTTP 会话中的 WebAppKituraCredentialsPlugin.AuthContext 下。

以下代码演示了如何在 Kitura 应用程序中使用 WebAppKituraCredentialsPlugin 来保护 `/protected` 端点。

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
