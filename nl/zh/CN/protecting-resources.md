---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 保护后端资源的安全

您可以使用 {{site.data.keyword.appid_short_notm}} 服务器 SDK 来保护并访问应用程序中的端点。您还可以使用客户端 SDK 来访问受保护资源。

**注**：调用受保护资源会根据需要启动登录窗口小部件。如果已经获取有效的令牌，那么不会启动登录窗口小部件，而是会直接访问该资源。

## 保护 Liberty for Java 中的资源
{: #protecting-liberty}

可以使用 {{site.data.keyword.appid_short_notm}} 来保护 IBM Liberty for Java 应用程序中的端点。Liberty for Java 中内置了处理 OpenID Connect (OIDC) 请求的能力。

开始之前：
* 您需要一个未绑定的现有 [IBM Liberty for Java 应用程序](https://console.bluemix.net/catalog/starters/liberty-for-java)。要熟悉如何开发 Liberty for Java 应用程序，请参阅相关[文档](/docs/runtimes/liberty/index.html)。
* 确保已安装 [Apache Maven](https://maven.apache.org/download.cgi)。
* 了解 OIDC 如何与 Liberty for Java 一起运作。

要保护您的资源，请执行以下操作：

1. 从 UI 下载 Liberty for Java 样本。该样本包含一个 zip 文件，其中含有标准 Liberty 文件。
2. 在解压缩样本的目录中打开终端。
3. 使用 Cloud Foundry 命令行，登录到 {{site.data.keyword.Bluemix_notm}}。根据提示，输入您的凭证。

  ```
  cf login
  ```
  {: codeblock}

4. 部署应用程序。运行以下命令会创建一个名称与租户标识相关的 Liberty for Java 实例。

  ```
  cf push
  ```
  {: codeblock}

5. 将您的服务实例绑定到新的 Liberty for Java 实例，然后重新部署应用程序。
6. 在浏览器中打开您的应用程序，然后使用您的凭证进行登录，以查看认证活动。

## 在 Node.js 中保护资源
{: #protecting-resources-nodesdk}

{{site.data.keyword.appid_short_notm}} 服务器 SDK 提供了用于 {{site.data.keyword.Bluemix_notm}} 上部署的后端应用程序的 ApiStrategy 通行证策略。要保护应用程序不受未经授权的访问，您必须使用 ApiStrategy 检测 Node.js 服务器。`appid-serversdk-nodejs npm 模块`提供了 ApiStrategy 通行证策略和验证方法，以验证 {{site.data.keyword.appid_short_notm}} 发出的访问令牌和身份令牌。

{{site.data.keyword.appid_short_notm}} 服务器 SDK 使用 <a href="http://passportjs.org/" target="_blank">Passport 框架 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来强制实施授权。

以下片段演示了如何在简单 Express 应用程序中使用 `APIStrategy` 来保护 `/protected` 端点 GET 方法。

  ```JavaScript

var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)    
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
```
  {: codeblock}


## 使用 iOS Swift SDK 访问受保护资源
{: #requesting-swift}

1. 导入 BMSCore。

  ```swift
  import BMSCore
  ```
  {: codeblock}

2. 调用受保护资源请求。

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## 使用 Android SDK 访问受保护资源
{: #requesting-android}

1. 调用受保护资源请求。

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
			//code handling the response here
  }
  @Override
	public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
		//code handling the failure here
  });
  ```
  {: codeblock}
