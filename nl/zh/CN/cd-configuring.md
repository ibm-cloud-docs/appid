---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# 配置 Cloud Directory
{: #cloud-directory}

通过 {{site.data.keyword.appid_full}}，用户可以使用电子邮件或用户名和密码注册并登录到移动应用程序和 Web 应用程序。Cloud Directory 是在云中维护的用户注册表。当用户注册应用程序时，会将其添加到您的用户目录中。利用此功能，用户可以在应用程序中自由管理自己的帐户。
{: shortdesc}


## 管理目录设置
{: #cd-settings}

您可以配置通知以及用户对应用程序的控制级别。按照下图所示，可以快速完成 Cloud Directory 的设置。这些设置可以随时通过服务仪表板进行更新，并反映在应用程序中，无需更改任何代码。
{: shortdesc}


![配置 Cloud Directory](images/cloud-directory.png)
图. Cloud Directory 的配置过程


1. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的**管理认证**选项卡，确保将 Cloud Directory 设置为**开启**。

2. 在 **Cloud Directory > 设置**选项卡中，将**允许用户注册和登录**设置为**电子邮件和密码**或**用户名和密码**。用户可以使用自己已拥有的电子邮件登录，或者创建用户名以在与应用程序交互时使用。

  在将用户添加到目录之前，可以在选项之间切换。添加第一个用户后，未来的用户也必须使用相同的配置。
  {: note}

2. 决定您希望用户在登录时是创建用户名还是使用其电子邮件。这两个选项都需要密码。将用户添加到目录后，就无法再在选项之间切换。

3. 单击密码条件行中的**编辑**以指定要落实的任何需求。密码条件以正则表达式提供。有关确定强度的帮助或要查看常用示例，请参阅[管理密码强度](/docs/services/appid?topic=appid-cd-strength#cd-strength)。单击**保存**以落实需求。

4. 将**允许用户向应用程序注册**设置为**是**。如果此项设置为**否**，您仍可以通过控制台来添加用户。但是，通过控制台来添加用户最常用于仅开发目的。

5. 如果您希望用户能够重置其密码、更改其密码或重置其详细信息，请将**允许用户通过应用程序管理自己的帐户**设置为**是**。如果要限制用户的自助服务功能，请将此值设置为**否**。

6. 配置电子邮件设置。单击**发件人详细信息**行中的**编辑**以更新电子邮件设置。电子邮件设置会应用于通过 {{site.data.keyword.appid_short_notm}} 发送的所有通信。

    1. 指定应发送电子邮件的电子邮件地址。如果选择更改缺省值，那么电子邮件可能会发送到用户的垃圾邮件文件夹。

    2. 为发件人添加名称。

    3. 输入可用于发送响应的电子邮件。

    4. 单击**保存**。
