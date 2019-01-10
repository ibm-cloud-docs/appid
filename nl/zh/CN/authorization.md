---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}




# 重要概念
{: #key-concepts}

搞不清楚授权与认证的区别？搞不清的不止您一人。请查看此页面上的信息以了解特定术语、流程以及服务使用令牌的方式。
{: shortdesc}


## 术语
{: #terms}


这些关键术语可以帮助您了解服务划分认证和验证流程的方式。

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 是用于提供应用程序授权的开放式标准协议。</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 是在 OAuth 2 之上运行的认证层。</p>
    <p>在将 OIDC 和 {{site.data.keyword.appid_short_notm}} 一起使用时，服务凭证可帮助配置 OAuth 端点。使用 SDK 时，将自动构建端点 URL。但是，您还可以使用服务凭证自行构建 URL。在以下示例和表中，您可以查看如何将 URL 组合在一起。</p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
      "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
      "profilesUrl": "https://appid-profiles.ng.bluemix.net/"
    }</code></pre>
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
    <p><strong>注</strong>：使用 SDK 时，将自动构建端点 URL。</p></dd>
  <dt>令牌</dt>
    <dd>服务使用三种不同类型的令牌。访问令牌表示授权，并且支持与受 {{site.data.keyword.appid_short}} 设置的授权过滤器所保护的[后端资源](/docs/services/appid/backend-apps.html)通信。身份令牌表示认证并包含关于用户的信息。可以使用刷新令牌来获取新的访问令牌，而无需重新认证该用户。通过使用刷新令牌，用户可以允许应用程序记住其信息。这样他们就可以保持登录。有关令牌及其在 {{site.data.keyword.appid_short}} 中的使用方式的更多信息，请查看[验证令牌](tokens.html#remote-validation)。
  </dd>
  <dt>授权头</dt>
    <dd><p>{{site.data.keyword.appid_short}} 符合<a href="https://tools.ietf.org/html/rfc6750" target="blank">令牌持有者规范 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，并且组合使用作为 HTTP 授权头发送的访问令牌和身份令牌。授权头包含以空格分隔的三个不同部分。这些令牌采用 Base64 编码。身份令牌是可选的。</br>
    示例：</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API 策略</dt>
    <dd><p>API 策略期望请求包含带有有效访问令牌的授权头。该请求还可以包含身份令牌，但这并不是必需的。如果令牌无效或到期，那么 API 策略会返回 HTTP 401 错误，其中包含以下 HTTP 头：</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>如果请求返回有效的令牌，那么控制权会传递到下一个中间件，并且 <code>appIdAuthorizationContext</code> 属性会注入请求对象中。此属性包含原始访问令牌和身份令牌，以及解码为纯 JSON 对象的有效内容信息。</dd>
  <dt>Web 应用程序策略</dt>
    <dd>Web 应用程序策略检测到对受保护资源的未经授权的访问尝试时，会自动将用户的浏览器重定向到认证页面，该页面可以由 {{site.data.keyword.appid_short}} 提供。成功认证后，用户会返回到 Web 应用程序的回调 URL。Web 应用程序策略会获取访问令牌和身份令牌，并将其存储在 HTTP 会话中的 <code>WebAppStrategy.AUTH_CONTEXT</code> 下。由用户决定是否将访问令牌和身份令牌存储在应用程序数据库中。</dd>
  <dt>数据分隔和加密</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} 存储并加密用户概要文件属性。作为多租户服务，每个租户都具有指定的加密密钥，并且每个租户中的用户数据只使用该租户的密钥进行加密。</p>
    <p>{{site.data.keyword.appid_short_notm}} 确保私有信息在加密后才进行存储。</p></dd>
</dl>

</br>
</br>


## 了解令牌
{: #tokens}

成功认证用户后，应用程序将从 {{site.data.keyword.appid_short_notm}} 接收令牌。服务使用三种主要类型的令牌来完成认证流程。
{: shortdesc}


**什么是访问令牌？**

访问令牌表示授权，并且支持与受 {{site.data.keyword.appid_short}} 设置的授权过滤器所保护的[后端资源](/docs/services/appid/backend-apps.html)通信。访问令牌符合 JavaScript 对象签名和加密 (JOSE) 规范。令牌的格式为 <a href="https://jwt.io/introduction/" target="blank">JSON Web 令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，并通过使用 RS256 算法的 JSON Web 密钥对令牌签名。


示例令牌：
  ```
  Header: {
      "typ": "JOSE",
      "alg": "RS256",
  }
  Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "exp": "1495562664",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "amr": ["facebook"],
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "iat": "1495559064",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
  ```
  {: screen}

**什么是身份令牌？**

身份令牌表示认证并包含关于用户的信息。身份令牌可以为您提供有关用户的姓名、电子邮件、性别和位置的信息。令牌还可以返回用户图像的 URL。令牌的格式为 <a href="https://jwt.io/introduction/" target="blank">JSON Web 令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，并通过使用 RS256 算法的 JSON Web 密钥对令牌签名。


示例令牌：
  ```
  Header: {
      "typ": "JOSE",
      "alg": "RS256",
  }
  Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "exp: "1495562664",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "iat": "1495559064",
      "name": "John Smith",
      "email": "js@mail.com",
      "gender", "male",
      "locale": "en",
      "picture": "<URL-to-photo>",
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "identities": [
          "provider": "facebook"
          "id": "377440159275659"
      ],
      "amr": ["facebook"],
      "oauth_client":{
        "name": "BluemixApp",
        "type": "serverapp",
        "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
        "software_version": "1.0.0",
      }
  }
  ```
  {: screen}

身份令牌仅包含部分用户信息。要查看身份提供者提供的所有信息，可以使用[用户信息端点](/docs/services/appid/predefined.html#api)。

**什么是刷新令牌？**

{{site.data.keyword.appid_short}} 支持获取新访问令牌和身份令牌而不重新认证的功能，如 <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 中所定义。可以使用刷新令牌来更新访问令牌，这样用户就不必执行任何操作来登录，例如提供凭证。与访问令牌类似，刷新令牌也包含允许 {{site.data.keyword.appid_short_notm}} 确定您是否已获授权的数据。但是，这些令牌是不透明的。

刷新令牌的生命周期配置为比常规访问令牌长，因此访问令牌到期时，刷新令牌仍将有效，并且可用于更新访问令牌。{{site.data.keyword.appid_short_notm}} 的刷新令牌可配置为持续 1 到 90 天。要充分利用刷新令牌，请在令牌完整生命周期内持久存储令牌，或者将令牌持久存储至更新为止。用户不能只使用刷新令牌来直接访问资源，因此持久存储刷新令牌比持久存储访问令牌更安全。最佳做法是，刷新令牌应由客户端安全地存储，客户端接收这些令牌，并仅将其发送到颁发令牌的授权服务器。

为了使用更加方便，{{site.data.keyword.appid_short_notm}} 还会在更新访问令牌时，更新其刷新令牌及其到期日期，这允许用户保持登录状态，但条件是该用户在当前刷新令牌到期之前的某个时间点处于活动状态。另一方面，如果要使用刷新令牌，但强制用户定期登录，那么应用程序只能使用用户通过输入其凭证登录时返回的刷新令牌。但是，我们建议始终使用从 App ID 收到的最新刷新令牌，如 <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">Oauth 规范 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 所述。


尽管这些令牌可以简化登录过程，但应用程序不应依赖于这些令牌，因为令牌可以随时撤销，例如您认为刷新令牌已泄露时。如果需要撤销刷新令牌，有两种方法可撤销刷新令牌。如果您有刷新令牌，那么可以根据 <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来撤销刷新令牌。或者，如果您有用户标识，那么可以使用<a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来撤销刷新令牌。有关访问管理 API 的更多信息，请参阅[管理服务访问权](iam.html#service-access-management)。

有关使用刷新令牌以及如何使用这些刷新令牌来实现“记住我”功能的示例，请参阅[入门样本](index.html)。


**令牌来自何处？**

令牌是通过 {{site.data.keyword.appid_short_notm}} OAuth 服务器颁发的，并格式化为 [JSON Web 令牌 (JWT)](https://jwt.io/introduction/)。令牌已使用 RS256 算法通过 [JSON Web 密钥 (JWK)](https://tools.ietf.org/html/rfc7517) 签名。

**会怎样处理令牌包含的信息？**

访问令牌包含一组标准 JWT 声明和一组特定于 {{site.data.keyword.appid_short_notm}} 的声明，例如租户标识。身份令牌包含特定于用户的信息。令牌中的信息在[用户概要文件](/docs/services/appid/user-profile.html)中存储为声明。

**如何接收令牌？**

成功认证后，应用程序将接收到令牌。应用程序可以使用这些令牌来检索有关用户授权和认证的信息。访问令牌可用于通过向资源发送请求来获取对受保护资源的访问权。在请求中，访问令牌在[持有者认证方案](https://tools.ietf.org/html/rfc6750#page-5)中进行描述。要抽取令牌，应用程序必须解析头。

示例请求：

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

</br>
</br>
