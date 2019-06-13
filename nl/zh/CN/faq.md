---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-17"

keywords: authentication, authorization, identity, app security, secure

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
{:faq: data-hd-content-type='faq'}


# 常见问题
{: #faq}

此常见问题提供了对 {{site.data.keyword.appid_full}} 服务相关常见问题的解答。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} 如何计算定价？
{: #faq-pricing}
{: faq}

通过 {{site.data.keyword.appid_short_notm}}，使用更多的资源反而花费变少。
{: shortdesc}

累进层套餐由三部分组成：认证事件数、常规和高级安全性以及授权用户数。每月根据这两部分的汇总进行收取费用。总价是每级使用量的累计费用，每级使用量的费用等于使用量乘以该层的单价。

每月前 1000 个认证事件和前 1000 个授权用户免费，但任何高级安全事件除外。任何高级安全事件都会产生额外的费用。

### 认证事件
{: #faq-authentication}

颁发新访问令牌（常规或匿名）时会发生认证事件。可以使颁发令牌以响应由用户发起或由应用程序代表用户发起的登录请求。缺省情况下，访问令牌的有效期为一小时，匿名令牌的有效期为 30 天。令牌到期后，必须创建新令牌才能访问受保护资源。您可以在服务仪表板的**身份提供者 > 管理 > 认证设置**页面上更新 {{site.data.keyword.appid_short_notm}} 令牌的到期时间。

#### 高级安全功能

通过高级安全功能，您能够增强应用程序的安全性。
{: shortdesc}

<table>
  <tr>
    <th>功能</th>
    <th>优点</th>
  </tr>
  <tr>
    <td>多因子认证</td>
    <td>[Cloud Directory 的 MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) 要求用户除了输入其电子邮件和密码外，还要输入发送到其电子邮件的一次性密码，以此来确认用户身份。</td>
  </tr>
  <tr>
    <td>密码策略管理</td>
    <td>作为帐户所有者，您可以通过配置用户密码必须符合的一组规则来对 Cloud Directory 强制实施更安全的密码。示例包括：锁定前尝试登录的次数、到期时间、密码更新最短间隔时间或密码不能重复使用的次数。有关选项和设置信息的完整列表，请参阅[高级密码管理](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password)。</td>
  </tr>
</table>

缺省情况下，高级安全功能已禁用。如果开启 MFA 或密码策略管理，那么会产生额外的费用。如果禁用所有高级功能，那么帐户会还原为更低成本的策略。例如，如果您已获取了 10,000 个访问令牌，然后，您开启了密码策略管理，并且又获取了 10,000 个访问令牌。您将为 20,000 个认证事件和 10,000 个高级安全事件付费。

这些功能仅可用于位于累进层价格套餐上并且在 2018 年 3 月 15 日之后创建的实例。
{: note}

### 授权用户
{: #faq-authorized}

授权用户是（直接或间接）登录到服务的唯一用户，包括匿名用户。每当一个新用户（包括匿名用户）登录到应用程序时，都会按一个授权用户进行收费。例如，如果用户使用 Facebook 登录，而稍后使用 Google 登录，那么将视为两位单独的授权用户。

要获取最新的定价信息，可以通过单击 [{{site.data.keyword.cloud_notm}} 目录](https://cloud.ibm.com/catalog/services/app-id)的 {{site.data.keyword.appid_short_notm}} 部分中的**添加到估算**来创建成本估算。
{: tip}



## 为什么需要将重定向 URI 列入白名单？
{: #faq-redirect}
{: faq}

重定向 URI 是应用程序的回调端点。为防止钓鱼攻击，{{site.data.keyword.appid_short_notm}} 会根据重定向 URL 的白名单来验证 URI。发生钓鱼攻击时，攻击者可能会获取您的用户令牌的访问权。有关重定向 URI 的更多信息，请参阅[添加重定向 URI](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)。

不要在 URL 中包含任何查询参数。在验证过程中将忽略这些参数。URL 示例：`http://host:[port]/path`
{: tip}



## 加密在 {{site.data.keyword.appid_short_notm}} 中如何工作？
{: #faq-encryption}
{: faq}

请查看下表以获取有关加密的常见问题的答案。

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>为什么使用加密？</td>
      <td>我们保护用户信息的一种方法是对静态客户数据进行加密。服务会使用按租户分发的密钥对静态客户数据进行加密。</td>
    </tr>
    <tr>
      <td>您是否构建了自己的算法？您在代码中使用哪些？</td>
      <td>我们未构建自己的算法，服务将 <code>AES</code> 和 <code>SHA-256</code> 用于 salting。</td>
    </tr>
    <tr>
      <td>您是否使用公共或开放式源代码加密模块或提供程序？您是否公开过加密功能？</td>
      <td>服务使用 <code>javax.crypto</code> Java 库，但是从不会公开加密功能。</td>
    </tr>
    <tr>
      <td>如何存储密钥？</td>
      <td>密钥生成后，会使用特定于每个区域的主密钥进行加密，然后存储在本地。主密钥存储在 {{site.data.keyword.keymanagementserviceshort}} 中。在存储器和中间件级别，存在服务级别加密，这意味着有一个用于所有客户的密钥。在应用程序级别，每个客户都有自己的加密密钥。</td>
    </tr>
    <tr>
      <td>您使用何种密钥强度？</td>
      <td>该服务使用 16 字节。</td>
    </tr>
    <tr>
      <td>是否调用任何公开加密功能的远程 API？</td>
      <td>不调用。</td>
    </tr>
  </tbody>
</table>



## {{site.data.keyword.appid_short_notm}} 和 Keycloak 有什么区别？
{:# faq-keycloak}

{{site.data.keyword.appid_short_notm}} 和 Keycloak 都可用于向应用程序添加认证以及保护服务。这两个产品的主要区别在于其打包方式。
{: shortdesc}

Keycloak 打包成软件，这意味着作为开发者，您将在下载产品后负责维护产品的功能。您负责托管、高可用性、合规性、备份、DDoS 防御、负载均衡、Web 防火墙、数据库等。

{{site.data.keyword.appid_short_notm}} 是以“即服务”形式提供的完全受管产品。这意味着 IBM 将负责服务的运行，处理合规性、多个专区中的可用性、SLA 等。{{site.data.keyword.appid_short_notm}} 还具有 {{site.data.keyword.cloud_notm}} 平台的现成集成体验，该平台包含多种本机运行时和服务，例如 {{site.data.keyword.containershort_notm}}、{{site.data.keyword.openwhisk_short}} 和 {{site.data.keyword.cloudaccesstrailshort}}。
