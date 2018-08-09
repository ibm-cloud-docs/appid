---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# 入门教程
{: #gettingstarted}

应用程序安全性复杂程度之深令人难以置信。对于大多数开发人员而言，这是创建应用程序的最困难的一个部分。如何确保用户信息得到安全保护？通过将 IBM® Cloud App ID 集成到应用程序中，即使您没有大量安全体验的情况下，也可以保护资源并添加认证。
{: shortdesc}

通过要求用户登录到应用程序，可以存储用户数据（如应用程序首选项或公共社交个人档案中的信息），然后使用该数据来定制每一种应用程序体验。App ID 为您提供了登录框架，但是使用 Cloud Directory 时，还可以使用您自己品牌的登录屏幕。


作为帐户所有者，现在可以设置策略，来定义团队成员如何与 {{site.data.keyword.appid_short_notm}} 的实例进行交互。您可以决定谁可以创建、更新和删除服务实例。有关更多信息，请参阅[服务访问管理](/docs/services/appid/iam.html)。
{:tip}

## 创建服务实例
{: #create}

创建 {{site.data.keyword.appid_short_notm}} 实例并将其绑定到您的应用程序中以开始使用。
{: shortdesc}

1. 在 {{site.data.keyword.Bluemix}} 目录中，选择 {{site.data.keyword.appid_short_notm}}。这将打开服务配置屏幕。
2. 对您的服务实例命名，或者使用预设的名称。
3. 选择定价套餐，然后单击**创建**。
4. 绑定 {{site.data.keyword.appid_short_notm}} 的实例。
    1. 要查看可绑定到服务实例的应用程序的列表，请单击**连接**。
    2. 单击**创建连接**。此时将打开一个页面，其中包含您可以选择绑定的所有应用程序。
    3. 单击要绑定的应用程序上的**连接**。
    4. 单击**重新编译打包**以应用更改。

就是这么简单！您已做好准备，可以开始配置应用程序设置了。


## 配置样本应用程序
{: #sample-app}

您可以使用预配置的样本应用程序来熟悉如何使用该服务。
{: shortdesc}

样本应用程序是开箱即用的，不但配置了两个身份提供者，而且能够复查认证。您还可以使用登录窗口小部件功能来定制登录页面，查看更新显示在应用程序中需要多长时间。

要从 GUI 配置样本应用程序：

1. 在创建服务实例之后，您可以选择您习惯使用的某种语言的样本应用程序。您可以在 iOS Swift、Android、Node.js 和 Java 中进行选择。不想使用 SDK？检查此示例，开始<a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">使用采用其他语言（例如 Python）的 {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
2. 按照 GUI 中的步骤**构建和运行**样本应用程序。每种语言的配置略有不同，请务必从下拉列表中选择您下载的语言的应用程序。完成应用程序配置之后，即可在浏览器中打开应用程序并使用凭证登录。
一定要安装适用于您的应用程序语言的必备软件。
  <dl>
    <dt> Android</dt>
      <dd><ul><li> Android API 25 或更高版本</li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools V25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods（V1.1.0 或更高版本）</li><li> iOS 9 或更高版本</li><li> MacOS 10.11.5 </li><li> Xcode（V9.0.1 或更高版本）</li></ul></dd>
    <dt> Node.js</dt>
      <dd><ul><li> Cloud Foundry CLI </li></ul></dd>
    <dt> Java</dt>
      <dd><ul><li> Cloud Foundry CLI </li><li> Maven </li></ul></dd>
  </dl>
3. 单击**复审活动**以查看所发生的认证事件。登录后，您可以看到一个事件。
4. 定制登录体验。您可以选择图像，如徽标和标题颜色。您可以选择一个颜色选项，也可以插入十六进制值。如果对预览满意，请单击**保存更改**。
5. 在浏览器中刷新登录页面。已经可以看到您在上一步中所做的更改。
