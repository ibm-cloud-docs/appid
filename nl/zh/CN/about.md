---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 关于
{: #about}

您可以使用 {{site.data.keyword.appid_full}} 向应用程序添加认证，并保护后端资源。
{:shortdesc}

## 使用此服务的原因
{: #reasons}

您为何想要使用 {{site.data.keyword.appid_short_notm}}？请查看以下场景，看看是否有场景适用于您的情况。
{: shortdesc}

<table>
  <tr>
    <th> 场景 </th>
    <th> 原因 </th>
  </tr>
  <tr>
    <td> 您需要向移动和 Web 应用程序添加[授权和认证](/docs/services/appid/authorization.html)，但不具有安全后台。</td>
    <td> 使用 {{site.data.keyword.appid_short_notm}}，可以轻松地向您的应用程序中添加认证步骤。您可以使用该服务与[身份提供者](/docs/services/appid/identity-providers.html)进行通信，以管理对应用程序的访问权。</td>
  </tr>
  <tr>
    <td> 您想要限制对应用程序和后端资源的访问权。</td>
    <td> 使用该服务，可以针对已认证用户和匿名用户来[保护您的资源](/docs/services/appid/protecting-resources.html)。</td>
  </tr>
  <tr>
    <td> 您想要为用户构建个性化的应用程序体验。</td>
    <td> 利用 {{site.data.keyword.appid_short_notm}}，可以[存储用户数据](/docs/services/appid/user-profile.html)（如应用程序首选项或公共社交个人档案中的信息），然后使用这些数据来定制每一种应用程序体验。</td>
  </tr>
  <tr>
    <td> 应该让用户能够通过电子邮件使用密码来访问应用程序。 </td>
    <td> {{site.data.keyword.appid_short_notm}} 提供创建 [Cloud Directory](/docs/services/appid/cloud-directory.html) 的功能。因此您可以将用户注册和用户登录添加到移动应用程序和 Web 应用程序。Cloud Directory 为您提供的框架可以维护用户注册表，该表会随着用户数量的增加而扩展。利用预先构建的自助服务（如电子邮件验证和密码重置），就可以确信应用程序会对用户进行安全的认证。</td>
  </tr>
</table>


## 体系结构
{: #architecture}

利用 {{site.data.keyword.appid_short_notm}}，您可以通过要求用户登录来提高应用程序安全性级别。您还可以使用服务器 SDK 来保护后端资源。
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 体系结构图](/images/appid_architecture.png)

<dl>
  <dt> 应用程序</dt>
    <dd> 服务器 SDK：您可以使用服务器 SDK 保护在 {{site.data.keyword.Bluemix_notm}} 上托管的后端资源以及您的 Web 应用程序。其会从请求中抽取访问令牌，并使用 {{site.data.keyword.appid_short_notm}} 进行验证。</br>
    客户端 SDK：您可以使用 Android 或 iOS 客户端 SDK 保护您的移动应用程序。客户端 SDK 在检测到授权质询时将与云资源通信，以启动认证流程。</dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd> App ID：成功认证后，{{site.data.keyword.appid_short_notm}} 会将访问令牌和身份令牌返回到应用程序。</br>
    Cloud Directory：用户可以使用其电子邮件和密码注册服务。然后，您可以通过 UI 管理列表视图中的用户。</dd>
  <dt> 外部（第三方）</dt>
    <dd>  {{site.data.keyword.appid_short_notm}} 支持两种社交身份提供者：Facebook 和 Google+。该服务会安排“重定向到身份提供者”，并在验证认证之后提供对应用程序的访问权。{{site.data.keyword.appid_short_notm}} 会验证凭证，而无需访问实际口令。</dd>
</dl>


## 请求流程
{: #request}

下图描述了请求是如何从客户端 SDK 流向后端资源和身份提供者的。
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 请求流程](/images/appidrequestflow.png)


* {{site.data.keyword.appid_short_notm}} 客户端 SDK 对受 {{site.data.keyword.appid_short_notm}} 服务器 SDK 保护的后端资源发起请求。
* {{site.data.keyword.appid_short_notm}} 服务器 SDK 检测到未授权的请求，然后返回 HTTP 401 和授权作用域。
* 客户端 SDK 自动检测到 HTTP 401，然后启动认证过程。
* 当客户端 SDK 联系服务时，如果配置了多个身份提供者，那么服务器 SDK 返回登录窗口小部件。{{site.data.keyword.appid_short_notm}} 会调用身份提供者并为该提供者呈现登录表单，如果没有配置身份提供者，那么将返回授权代码，以允许他们进行认证。
* {{site.data.keyword.appid_short_notm}} 通过提供认证质询，要求客户端进行认证。
* 如果已配置身份提供者，那么在用户登录时，相应的 OAuth 流程会处理认证。
* 如果认证以相同的授权代码结束，那么该代码会发送到令牌端点。端点会返回两个令牌：访问令牌和身份令牌。从此刻开始，通过客户端 SDK 发起的所有请求都有新获取的授权头。
* 客户端 SDK 自动重新发送触发了授权流程的原始请求。
* 服务器 SDK 从请求中抽取授权头，通过服务对该头进行验证，然后授予对后端资源的访问权。

**注**：实施的协议完全符合 OpenID Connect (OIDC)。
