---

copyright:
  years: 2017
lastupdated: "2017-12-12"

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


有关累进层定价的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 定价文档](/docs/pricing/index.html#pricing)。
