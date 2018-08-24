---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# 配置企业身份提供者
{: #enterprise}

如果您已经拥有现有用户存储库和经验证的向内部系统认证用户的方式，那么可以配置 {{site.data.keyword.appid_full}} 服务使用企业身份提供者。
{: shortdesc}

## 了解 SAML
{: #saml}

SAML 是断言用户身份的身份提供者和使用用户身份信息的服务提供者之间交换认证和授权数据的开放式标准。
{: shortdesc}

它如何运作？

{{site.data.keyword.appid_short_notm}} 充当服务提供者，并启动向第三方提供者（例如，Active Directory Federation Services）的单点登录 (SSO) 。
<a href="http://saml.xml.org/saml-specifications" target="_blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 协议支持不同的概要文件和绑定选项。{{site.data.keyword.appid_short_notm}} 通过 HTTP Post 绑定支持 Web 浏览器 SSO 概要文件。

### SAML 断言和身份令牌声明

SAML 断言是包含一条或多条语句的信息包。该断言包含授权决策，它可能包含有关用户的身份信息。

当用户登录身份提供者时，该提供者将断言发送到 {{site.data.keyword.appid_short_notm}}。{{site.data.keyword.appid_short_notm}} 将 SAML 断言中返回的用户身份信息作为 OIDC 令牌声明传播到您的应用程序。SAML 属性必须与以下 OIDC 声明中某一项对应，以添加到身份令牌中。

可以添加以下声明：
* `name`
* `email`
* `locale`
* `picture`

将忽略不对应于任何标准名称的其余 SAML 属性元素。请注意，如果在提供者侧其中一个或多个值发生更改，那么只有在用户重新登录后新值才可用。

## 配置应用程序以使用外部 SAML 身份提供者
{: #configuring-saml}

您可以将 {{site.data.keyword.appid_short_notm}} 服务配置为使用安全性断言标记语言 (SAML) 身份提供者。
{: shortdesc}

有关如何使用特定 SAML 身份提供者的步骤，请查看以下有关设置 {{site.data.keyword.appid_short_notm}} 的博客帖子：[Ping One ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/)、[an Azure Active Directory ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) 或 [an Active Directory Federation Service ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/)。
{: tip}

### 为身份提供者提供元数据

要配置应用程序，需要向与 SAML 兼容的身份提供者提供信息。通过元数据 XML 文件交换信息，该 XML 文件还包含用于建立信任的配置数据。

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

### 向 {{site.data.keyword.appid_short_notm}} 提供元数据

您将需要从身份提供者获取数据，然后将其提供给 {{site.data.keyword.appid_short_notm}}。

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


### 测试您的配置

您可以在 SAML 身份提供者与 {{site.data.keyword.appid_short_notm}} 之间测试配置。

1. 请确保已保存配置。
2. 浏览到 {{site.data.keyword.appid_short_notm}} 仪表板的 **SAML 2.0** 选项卡，并单击**测试**。这样会打开一个新选项卡。
3. 使用身份提供者已认证的用户登录。
4. 完成表单后，会将您重定向到其他页面。
  * 认证成功：{{site.data.keyword.appid_short_notm}} 与身份提供者之间的连接正常运作。此页面显示有效的[访问令牌和身份令牌](/docs/services/appid/authorization.html#key-concepts)。
  * 认证失败：连接已中断。此页面显示错误和 SAML 响应 XML 文件。
