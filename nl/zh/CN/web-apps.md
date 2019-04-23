---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, web apps, client, server

subcollection: appid

---

{:new_window: target="_blank"}
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


# Web 应用程序
{: #web-apps}

通过 {{site.data.keyword.appid_full}}，可以为 Web 应用程序快速构造认证层。
{: shortdesc}

## 了解流程
{: #web-understanding}

**此流程在什么时候有用？**

开发 Web 应用程序时，可以使用 {{site.data.keyword.appid_short_notm}} Web 流程来安全地认证用户。然后，用户就可以在 Web 应用程序中访问服务器端受保护的内容。

**流程的技术基础是什么？**

Web 应用程序通常需要用户进行认证才能访问受保护的内容。{{site.data.keyword.appid_short_notm}} 使用 OIDC 授权代码流程来安全地认证用户。通过此流程，在认证用户时，应用程序会收到授权代码。然后，会使用此代码来交换访问令牌、身份令牌和刷新令牌。在代码中，始终通过应用程序和 OIDC 服务器之间的安全反向通道来发送令牌。这使得攻击者无法拦截令牌，因而提供了一层额外的安全性。可以将这些令牌直接发送到托管应用程序的 Web 服务器以进行用户认证。

**此流程是如何运作的？**

![{{site.data.keyword.appid_short_notm}} 请求流程](images/web-flow.png)

1. 用户通过 {{site.data.keyword.appid_short_notm}} SDK 或 API 向 `/authorization` 端点发送请求，以启动授权流程。

2. 如果用户未获授权，那么启动的认证流程会重定向到 {{site.data.keyword.appid_short_notm}}。

3. 根据用户的 `/authorization` 请求参数或身份提供者配置，将在用户的浏览器中启动登录窗口小部件。

4. 用户选择身份提供者以进行认证并完成登录过程。

5. 身份提供者使用授权代码重定向到客户端应用程序。

6. {{site.data.keyword.appid_short_notm}} SDK 使用授权代码来交换来自 {{site.data.keyword.appid_short_notm}} 服务的访问令牌、身份令牌和可选的刷新令牌。

7. 令牌由 {{site.data.keyword.appid_short_notm}} SDK 保存，然后重定向到客户端应用程序。

8. 授权用户访问应用程序。


## 配置 Node.js SDK
{: #web-configuring-nodejs}

可以将 {{site.data.keyword.appid_short_notm}} 配置为使用 Node.js Web 应用程序。
{: shortdesc}

**开始之前**

您必须满足以下先决条件：

* {{site.data.keyword.appid_short_notm}} 服务的实例
* 一组服务凭证
* NPM V4 或更高版本
* Node V6 或更高版本
* 在 {{site.data.keyword.appid_short_notm}} 服务仪表板中设置的重定向 URI


### 安装 Node.js SDK
{: #web-nodejs-install}

1. 使用命令行切换到包含 Node.js 应用程序的目录。

2. 安装 {{site.data.keyword.appid_short_notm}} 服务。

  ```bash
  npm install --save ibmcloud-appid
  ```
  {: pre}

### 初始化 Node.js SDK
{: #web-nodejs-initialize}

1. 将以下 `require` 定义添加到 `server.js` 文件。
    

  ```javascript
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
  {: pre}

2. 将 express 应用程序设置为使用 express-session 中间件。

  ```javascript
    const app = express();
    app.use(session({
        secret: "123456",
        resave: true,
        saveUninitialized: true
        }));
    app.use(passport.initialize());
    app.use(passport.session());
    ```
  {: pre}

  必须针对生产环境为中间件配置合适的会话存储量。有关更多信息，请参阅 <a href="https://github.com/expressjs/session" target="_blank">express.js 文档 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。
  {: note}

3. 通过以下其中一种方式获取凭证。

  * 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的**应用程序**选项卡。如果未列出应用程序，那么可以单击**添加应用程序**来创建新应用程序。

  * 对 [`/management/v4/{tenantId}/applications` 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication)发出 POST 请求。

    请求格式：
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: pre}

    示例响应：
    ```
    {
    "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
    "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
    "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
    "name": "ApplicationName",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61"
    }
    ```
    {: screen}

4. 可选：决定如何设置重定向 URI 的格式。重定向的格式可以通过两种不同方式进行设置。

  * 在新的 `WebAppStrategy({redirectUri: "...."})` 中手动设置
  * 设置为名为 `redirectUri` 的环境变量

  如果未提供以上任何一个选项，那么 {{site.data.keyword.appid_short_notm}} SDK 将尝试检索正在 {{site.data.keyword.cloud_notm}} 上运行的应用程序的 `application_uri` 并附加缺省后缀 `/ibm/cloud/appid/callback`。

5. 使用先前步骤中获取的信息来初始化 SDK。

  ```javascript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: pre}

6. 使用序列化和反序列化来配置 passport。此配置对于跨 HTTP 请求的已认证会话持久性是必需的。有关更多信息，请参阅 <a href="http://passportjs.org/docs" target="_blank">passport 文档 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。

  ```javascript
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

    passport.deserializeUser(function(obj, cb) {
      cb(null, obj);
    });
  ```
  {: pre}

5. 将以下代码添加到 `server.js` 文件以发出服务重定向。

   ```javascript
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   ```
   {: pre}

6. 注册受保护端点。

   ```javascript
   app.get(‘/protected’, passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res) {res.json(req.user); });
   ```
   {: pre}

有关更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub 存储库 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。



## 配置 Liberty for Java SDK
{: #web-configuring-liberty}

可以将 {{site.data.keyword.appid_short_notm}} 配置为与 Liberty for Java Web 应用程序一起运作。
{:shortdesc}

**开始之前**

您必须满足以下先决条件：
* {{site.data.keyword.appid_short_notm}} 服务的实例
* 一组服务凭证
* Apache Maven 3.5 或更高版本
* Java 1.8
* Liberty for Java Web 应用程序

### 安装 Liberty for Java SDK
{: #web-liberty-install}

1. 向 `server.xml` 添加 OpenID Connect 功能。

  ```xml
  <featureManager>
      <feature>ssl-1.0</feature>
      <feature>appSecurity-2.0</feature>
      <feature>openidConnectClient-1.0</feature>
  </featureManager>
  ```
  {: pre}

2. 通过以下两种方式之一来获取凭证。

  * 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的**应用程序**选项卡。如果尚未具有应用程序，那么可以单击**添加应用程序**来创建新应用程序。

  * 对 [`/management/v4/{tenantId}/applications` 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication)发出 POST 请求。

    请求格式：
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: pre}

    示例响应：
    ```
    {
    "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
    "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
    "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
    "name": "ApplicationName",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61"
    }
    ```
    {: screen}

3. 创建 OpenID Connect 客户端功能，并定义以下占位符。使用服务凭证来填充占位符。

  ```xml
  <openidConnectClient
    clientId='{{site.data.keyword.appid_short_notm}} client_ID'
    clientSecret='{{site.data.keyword.appid_short_notm}} Secret'
    authorizationEndpointUrl='oauthServerUrl/authorization'
    tokenEndpointUrl='oauthServerUrl/token'
    jwkEndpointUrl='oauthServerUrl/publickeys'
    issuerIdentifier='Changed according to the region'
    tokenEndpointAuthMethod="basic"
    signatureAlgorithm="RS256"
    authFilterid="myAuthFilter"
    trustAliasName="ibm.com"
  />
  ```
  {: pre}

  <table>
  <caption>表. Liberty for Java 应用程序的 OIDC 元素变量</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
    <td><code>clientID</code></br> <code>secret</code></br> <code>oauth-server-url</code></br></td>
    <td>完成步骤 2 以获取服务凭证。</td>
    </tr>
    <tr>
      <td><code>authorizationEndpointURL</code></td><td> 将 <code>/authorization</code> 添加到 <code>oauthServerURL</code> 的末尾。</td>
    </tr>
    <tr>
      <td><code>tokenEndpointUrl</code></td><td>将 <code>/token</code> 添加到 <code>oauthServerURL</code> 的末尾。</td>
    </tr>
    <tr>
      <td><code>jwkEndpointUrl</code></td><td>将 <code>/publickeys</code> 添加到 <code>oauthServerURL</code> 的末尾。</td>
    </tr>
    <tr>
      <td><code>issuerIdentifier</code></td><td>颁发者标识采用以下格式：<code>&lt;region>&gt;.cloud.ibm.com</code>。区域选项包括：<code>au-syd</code>、<code>eu-de</code>、<code>eu-gb</code>、<code>jp-tok</code> 和 <code>us-south</code>。</td>
    </tr>
    <tr>
      <td><code>tokenEndpointAuthMethod</code></td><td>被指定为“basic”。</td>
    </tr>
    <tr>
      <td><code>signatureAlgorithm</code></td><td>被指定为“RS256”。</td>
    </tr>
    <tr>
      <td><code>authFilterid</code></td><td>要保护的资源的列表。</td>
    </tr>
    <tr>
      <td><code>trustAliasName</code></td><td>信任库中证书的名称。</td>
    </tr>
  </table>

### 初始化 Liberty for Java SDK
{: #web-liberty-initialize}

1. 在 `server.xml` 文件中，定义授权过滤器以指定受保护资源。如果未<a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">定义 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 过滤器，那么服务将保护所有资源。

  ```xml
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: pre}

2. 将特殊主体类型定义为 `ALL_AUTHENTICATED_USERS`。

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample"
  location="${server.config.dir}/apps/libertySample-1.0.0.war">
    <application-bnd>
        <security-role name="myrole">
        <special-subject type="ALL_AUTHENTICATED_USERS"/>
        </security-role>
            </application-bnd>
        </application>
  ```
  {: pre}

3. 从 <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/liberty-for-java" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 下载 `libertySample-1.0.0.war` 文件，并将其放在服务器的 apps 文件夹中。例如，如果服务器名为 `defaultServer`，那么该 WAR 文件将位于以下位置：`target/liberty/wlp/usr/servers/defaultServer/apps/`。

4. 通过将以下内容添加到 `server.xml` 文件来配置 SSL。您还需要创建信任库。

  ```xml
    <keyStore id="defaultKeyStore" password="myPassword"/>
  <keyStore id="appidtruststore" password="Liberty" location="${server.config.dir}/mytruststore.jks"/>
  <ssl id="defaultSSLConfig" keyStoreRef="defaultKeyStore" trustStoreRef="appidtruststore"/>
```
  {: pre}

缺省情况下，SSL 配置需要为 OpenID Connect 配置信任库。了解有关<a href="https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_config_oidc_rp.html" target="_blank">在 Liberty 中配置 OpenID Connect 客户端 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 的更多信息。
{: tip}



## 配置 Spring Boot for Java SDK
{: #web-configuring-spring-boot}

可以将 {{site.data.keyword.appid_short_notm}} 配置为使用 Spring Boot 应用程序。
{:shortdesc}

**开始之前**

您必须满足以下先决条件：

* {{site.data.keyword.appid_short_notm}} 服务的实例
* 一组服务凭证
* Java + Maven 项目
* Apache Maven 3.5 或更高版本
* Java 1.8
* Spring Boot 2.0 和 Security OAuth 2.0 或更高版本


### 初始化 Spring Boot 框架
{: #web-spring-boot-initialize}

1. 将以下内容添加到 Maven `pom.xml` 文件的 `<project> </project>` 标记之间。

  ```xml
  <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.2.RELEASE</version>
      <relativePath/>
  </parent>
  ```
  {: pre}

2. 将以下依赖项添加到 Maven `pom.xml` 文件。

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-web</artifactId>
      </dependency>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-security</artifactId>
      </dependency>
      <dependency>
          <groupId>org.springframework.security.oauth.boot</groupId>
          <artifactId>spring-security-oauth2-autoconfigure</artifactId>
          <version>2.0.0.RELEASE</version>
      </dependency>
  </dependencies>
  ```
  {: pre}

3. 在同一文件中，包含 Maven 插件。

  ```xml
  <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
  </plugin>
  ```
  {: pre}

### 初始化 OAuth2
{: #web-oauth-initialize}

1. 将以下注释添加到 Java 文件中。

  ```java
  @SpringBootApplication
  @EnableOAuth2Sso
  ```
  {: pre}

2. 使用 `WebSecurityConfigurerAdapter` 扩展该类。
3. 覆盖任何安全配置并注册受保护端点。

  ```java
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .antMatchers("/protectedResource").authenticated()
                .and().logout().logoutSuccessUrl("/").permitAll();
    }
  ```
  {: pre}


### 添加凭证
{: #web-spring-boot-credentials}

1. 通过以下其中一种方式获取凭证。

  * 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的**应用程序**选项卡。如果尚未具有应用程序，那么可以单击**添加应用程序**来创建新应用程序。

  * 对 [`/management/v4/{tenantId}/applications` 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication)发出 POST 请求。

    请求格式：
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: pre}

    示例响应：
    ```
    {
    "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
    "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
    "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
    "name": "ApplicationName",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61"
    }
    ```
    {: screen}

2. 将 `application.yml` 配置文件添加到 `/springbootsample/src/main/resources/` 目录。可以使用服务凭证中的信息来完成配置。

  ```
  security:
  oauth2:
    client:
      clientId: {client ID}
      clientSecret: {client Secret}
      accessTokenUri: {oauthServerUrl}/token
      userAuthorizationUri: {oauthServerUrl}/authorization
    resource:
      userInfoUri: {oauthServerUrl}/userinfo
  ```
  {: pre}

有关逐步指导示例，请查看<a href="https://www.ibm.com/blogs/bluemix/2018/06/creating-spring-boot-applications-app-id/" target="_blank">此博客</a>！


## 使用 {{site.data.keyword.appid_short_notm}} 的其他语言版本
{: #web-other-languages}

对于符合 OIDC 的客户端 SDK，可以使用 {{site.data.keyword.appid_short_notm}} 的其他语言版本。请查看<a href="https://openid.net/developers/certified/">认证的库</a>的列表以获取更多信息。

## 后续步骤
{: #web-next}

在应用程序中安装 {{site.data.keyword.appid_short_notm}} 后，您几乎已准备好开始对用户进行认证！接着请尝试执行以下其中一个活动：



* 配置[身份提供者](/docs/services/appid?topic=appid-social)。
* 定制并配置[登录窗口小部件](/docs/services/appid?topic=appid-login-widget)
* 了解有关 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 的更多信息
