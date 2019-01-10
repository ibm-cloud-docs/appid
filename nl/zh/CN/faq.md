---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:faq: data-hd-content-type='faq'}


# 常见问题
{: #faq}

此常见问题提供了对 {{site.data.keyword.appid_full}} 服务相关常见问题的解答。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} 如何计算定价？
{: #pricing}
{: faq}

通过 {{site.data.keyword.appid_short_notm}}，使用更多的资源反而花费变少。
{: shortdesc}

累进层套餐由三部分组成：认证事件数、常规和高级安全性以及授权用户数。每月根据这两部分的汇总进行收取费用。总价是每级使用量的累计费用，每级使用量的费用等于使用量乘以该层的单价。

每月前 1000 个认证事件和前 1000 个授权用户免费，但任何高级安全事件除外。任何高级安全事件都会产生额外的费用。

### 认证事件

颁发新访问令牌（常规或匿名）时会发生认证事件。可以使颁发令牌以响应由用户发起或由应用程序代表用户发起的登录请求。缺省情况下，访问令牌的有效期为一小时，匿名令牌的有效期为 30 天。令牌到期后，必须创建新令牌才能访问受保护资源。您可以在服务仪表板中**登录到期时间**页面上更新 {{site.data.keyword.appid_short_notm}} 令牌的到期时间。

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
    <td>[Cloud Directory 的 MFA](mfa.html) 要求用户除了输入其电子邮件和密码外，还要输入发送到其电子邮件的一次性密码，以此来确认用户身份。</td>
  </tr>
  <tr>
    <td>密码策略管理</td>
    <td>作为帐户所有者，您可以通过配置用户密码必须符合的一组规则来对 Cloud Directory 强制实施更安全的密码。示例包括：锁定前尝试登录的次数、到期时间、密码更新最短间隔时间或密码不能重复使用的次数。有关选项和设置信息的完整列表，请参阅[高级密码管理](cloud-directory.html#advanced-password)。</td>
  </tr>
</table>

缺省情况下，高级安全功能已禁用。如果开启多因子认证或密码策略管理，那么会产生额外的费用。如果禁用所有高级功能，那么帐户会还原为更低成本的策略。例如，如果您已获取了 10,000 个访问令牌，然后开启了 MFA 和密码策略管理，并且再获取了 10,000 个访问令牌，您将为 20,000 个认证事件和 10,000 个高级安全事件付费。

这些功能仅可用于累进层价格套餐上的实例以及在 2018 年 3 月 15 日之后创建的实例。
{: note}

### 授权用户

授权用户是（直接或间接）登录到服务的唯一用户，包括匿名用户。每当一个新用户（包括匿名用户）登录到应用程序时，都会按一个授权用户进行收费。例如，如果用户使用 Facebook 登录，而稍后使用 Google 登录，那么将视为两位单独的授权用户。

有关 {{site.data.keyword.appid_short_notm}} 的最新定价信息，请参阅[定价计算器](https://console.cloud.ibm.com/pricing/configure/service/AdvancedMobileAccess-d6aece47-d840-45b0-8ab9-ad15354deeea)。
{: important}

</br>


## 为什么需要将重定向 URL 列入白名单？
{: #redirect}
{: faq}

重定向 URL 是应用程序的回调端点。为防止钓鱼攻击，{{site.data.keyword.appid_short_notm}} 会根据重定向 URL 的白名单来验证 URL。发生钓鱼攻击时，攻击者可能会获取您的用户令牌的访问权。

要将 URL 添加到白名单，请执行以下操作：

1. 浏览到**身份提供者 > 管理**。
2. 在**添加 Web 重定向 URL** 字段中，输入 URL 并单击 **+**。

不要在 URL 中包含任何查询参数。在验证过程中将忽略这些参数。URL 示例：`http://host:[port]/path`
{: tip}

</br>

## 加密在 {{site.data.keyword.appid_short_notm}} 中如何工作？
{: #encryption}
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
      <td>服务使用 <code>javax.crypto</code> Java 库，但是从未公开加密功能。</td>
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

</br>

## {{site.data.keyword.appid_short_notm}} 想要的 SAML 断言是什么样子的？
{: #saml-example}
{: faq}

该服务希望获取类似于以下示例的 SAML 断言。

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}

</br>

## SAML 签名支持哪种类型的算法
{: #saml-signatures}
{: faq}

您可以使用以下任意算法来处理 XML 数字签名。

<table>
  <tr>
    <th> 算法类型</th>
    <th> 算法选项</th>
  </tr>
  <tr>
    <td>带有和不带有注释的规范和变换算法</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">规范 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">带有和不带有注释的排除规范 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">包络签名变换 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li></ul></td>
  </tr>
  <tr>
    <td>散列算法</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">SHA1 摘要 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">SHA256 摘要 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">SHA512 摘要 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li></ul></td>
  </tr>
  <tr>
    <td>签名算法</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></li></ul></td>
  </tr>
</table>

有关使用 SAML 身份提供者的更多信息，请参阅[配置企业身份提供者](enterprise.html)。
