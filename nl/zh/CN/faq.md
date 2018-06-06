---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# 常见问题

此常见问题提供了对 {{site.data.keyword.appid_full}} 服务相关常见问题的解答。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} 如何计算定价？
{: #pricing}

通过 {{site.data.keyword.appid_short_notm}}，使用更多的资源反而花费变少。
{: shortdesc}

累进层计划由两部分组成：认证事件数和授权用户数。每月根据这两部分的汇总进行收取费用。总价是每级使用量的累计费用，每级使用量的费用等于使用量乘以该层的单价。

### 认证事件

颁发新的 {{site.data.keyword.appid_short_notm}} 令牌时会产生认证事件。对于已识别用户，每个新令牌在一小时内有效。对于匿名用户，令牌在一个月内有效。令牌到期后，必须创建新令牌才能访问受保护资源。使用 App ID 进行移动认证时，用户令牌存储于 `key-store/key-chain` 中，并会添加到未来的每一个请求中。使用 {{site.data.keyword.appid_short_notm}} Android 或 iOS Swift SDK 可访问这些令牌。使用服务进行 Web 认证时，请在会话 cookie 中<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">存储用户令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

### 授权用户

授权用户是使用服务直接或间接登录的唯一用户。每次当新用户（包括匿名用户）从各个身份提供者登录时，将各按一个授权用户进行收费。例如，如果用户使用 Facebook 登录，而稍后使用 Google 登录，那么将视为两位单独的授权用户。

有关累进层定价的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 定价文档](/docs/billing-usage/how_charged.html#services)。

</br>

## App ID 监视哪种类型的活动？
{: #activity-monitor}

您可以跟踪在绑定到服务实例的应用程序中生成的活动。还可以使用“活动跟踪程序”服务来监视在 App ID 中生成的管理活动。

要查看应用程序生成的活动：

1. 登录 IBM Cloud 帐户。
2. 在仪表板中选择 App ID 的实例。
3. 单击**概述**选项卡。
4. 查看**活动日志**中列出的活动。

</br>
要监视管理活动：

1. 登录 IBM Cloud 帐户。导航到供应 App ID 实例的组织和空间。
2. 在目录中供应“活动跟踪程序”服务的实例。确保您所在的空间就是 App ID 实例所在的空间。
3. 在“活动跟踪程序”仪表板中，单击**管理**选项卡。
4. 在下拉列表中选择以下配置以搜索 App ID 生成的任何事件。
<table>
  <tr>
    <th> 字段 </th>
    <th> 配置</th>
  </tr>
  <tr>
    <td><i>查看日志</i></td>
    <td><b>空间日志</b></td>
  </tr>
  <tr>
    <td><i>搜索</i></td>
    <td><b>target.name</b></td>
  </tr>
  <tr>
    <td>过滤器</td>
    <td>appid</td>
  </tr>
</table>
5. 单击**过滤器**。

查看[活动跟踪程序文档](/docs/services/cloud-activity-tracker/index.html)以了解有关该服务工作方式的更多信息。
