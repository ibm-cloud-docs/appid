---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

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

# SAML
{: #enterprise}

具有基于 SAML 的身份提供者时，可以将 {{site.data.keyword.appid_short_notm}} 配置为充当服务提供者，用于启动向第三方提供者的单点登录 (SSO)。在登录流程中，用户可以轻松进行认证，并能够获取 {{site.data.keyword.appid_short_notm}} 安全性令牌，通过这些令牌，用户可以访问应用程序和受保护的 API。
{: shortdesc}

 
使用的是特定 SAML 身份提供者？请查看有关使用 [Ping One ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-ping-one)、[Azure Active Directory ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory) 或 [Active Directory Federation Service ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service) 设置 {{site.data.keyword.appid_short_notm}} 的其中一个博客帖子。
{: tip}


## 了解 SAML
{: #saml-understanding}

安全性断言标记语言 (SAML) 是断言用户身份的身份提供者和使用用户身份信息的服务提供者之间交换认证和授权数据的开放式标准。
{: shortdesc}


<a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 协议支持不同的概要文件和绑定选项。{{site.data.keyword.appid_short_notm}} 通过 HTTP Post 绑定支持 Web 浏览器 SSO 概要文件。

### 流程的技术基础是什么?
{: #saml-tech-basis}

SAML 2.0 是最成熟的认证和授权标准框架之一。这是服务提供者 ({{site.data.keyword.appid_short_notm}}) 与身份提供者之间基于 XML 的协议。身份提供者认证用户时，会创建 SAML 令牌，其中包含有关用户的断言或陈述。陈述可能包含：

- 认证信息，例如如何对用户进行认证 - 密码、MFA 等...
- 与用户关联的属性 - 用户所属的组。
- 授权决策，指出是否允许用户对特定资源执行特定操作。

断言返回到 {{site.data.keyword.appid_short_notm}} 时，服务会联合用户身份，并生成相应的令牌。如果 SAML 断言对应于以下其中一个 OIDC 声明，那么会自动将其添加到身份令牌。如果在提供者端其中一个或多个值发生更改，那么只有在用户重新登录后新值才可用。

 * `name`
 * `email`
 * `locale`
 * `picture`

缺省情况下，将忽略不对应于任何标准名称的断言，但如果 SAML 提供者返回其他断言，那么可以在用户登录时获取这些信息。通过创建要使用的断言的数组，可以[将信息注入到令牌中](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)。但是，请确保除了必要的信息外，不要向令牌添加更多信息。令牌通常在 HTTP 头中发送，并且头的大小有限制。
{: tip}

### 此流程是什么样子的？
{: #saml-flow}

虽然 {{site.data.keyword.appid_short_notm}} 和身份提供者使用 SAML 框架来认证用户，但 {{site.data.keyword.appid_short_notm}} 仍使用更先进的 OAuth 2.0/OIDC 框架与应用程序交换安全性令牌。请查看下图以了解详细的信息流程。

![SAML 企业认证流程](/images/ibmid-flow.png)

1. 用户在其应用程序上访问登录页面或受限资源，这将通过 {{site.data.keyword.appid_short_notm}} SDK 或 API 发起对 {{site.data.keyword.appid_short_notm}} `/authorization` 端点的请求。如果用户未获授权，那么认证流程会首先重定向到 {{site.data.keyword.appid_short_notm}}。
2. {{site.data.keyword.appid_short_notm}} 生成 SAML 认证请求 (AuthNRequest)，并且浏览器会自动将用户重定向到 SAML 身份提供者。
3. 身份提供者对 SAML 请求进行解析，对用户进行认证，然后生成包含其断言的 SAML 响应。
4. 身份提供者通过 SAML 响应将用户和响应重定向回 {{site.data.keyword.appid_short_notm}}。
5. 如果认证成功，{{site.data.keyword.appid_short_notm}} 将创建表示用户授权和认证的访问令牌及身份令牌，并将这些令牌返回给应用程序。如果认证失败，{{site.data.keyword.appid_short_notm}} 会向应用程序返回身份提供者错误代码。
6. 授予用户对应用程序或受保护资源的访问权。



### SSO 会更改流程吗？
{: #saml-sso-flow}

{{site.data.keyword.appid_short_notm}} 实现的 Web 浏览器 SSO 概要文件是由服务提供者启动的，这意味着 {{site.data.keyword.appid_short_notm}} 必须向身份提供者发送 SAML 请求，才可启动认证会话。 

目前，{{site.data.keyword.appid_short_notm}} 不支持身份提供者启动的流程，因此现在不应将此流程用于该服务。
{: note}

如果身份提供者支持 SSO，那么 SAML 认证有可能使用已建立的 SSO 会话来认证用户。否则，系统会将用户重定向到登录页面。如果身份提供者无法将 {{site.data.keyword.cloud_notm}} 的认证请求中定义的认证需求与用于建立 SSO 的认证需求相匹配，那么可能会对用户执行重定向。例如，如果身份提供者使用生物识别建立了用户 SSO 会话，那么必须更改 {{site.data.keyword.appid_short_notm}} 的缺省认证上下文。缺省情况下，{{site.data.keyword.appid_short_notm}} 需要用户使用密码通过 HTTPS 进行认证：`urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`。



## 配置 SAML 以使用 {{site.data.keyword.appid_short_notm}}
{: #saml-configure}

可以通过向身份提供者提供 {{site.data.keyword.appid_short_notm}} 中的元数据以及向 {{site.data.keyword.appid_short_notm}} 提供身份提供者中的元数据，将 SAML 配置为使用 {{site.data.keyword.appid_short_notm}}。



### 为身份提供者提供元数据
{: #saml-provide-idp}

要配置应用程序，需要向与 SAML 兼容的身份提供者提供信息。通过元数据 XML 文件交换信息，该 XML 文件还包含用于建立信任的配置数据。
{: shortdesc}

在将 SAML 配置为身份提供者后，才能启用 SAML。
{: tip}

1. 在 {{site.data.keyword.appid_short_notm}} 仪表板的**管理**选项卡中，单击 **SAML** 行中的**编辑**以配置设置。
2. 单击**下载 SAML 元数据文件**。您的身份提供者希望该文件提供以下信息。
  <table>
    <tr>
      <th> 变量 </th>
      <th> 描述</th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>这是一个标识，让身份提供者知道 {{site.data.keyword.appid_short_notm}} 已发出 SAML 请求。</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>身份提供者在成功认证用户后发送 SAML 断言的位置。</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>有关身份提供者应如何发送 SAML 响应的指示信息。</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>身份提供者借以知道需要在断言主题中发送的标识格式的方式，以及 {{site.data.keyword.appid_short_notm}} 如何标识用户。标识应该采用以下格式：<code><saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"/></code></td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>这是身份提供者检查其是否需要签署断言的方式。该服务需要签署断言，但不支持已加密的断言。</td>
    </tr>
  </table>

3. 向身份提供者提供数据。如果身份提供者支持上传元数据文件，那么您可以执行此操作。否则，请手动配置属性。并非每个身份提供者都使用相同的属性，因此，您可能不会使用所有这些属性。

  针对不同的身份提供者，属性名可能有所不同。
  {: tip}

4. 将 **SAML 2.0 联合**切换为**已启用**。



### 向 {{site.data.keyword.appid_short_notm}} 提供元数据
{: #saml-provide-appid}

您可以从身份提供者那里获取数据，然后将其提供给 {{site.data.keyword.appid_short_notm}}。
{: shortdesc}

**使用 GUI 提供元数据** 

1. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的 **SAML 2.0** 选项卡。在**提供来自 SAML IdP 的元数据**部分中，输入您从身份提供者获取的以下元数据。
  <table>
    <tr>
      <th> 变量 </th>
      <th> 描述</th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>为了进行认证而将用户重定向到的 URL。它由 SAML 身份提供者托管。</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>SAML 身份提供者的全局唯一名称。</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>SAML 身份提供者发放的证书。用于签署和验证 SAML 断言。所有提供者都不同，但您可能可以下载身份提供者的签名证书。证书必须采用 <code>.pem</code> 格式。</td>
    </tr>
  </table>

2. 可选：提供在主证书上签名验证失败时使用的**辅助证书**。如果签名密钥保持不变，那么 {{site.data.keyword.appid_short_notm}} 不会阻止对到期证书进行认证。
3. 更新**提供程序名称**，然后单击**保存**。缺省名称为 SAML。

要设置认证上下文？您可以通过 API 来执行此操作。
{: tip}

</br>

**使用 API 提供元数据**

1. 通过向 [`/saml` API 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp)发出 GET 请求来查看当前 SAML 配置，包括认证上下文和证书。

  示例代码：
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
  ```
  {: codeblock}

  下面是输出示例：
  ```
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    }
  }
  ```
  {: screen}

2. 通过将以下示例中的值替换为提供者中的信息，以创建 SAML 配置。示例中显示的是必需值，但您可以选择包含更多信息，如表中所示。

  ```
  "config": {
    "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
    "displayName": "my saml example",
  }
  ```
  {: codeblock}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> 变量 </th>
      <th> 描述</th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>为了进行认证而将用户重定向到的 URL。它由 SAML 身份提供者托管。</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>SAML 身份提供者的全局唯一名称。</td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>为 SAML 配置指定的名称。</td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>SAML 身份提供者发放的证书。用于签署和验证 SAML 断言。所有提供者都不同，但您可能可以下载身份提供者的签名证书。证书必须采用 <code>.pem</code> 格式。</td>
    </tr>
    <tr>
      <td>可选：<code>secondary-certificate-example-pem-format</code></td>
      <td>SAML 身份提供者发放的备份证书。如果使用主证书进行签名验证失败，那么会使用备份证书。<strong>注</strong>：如果签名密钥保持不变，那么 {{site.data.keyword.appid_short_notm}} 不会阻止对到期证书进行认证。</td>
    </tr>
    <tr>
      <td>可选：<code>authnContext</code></td>
      <td>认证上下文用于验证认证和 SAML 断言的质量。可以通过向代码添加类数组和比较字符串来添加认证上下文。确保使用您的值来更新 <code>class</code> 和 <code>comparison</code> 参数。例如，<code>class</code> 参数可能类似于 <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code>。</td>
    </tr>
  </table>

3. 对 [`/saml` API 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)发出 PUT 请求，以向 {{site.data.keyword.appid_short_notm}} 提供在步骤 2 中创建的配置。请查看以下示例以了解请求可能会是什么样子。

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        ],
      "displayName": "my saml example",
    }
  }
  ```
  {: screen}



## 测试您的配置
{: #saml-testing}

您可以在 SAML 身份提供者与 {{site.data.keyword.appid_short_notm}} 之间测试配置。

1. 请确保已保存配置。
2. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的 **SAML 2.0** 选项卡，并单击**测试**。这样会打开一个新选项卡。
3. 使用身份提供者已认证的用户登录。
4. 完成表单后，会将您重定向到其他页面。
  * 认证成功：{{site.data.keyword.appid_short_notm}} 与身份提供者之间的连接正常运作。此页面显示有效的[访问令牌和身份令牌](/docs/services/appid?topic=appid-tokens#tokens)。
  * 认证失败：连接已中断。此页面显示错误和 SAML 响应 XML 文件。


遇到困难？请查看[故障诊断：SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp)。
{: tip}




## SAML 常见问题
{: #saml-assertions}

SAML 断言可以通过不同方式返回。请查看以下示例，以了解 {{site.data.keyword.appid_short_notm}} 期望对响应进行格式设置的方式。
{: shortdesc}


### {{site.data.keyword.appid_short_notm}} 想要的 SAML 断言是什么样子的？
{: #saml-example}

该服务希望获取类似于以下示例的 SAML 断言。

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}


### {{site.data.keyword.appid_short_notm}} 支持哪些类型的算法？
{: #saml-signatures}

{{site.data.keyword.appid_short_notm}} 使用 <a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 算法来处理 XML 数字签名。

