---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 入门教程
{: #gettingstarted}

{{site.data.keyword.appid_full}} 可帮助您为移动和 Web 应用程序添加认证，并保护后端资源。
{: shortdesc}

## 创建服务实例
{: #create}

创建 {{site.data.keyword.appid_short_notm}} 的实例以开始操作。
{: shortdesc}

1. 在 {{site.data.keyword.Bluemix}} 目录中，选择 {{site.data.keyword.appid_short_notm}}。这将打开服务配置屏幕。
2. 对您的服务实例命名，或者使用预设的名称。
3. 要绑定实例，请从**连接到**菜单中选择一个应用程序。如果选择**保持未绑定**，可以在将来绑定该服务实例。
4. 选择定价套餐，然后单击**创建**。

## 配置样本应用程序
{: #sample-app}

您可以使用预配置的样本应用程序来熟悉如何使用该服务。
{: shortdesc}

样本应用程序是开箱即用的，不但配置了两个身份提供者，而且能够复查认证。您还可以使用登录窗口小部件功能来定制登录页面，查看更新显示在应用程序中需要多长时间。

要从 GUI 配置样本应用程序：

1. 在创建服务实例之后，您可以选择您习惯使用的某种语言的样本应用程序。您可以在 iOS Swift、Android、Node.js 和 Java 中进行选择。不想使用 SDK？查看关于<a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">使用其他语言的 {{site.data.keyword.appid_short_notm}}（如 Python）<img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 的博客。
2. 按照 GUI 中的步骤**构建和运行**样本应用程序。每种语言的配置略有不同，请务必从下拉列表中选择您下载的语言的应用程序。完成应用程序配置之后，即可在浏览器中打开应用程序并使用凭证登录。
**注**：确保针对您要使用的语言，已安装好所有必备软件。 
  <dl>
    <dt> Android</dt>
      <dd><ul><li> Android API 25 或更高版本</li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools V25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods（V1.1.0 或更高版本）</li><li> iOS 9 或更高版本</li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js</dt>
      <dd><ul><li> Cloud Foundry CLI </li></ul></dd>
    <dt> Java</dt>
      <dd><ul><li> Cloud Foundry CLI </li><li> Maven </li></ul></dd>
  </dl>
3. 单击**查看活动**以查看已发生的认证事件。如果已登录，应至少查看一个事件。
4. 定制登录体验。您可以选择图像，如徽标和标题颜色。您可以选择一个颜色选项，也可以插入十六进制值。如果对预览满意，请单击**保存更改**。您可以在下图中查看示例登录体验的示例。
5. 在浏览器中刷新登录页面。已经可以看到您在上一步中所做的更改。
