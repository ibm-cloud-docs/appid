---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# 常见问题

此常见问题提供了对 {{site.data.keyword.appid_full}} 服务相关常见问题的解答。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} 如何计算定价？
{: #pricing}

通过 {{site.data.keyword.appid_short_notm}}，使用更多的资源反而花费变少。
{: shortdesc}

累进层计划由两部分组成：认证事件数和授权用户数。每月根据这两部分的汇总进行收取费用。总价是每级使用量的累计费用，每级使用量的费用等于使用量乘以该层的单价。

### 认证事件

颁发新访问令牌（常规或匿名）时会发生认证事件。对于已识别用户，缺省情况下每个新访问令牌的有效期为 1 小时（通过实际用户认证或通过刷新令牌）。缺省情况下，匿名令牌的有效期为 1 个月。令牌到期后，必须创建新令牌才能访问受保护资源。您可以在 {{site.data.keyword.appid_short_notm}} 仪表板中**登录到期时间**页面上更新 {{site.data.keyword.appid_short_notm}} 令牌的到期时间。

在移动应用程序中使用 {{site.data.keyword.appid_short_notm}} 时，令牌存储在 key-store 或 key-chain 中并会添加到未来的每一个请求中。使用 App ID Android 或 iOS SDK 可访问这些令牌。在 Web 应用程序中使用 {{site.data.keyword.appid_short_notm}} 时，建议在应用程序会话 cookie 中存储令牌。


### 授权用户

授权用户是使用服务直接或间接登录的唯一用户。每次当新用户（包括匿名用户）从各个身份提供者登录时，将各按一个授权用户进行收费。例如，如果用户使用 Facebook 登录，而稍后使用 Google 登录，那么将视为两位单独的授权用户。

有关累进层定价的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 定价文档](/docs/billing-usage/how_charged.html#services)。

</br>


## 加密在 {{site.data.keyword.appid_short_notm}} 中如何工作？
{: #encryption}

请查看下表以获取有关加密的常见问题的答案。

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>为什么使用加密？</td>
      <td>该服务加密静态的客户数据。</td>
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
      <td>密钥是生成的，然后使用特定于每个区域的主密钥加密后存储在本地。主密钥存储在 {{site.data.keyword.keymanagementserviceshort}} 中。</td>
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
