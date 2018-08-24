---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# 授权和认证
{: #authorization}

借助 {{site.data.keyword.appid_full}}，用户可以利用令牌和授权过滤器确保应用程序受到保护。身份提供者必须对用户身份进行认证，用户才能够向应用程序授权。
{: shortdesc}


## 重要概念
{: #key-concepts}

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
    <dd>服务使用三种不同类型的令牌来提供认证。访问令牌表示授权，并且支持与受 {{site.data.keyword.appid_short}} 设置的授权过滤器所保护的[后端资源](/docs/services/appid/protecting-resources.html)通信。身份令牌表示认证并包含关于用户的信息。刷新令牌是具有扩展有效期的访问令牌。通过使用刷新令牌，用户可以允许应用程序记住其信息。这样他们就可以保持登录。</dd>
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

## 流程运行方式
{: #process}

在进行应用程序编码时，一个最重要的问题就是安全性。如何确保只有拥有正确访问权限的用户才能使用应用程序？使用授权流程。在大多数流程中，授权和认证一起进行耦合，这会让更改安全策略和身份提供者变得复杂。利用 {{site.data.keyword.appid_short}}，可以将授权和认证分为不同的流程。
{: shortdesc}

在配置社交身份提供者（如 Facebook）时，会使用 [Oauth2 授权流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)来调用登录窗口小部件。利用 Cloud Directory 作为身份提供者，会使用[资源所有者密码凭证流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)来提供访问令牌和身份令牌。

![成为已识别用户的途径。](/images/authenticationtrail.png)

当用户选择登录时，他们将成为已识别用户。身份提供者将访问令牌和身份令牌返回到包含用户相关信息的 {{site.data.keyword.appid_short}}。该服务接收提供的令牌，并确定用户有没有可访问应用程序的正确凭证。如果令牌通过了验证，那么该服务会授权用户进行访问。用户获得授权后，认证信息与用户的记录相关联。该记录及其属性还可由使用相同身份进行认证的任何客户端再次访问。

### 渐进式认证

利用 {{site.data.keyword.appid_short_notm}}，匿名用户可以选择成为已识别用户。

但应如何操作呢？

如果用户选择不立即登录，就会被视为匿名用户。例如，用户无需登录就可以立即开始向购物车添加项目。对于匿名用户，{{site.data.keyword.appid_short_notm}} 会创建特别用户记录，并调用将返回匿名访问令牌和身份令牌的 OAuth 登录 API。通过使用这些令牌，应用程序可以创建、读取、更新和删除存储在用户记录中的属性。

![在以匿名用户身份启动时成为已识别用户的途径。](/images/anon-authenticationtrail.png)

在匿名用户登录时，他们的访问令牌将会传递到登录 API。该服务会通过身份提供者认证调用。然后，该服务会使用访问令牌查找匿名记录并将身份附加到其中。新的访问令牌和身份令牌包含身份提供者共享的公共信息。识别用户之后，其匿名令牌将失效。不过，用户仍可访问其属性，因为使用新令牌即可访问。

仅当尚未将身份分配给其他用户时，才能将其分配给匿名记录。
{: tip}

如果身份已经与其他 {{site.data.keyword.appid_short_notm}} 用户关联，那么令牌会包含该用户的记录信息，并提供对其属性的访问权。先前的匿名用户属性将无法通过新的令牌进行访问。在此令牌到期之前，仍可通过匿名访问令牌来访问这些信息。开发期间，您可以选择要如何将匿名属性合并到已知用户。
