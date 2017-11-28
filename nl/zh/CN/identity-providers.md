---

copyright:
  years: 2017
lastupdated: "2017-11-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 配置身份提供者
{: #setting-up-idp}

身份提供者能够为移动和 Web 应用程序提供额外级别的认证。使用 {{site.data.keyword.appid_full}}，可以配置一个或多个身份提供者来为应用程序设置单点登录体验。
{: shortdesc}

可以使用以下身份提供者：

<dl>
  <dt> Facebook</dt>
    <dd> 用户使用其在登录到 Facebook 帐户时使用的密码和电子邮件来登录到您的应用程序。</dd>
  <dt> Google</dt>
    <dd> 用户使用其在登录到 Google 帐户时使用的密码和电子邮件来登录到您的应用程序。</dd>
</dl>


</br>
</br>

## 缺省配置
{: #default}

{{site.data.keyword.appid_short_notm}} 提供了可帮助您完成身份提供者初始设置的缺省配置。
{: shortdesc}

为 Facebook 和 Google 设置了缺省凭证。每个实例每天对凭证的使用次数只有 100 次。这些凭证是 IBM 凭证，因此只能在开发方式下用于您的应用程序。在发布应用程序之前，请将[该配置更新为您自己的凭证](/docs/services/appid/identity-providers.html)。


</br>

## 配置 Facebook
{: #facebook}

可以将 {{site.data.keyword.appid_short}} 服务配置为将 Facebook 用作身份提供者。
{: shortdesc}

### 从 Facebook 获取应用程序标识和私钥

要将 Facebook 用作身份提供者，必须在 Facebook 应用程序上添加并配置 Web 站点平台。

1. 在 <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for Developers 站点 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 上登录到您的帐户。
2. 记录 Facebook 应用程序标识和私钥。在服务仪表板中配置 Web 项目进行认证时，需要这些值。
3. 添加 Web 平台并输入站点 URL。
4. 从产品列表中，选择 **Facebook 登录**。
5. 在“有效的 OAuth 重定向 URL”字段中，输入授权服务器回调端点 URL。配置服务实例后，可以添加此值。
6. 单击**保存更改**。


### 配置 {{site.data.keyword.appid_short_notm}} 进行 Facebook 认证

已拥有 Facebook 应用程序标识和私钥并且将 Facebook for Developers 应用程序配置为向 Web 客户端提供服务后，可以在服务仪表板中编辑 Facebook 认证。

1. 在服务仪表板的**管理**选项卡中，选择 **Facebook**，然后单击**编辑**。
2. 输入从 Facebook for Developers Web 站点获取的 Facebook 应用程序标识和私钥。
3. 复制 **Facebook for Developers 的重定向 URI** 字段中的 URI。将此 URI 粘贴到 Facebook 开发者门户网站上 **Facebook 登录**部分中的**有效的 OAuth 重定向 URI** 字段中。
4. 单击**保存**。
5. 可选：对于 Web 应用程序，请在 **Web 应用程序重定向 URL** 字段中输入重定向 URL。此值由开发者确定，并用于在完成授权过程之后访问该重定向 URL。


</br>

## 配置 Google
{: #google}

可以将 {{site.data.keyword.appid_short}} 服务配置为将 Google 用作身份提供者。
{: shortdesc}

### 从 Google 获取客户端标识和私钥

在 <a href="https://developers.google.com/" target="_blank">Google Developers Console <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 中创建一个项目，将该项目配置为向 Web 客户端提供服务，然后获取客户端标识和私钥。

1. 创建一个项目。
2. 向您的 Google 项目添加 Google+ API。
3. 向 Google+ API 添加凭证。
    1. 对于 API 的类型，选择 Google+ API。
    2. 对于要在何处调用 API，选择 **Web 浏览器**。
    3. 选择**用户数据**。
    4. 完成必填字段来创建客户端标识。同时还会创建私钥。
4. 记录 Google 客户端标识和私钥。在凭证选项卡中，选择您创建用于获取私钥和客户端标识的标识。

### 配置 {{site.data.keyword.appid_short}} 进行 Google 认证

配置完 Google 项目并获得客户端标识和私钥后，可以编辑服务仪表板来进行 Google 认证。

1. 在服务仪表板的**管理**选项卡中，选择 **Google**，然后单击**编辑**。
2. 输入从 Google Developers Console 获取的客户端标识和私钥。
3. 授权 {{site.data.keyword.appid_short}} URL。
    1. 从 Google 身份提供者详细信息中复制 **Google Developer Console 的重定向 URL**。
    2. 在 Google 项目的凭证选项卡中，选择您为此集成创建的客户端标识。
    3. 将 URL 从 {{site.data.keyword.appid_short}} 粘贴到**授权重定向 URI** 字段中，然后单击**保存**。
4. 单击**保存**，以更新 {{site.data.keyword.appid_short}} 中的 Google 配置。
5. 可选：对于 Web 应用程序，请在**管理**选项卡中输入重定向 URL。授权过程完成后，用户将被发送到此 URL。
