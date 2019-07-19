---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-11"

keywords: Authentication, authorization, identity, app security, secure, development, access management, liberty, backend, java, token

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


# 后端：Liberty for Java
{: #backend-liberty}

通过 {{site.data.keyword.appid_short_notm}}，您可以轻松保护 API 端点，并确保 Liberty for Java 后端应用程序的安全性。使用本指南，您可以在不到 20 分钟的时间内快速入门和熟悉运用简单的认证流程。
{: shortdesc}


![后端 Liberty for Java 应用程序](images/backend_liberty.png)

1. 要向受保护资源发出请求，客户机必须具有访问令牌。在步骤 1 中，客户机向 {{site.data.keyword.appid_short_notm}} 发出请求以获取令牌。有关获取访问令牌的更多信息，请参阅[获取令牌](/docs/services/appid?topic=appid-obtain-tokens)。
2. {{site.data.keyword.appid_short_notm}} 返回令牌。
3. 客户机使用访问令牌来发出访问受保护资源的请求。
4. 资源验证令牌，包括结构、到期时间、签名、受众和其他任何提供的字段。如果令牌无效，那么资源服务器将拒绝访问。如果令牌验证成功，资源服务器将返回数据。


## 视频教程
{: #backend-liberty-video}

请查看以下视频，以了解如何使用 {{site.data.keyword.appid_short_notm}} 来保护简单的 Liberty for Java 应用程序。视频中涵盖的所有信息还可在此页面上找到对应的书面文字。

<iframe class="embed-responsive-item" id="appid-liberty-backend-app" title="关于 {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/QA6DY2qqLaw?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe> 您没有可以试用此流程的应用程序吗？没问题！{{site.data.keyword.appid_short_notm}} 提供了[简单的 Liberty for Java 样本应用程序](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02d-simple-liberty-backend-app)。


## 开始之前
{: #liberty-before}

在 Liberty for Java 后端应用程序中开始使用 {{site.data.keyword.appid_short_notm}} 之前，您必须满足以下先决条件：


* [{{site.data.keyword.appid_short_notm}} 服务](https://cloud.ibm.com/catalog/services/app-id){: external}的实例
* [IBM Cloud CLI](/docs/cli?topic=cloud-cli-getting-started)
* [Apache Maven 3.5+](https://maven.apache.org/download.cgi){: external}
* [Java 8+](https://www.java.com/download/){: external}
* [{{site.data.keyword.appid_short_notm}} Postman 集合](https://github.com/ibm-cloud-security/appid-postman){: external}，用于测试

## 步骤 1：获取凭证
{: #liberty-obtain-credentials}

可以通过以下两种方式之一来获取凭证。

  * 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的**应用程序**选项卡。如果尚未具有应用程序，那么可以单击**添加应用程序**来创建新应用程序。

  * 对 [`/management/v4/{tenantId}/applications` 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication){: external}发出 POST 请求。

    请求格式：
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    示例响应：
    ```
    {
      "clientId": "xxxxx-34a4-4c5e-b34d-d12cc811c86d",
      "tenantId": "xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "secret": "ZDk5YWZkYmYt*******",
      "name": "app1",
      "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "profilesUrl": "https://us-south.appid.cloud.ibm.com",
      "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxxx-9b1f-433e-9d46-0a5521f2b1c4/.well-known/openid-configuration"
    }
    ```
    {: screen}


## 步骤 2：配置 `server.xml` 文件
{: #liberty-configure-server}
 
1. 打开 `server.xml` 文件。
2. 将以下功能添加到 `featureManager` 部分。某些功能可能内置于 Liberty。如果在运行服务器时收到错误，那么可以通过从 Liberty 安装的 bin 目录中运行 `.installUtility install <name_of_server>` 来安装这些功能。

    ```xml
    <featureManager>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
    </featureManager>
    ```
    {: codeblock}

3. 通过将以下内容添加到 `server.xml` 文件来配置 SSL。 

    ```xml
    <keyStore id="defaultKeyStore" password="{password}"/>
    <keyStore id="RootCA" password="{password}" location="${server.config.dir}/resources/security/{myTrustStore}"/>
    <ssl id="{sslID}" keyStoreRef="defaultKeyStore" trustStoreRef="{truststore-ref}"/>
    ```
    {: codeblock}

4. 创建 OpenID Connect 客户端功能，并定义以下占位符。使用获取的凭证来填充占位符。

    ```xml
    <openidConnectClient 
        id="oidc-client-simple-liberty-backend-app" 		
        inboundPropagation="required"
        jwkEndpointUrl="{region}.appid.cloud.ibm.com/oauth/v4/{tenantID}/publickeys"
        issuerIdentifier="{region).appid.cloud.ibm.com/oauth/v4/{tenantID}"
        signatureAlgorithm="RS256"
        audiences="{client-id}"
        sslRef="oidcClientSSL"
    /> 	
    ```
    {: codeblock}

    <table>
    <caption>表. Liberty for Java 应用程序的 OIDC 元素变量</caption>
        <tr>
            <th colspan="2"> 了解 OIDC 元素变量</th>
        </tr>
        <tr>
            <td><code>id</code></td>
            <td>应用程序的名称。</td>
        </tr>
        <tr>
            <td><code>inboundPropagation</code></td>
            <td>为了传播在令牌中接收到的信息，该值必须设置为“required”。</td>
        </tr>
        <tr>
            <td><code>jwkEndpointUrl</code></td><td>用于获取密钥以验证令牌的端点。区域选项包括：<code>au-syd</code>、<code>eu-de</code>、<code>eu-gb</code>、<code>jp-tok</code> 和 <code>us-south</code>。您可以在先前创建的凭证中找到租户标识。</td>
        </tr>
        <tr>
            <td><code>issuerIdentifier</code></td><td>颁发者标识用于定义授权服务器。区域选项包括：<code>au-syd</code>、<code>eu-de</code>、<code>eu-gb</code>、<code>jp-tok</code> 和 <code>us-south</code>。您可以在先前创建的凭证中找到租户标识。</td>
        </tr>
        <tr>
            <td><code>signatureAlgorithm</code></td><td>被指定为“RS256”。</td>
        </tr>
        <tr>
            <td><code>audiences</code></td>
            <td>缺省情况下，将为可在应用程序凭证中找到的 {{site.data.keyword.appid_short_notm}} 客户机标识颁发令牌。</td>
        </tr>
        <tr>
            <td><code>sslRef</code></td>
            <td>要使用的 SSL 配置的名称。</td>
        </tr>
    </table>

5. 将特殊主体类型定义为 `ALL_AUTHENTICATED_USERS`。

    ```xml
    <application 
        id="simple-liberty-backend-app" 
        location="location-of-your-war-file" 
        name="simple-liberty-backend-app" 
        type="war">

        <application-bnd>
            <security-role name="myrole">
                <special-subject type="ALL_AUTHENTICATED_USERS"/>
            </security-role>
        </application-bnd>
    </application>
    ```
    {: codeblock}


## 步骤 3：配置 `web.xml` 文件
{: #liberty-configure-web}

在 `web.xml` 文件中，定义要保护的应用程序的区域。

1. 定义安全角色。此角色应该与在 `server.xml` 文件中定义的角色相同。

    ```
    <security-role>
		<role-name>myrole</role-name>
	</security-role>
    ```
    {: codeblock}

2. 定义安全性约束。

    ```
	<security-constraint>
		<display-name>Security Constraints</display-name>
		<web-resource-collection>
			<web-resource-name>ProtectedArea</web-resource-name>
			<url-pattern>/api/*</url-pattern>
		</web-resource-collection>
		<auth-constraint>
			<role-name>myrole</role-name>
		</auth-constraint>
		<user-data-constraint>
			<transport-guarantee>NONE</transport-guarantee>
		</user-data-constraint>
	</security-constraint>
    ```
    {: codeblock}


## 步骤 4：测试配置
{: #liberty-test}

既然您已完成了初始安装，接下来请构建应用程序并测试配置，以确保一切按预期正常运行。

1. 切换到应用程序目录。

2. 构建应用程序。

    ```
    server run
    ```
    {: codeblock}

3. 向受保护端点发出请求。这将返回错误。

4. [获取访问令牌](/docs/services/appid?topic=appid-obtain-tokens)。

5. 使用在上一步中获取的访问令牌，向该端点发出请求。现在，您应该能够访问受保护端点。验证响应是否包含期望的内容。


## 后续步骤
{: #liberty-next}

准备好开始完善认证体验了吗？请尝试完整浏览[此博客](https://www.ibm.com/cloud/blog/perfecting-the-login-experience-with-liberty-oauth2-and-appid){: external}，或了解有关[应用程序到应用程序通信](/docs/services/appid?topic=appid-app)的更多信息。


