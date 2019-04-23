---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-05"

keywords: authentication, authorization, identity, app security, secure, application identity, app to app, access token, activity

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


# {{site.data.keyword.cloudaccesstrailshort}} 事件
{: #at-events}

您可以使用 {{site.data.keyword.cloudaccesstrailshort}} 服务查看、管理和分析在 {{site.data.keyword.appid_full}} 服务实例中执行的用户启动的活动。
{: shortdesc}



有关服务如何工作的更多信息，请参阅 [{{site.data.keyword.cloudaccesstrailshort}} 文档](/docs/services/cloud-activity-tracker/reference?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla)。


## 查看管理事件
{: #at-monitor-admin}

您可以使用 {{site.data.keyword.cloudaccesstrailshort}} 服务查看、管理和分析在 {{site.data.keyword.appid_short_notm}} 实例中执行的配置活动。
{: shortdesc}

要监视管理活动：

1. 登录到 {{site.data.keyword.cloud_notm}} 帐户。
2. 在与 {{site.data.keyword.appid_short_notm}} 实例相同的帐户中，从目录供应“{{site.data.keyword.cloudaccesstrailshort}}”服务的实例。
3. 在“{{site.data.keyword.cloudaccesstrailshort}}”仪表板中，单击**管理**选项卡。
4. 在下拉列表中生成以下配置以搜索 {{site.data.keyword.appid_short_notm}} 生成的事件。
    * 对于**查看日志**，选择**帐户日志**。
    * 对于**搜索**，选择 **target.Management**。
    * 对于**过滤器**，输入 **appid**。
5. 单击**过滤器**。

</br>

## 管理事件列表
{: #at-events-admin}

请查看下表以获取发送到 {{site.data.keyword.cloudaccesstrailshort}} 的事件的列表。

<table>
  <tr>
    <th>操作</th>
    <th>描述</th>
    <th>UI 位置</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>查看最新活动。</td>
    <td>位于<strong>概述</strong>选项卡上的<strong>活动日志</strong>框中。</td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>查看身份提供者配置。</td>
    <td>位于<strong>身份提供者 > 管理</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>更新身份提供者配置。</td>
    <td>可在<strong>身份提供者 > 管理</strong>选项卡中进行更新。</td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>查看令牌到期时间配置。</td>
    <td>位于<strong>身份提供者 > 令牌到期时间</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>查看用户概要文件存储配置。</td>
    <td>位于<strong>概述</strong>选项卡上的<strong>活动日志</strong>中。</td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>更新用户概要文件存储配置。</td>
    <td>位于<strong>概要文件</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>查看登录窗口小部件标题的主题颜色。</td>
    <td>位于<strong>登录定制</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>更新登录窗口小部件主标题的主题颜色。</td>
    <td>可在<strong>登录定制</strong>选项卡中进行更新。</td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>查看登录窗口小部件中显示的图像。</td>
    <td>位于<strong>登录定制</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>更新登录窗口小部件中显示的图像。</td>
    <td>可在<strong>登录定制</strong>选项卡中进行更新。</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>查看登录窗口小部件 UI 配置，包括标题颜色和图像。</td>
    <td>位于<strong>登录定制</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>查看支持语言的列表。</td>
    <td>必须从 API 进行查看。</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>更新支持的语言。</td>
    <td>必须通过 API 进行更新。</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>查看 {{site.data.keyword.appid_short_notm}} SAML 元数据。</td>
    <td>位于<strong>身份提供者 > SAML 2.0 联合</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>查看 Cloud Directory 用户。</td>
    <td>位于<strong>用户</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>更新 Cloud Directory 用户。</td>
    <td>可在<strong>用户</strong>选项卡中进行更新。</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>删除 Cloud Directory 用户。</td>
    <td>可在<strong>用户</strong>选项卡中进行删除。</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>查看 Cloud Directory 用户列表。</td>
    <td>位于<strong>用户</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>更新 Cloud Directory 用户列表。</td>
    <td>可在<strong>用户</strong>选项卡中进行更新。</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>删除 Cloud Directory 用户列表。</td>
    <td>可在<strong>用户</strong>选项卡中进行删除。</td>
  </tr>
  <tr>
    <td><code>read.emailTemplate</code></td>
    <td>查看电子邮件模板。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 模板</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.emailTemplate</code></td>
    <td>更新电子邮件模板。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 模板</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>delete.emailTemplate</code></td>
    <td>删除要重置为缺省值的电子邮件模板。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 模板</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>read.senderDetails</code></td>
    <td>查看发件人详细信息。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 设置</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.senderDetails</code></td>
    <td>更新发件人详细信息</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 设置</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.resendNotification</code></td>
    <td>重新发送用户通知。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 设置</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>更新忘记密码流程。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 设置</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>查看忘记密码确认结果。</td>
    <td>必须通过 API 完成。</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>更新注册流程。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 设置</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>查看注册结果确认。</td>
    <td>必须通过 API 完成。</td>
  </tr>
  <tr>
    <td><code>read.action_url</code></td>
    <td>查看在执行操作时调用的定制 URL。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 定制登录页面</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>更新在执行操作时调用的定制 URL。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 设置</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.changePassword</code></td>
    <td>更改 Cloud Directory 用户密码。</td>
    <td>位于<strong>身份提供者 > Cloud Directory > 设置</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>read.loginWidgetConfig</code></td>
    <td>查看登录窗口小部件配置。</td>
    <td>位于<strong>登录定制</strong>选项卡中。</td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>更新登录窗口小部件配置。</td>
    <td>可在<strong>登录定制</strong>选项卡中进行更新。</td>
  </tr>
</table>



