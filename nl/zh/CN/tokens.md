---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-23"

keywords: authentication, authorization, identity, app security, secure, tokens, jwt, development

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


# 验证令牌
{: #token-validation}

令牌验证是现代应用程序开发中的重要组成部分。通过验证令牌，可以保护应用程序或 API，防止未经授权的用户访问。{{site.data.keyword.appid_full}} 使用访问令牌和身份令牌来确保在授予用户或应用程序访问权之前，已对其进行认证。如果使用的是 {{site.data.keyword.appid_short_notm}} 提供的其中一个 SDK，那么已为您获取并验证令牌！
{: shortdesc}

有关如何在 {{site.data.keyword.appid_short_notm}} 中使用令牌的更多信息，请参阅[了解令牌](/docs/services/appid?topic=appid-tokens#tokens)。
{: tip}

令牌用于验证个人的身份是否与其声明的一致。令牌确认用户在指定的时间长度内可能拥有的任何访问许可权。用户登录到应用程序，并向其颁发了令牌后，应用程序必须先验证用户，然后才会为其提供访问权。

</br>

**如果 {{site.data.keyword.appid_short_notm}} 没有与我所用语言对应的 SDK 该怎么做？**

别担心！有三个选项供您使用：

* 使用 {{site.data.keyword.appid_short_notm}} API
* 实现您自己的验证逻辑
* 使用符合 OIDC 的任何开放式源代码 SDK

根据反馈，选项 1 通常是最简单的方法。
{: tip}

</br>
</br>

## 使用 {{site.data.keyword.appid_short_notm}} API
{: #remote-validation}

可以使用 {{site.data.keyword.appid_short_notm}} 通过自省来验证令牌。
{: shortdesc}

1. 向 [/introspect](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token) API 端点发送 POST 请求以验证令牌。请求必须提供令牌以及包含客户端标识和私钥的基本授权头。

  示例请求：

    ```
    POST /oauth/v4/{tenant_id}/introspect HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. 服务器会检查令牌的到期时间和签名，并返回一个 JSON 对象，指示令牌是处于活动状态还是不活动状态。

  示例响应：

    ```
    {
      "active": true
    }
    ```
    {: screen}


## 手动验证令牌
{: #local-validation}

您可以在本地通过解析令牌，验证令牌签名和验证存储在令牌中的声明来验证令牌。
{: shortdesc}


1. 解析令牌。[JSON Web 令牌 (JWT)](https://tools.ietf.org/html/rfc7519) 是安全传递信息的标准方法。它包含三个主要部分：头、有效内容和签名。这些是 base64URL 编码的令牌并以点 (.) 分隔. 可以使用任何可用的 base64URL 解码器来解析令牌。或者，可以使用任一[列出的库](https://jwt.io/#libraries-io)来解析令牌。

  已编码的令牌示例：

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  已解码的头示例：

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  已解码的有效内容：

    ```
    {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. 调用 [/publickeys 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys)以检索公用密钥。返回的公用密钥的格式会设置为 [JSON Web 密钥 (JWK)](https://tools.ietf.org/html/rfc7517)。

  示例请求：

    ```
    GET /oauth/v4/{tenant_id}/publickeys HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Cache-Control: no-cache
    ```
    {: screen}

3. 将密钥存储在应用程序高速缓存中以供未来使用。存储密钥会加快进程，并可在发出其他调用时防止网络延迟。

4. 导入公用密钥参数。

  示例响应：

    ```
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 公用密钥参数</th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>定义所使用的算法。</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>定义密钥的用途。</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>定义密钥的唯一标识。</td>
      </tr>
      <tr>
        <td>其他</td>
        <td>可能还有特定于算法的其他剩余参数也必须导入。</td>
      </tr>
    </tbody>
  </table>

5. 验证令牌的签名。令牌头包含用于对令牌签名的算法以及匹配的公用密钥的密钥标识或 `kid` 声明。公用密钥不会频繁更改，所以可以在应用程序中高速缓存公用密钥，有时也可以对公用密钥进行刷新。如果高速缓存的密钥缺少 `kid` 声明，那么可以在本地验证令牌。

  1. 使应用程序验证入局令牌头的内容是否与公用密钥的参数相匹配。
  2. 具体检查是否使用了相同的算法，以及公用密钥高速缓存是否包含具有相关密钥标识的密钥。
  3. 确保散列值与公用密钥的 PEM 格式的签名相同。可以通过组合并散列化令牌的有效内容头来获取散列值。由于此过程可能很复杂，难以手动实现，因此使用其中一个[列出的库](https://jwt.io/)来验证签名可能会很有用。

6. 验证存储在令牌中的声明。要验证未来检查，可以使用[此列表](https://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation)。
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 必须验证的声明</th>
    </thead>
    <tbody>
      <tr>
        <td><code>iss</code></td>
        <td>颁发者必须与 {{site.data.keyword.appid_short_notm}} OAuth 服务器相同。</td>
      </tr>
      <tr>
        <td><code>exp</code></td>
        <td>当前时间必须早于到期时间。</td>
      </tr>
      <tr>
        <td><code>aud</code></td>
        <td>受众必须包含应用程序的客户端标识。</td>
      </tr>
      <tr>
        <td><code>tenant</code></td>
        <td>租户必须包含应用程序的租户标识。</td>
      </tr>
      <tr>
        <td><code>scope</code></td>
        <td>授予用户的许可权的作用域。这是特定于访问令牌的。</td>
      </tr>
    </tbody>
  </table>
