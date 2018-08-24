---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 关于
{: #about}

应用程序安全性复杂程度之深令人难以置信。对于大多数开发人员而言，这是创建应用程序的最困难的一个部分。如何确保用户信息得到安全保护？即使您在安全性方面没有太多经验，也可以通过将 {{site.data.keyword.appid_full}} 集成到应用程序中来保护资源并添加认证。
{:shortdesc}


## 使用此服务的原因
{: #reasons}

{{site.data.keyword.appid_short_notm}} 帮助开发者仅需几行代码即可轻松地向 Web 和移动应用程序添加认证，并在 {{site.data.keyword.Bluemix_notm}} 上保护其云本机应用程序和服务。通过要求用户登录到应用程序，可以存储用户数据（例如，应用程序首选项或来自公共社交个人档案的信息），然后利用数据来定制应用程序中的每个用户的体验。{{site.data.keyword.appid_short_notm}} 为您提供了登录框架，但是使用 Cloud Directory 时，还可以使用自己的品牌登录屏幕。
{: shortdesc}

您为何想要使用 {{site.data.keyword.appid_short_notm}}？请查看以下场景，看看是否有场景适用于您的情况。


<table>
  <tr>
    <th>场景 </th>
    <th>解决方案</th>
  </tr>
  <tr>
    <td>您需要向移动和 Web 应用程序添加[授权和认证](/docs/services/appid/authorization.html)，但不具有安全后台。</td>
    <td>使用 {{site.data.keyword.appid_short_notm}}，可以轻松地向您的应用程序中添加认证步骤。您可以使用 API、SDK、预先构建的 UI 或您自己的品牌 UI 向应用程序添加电子邮件或用名登录、社交登录或企业登录。</td>
  </tr>
  <tr>
    <td>您想要限制对应用程序和后端资源的访问权。</td>
    <td>您可以使用 {{site.data.keyword.appid_short_notm}} 提供的基于标准的认证来轻松保护应用程序、后端资源和 API。</td>
  </tr>
  <tr>
    <td>您想要为用户构建个性化的应用程序体验。</td>
    <td>利用 {{site.data.keyword.appid_short_notm}}，可以[存储用户数据](/docs/services/appid/user-profile.html)（如应用程序首选项或公共社交个人档案中的信息），然后使用这些数据来定制每一种应用程序体验。</td>
  </tr>
  <tr>
    <td>您希望以可扩展的方式管理用户。</td>
    <td> {{site.data.keyword.appid_short_notm}} 允许您创建 [Cloud Directory](/docs/services/appid/cloud-directory.html)，使得您可以将用户注册和用户登录添加到您的应用程序中。Cloud Directory 为您提供的框架可以维护用户注册表，该表会随着用户数量的增加而扩展。利用预先构建的自助服务（如电子邮件验证和密码重置），就可以确信应用程序会对用户进行安全的认证。</td>
  </tr>
</table>


## 集成
{: #integrations}

您可以将 {{site.data.keyword.appid_short_notm}} 与其他 {{site.data.keyword.Bluemix_notm}} 产品配合使用。
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>通过在标准集群中配置入口，您可以在集群级别保护应用程序。请查看 <a href="/docs/containers/cs_annotations.html#appid-auth">{{site.data.keyword.appid_short_notm}} authentication Ingress annotation</a> 或 <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Announcing App ID integration to IBM Cloud Kubernetes Service <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 博客帖子以开始使用。</dd>
  <dt>{{site.data.keyword.openwhisk}} 和 API Connect</dt>
    <dd>使用 [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) 和 [API Connect](/docs/apis/management/manage_apis.html) 创建 API 时，您可以在网关而不是应用程序代码级别保护应用程序。要了解如何进行集成，请观看<a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">使用 APIC 和
{{site.data.keyword.appid_short_notm}} 的简单快速社交登录 OAUTH <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。</dd>
  <dt>Cloud Foundry</dt>
    <dd>试用提供的某个样本 Cloud Foundry 应用程序，以了解如何将 {{site.data.keyword.appid_short_notm}} 集成到应用程序中。</dd>
  <dt>iOS 编程指南</dt>
    <dd>是否开发 Apple 应用程序？试用 <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS 编程指南 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，借助 {{site.data.keyword.Bluemix_notm}} 来学习、试验以及改进现有的 iOS 应用程序。</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>您可以使用 [{{site.data.keyword.cloudaccesstrailshort}} 服务](/docs/services/cloud-activity-tracker/index.html)来监视在 {{site.data.keyword.appid_short_notm}} 中生成的管理活动，例如更改仪表板配置。</dd>
  <dt>Node.js 编程指南</dt>
    <dd>是否在 Node.js 中开发应用程序？试用 <a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Node.js 编程指南 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，借助 {{site.data.keyword.Bluemix_notm}} 来学习、试验以及改进现有的 Node.js 应用程序。</dd>
</dl>


## 体系结构
{: #architecture}

利用 {{site.data.keyword.appid_short_notm}}，可以通过要求用户登录来提高应用程序安全级别。您还可以使用服务器 SDK 或 API 来保护后端资源。
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 体系结构图](/images/appid_architecture1.png)

<dl>
  <dt>应用程序</dt>
    <dd><strong>服务器 SDK</strong>：您可以使用服务器 SDK，保护在 {{site.data.keyword.Bluemix_notm}} 以及您的 Web 应用程序上托管的后端资源。其会从请求中抽取访问令牌，并使用 {{site.data.keyword.appid_short_notm}} 进行验证。</br>
    <strong>客户端 SDK</strong>：您可以使用 Android 或 iOS 客户端 SDK 保护您的移动应用程序。客户端 SDK 在检测到授权质询时将与云资源通信，以启动认证流程。</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>：成功认证后，{{site.data.keyword.appid_short_notm}} 会将访问令牌和身份令牌返回到应用程序。</br>
     <strong>Cloud Directory</strong>：用户可以使用其电子邮件和密码注册服务。然后，您可以通过 UI 管理列表视图中的用户。使用 Cloud Directory 时，{{site.data.keyword.appid_short_notm}} 充当身份提供者。</dd>
  <dt>外部（第三方）</dt>
    <dd><strong>社交和企业身份提供者</strong>：{{site.data.keyword.appid_short_notm}} 支持 Facebook、Google+ 和 SAML 2.0 Federation 作为身份提供者选项。该服务会安排“重定向到身份提供者”，并验证返回的认证令牌。如果令牌有效，那么该服务将授予应用程序的访问权，而不必访问实际的口令。</dd>
</dl>


## 请求流程
{: #request}

虽然您的请求流程可能根据应用程序配置的不同而变化，但在使用 App ID 时可能会遇到三个主要流。您可以创建移动应用程序流、Web 应用程序流或使用其他流程来保护资源。请查看一些示例流程以了解是否可在配置应用程序时使用。
{: shortdesc}

### Web 应用程序请求流程
{: #web-flow}

![{{site.data.keyword.appid_short_notm}} 请求流程](/images/web_flow1.png)

1. 通过使用浏览器，用户执行将触发 App ID SDK 请求的操作。
2. 如果用户未获授权，那么将启动到 App ID 的重定向。
3. App ID 启动登录窗口小部件并将其发送到浏览器。
4. 用户选择身份提供者以进行认证并完成登录过程。
5. 身份提供者使用身份令牌重定向到 App ID SDK。
6. App ID SDK 从 App ID 服务获取访问令牌。
7. App ID SDK 保存令牌并发生重定向。
8. 授权用户访问应用程序。

### 移动请求流程
{: #mobile-flow}

![{{site.data.keyword.appid_short_notm}} 请求流程](/images/mobile_flow.png)

1. 用户执行一个操作，触发客户机应用程序对 App ID SDK 的请求。
2. 如果用户无有效的访问令牌，那么 App ID SDK 启动授权流程。
3. 这样将向用户显示登录窗口小部件。
4. 通过使用其中一个已配置的身份提供者，用户进行认证。
5. 一旦用户获取身份令牌，那么 SDK 将从 App ID 服务获取访问令牌。
6. 使用这两个令牌，SDK 再次执行请求。
7. 如果令牌有效，就会授权用户访问应用程序。

### 受保护资源请求流程
{: #pr-flow}

![{{site.data.keyword.appid_short_notm}} 请求流程](/images/pr_flow.png)

1. 在对资源进行请求前，客户机应用程序必须具有一组公用密钥。
2. 通过公用密钥，客户机应用程序发出请求。
3. 如果没有有效的访问令牌，那么应用程序会收到错误。
4. 获取有效令牌后，客户机应用程序可再次发出请求。但是此时包含令牌。
5. 如果应用程序可以验证访问令牌授予的许可权，那么就会授权应用程序访问受保护资源。
