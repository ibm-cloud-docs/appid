---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

keywords: authentication, authorization, identity, app security, secure, access, platform, management, permissions

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


# 管理服务访问权
{: #service-access-management}

使用 {{site.data.keyword.appid_full}} 和 {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM)，帐户所有者可以管理您帐户中的用户访问权。
{: shortdesc}

作为帐户所有者，您可以在帐户内设置策略，以便为不同用户创建不同级别的访问权。例如，某些用户可以对一个实例具有**只读**访问权，而对另一个实例具有**写**访问权。您可以决定哪些用户有权创建、更新和删除 {{site.data.keyword.appid_short_notm}} 的实例。

有关 IAM 的更多信息，请参阅 [IAM 访问权](/docs/iam?topic=iam-userroles)。

## 用户角色
{: #iam-roles}

访问策略的作用域基于用户分配的角色。
{: shortdesc}

策略允许在不同级别授予访问权。部分选项包括：
<ul><ul>
  <li>对帐户中所有服务实例的访问权</li>
  <li>对帐户中个别服务实例的访问权</li>
  <li>对实例中特定资源的访问权</li>
  <li>对帐户中所有启用 IAM 的服务的访问权</li>
</ul></ul>

### 平台角色
{: #iam-platform-roles}

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

### 服务访问角色
{: #iam-service-roles}
下表详细描述了映射到服务访问角色的操作。服务访问角色支持用户访问 {{site.data.keyword.appid_short_notm}} 以及调用 {{site.data.keyword.appid_short_notm}} API。


<table>
  <tr>
    <th>服务角色</th>
    <th>许可权</th>
    <th>操作示例</th>
  </tr>
  <tr>
    <td><i>读取者</i></td>
    <td>查看 {{site.data.keyword.appid_short_notm}} 实例数据。</td>
    <td>可以查看服务实例的详细信息，例如用户数据或身份提供者信息。</td>
  </tr>
  <tr>
    <td> <i>写入者或管理者</i></td>
    <td>查看和更改 {{site.data.keyword.appid_short_notm}} 实例。</td>
    <td>可以执行所有读取者操作并编辑服务实例，例如编辑身份提供者配置。</li></ul></td>
  </tr>
</table>

有关在 UI 中分配用户角色的更多信息，请参阅[管理 IAM 访问权](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)。


## {{site.data.keyword.appid_short_notm}} 访问策略
{: #iam-access}

对于访问您帐户中的 {{site.data.keyword.appid_short_notm}} 服务的每个用户，必须向其分配定义了 IAM 用户角色的访问策略。该策略确定用户可在您所选服务或实例的上下文中执行的操作。
{: shortdesc}

这些操作由 {{site.data.keyword.cloud_notm}} 服务定制和定义，作为允许在服务中执行的操作。然后，这些操作将映射到 IAM 用户角色。可使用 {{site.data.keyword.cloudaccesstrailshort}} 服务来跟踪所执行的某些操作。在下表中，{{site.data.keyword.appid_short_notm}} 的操作和必需的许可权一一对应。

<table>
  <tr>
    <th>操作</th>
    <th>说明</th>
    <th>必需的角色</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>查看认证后重定向 URL。</td>
    <td>读取者、写入者和管理者</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>添加或更新认证后重定向 URL。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>更新身份提供者配置。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>查看身份提供者配置。</td>
    <td>读取者、写入者和管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>以列表形式查看任何最近的认证事件。</td>
    <td>读取者、写入者和管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>查看登录窗口小部件配置，例如徽标和颜色。</td>
    <td>读取者、写入者和管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>更新登录窗口小部件配置。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>查看用户概要文件配置。</td>
    <td>读取者、写入者和管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>更改用户概要文件配置。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>查看用户概要文件配置。</td>
    <td>读取者、写入者和管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>将新用户添加到 Cloud Directory。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>更新 Cloud Directory 用户详细信息。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>从 Cloud Directory 中删除用户。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>查看 Cloud Directory 电子邮件模板。</td>
    <td>读取者、写入者和管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>使用您自己的内容更新电子邮件模板。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>删除 Cloud Directory 电子邮件模板。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>查看 Cloud Directory 的 SAML 服务提供者 (SP) 元数据。</td>
    <td>读取者、写入者和管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>在登录窗口小部件中为 SAML 身份提供者设置或更新图片。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>根据模板向用户发送电子邮件。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>查看电子邮件的发件人详细信息。</td>
    <td>读取者、写入者和管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>更新发件人详细信息。</td>
    <td>写入者、管理者</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>使用用户标识撤销用户的刷新令牌。</td>
    <td>写入者、管理者</td>
  </tr>
</table>

</br>

## 示例：授予其他用户对 {{site.data.keyword.appid_short_notm}} 实例的访问权
{: #iam-example}

在此场景中，管理员创建了 {{site.data.keyword.appid_short_notm}} 实例，需要将查看者访问权授予另一个团队成员。
{: shortdesc}

开始之前：
* 安装 [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)。

要更新访问许可权，管理员将完成下列步骤：

1. 登录到 {{site.data.keyword.cloud_notm}} 控制台。

2. 通过遵循 [IAM 文档](/docs/iam?topic=iam-iammanidaccser)中列出的步骤，授予员工查看访问权。

3. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的**服务凭证**选项卡。单击**查看凭证**并复制**租户标识**。

4. 使用终端中的 {{site.data.keyword.cloud_notm}} CLI 进行登录。
    

    ```
    ibmcloud login -api -a https://api.<region>.cloud.ibm.com
    ```
    {: pre}

    <table>
      <tr>
        <th>区域</th>
        <th>端点</th>
      </tr>
      <tr>
        <td>达拉斯</td>
        <td><code>us-south</code></td>
      </tr>
      <tr>
        <td>法兰克福</td>
        <td><code>eu-de</code></td>
      </tr>
      <tr>
        <td>悉尼</td>
        <td><code>au-syd</code></td>
      </tr>
      <tr>
        <td>伦敦</td>
        <td><code>eu-gb</code></td>
      </tr>
      <tr>
        <td>东京</td>
        <td><code>jp-tok</code></td>
      </tr>
    </table>

5. 获取 IAM 令牌并记下它。
    

    ```
    ibmcloud iam oauth-tokens
    ```
    {: pre}

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
    'https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/facebook'
    ```
    {: pre}

    结果显示 403 未经授权的消息。

要从 CLI 查看 {{site.data.keyword.appid_short_notm}} 配置，团队成员将完成以下步骤：

1. 使用您的终端的 {{site.data.keyword.cloud_notm}} CLI 进行登录。
    

    ```
    ibmcloud login -a api.<region>.console.cloud.ibm.com
    ```
    {: pre}

2. 获取 IAM 令牌并记下它。
    

    ```
    ibmcloud iam oauth-tokens
    ```
    {: pre}

3. 使用 cURL 查看 Facebook 的身份提供者配置。
    

    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/facebook'
    ```
    {: pre}

    结果显示包含身份提供者信息的 200 条消息。

