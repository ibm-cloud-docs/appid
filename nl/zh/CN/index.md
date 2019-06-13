---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, development,

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

# 入门教程
{: #getting-started}

应用程序安全性复杂程度之深令人难以置信。对于大多数开发者而言，这是创建应用程序的最困难的一个部分。如何确保用户信息得到安全保护？即使您在安全性方面没有太多经验，也可以通过将 {{site.data.keyword.appid_full}} 集成到应用程序中来保护资源并添加认证。
{: shortdesc}

通过要求用户登录到应用程序，可以存储用户数据（如应用程序首选项或公共社交个人档案中的信息），然后使用该数据来定制每一种应用程序体验。{{site.data.keyword.appid_short_notm}} 为您提供了框架，但是使用 Cloud Directory 时，还可以使用您自己品牌的登录屏幕。

我们希望听取您的反馈和问题！
* 如果有关于 {{site.data.keyword.appid_short_notm}} 的技术问题，请在 <a href="https://stackoverflow.com" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 上发帖提问，并使用 `ibm-appid` 标记您的问题。
* 有关服务和入门指示信息的问题，请使用 <a href="https://developer.ibm.com" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 论坛。包含 `appid` 标记。

## 创建服务实例
{: #create}

创建 {{site.data.keyword.appid_short_notm}} 实例并将其绑定到您的应用程序中以开始使用。
{: shortdesc}

1. 在 {{site.data.keyword.cloud_notm}} 目录中，选择 {{site.data.keyword.appid_short_notm}}。这将打开服务配置屏幕。
2. 对您的服务实例命名，或者使用预设的名称。
3. 选择价格套餐，然后单击**创建**。
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

样本应用程序是开箱即用的，不但配置了两个身份提供者，而且能够复查认证。样本应用程序以 `iOS Swift`、`Android`、`Node.js` 和 `Java` 语言提供。如果您看不到自己惯用的语言，不必担心！您可以使用提供的 API 将 {{site.data.keyword.appid_short_notm}} 集成到自己的样本应用程序中。

要构建样本应用程序，请执行以下操作：

1. 单击**下载样本**。
2. 单击您选择的语言以下载样本。
  看不到要查找的语言？别担心！您可以通过 API 来使用 {{site.data.keyword.appid_short_notm}}。您还可以查看<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">博客 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 以获取其他语言的额外帮助。
  {: tip}
3. 请确保已安装或完成了先决条件。
4. 按照**构建和运行**步骤，使用 {{site.data.keyword.appid_short_notm}} 设置样本。
5. 单击**复查活动**以查看所发生的任何认证事件。任何类型的登录都将创建一个事件并在此页面上显示。
6. 定制登录窗口小部件。
  1. 通过单击**选择**并浏览本地系统以查找要上传的图像，从而添加图像（例如，品牌徽标）。
  2. 通过选择其中一个颜色选项或以十六进制值指定颜色来选择颜色方案。
  3. 在 Web 和移动设备之间进行切换，以了解颜色方案在每种类型的设备上的显示情况。
  4. 对选项感到满意时，单击**保存更改**。
7. 在浏览器中，刷新登录页面。已经可以看到您在上一步中所做的更改。


## 后续步骤
{: #next}

准备好进入主题开始使用自己的应用程序了吗？首先[将服务添加到您的应用程序](/docs/services/appid?topic=appid-web-apps#web-apps)。服务针对最常用语言提供 SDK，但如果看不到编写应用程序所用语言的 SDK，仍可以使用 API 来利用 {{site.data.keyword.appid_short_notm}}。
