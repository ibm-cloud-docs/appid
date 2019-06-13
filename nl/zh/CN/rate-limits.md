---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-06"

keywords: Authentication, authorization, identity, app security, secure, rates, cloud directory, rate limit, attempts

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


# App ID 限制
{: #limits}

速率限制用于控制 App ID 实例的进出流量。通过限制请求或资源，可以保护应用程序。
{: shortdesc}

## App ID 轻量套餐 
{: #lite-limits}

请查看下表以了解针对 App ID 轻量实例实施的限制。 

<table>
    <tr>
        <th>资源</th>
        <th>最大值</th>
    </tr>
    <tr>
        <td>用户</td>
        <td>1000</td>
    </tr>
    <tr>
        <td>认证</td>
        <td>1000 次/月</td>
    </tr>
</table>

## 常规
{: #general-limits}

下表列出了 IBM Cloud App ID 资源的每个用户的最大限制以及超过限制时的阻塞时间段。这些限制适用于可以创建 IBM Cloud App ID 资源的任何用户。
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>限制</th>
        <th>超过时</th>
    </tr>
    <tr>
        <td>一个用户的登录尝试次数</td>
        <td>5 次/分钟</td>
        <td>用户在 1 分钟内无法登录。</td>
    </tr>
    <tr>
        <td>更新用户概要文件属性</td>
        <td>5 次/分钟</td>
        <td>用户在 1 分钟内无法更新概要文件。</td>
    </tr>
        <td>删除用户概要文件属性</td>
        <td>5 次/分钟</td>
        <td>用户在 1 分钟内无法更新概要文件。</td>
    </tr>
</table>



## Cloud Directory
{: #limits-cd}

请查看下表以了解与 Cloud Directory 关联的限制。
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>可配置</th>
        <th>限制</th>
        <th>超过时</th>
    </tr>
    <tr>
        <td>每个帐户的登录尝试次数</td>
        <td>是</td>
        <td>无限制</td>
        <td>在 1 分钟内阻止该实例的所有登录尝试。</td>
    </tr>
    <tr>
        <td>每个帐户的注册尝试次数</td>
        <td>是</td>
        <td>无限制</td>
        <td>在 1 分钟内阻止该实例的所有注册尝试。</td>
    </tr>
    <tr>
        <td>电子邮件发送请求</td>
        <td>否</td>
        <td>每个用户 10 分钟内发送 10 封电子邮件</td>
        <td>在 30 分钟内阻止该用户的电子邮件请求。</td>
    </tr>
</table>

有关更多信息，请参阅<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">速率限制管理 API</a>。
