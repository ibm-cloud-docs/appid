---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# SAML
{: #enterprise}


安全性断言标记语言 (SAML) 是断言用户身份的身份提供者和使用用户身份信息的服务提供者之间交换认证和授权数据的开放式标准。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 充当服务提供者，并启动向第三方提供者（例如，Active Directory Federation Services）的单点登录 (SSO) 。
<a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 协议支持不同的概要文件和绑定选项。{{site.data.keyword.appid_short_notm}} 通过 HTTP Post 绑定支持 Web 浏览器 SSO 概要文件。

有关如何使用特定 SAML 身份提供者的步骤，请查看以下有关设置 {{site.data.keyword.appid_short_notm}} 的博客帖子：[Ping One ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/)、[an Azure Active Directory ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) 或 [an Active Directory Federation Service ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/)。
{: tip}


## SAML 断言和身份令牌声明

SAML 断言是包含一条或多条语句的信息包。该断言包含授权决策，它可能包含有关用户的身份信息。

当用户登录身份提供者时，该提供者将断言发送到 {{site.data.keyword.appid_short_notm}}。{{site.data.keyword.appid_short_notm}} 将 SAML 断言中返回的用户身份信息作为 OIDC 令牌声明传播到您的应用程序。SAML 属性必须与以下 OIDC 声明中某一项对应，以添加到身份令牌中。

可以添加以下声明：
* `name`
* `email`
* `locale`
* `picture`

将忽略不对应于任何标准名称的其余 SAML 属性元素。请注意，如果在提供者侧其中一个或多个值发生更改，那么只有在用户重新登录后新值才可用。


在寻找示例？请查看 <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Setting up {{site.data.keyword.appid_long}} with your Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 或 <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/" target="_blank">Setting up {{site.data.keyword.appid_long}} with Ping One <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

## 为身份提供者提供元数据
{: #provide-idp}

要配置应用程序，需要向与 SAML 兼容的身份提供者提供信息。通过元数据 XML 文件交换信息，该 XML 文件还包含用于建立信任的配置数据。
{: shortdesc}

1. 在 {{site.data.keyword.appid_short_notm}} 仪表板的**管理**选项卡上，将 **SAML 2.0** 设置为**开启**。然后，单击**编辑**以配置 SAML 设置。
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

3. 向身份提供者提供数据。如果身份提供者支持上传元数据文件，那么您可以执行此操作。否则，请手动配置属性。并非每个身份提供者都将使用相同的属性，因此，如果您不全部使用，也是可以的。

针对不同的身份提供者，属性名可能有所不同。
{: tip}

## 向 {{site.data.keyword.appid_short_notm}} 提供元数据
{: #provide-appid}

从身份提供者那里获取数据，然后将其提供给 {{site.data.keyword.appid_short_notm}}。
{: shortdesc}

**使用 GUI 提供元数据**

1. 浏览到 {{site.data.keyword.appid_short_notm}} 仪表板的 **SAML 2.0** 选项卡。在**提供来自 SAML IdP 的元数据**部分中，输入您从身份提供者获取的以下元数据。
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
      <td>SAML 身份提供者发放的证书。用于签署和验证 SAML 断言。所有提供者都不同，但您可能可以下载身份提供者的签署证书。证书必须采用 <code>.pem</code> 格式。</td>
    </tr>
  </table>

2. 可选：提供在主证书上签名验证失败时使用的**辅助证书**。如果签名密钥保持不变，那么 {{site.data.keyword.appid_short_notm}} 不会阻止对到期证书进行认证。
3. 更新**提供程序名称**，然后单击**保存**。缺省名称为 SAML。

要设置认证上下文？您可以通过 API 来执行此操作。
{: tip}

</br>
</br>

**使用 API 提供元数据**

1. 通过对 [/getSamlMetadata API 端点](https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/getSamlMetadata)发出 GET 请求来获取 SAML 元数据。

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

2. 配置对 [/set_saml_idp API 端点](https://appid-management.ng.bluemix.net/swagger-ui/#!/Identity_Providers/set_saml_idp)的 POST 请求。

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
        <td>SAML 身份提供者发放的证书。用于签署和验证 SAML 断言。所有提供者都不同，但您可能可以下载身份提供者的签署证书。证书必须采用 <code>.pem</code> 格式。</td>
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
{: #testing}

您可以在 SAML 身份提供者与 {{site.data.keyword.appid_short_notm}} 之间测试配置。

1. 请确保已保存配置。
2. 浏览到 {{site.data.keyword.appid_short_notm}} 仪表板的 **SAML 2.0** 选项卡，并单击**测试**。这样会打开一个新选项卡。
3. 使用身份提供者已认证的用户登录。
4. 完成表单后，会将您重定向到其他页面。
  * 认证成功：{{site.data.keyword.appid_short_notm}} 与身份提供者之间的连接正常运作。此页面显示有效的[访问令牌和身份令牌](/docs/services/appid/authorization.html#tokens)。
  * 认证失败：连接已中断。此页面显示错误和 SAML 响应 XML 文件。


遇到困难？请查看[有关身份提供者配置的故障诊断](/docs/services/appid/ts_saml.html)。
{: tip}
