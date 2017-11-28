---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 访问令牌和身份令牌

{{site.data.keyword.appid_short}} 使用两种类型的令牌：访问令牌和身份令牌。令牌的格式为 <a href="https://jwt.io/introduction/" target="_blank">JSON Web 令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
{:shortdesc}


## 访问令牌
{: #access-tokens}

有了访问令牌，就可以与受 {{site.data.keyword.appid_short_notm}} 授权过滤器保护的[后端资源](/docs/services/appid/protecting-resources.html)进行通信。令牌符合 JavaScript 对象签名和加密 (JOSE) 规范，并且具有以下格式：

```
Header: {

    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": "facebook",
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
    <td> <i>typ</i></td>
    <td> 头类型，指定为“JOSE”。</td>
  </tr>
  <tr>
    <td> <i>alg</i></td>
    <td> 使用的算法，指定为“RS256”。</td>
  </tr>
  <tr>
    <td> <i>iss</i></td>
    <td> 颁发令牌的 {{site.data.keyword.appid_short}} 服务器；指定为字符串或 URL。</td>
  </tr>
  <tr>
    <td> <i>sub</i></td>
    <td> 向其颁发令牌的用户的标识。</td>
  </tr>
  <tr>
    <td> <i>aud</i></td>
    <td> 令牌旨在用于的客户端标识。</td>
  </tr>
  <tr>
    <td> <i>exp</i></td>
    <td> 时间戳记到期的时间，指定为戳记时间。</td>
  </tr>
  <tr>
    <td> <i>iat</i></td>
    <td> 发出时间戳记的时间，指定为戳记时间。</td>
  </tr>
  <tr>
    <td> <i>tenant</i></td>
    <td> 对其颁发令牌的租户标识。</td>
  </tr>
  <tr>
    <td> <i>amr</i></td>
    <td> 用于认证的身份提供者。此变量可以是 <i>appid_facebook</i> 或 <i>appid_google</i>。</td>
  </tr>
  <tr>
    <td> <i>scope</i></td>
    <td> 颁发令牌所适用的作用域。</td>
  </tr>
</table>


## 身份令牌
{: #identity-tokens}

身份令牌包含有关用户的信息，包括姓名、电子邮件、性别、照片和位置。

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
        "id": "377440159275659",
        "amr: "facebook",
    ],
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
    <td> <i>identities:</br> <ul><li> provider<li> id<li> amr</ul></i></td>
    <td> </br><ul><li> 用于认证的身份提供者。此变量可以是 <code>appid_facebook</code> 或 <code>appid_google</code>，并且必须返回此变量。</li><li> 身份提供者所报告的唯一用户标识。</li><li> 必须由身份提供者返回的 JSON 对象。</li></ul></td>
  </tr>
  <tr>
    <td> <i>oauth_client:</br> <ul><li> type<li> name<li> software_id<li> software_version</ul></i> </td>
    <td> </br><ul><li> 客户端注册期间确定的应用程序类型。此变量可以是 <i>serverapp</i> 或 <i>mobileapp</i>。<li> 客户端注册期间所报告的客户端名称。<li> 客户端注册期间所报告的软件标识。<li> 客户端注册期间使用的软件版本。</ul></td>
  </tr>
</table>
