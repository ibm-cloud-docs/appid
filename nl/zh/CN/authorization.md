---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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

# 重要概念
{: #key-concepts}

搞不清楚授权与认证的区别？搞不清的不止您一人。请查看此页面上的信息以了解特定术语、流程以及服务使用令牌的方式。
{: shortdesc}

要了解有关一些授权和认证基本概念的更多信息？请查看此处。在以下视频中，可以了解 OAuth 2.0、授权类型、OIDC 等内容。

<iframe class="embed-responsive-item" id="about-appid-basics" title="关于 {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/ndlk-ZhKGXM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


## 术语
{: #terms}

这些关键术语可以帮助您了解服务划分认证和验证流程的方式。

### OAuth 2
{: #term-oauth}
<a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 是用于提供应用程序授权的开放式标准协议。


### Open ID Connect (OIDC)
{: #term-oidc}

<a href="https://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 是基于 OAuth 2 工作的认证层。在将 OIDC 和 {{site.data.keyword.appid_short_notm}} 一起使用时，应用程序凭证可帮助配置 OAuth 端点。使用 SDK 时，将自动构建端点 URL。但是，您还可以使用服务凭证自行构建 URL。URL 采用以下格式：{{site.data.keyword.appid_short_notm}} 服务端点 + "/oauth/v4" + /tenantID。

    示例：

```
{
  "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
  "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
  "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
  "name":testing",
  "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
  "profilesUrl": "https://us-south.appid.cloud.ibm.com",
  "discoveryEndpoint": "https://us-south.appid.ibm.cloud.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
}
```
{: screen}

使用此示例时，URL 将为 `https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0`。然后，附加要向其发出请求的端点。请查看下表以了解一些示例端点。

<table>
  <tr>
    <th>端点</th>
    <th>格式</th>
  </tr>
  <tr>
    <td>授权</td>
    <td>{oauthServerUrl}/authorization</td>
  </tr>
  <tr>
    <td>令牌</td>
    <td>{oauthServerUrl}/token</td>
  </tr>
  <tr>
    <td>用户信息</td>
    <td>{oauthServerUrl}/userinfo</td>
  </tr>
  <tr>
    <td>JWKS</td>
    <td>{oauthServerUrl}/publickeys</td>
  </tr>
</table>

使用 SDK 时，将自动构建端点 URL。
{: note}

### 令牌
{: #term-token}

服务使用三种不同类型的令牌。访问令牌表示授权，并且支持与受 {{site.data.keyword.appid_short}} 设置的授权过滤器所保护的[后端资源](/docs/services/appid?topic=appid-backend)通信。身份令牌表示认证并包含关于用户的信息。可以使用刷新令牌来获取新的访问令牌，而无需重新认证该用户。通过使用刷新令牌，用户可以允许应用程序记住其信息。这样他们就可以保持登录。令牌在 {{site.data.keyword.appid_short}} 仪表板的**身份提供者 > 管理**中进行设置。有关令牌及其在 {{site.data.keyword.appid_short}} 中的使用方式的更多信息，请查看[管理令牌](/docs/services/appid?topic=appid-tokens#tokens)。
  

### 授权头
{: #term-auth-header}

{{site.data.keyword.appid_short}} 符合<a href="https://tools.ietf.org/html/rfc6750" target="blank">令牌持有者规范 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，并且组合使用作为 HTTP 授权头发送的访问令牌和身份令牌。授权头包含以空格分隔的三个不同部分。这些令牌采用 Base64 编码。身份令牌是可选的。

    示例：

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


### API 策略
{: #term-api-strategy}

API 策略期望请求包含带有有效访问令牌的授权头。该请求还可以包含身份令牌，但这并不是必需的。如果令牌无效或到期，那么 API 策略会返回 HTTP 401 错误，其中包含以下 HTTP 头：
```
Www-Authenticate=Bearer scope="{scope}" error="{error}"
```
{: screen}

如果请求返回有效的令牌，那么控制权会传递到下一个中间件，并且 `appIdAuthorizationContext` 属性会注入请求对象中。此属性包含原始访问令牌和身份令牌，以及解码为纯 JSON 对象的有效内容信息。

### Web 应用程序策略
{: #term-web-strategy}

Web 应用程序策略检测到对受保护资源的未经授权的访问尝试时，会自动将用户的浏览器重定向到认证页面，该页面可以由 {{site.data.keyword.appid_short}} 提供。成功认证后，用户会返回到 Web 应用程序的回调 URL。Web 应用程序策略会获取访问令牌和身份令牌，并将其存储在 HTTP 会话中的 `WebAppStrategy.AUTH_CONTEXT` 下。由用户决定是否将访问令牌和身份令牌存储在应用程序数据库中。

### 数据分隔和加密
{: #term-data-encryption}

{{site.data.keyword.appid_short_notm}} 存储并加密用户概要文件属性。作为多租户服务，每个租户都具有指定的加密密钥，并且每个租户中的用户数据只使用该租户的密钥进行加密。

{{site.data.keyword.appid_short_notm}} 确保私有信息在加密后才进行存储。
{: note}


### 重定向 URI
{: #term-redirect}

{{site.data.keyword.appid_short_notm}} 使用已核准的标准 URI 列表，在用户与应用程序交互后重定向用户。例如，如果用户成功登录，{{site.data.keyword.appid_short_notm}} 会将用户重定向到应用程序的主页或您指定的其他页面。根据应用程序，URI 的格式可能会变化。请查看[添加重定向 URI](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri) 以获取更多信息。


### JSON Web 密钥集 (JWKS)
{: #term-jwks}

JWKS 表示一组密钥。{{site.data.keyword.appid_short_notm}} 使用 JWKS 来验证服务生成的令牌的真实性。通过使用密钥标识来验证签名，可以确保令牌是由可信源（即 {{site.data.keyword.appid_short_notm}}）发出的，并且令牌中的信息从未被更改。


