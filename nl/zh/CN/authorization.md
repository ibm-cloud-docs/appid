---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 授权和认证
{: authorization}

授权是对应用程序授予访问权的过程。{{site.data.keyword.appid_short}} 服务使用令牌、过滤器和头来认证用户。
{: shortdesc}


## OAuth 身份
{: #oauth}

服务调用 OAuth 登录 API 时，{{site.data.keyword.appid_short_notm}} 会使用 OAuth 2.0 和 OpenID Connect (OIDC) 协议通过所选身份提供者来授权和认证调用者。认证后，该身份就与 {{site.data.keyword.appid_short_notm}} 用户记录相关联。{{site.data.keyword.appid_short_notm}} 会返回一个可用于访问用户属性的访问令牌，以及一个保存了身份提供者所提供身份信息的身份令牌。相同的用户记录及其属性还可由使用此相同身份进行认证的任何客户端再次访问。

## 访问令牌和身份令牌

{{site.data.keyword.appid_short}} 使用两种类型的令牌：访问令牌和身份令牌。{:shortdesc}

**注**：令牌的格式为 <a href="https://jwt.io/introduction/" target="_blank">JSON Web 令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

### 访问令牌
{: #access-tokens}

有了访问令牌，就可以与受“App ID”所设置授权过滤器保护的[后端资源](/docs/services/appid/protecting-resources.html)进行通信。令牌符合 JavaScript 对象签名和加密 (JOSE) 规范。

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
}
```
{:screen}

<table>
<caption> 表 1. 访问令牌组成部分说明</caption>
  <tr>
    <th> 组成部分</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td><i>typ</i></td>
    <td> 头类型，指定为“JOSE”。</td>
  </tr>
  <tr>
    <td><i>alg</i></td>
    <td> 使用的算法，指定为“RS256”。</td>
  </tr>
  <tr>
    <td><i>iss</i></td>
    <td> 颁发令牌的 {{site.data.keyword.appid_short}} 服务器；指定为字符串或 URL。</td>
  </tr>
  <tr>
    <td><i>sub</i></td>
    <td> 向其颁发令牌的用户的标识。</td>
  </tr>
  <tr>
    <td><i>aud</i></td>
    <td> 令牌旨在用于的客户端标识。</td>
  </tr>
  <tr>
    <td><i>exp</i></td>
    <td> 时间戳记到期的时间，指定为戳记时间。</td>
  </tr>
  <tr>
    <td><i>iat</i></td>
    <td> 发出时间戳记的时间，指定为戳记时间。</td>
  </tr>
  <tr>
    <td><i>tenant</i></td>
    <td> 使用令牌颁发的唯一用户标识。</td>
  </tr>
  <tr>
    <td><i>amr</i></td>
    <td> 用于认证的身份提供者。此变量可以是 <i>appid_facebook</i>、<i>appid_google</i> 或 <i>cloud_directory</i>。</td>
  </tr>
  <tr>
    <td><i>scope</i></td>
    <td> 颁发令牌所适用的作用域。</td>
  </tr>
</table>


### 身份令牌
{: #identity-tokens}

身份令牌包含有关用户的信息。其可提供有关用户名称、性别和位置的信息。令牌还可返回链接至用户图像的 URL。

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
    "picture": "https://url.to.photo",
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
{:screen}


<table>
<caption> 表 2. 身份令牌组成部分说明</caption>
  <tr>
    <th> 组成部分</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td> <i>name</i></td>
    <td> 身份提供者所报告的用户全名。必须返回此项。</td>
  </tr>
  <tr>
    <td> <i>email</i></td>
    <td> 身份提供者所报告的用户电子邮件。仅当可用时返回。</td>
  </tr>
  <tr>
    <td> <i>gender</i></td>
    <td> 身份提供者所报告的用户性别（如果可用）。</td>
  </tr>
  <tr>
    <td> <i>locale</i></td>
    <td> 身份提供者所报告的用户语言环境。</td>
  </tr>
  <tr>
    <td> <i>picture</i></td>
    <td> 用户照片的 URL（如果可用）。</td>
  </tr>
  <tr>
    <td> <i>identities:</br> <ul><li> provider<li> id</ul></i></td>
    <td> </br><ul><li> 用于认证的身份提供者。此变量可以是 <code>appid_facebook</code>、<code>appid_google</code> 或 <code>cloud_directory</code>，并且必须返回此变量。<li> 身份提供者所报告的唯一用户标识。<li> 必须由身份提供者返回的 JSON 对象。</ul></li></td>
  </tr>
  <tr>
    <td> <i>oauth_client:</br> <ul><li> type</br><li> name<li> software_id<li> software_version<li> device_id <li>device_model<li>device_os<li>device_os_version </ul></i> </td>
    <td> </br><ul><li> 客户端注册期间确定的应用程序类型。此变量可以是 <em>serverapp</em> 或 <em>mobileapp</em>。<li> 客户端注册期间所报告的客户端名称。<li> 客户端注册期间所报告的软件标识。<li> 客户端注册期间使用的软件版本。<li> 移动客户端设备标识。<li> 移动客户端设备模型。<li> 移动客户端设备操作系统。<li> 移动客户端设备操作系统版本。</ul></td>
  </tr>
</table>

## 头
{: #auth-header}

授权头是所返回令牌的组合。对于 {{site.data.keyword.appid_short}}，授权头由三个以空格分隔的不同令牌组成：不记名、访问和身份。必须使用不记名和访问令牌才能授予对应用程序的访问权。身份令牌是可选的，主要用于存储使用应用程序的那些用户的信息。

示例头结构：

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


## 过滤器
{: #auth-filter}

{{site.data.keyword.appid_short}} 服务器 SDK 提供了用于保护以下两种类型的资源的策略：API 和 Web 应用程序。
{:shortdesc}

API 保护策略会返回 HTTP 401 响应，其中包含用于为未经认证的客户端获取授权的作用域列表。Web 应用程序保护策略会返回 HTTP 302 重定向。根据配置，重定向会将未经认证的客户端发送到 {{site.data.keyword.appid_short_notm}} 服务托管的登录页面，或者直接发送到身份提供者的登录页面。



### API 策略
{: #api}

API 策略期望请求包含带有有效访问令牌的授权头。响应还可以包含身份令牌，但这并不是必需的。

如果令牌无效或到期，那么 API 策略会返回 HTTP 401 错误，其中包含以下信息：Www-Authenticate=Bearer scope="{scope}" error="{error}"。`error` 组成部分是可选的。

如果请求返回有效的令牌，那么控制权会传递到下一个中间件，并且 `appIdAuthorizationContext` 属性会注入请求对象中。此属性包含原始访问令牌和身份令牌，以及解码为纯 JSON 对象的有效内容信息。


### Web 应用程序策略
{: #web}

Web 应用程序策略类检测到对受保护资源的未经认证的访问尝试时，会自动将用户的浏览器重定向到认证页面。成功认证后，用户会返回到 Web 应用程序的回调 URL。服务使用 Web 应用程序策略类来获取访问令牌和身份令牌。获取这些令牌后，Web 应用程序策略类会将其存储在 `WebAppStrategy.AUTH_CONTEXT` 下的 HTTP 会话中。由用户决定是否将访问令牌和身份令牌存储在应用程序数据库中。


## 渐进式认证
{: #oauth}

{{site.data.keyword.appid_short_notm}} 使用 OAuth 2.0 和 OIDC 协议来授权和认证用户。认证后，他们的身份就与用户记录相关联。该服务会返回一个可用于访问用户属性的访问令牌，以及一个保存了身份提供者所提供用户信息的身份令牌。该记录及其属性还可由使用相同身份进行认证的任何客户端再次访问。

现在，您可能会问：“我可以选择是否要登录吗？”{{site.data.keyword.appid_short_notm}} 使用称为渐进式认证的认证来创建[用户概要文件](/docs/services/appid/user-profile.html)，即使他们匿名也是如此。然后，您可以在用户登录之后将该信息传输给已知用户概要文件。

![显示成为已识别用户的路径的图。](/images/authenticationtrail.png)

图 2. 显示成为已识别用户的路径的图

当用户选择保持匿名状态时，{{site.data.keyword.appid_short_notm}} 会创建特别用户记录，并调用将返回匿名访问令牌和身份令牌的 OAuth 登录 API。通过使用这些令牌，应用程序可以创建、读取、更新和删除存储在用户记录中的属性。例如，用户无需登录即可立即开始向购物车添加项目。


当用户选择登录到应用程序时，他们将成为已识别用户。有关这些用户的信息将从他们选择用于登录的身份提供者获取。他们将接收包含用户信息的访问令牌和身份令牌。

匿名用户可选择成为已识别用户。但应如何操作呢？

首先将匿名访问令牌传递到登录 API。该服务会通过身份提供者认证调用。然后，该服务会使用访问令牌查找匿名记录并将身份附加到其中。新的访问身份令牌包含身份提供者共享的公共信息。识别用户之后，其匿名令牌将失效。不过，用户仍可访问其属性，因为使用新令牌即可访问。

**注**：如果身份尚未分配给其他用户，那么只能将其分配给匿名记录。如果身份已经与其他 {{site.data.keyword.appid_short_notm}} 用户关联，那么令牌会包含该用户的记录信息，并提供对其属性的访问权。先前的匿名用户属性将无法通过新的令牌进行访问。在此令牌到期之前，仍可通过匿名访问令牌来访问这些信息。开发期间，您可以选择要如何将匿名属性合并到已知用户。
