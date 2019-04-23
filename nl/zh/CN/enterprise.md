---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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

安全性断言标记语言 (SAML) 是断言用户身份的身份提供者和使用用户身份信息的服务提供者之间交换认证和授权数据的开放式标准。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 充当服务提供者，并启动向第三方提供者（例如，Active Directory Federation Services）的单点登录 (SSO) 。
<a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 协议支持不同的概要文件和绑定选项。{{site.data.keyword.appid_short_notm}} 通过 HTTP Post 绑定支持 Web 浏览器 SSO 概要文件。

有关如何使用特定 SAML 身份提供者的步骤，请查看以下有关设置 {{site.data.keyword.appid_short_notm}} 的博客帖子：[Ping One ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/)、[an Azure Active Directory ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) 或 [an Active Directory Federation Service ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/)。
{: tip}



## 了解断言
{: #saml-assertions}

SAML 断言类似于[用户属性](/docs/services/appid?topic=appid-user-profile#user-profile)。这是有关用户的声明或信息，在用户成功登录到应用程序时，由身份提供者返回给 {{site.data.keyword.appid_short_notm}}。根据应用程序配置和使用的身份提供者，信息可能包含用户名、电子邮件或您要求指定的其他字段。
{: shortdesc}

断言返回到 {{site.data.keyword.appid_short_notm}} 时，服务会联合用户身份。如果 SAML 断言对应于以下其中一个 OIDC 声明，那么会自动将其添加到身份令牌。如果在提供者端其中一个或多个值发生更改，那么只有在用户重新登录后新值才可用。

 * `name`
 * `email`
 * `locale`
 * `picture`

缺省情况下，将忽略不对应于任何标准名称的断言，但如果 SAML 提供者返回其他断言，那么可以在用户登录时获取这些信息。通过创建要使用的断言的数组，可以[将信息注入到令牌中](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)。但是，请确保除了必要的信息外，不要向令牌添加更多信息。令牌通常在 HTTP 头中发送，并且头的大小有限制。
{: tip}

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




## 为身份提供者提供元数据
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
      <td>身份提供者知道需要在断言主题中发送的标识格式的方式。{{site.data.keyword.appid_short_notm}} 识别用户的方式。</td>
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

## 向 {{site.data.keyword.appid_short_notm}} 提供元数据
{: #saml-provide-appid}

您可以从身份提供者那里获取数据，然后将其提供给 {{site.data.keyword.appid_short_notm}}。
{: shortdesc}

### 使用 GUI 提供元数据
{: #saml-provide-gui}

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


### 使用 API 提供元数据
{: #saml-provide-api}

1. 通过对 [/getSamlMetadata API 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp)发出 GET 请求来获取 SAML 元数据。

  示例代码：
  ```
  <?xml version="1.0"?>
  <getSamlMetadata>
    <?xml version="1.0"?> <EntityDescriptor> <SPSSODescriptor> <NameIDFormat> </NameIDFormat> <AssertionConsumerService /> </SPSSODescriptor>
   </EntityDescriptor>
    </getSamlMetadata>
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
    },
    "validation_data": {
      "certificates": [
        {
          "certificate_index": 0,
          "expiration_timestamp": 1674473996,
          "warning": "Your certificate will expire in 18 days."
        }
      ]
    }
  }
  ```
  {: screen}

2. 配置对 [/set_saml_idp API 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)的 POST 请求。

  1. 在以下元数据示例中，将变量替换为您自己的信息。

    ```
    Put {Management URI}/config/idps/saml
    Content-Type: application/json
    {
      "isActive": true,
      "config": {
        "entityID": "https://example.com/saml2/metadata/706634",
        "signInUrl": "https://example.com/saml2/sso-redirect/706634",
        "certificates": [
          "primary-certificate-example-pem-format"
        ],
        "displayName": "my saml example"
      }
    }
    ```
    {: codeblock}

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

  2. 可选：将辅助证书添加到证书数组中主证书之后的位置。如果使用主证书进行签名验证失败，那么会使用辅助证书。如果签名密钥保持不变，那么 {{site.data.keyword.appid_short_notm}} 不会阻止对到期证书进行认证。

    示例：
    ```
    {
      "isActive": true,
      "config": {
        ...
        "certificates": [
          "primary-certificate-example-pem-format",
          "secondary-certificate-example-pem-format"
        ],
        ...
      }
    }
    ```
    {: screen}
  {: #configuring-saml-new}
  3. 可选：通过向代码添加类数组和比较字符串来添加认证上下文。确保使用您的值来更新 `class` 和 `comparison` 参数。认证上下文用于验证认证和 SAML 断言的质量。

    示例：
    ```
    {
      "isActive": true,
      "config": {
        ...
        "authnContext": {
          "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
          "comparison": "sampleComparisonValue"
        }
      }
    }
    ```
    {: screen}

3. 发出请求。如果选择添加可选值，那么请求应该类似于以下示例。

  ```
  Put {Management URI}/config/idps/saml
  Content-Type: application/json
  {
    "isActive": true,
    "config": {
      ...
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
        "comparison": "sampleComparisonValue"
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
      "displayName": "my saml example"
    }
  }
  ```
  {: codeblock}


## 测试您的配置
{: #saml-testing}

您可以在 SAML 身份提供者与 {{site.data.keyword.appid_short_notm}} 之间测试配置。

1. 请确保已保存配置。
2. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的 **SAML 2.0** 选项卡，并单击**测试**。这样会打开一个新选项卡。
3. 使用身份提供者已认证的用户登录。
4. 完成表单后，会将您重定向到其他页面。
  * 认证成功：{{site.data.keyword.appid_short_notm}} 与身份提供者之间的连接正常运作。此页面显示有效的[访问令牌和身份令牌](/docs/services/appid?topic=appid-tokens#tokens)。
  * 认证失败：连接已中断。此页面显示错误和 SAML 响应 XML 文件。


遇到困难？请查看[有关身份提供者配置的故障诊断](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp)。
{: tip}
