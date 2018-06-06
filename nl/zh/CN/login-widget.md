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

# 管理登录体验

利用登录窗口小部件，您可以随时更新登录流程，而无需添加、除去或更改源代码。使用样本应用程序中提供的代码，只需几分钟就可以启动并运行。
{: shortdesc}

**注**：在配置社交身份提供者（如 Facebook）时，会使用 [Oauth2 授权流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)来调用登录窗口小部件。

</br>

## 定制样本应用程序代码
{: #login-widget}

您可以定制预配置的登录屏幕以显示您选择的徽标和颜色。如果要显示自己的品牌 UI，请查看 [Cloud Directory](/docs/services/appid/cloud-directory.html)。
{: shortdesc}

![定制登录体验示例](/images/customize.gif)

要定制屏幕：

1. 打开 {{site.data.keyword.appid_short_notm}} 服务仪表板。
2. 选择**登录定制**部分，在其中可以修改登录窗口小部件的外观，使其与您公司的品牌保持一致。
3. 通过从本地系统中选择 PNG 或 JPG 文件来上传您公司的徽标。建议的图像大小为 320 x 320 像素。最大文件大小为 100 Kb。
4. 从颜色选取器中选择窗口小部件的标题颜色，或者输入其他颜色的十六进制代码。
5. 检查预览窗格，对定制满意后，单击**保存更改**。此时将显示确认消息。
6. 访问应用程序以验证更改是否生效。您无需重新构建应用程序。图像会存储在 {{site.data.keyword.appid_short}} 数据库中，并在下次调用登录窗口小部件时显示。


</br>

## 使用 Android SDK 调用登录窗口小部件
{: #android}

在启用社交身份提供者的情况下，可以使用 Android SDK 来调用预配置的登录屏幕。
{: shortdesc}

1. 配置身份提供者。
2. 将以下命令放在代码中。
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


</br>

## 使用 iOS Swift SDK 调用登录窗口小部件
{: ios-swift}

在启用社交身份提供者的情况下，可以使用 iOS Swift SDK 来调用预配置的登录屏幕。
{: shortdesc}

1. 配置身份提供者。
2. 将以下命令添加到应用程序代码中。
  ```swift
  import BluemixAppID
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


</br>

## 使用 Node.js SDK 调用登录窗口小部件
{: #nodejs}

在启用社交身份提供者的情况下，可以使用 Node.js SDK 来调用预配置的登录屏幕。
{: shortdesc}

1. 配置身份提供者。
2. 将以下命令添加到代码中。
    ```JavaScript

    var express = require('express');
    var passport = require('passport');
    var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
    ```
    {: codeblock}


</br>

## 使用 Swift SDK 调用登录窗口小部件
{: #swift}

在启用社交身份提供者的情况下，可以使用 Swift SDK 来调用预配置的登录屏幕。
{: shortdesc}

WebAppKituraCredentialsPlugin 基于 OAuth2 授权代码授予流程，必须用于使用浏览器的 Web 应用程序。此插件提供了用于实施认证和授权流程的工具。此插件还提供了相应机制来检测对受保护资源的未经认证的访问尝试，并自动将用户的浏览器重定向到认证页面。成功认证后，用户会转至 Web 应用程序的回调 URL，该 URL 使用此插件从 {{site.data.keyword.appid_short_notm}} 获取访问令牌和身份令牌。获取这些令牌后，此插件会将其存储在 HTTP 会话中的 WebAppKituraCredentialsPlugin.AuthContext 下。

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
