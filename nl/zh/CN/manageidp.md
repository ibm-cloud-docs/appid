---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# 管理
{: #managing}

身份提供者 (IdP) 通过认证为移动和 Web 应用程序添加了一层安全性。通过 {{site.data.keyword.appid_full}}，可以配置一个或多个身份提供者来为用户创建定制登录体验。
{: shortdesc}


**什么是身份提供者？**

身份提供者可创建和管理有关实体（例如，用户、功能标识或应用程序）的信息。提供者使用凭证（例如，密码）来验证实体的身份。然后，IdP 会将身份信息发送到其他服务提供者。因为身份提供者认证了该实体，所以 {{site.data.keyword.appid_short_notm}} 能够对其进行授权并授予对应用程序的访问权。

</br>

**{{site.data.keyword.appid_short_notm}} 为哪些身份提供者提供了集成？**

有几个提供者是服务预先配置为使用的。

<table>
  <tr>
    <th>提供者</th>
    <th>类型</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid/cloud-directory.html)</td>
    <td>受管注册表</td>
    <td>您可以在云中维护自己的用户注册表。用户向应用程序注册时，会将其添加到您的用户目录中。通过此选项，用户能够在应用程序中更自由地管理自己的帐户。</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid/enterprise.html)</td>
    <td>企业</td>
    <td>您可为最终用户创建单点登录体验。</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid/identity-providers.html#facebook)</td>
    <td>社交</td>
    <td>最终用户可以使用其 Facebook 凭证登录到应用程序。</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid/identity-providers.html#google)</td>
    <td>社交</td>
    <td>最终用户可以使用其 Google+ 凭证登录到应用程序。</td>
  </tr>
  <tr>
    <td>[定制](/docs/services/appid/custom.html)</td>
    <td> </td>
    <td>如果提供的选项都不符合您的特定需求，那么您可以配置自己的身份流程来使用 {{site.data.keyword.appid_short_notm}}。</td>
  </tr>
  
</table>

</br>

**{{site.data.keyword.appid_short_notm}} 如何与身份提供者进行交互？**

{{site.data.keyword.appid_short_notm}} 使用多种协议（例如，OpenID Connect 和 SAML 等）与身份提供者进行交互。例如，OpenID Connect 是用于许多社交提供者（例如，Facebook 和 Google）的协议。企业提供者（例如，<a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 或 <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>）通常使用 SAML 作为其身份协议。对于 [Cloud Directory](cloud-directory.html)，服务使用 SCIM 来验证身份信息。

在使用应用程序身份？请查看[应用程序身份](app-to-app.html)。
{: tip}

</br>
</br>

## 配置设置
{: #configuring}

您可以决定要使用的提供者、重定向 URL 以及应用程序的令牌信息。配置的设置将应用于此服务实例中的所有身份提供者。例如：设置令牌到期时间后，它将应用于已配置的所有提供者（不管是社交提供者还是企业提供者）。

</br>

**要配置提供者，请执行以下操作：**

1. 浏览到服务仪表板。
2. 在导航的**身份提供者**部分中，选择**管理**页面。
3. 在**身份提供者**选项卡上，将要使用的提供者设置为**开启**。
4. 可选：决定是关闭**匿名用户**还是保留缺省值（即**开启**）。设置为**开启**时，定制用户属性会在用户开始与应用程序交互的那一刻与用户相关联。有关如何成为已识别用户的更多信息，请参阅[渐进式认证](progressive.html#progressive)。

{{site.data.keyword.appid_short_notm}} 会提供缺省凭证以帮助您进行初始 Facebook 和 Google+ 设置。每个实例每天对凭证的使用次数只有 100 次。由于这些是 IBM 凭证，因此只能用于开发环境。在发布应用程序之前，请将配置更新为您自己的凭证。
{: tip}

</br>

**要配置设置，请执行以下操作：**

1. 添加重定向 URL。重定向 URL 是应用程序的回调端点。为防止钓鱼攻击，{{site.data.keyword.appid_short_notm}} 会根据白名单来验证 URL。
  1. 在**添加 Web 重定向 URL** 字段中，输入 URL 并单击 **+** 图标。
  2. 重复步骤 1，直到将所有可能的重定向 URL 添加到列表中。

  不要在 URL 中包含任何查询参数。在验证过程中将忽略这些参数。例如：`http://host:[port]/path`
  {: tip}

2. 配置令牌。令牌生存期在每次用户登录时会重新开始。例如，将刷新令牌生存期设置为 10 天。用户首次登录时，将创建访问令牌和刷新令牌。如果用户在若干天后返回到应用程序，假设 3 天后，那么他们无需再次登录。但是，如果用户在其初始登录后过了 12 天再返回到应用程序，那么他们需要重新登录，并且会有一组令牌与用户相关联。
  1. 要允许登录而无需用户交互，请将**刷新令牌**设置为**开启**。
  2. 设置刷新令牌生存期。到期时间以天为单位进行设置，可以是范围在 1 到 90 之间的任何值。该数字越小，用户必须重新登录的频率越高。
  3. 设置访问令牌生存期。到期时间以分钟为单位进行设置，可以是范围在 5 到 1440 之间的值。该值越小，防止令牌被盗的保护力度越大。
  4. 设置匿名令牌生存期。在用户开始与应用程序进行交互时，会为用户分配[匿名令牌](/docs/services/appid/progressive.html#anonymous)。用户登录后，匿名令牌中的信息随即会传输到与该用户关联的令牌。到期时间以天为单位进行设置，可以是 1 到 90 之间的任何值。

</br>
</br>
