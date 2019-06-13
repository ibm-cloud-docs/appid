---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-05"

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



# 了解令牌
{: #tokens}

成功认证用户后，应用程序将从 {{site.data.keyword.appid_short_notm}} 接收令牌。服务使用三种主要类型的令牌来完成认证流程。
{: shortdesc}


## 访问令牌
{: #access}

访问令牌表示授权，并且支持与受 {{site.data.keyword.appid_short}} 设置的授权过滤器所保护的[后端资源](/docs/services/appid?topic=appid-backend)通信。访问令牌符合 JavaScript 对象签名和加密 (JOSE) 规范。令牌的格式为 <a href="https://jwt.io/introduction/" target="blank">JSON Web 令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，并通过使用 RS256 算法的 JSON Web 密钥对令牌签名。


示例令牌：
  ```
  Header: {
      "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
  }
  ```
  {: screen}

## 什么是身份令牌？
{: #identity}

身份令牌表示认证并包含关于用户的信息。身份令牌可以为您提供有关用户的姓名、电子邮件、性别和位置的信息。令牌还可以返回用户图像的 URL。令牌的格式为 <a href="https://jwt.io/introduction/" target="blank">JSON Web 令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，并通过使用 RS256 算法的 JSON Web 密钥对令牌签名。


示例令牌：
  ```
  Header: {
      "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "exp": 1551903163,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "iat": 1551899553,
    "email": "appid155@mailinator.com",
    "name": "appid155@mailinator.com",
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "identities": [
      {
        "provider": "cloud_directory",
        "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
    ],
    "amr": [
      "cloud_directory"
    ]
  }
  ```
  {: screen}


身份令牌仅包含部分用户信息。要查看身份提供者提供的所有信息，可以使用 [/userinfo 端点](/docs/services/appid?topic=appid-profiles#profile-predefined-api)。

## 什么是刷新令牌？
{: #refresh}

{{site.data.keyword.appid_short}} 支持获取新访问令牌和身份令牌而不重新认证的功能，如 <a href="https://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 中所定义。可以使用刷新令牌来更新访问令牌，这样用户就不必执行任何操作来登录，例如提供凭证。与访问令牌类似，刷新令牌也包含允许 {{site.data.keyword.appid_short_notm}} 确定您是否已获授权的数据。但是，这些令牌是不透明的。

刷新令牌的生命周期配置为比常规访问令牌长，因此访问令牌到期时，刷新令牌仍将有效，并且可用于更新访问令牌。{{site.data.keyword.appid_short_notm}} 的刷新令牌可配置为持续 1 到 90 天。要充分利用刷新令牌，请在令牌完整生命周期内持久存储令牌，或者将令牌持久存储至更新为止。用户不能只使用刷新令牌来直接访问资源，因此持久存储刷新令牌比持久存储访问令牌更安全。最佳做法是，刷新令牌应由客户端安全地存储，客户端接收这些令牌，并仅将其发送到颁发令牌的授权服务器。

为了使用更加方便，{{site.data.keyword.appid_short_notm}} 还会在更新访问令牌时，更新其刷新令牌及其到期日期，这允许用户保持登录状态，但条件是该用户在当前刷新令牌到期之前的某个时间点处于活动状态。另一方面，如果要使用刷新令牌，但强制用户定期登录，那么应用程序只能使用用户通过输入其凭证登录时返回的刷新令牌。但是，我们建议始终使用从 {{site.data.keyword.appid_short_notm}} 收到的最新刷新令牌，如 <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">OAuth 2.0 规范 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 所述。


尽管这些令牌可以简化登录过程，但应用程序不应依赖于这些令牌，因为令牌可以随时撤销，例如您认为刷新令牌已泄露时。如果需要撤销刷新令牌，有两种方法可撤销刷新令牌。如果您有刷新令牌，那么可以根据 <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来撤销刷新令牌。或者，如果您有用户标识，那么可以使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来撤销刷新令牌。有关访问管理 API 的更多信息，请参阅[管理服务访问权](/docs/services/appid?topic=appid-service-access-management#service-access-management)。

有关使用刷新令牌以及如何使用这些刷新令牌来实现“记住我”功能的示例，请参阅[入门样本](/docs/services/appid?topic=appid-getting-started#getting-started)。


## 令牌来自何处？
{: #where}

令牌是通过 {{site.data.keyword.appid_short_notm}} OAuth 服务器颁发的，并格式化为 [JSON Web 令牌 (JWT)](https://jwt.io/introduction/)。令牌已使用 RS256 算法通过 [JSON Web 密钥 (JWK)](https://tools.ietf.org/html/rfc7517) 签名。

## 会怎样处理令牌包含的信息？
{: #contains}

访问令牌包含一组标准 JWT 声明和一组特定于 {{site.data.keyword.appid_short_notm}} 的声明，例如租户标识。身份令牌包含特定于用户的信息。令牌中的信息在[用户概要文件](/docs/services/appid?topic=appid-profiles)中存储为声明。

## 如何接收令牌？
{: #received}

成功认证后，应用程序将接收到令牌。应用程序可以使用这些令牌来检索有关用户授权和认证的信息。访问令牌可用于通过向资源发送请求来获取对受保护资源的访问权。在请求中，访问令牌在[持有者认证方案](https://tools.ietf.org/html/rfc6750#page-5)中进行描述。要抽取令牌，应用程序必须解析头。

示例请求：

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## 如何设置令牌？
{: #set}

可以通过 {{site.data.keyword.appid_short_notm}} 仪表板来启用和禁用令牌配置。有关配置选项的更多信息，请查看[管理令牌](/docs/services/appid?topic=appid-managing-idp#managing-idp)。
