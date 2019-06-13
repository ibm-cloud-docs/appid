---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, development, identity provider, tokens, customization, lifetime

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


# 管理认证
{: #managing-idp}

身份提供者 (IdP) 通过认证为移动和 Web 应用程序添加了一层安全性。通过 {{site.data.keyword.appid_full}}，可以配置一个或多个身份提供者来为用户创建定制登录体验。
{: shortdesc}


{{site.data.keyword.appid_short_notm}} 使用多种协议（例如，OpenID Connect 和 SAML 等）与身份提供者进行交互。例如，OpenID Connect 是用于许多社交提供者（例如，Facebook 和 Google）的协议。企业提供者（例如，<a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 或 <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>）通常使用 SAML 作为其身份协议。对于 [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)，服务使用 SCIM 来验证身份信息。

使用社交或企业身份提供者时，{{site.data.keyword.appid_short_notm}} 对用户帐户信息具有读访问权。服务使用身份提供者返回的令牌和断言来验证用户的身份是否与其声明的一致。由于服务从不具有对信息的写访问权，因此用户必须通过其所选身份提供者来执行操作，如重置其密码。例如，如果用户使用 Facebook 登录到应用程序，然后希望更改自己的密码，那么他们必须转至 `www.facebook.com` 来执行此操作。

使用 [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) 时，{{site.data.keyword.appid_short_notm}} 是身份提供者。该服务会使用注册表来验证用户身份。由于 {{site.data.keyword.appid_short_notm}} 是提供者，因此用户可以直接利用应用程序中的高级功能（例如，重置其密码）。

在使用应用程序身份？请查看[应用程序身份](/docs/services/appid?topic=appid-app)。
{: tip}

有几个提供者可供服务配置为加以使用。请查看下表以了解有关选项的信息。

<table>
  <tr>
    <th>提供者</th>
    <th>类型</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)</td>
    <td>受管注册表</td>
    <td>您可以在云中维护自己的用户注册表。用户向应用程序注册时，会将其添加到您的用户目录中。通过此选项，用户能够在应用程序中更自由地管理自己的帐户。</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid?topic=appid-enterprise#enterprise)</td>
    <td>企业</td>
    <td>可为最终用户创建单点登录体验。</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid?topic=appid-social#facebook)</td>
    <td>社交</td>
    <td>最终用户可以使用其 Facebook 凭证登录到应用程序。</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid?topic=appid-social#google)</td>
    <td>社交</td>
    <td>最终用户可以使用其 Google 凭证登录到应用程序。</td>
  </tr>
  <tr>
    <td>[定制](/docs/services/appid?topic=appid-custom-identity#custom-identity)</td>
    <td> </td>
    <td>如果提供的选项都不符合您的特定需求，那么您可以配置自己的身份流程来使用 {{site.data.keyword.appid_short_notm}}。</td>  
  </tr>
</table>

## 管理提供者
{: #managing-providers}

身份提供者可创建和管理有关实体（例如，用户、功能标识或应用程序）的信息。提供者使用凭证（例如，密码）来验证实体的身份。然后，IdP 会将身份信息发送到其他服务提供者。因为身份提供者认证了该实体，所以 {{site.data.keyword.appid_short_notm}} 能够对其进行授权并授予对应用程序的访问权。
{: shortdesc}

要管理身份提供者，请执行以下操作：

1. 导航至服务仪表板。
2. 在导航的**身份提供者**部分中，选择**管理**页面。
3. 在**身份提供者**选项卡上，将要使用的提供者设置为**开启**。
4. 可选：决定是关闭**匿名用户**还是保留缺省值（即**开启**）。设置为**开启**时，用户属性会在用户开始与应用程序交互的那一刻与用户相关联。有关如何成为已识别用户的更多信息，请参阅[渐进式认证](/docs/services/appid?topic=appid-anonymous#progressive)。

{{site.data.keyword.appid_short_notm}} 会提供缺省凭证以帮助您进行初始 Facebook 和 Google+ 设置。每个实例每天对凭证的使用次数只有 100 次。由于这些是 IBM 凭证，因此只能用于开发环境。在发布应用程序之前，请将配置更新为您自己的凭证。
{: tip}


## 添加重定向 URI
{: #add-redirect-uri}

重定向 URI 是应用程序的回调端点。在执行登录流程期间，{{site.data.keyword.appid_short_notm}} 在允许客户端参与授权工作流程之前，会先验证 URI，这有助于防止网络钓鱼攻击和授权代码泄漏。通过注册 URI，即向 {{site.data.keyword.appid_short_notm}} 表明该 URI 是可信的，重定向您的用户没有问题。

确保仅注册您信任的应用程序的 URI。
{: note}


1. 单击**认证设置**以查看 URI 和令牌配置选项。

2. 在**添加 Web 重定向 URI** 字段中，输入 URI。每个 URI 都应以 `http://` 或 `https://` 开头，并且必须包含完整路径，包括支持成功重定向的任何查询参数。需要帮助来设置 URI 的格式吗？请查看下表以获取一些示例。

  <table>
    <tr>
      <th>类型</th>
      <th>示例 URI</th>
    </tr>
    <tr>
      <td>定制域</td>
      <td><code>http://mydomain.net/myapp2path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Ingress 子域</td>
      <td><code>https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback</code></td>
    </tr>
    <tr>
      <td>注销</td>
      <td><code>http://mydomain.net/myapp2path/appid_logout</code></td>
    </tr>  
  </table>

3. 单击**添加 Web 重定向 URI** 框中的 **+** 号。

4. 重复步骤 1 到 3，直到将所有可能的 URI 都添加到列表中。



不确定重定向 URI 的来源？请观看以下简短视频，以了解如何获取该 URI 以及如何将其添加到列表。

<iframe class="embed-responsive-item" id="redirecturi" title="{{site.data.keyword.appid_short_notm}}: How to fix invalid redirect URI" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6hxqbvpc054?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>



## 配置令牌生存期
{: #idp-token-lifetime}

令牌生存期在每次用户登录时会重新开始。例如，将刷新令牌生存期设置为 10 天。用户首次登录时，将创建访问令牌和刷新令牌。如果用户在若干天后返回到应用程序，假设 3 天后，那么他们无需再次登录。但是，如果用户在其初始登录后过了 12 天再返回到应用程序，那么他们需要重新登录，并且会有一组令牌与用户相关联。有关令牌的更多信息，请查看[了解令牌](/docs/services/appid?topic=appid-tokens#tokens)。

1. 要允许登录而无需用户交互，请将**刷新令牌**设置为**开启**。

2. 设置刷新令牌生存期。到期时间以天为单位进行设置，可以是范围在 1 到 90 之间的任何值。该数字越小，用户必须重新登录的频率越高。

3. 设置访问令牌生存期。到期时间以分钟为单位进行设置，可以是范围在 5 到 1440 之间的值。该值越小，防止令牌被盗的保护力度越大。

4. 设置匿名令牌生存期。在用户开始与应用程序进行交互时，会为用户分配[匿名令牌](/docs/services/appid?topic=appid-anonymous#progressive)。用户登录后，匿名令牌中的信息随即会传输到与该用户关联的令牌。到期时间以天为单位进行设置，可以是 1 到 90 之间的任何值。


设置令牌到期时间后，它将应用于已配置的所有提供者（包括社交提供者和企业提供者）。
{: tip}
