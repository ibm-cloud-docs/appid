---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 管理服务访问权
{: #service-access-management}

使用 {{site.data.keyword.appid_full}} 和 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)，帐户所有者可以管理您帐户中的用户访问权。
{: shortdesc}

作为帐户所有者，您可以在帐户内设置策略，以便为不同用户创建不同级别的访问权。例如，某些用户可以对一个实例具有**只读**访问权，而对另一个实例具有**写**访问权。您可以决定哪些用户有权创建、更新和删除 {{site.data.keyword.appid_short_notm}} 的实例。

有关 IAM 的更多信息，请参阅 [IAM 访问权](/docs/iam/users_roles.html)。

## 用户角色
{: #roles}

访问策略的作用域基于用户分配的角色。
{: shortdesc}

策略允许在不同级别授予访问权。部分选项包括：
<ul><ul>
  <li>对帐户中所有服务实例的访问权</li>
  <li>对帐户中个别服务实例的访问权</li>
  <li>对实例中特定资源的访问权</li>
  <li>对帐户中所有启用 IAM 的服务的访问权</li>
</ul></ul>

平台管理角色支持用户对平台级别的服务资源执行任务。例如，可以分配角色以确定谁可以创建或删除标识、创建实例以及将实例绑定到应用程序。下表详细描述了与平台管理角色相关的操作。

<table>
  <tr>
    <th>平台角色</th>
    <th>许可权</th>
    <th>操作示例</th>
  </tr>
  <tr>
    <td><i>查看者</i></td>
    <td>查看 {{site.data.keyword.appid_short_notm}} 实例。</td>
    <td>您可以查看 Cloud Directory 用户数据或身份提供者配置。</td>
  </tr>
  <tr>
    <td><i>编辑者</i></td>
    <td>查看和绑定 {{site.data.keyword.appid_short_notm}} 实例。</td>
    <td>您可以将应用程序绑定到 {{site.data.keyword.appid_short_notm}} 的实例中。</td>
  </tr>
  <tr>
    <td><i>操作员</i></td>
    <td>创建、删除、编辑、暂挂、恢复，查看或绑定 {{site.data.keyword.appid_short_notm}} 实例。</td>
    <td>您可以从目录中创建或删除 {{site.data.keyword.appid_short_notm}} 实例。</td>
  </tr>
  <tr>
    <td><i>管理员</i></td>
    <td>帐户中所有服务的管理操作。</td>
    <td>您可以执行所有操作员操作，并可以将策略分配给其他用户。</td>
  </tr>
</table>

</br>
</br>
下表详细描述了映射到服务访问角色的操作。服务访问角色支持用户访问 {{site.data.keyword.appid_short_notm}} 以及调用 {{site.data.keyword.appid_short_notm}} API。


<table>
  <tr>
    <th>服务角色</th>
    <th>许可权</th>
    <th>操作示例</th>
  </tr>
  <tr>
    <td><i>读者</i></td>
    <td>查看 {{site.data.keyword.appid_short_notm}} 实例数据。</td>
    <td>可以查看服务实例的详细信息，例如用户数据或身份提供者信息。</td>
  </tr>
  <tr>
    <td> <i>作者或管理员</i></td>
    <td>查看和更改 {{site.data.keyword.appid_short_notm}} 实例。</td>
    <td>可以执行所有读者操作并编辑服务实例，例如编辑身份提供者配置。</li></ul></td>
  </tr>
</table>

有关在 UI 中分配用户角色的更多信息，请参阅[管理 IAM 访问权](/docs/iam/mngiam.html#iammanidaccser)。


## {{site.data.keyword.appid_short_notm}} 访问策略
{: #access}

对于访问您帐户中的 {{site.data.keyword.appid_short_notm}} 服务的每个用户，必须向其分配定义了 IAM 用户角色的访问策略。该策略确定用户可在您所选服务或实例的上下文中执行的操作。
{: shortdesc}

这些操作由 {{site.data.keyword.Bluemix_notm}} 服务定制和定义，作为允许在服务中执行的操作。然后，这些操作将映射到 IAM 用户角色。可使用 {{site.data.keyword.cloudaccesstrailshort}} 服务来跟踪所执行的某些操作。在下表中，{{site.data.keyword.appid_short_notm}} 的操作和必需的权限一一对应。

<table>
  <tr>
    <th>操作</th>
    <th>说明</th>
    <th>必需的角色</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>查看认证后重定向 URL。</td>
    <td>读者、作者和管理员</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>添加或更新认证后重定向 URL。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>更新身份提供者配置。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>查看身份提供者配置。</td>
    <td>读者、作者和管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>以列表形式查看任何最近的认证事件。</td>
    <td>读者、作者和管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>查看登录窗口小部件配置，例如徽标和颜色。</td>
    <td>读者、作者和管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>更新登录窗口小部件配置。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>查看用户概要文件配置。</td>
    <td>读者、作者和管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>更改用户概要文件配置。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>查看用户概要文件配置。</td>
    <td>读者、作者和管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>将新用户添加到 Cloud Directory。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>更新 Cloud Directory 用户详细信息。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>从 Cloud Directory 中删除用户。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>查看 Cloud Directory 电子邮件模板。</td>
    <td>读者、作者和管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>使用您自己的内容更新电子邮件模板。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>删除 Cloud Directory 电子邮件模板。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>查看 Cloud Directory 的 SAML 服务提供者 (SP) 元数据。</td>
    <td>读者、作者和管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>在登录窗口小部件中为 SAML 身份提供者设置或更新图片。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>根据模板向用户发送电子邮件。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>查看电子邮件的发件人详细信息。</td>
    <td>读者、作者和管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>更新发件人详细信息。</td>
    <td>作者、管理员</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>使用用户标识撤销用户的刷新令牌。</td>
    <td>作者、管理员</td>
  </tr>
</table>

## 跟踪 {{site.data.keyword.appid_short_notm}} 实例的更改
{: #tracking}

您可以使用 {{site.data.keyword.cloudaccesstrailshort}} 服务查看、管理和审计在 {{site.data.keyword.appid_short_notm}} 实例中执行的配置活动。
{: shortdesc}

要监视管理活动：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 帐户。
2. 在与 {{site.data.keyword.appid_short_notm}} 实例相同的帐户中，从目录供应“{{site.data.keyword.cloudaccesstrailshort}}”服务的实例。
3. 在“{{site.data.keyword.cloudaccesstrailshort}}”仪表板中，单击**管理**选项卡。
4. 在下拉列表中生成以下配置以搜索 {{site.data.keyword.appid_short_notm}} 生成的事件。
    * 对于**查看日志**，选择**帐户日志**。
    * 对于**搜索**，选择 **target.Management**。
    * 对于**过滤器**，输入 **appid**。
5. 单击**过滤器**。


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
    <td>查看 App ID SAML 元数据。</td>
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


有关服务如何工作的更多信息，请参阅 [{{site.data.keyword.cloudaccesstrailshort}} 文档](/docs/services/cloud-activity-tracker/index.html)。

</br>
</br>

## 示例：授予其他用户对 {{site.data.keyword.appid_short_notm}} 实例的访问权
{: #example}

在此场景中，管理员创建了 {{site.data.keyword.appid_short_notm}} 实例，需要将查看者访问权授予另一个团队成员。
{: shortdesc}

开始之前：
* 安装 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html)。

要更新访问许可权，管理员将完成下列步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。
2. 通过遵循 [IAM 文档](/docs/iam/iamusermanage.html#iamusermanage)中列出的步骤，授予员工查看访问权。
3. 浏览到 {{site.data.keyword.appid_short_notm}} 仪表板的**服务凭证**选项卡。单击**查看凭证**并复制**租户标识**。
4. 使用终端中的 {{site.data.keyword.Bluemix_notm}} CLI 进行登录。
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. 获取 IAM 令牌并记下它。
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
6. 请验证团队成员是否无法进行更改。
    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    结果显示 403 未经授权的消息。

要从 CLI 查看 {{site.data.keyword.appid_short_notm}} 配置，团队成员将完成以下步骤：

1. 使用您的终端的 {{site.data.keyword.Bluemix_notm}} CLI 进行登录。
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. 获取 IAM 令牌并记下它。
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. 使用 cURL 查看 Facebook 的身份提供者配置。
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
结果显示包含身份提供者信息的 200 条消息。

