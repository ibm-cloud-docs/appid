---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

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

颁发新的 {{site.data.keyword.appid_short_notm}} 令牌时会产生认证事件。对于已识别用户，每个新令牌在 1 小时内有效。匿名令牌的有效期为 1 个月。令牌到期后，必须创建新令牌才能访问受保护资源。使用 {{site.data.keyword.appid_short_notm}} 进行移动认证时，用户令牌存储于 `key-store/key-chain` 中，并会添加到未来的每一个请求中。使用 {{site.data.keyword.appid_short_notm}} Android 或 iOS Swift SDK 可访问这些令牌。使用服务进行 Web 认证时，请在会话 cookie 中<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">存储用户令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

### 授权用户

授权用户是使用服务直接或间接登录的唯一用户。每次当新用户（包括匿名用户）从各个身份提供者登录时，将各按一个授权用户进行收费。例如，如果用户使用 Facebook 登录，而稍后使用 Google 登录，那么将视为两位单独的授权用户。

有关累进层定价的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 定价文档](/docs/billing-usage/how_charged.html#services)。

</br>

## {{site.data.keyword.appid_short_notm}} 监视哪种类型的活动？
{: #activity-monitor}

您可以跟踪在绑定到服务实例的应用程序中生成的活动。您还可以使用 {{site.data.keyword.cloudaccesstrailshort}} 服务来监视在 {{site.data.keyword.appid_short_notm}} 中生成的管理活动。

要查看应用程序生成的活动：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 帐户。
2. 从仪表板中，选择 {{site.data.keyword.appid_short_notm}} 的实例。
3. 单击**概述**选项卡。
4. 查看**活动日志**中列出的活动。

</br>
要监视管理活动：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 帐户。浏览到供应 {{site.data.keyword.appid_short_notm}} 实例的组织和空间。
2. 从目录中供应“{{site.data.keyword.cloudaccesstrailshort}}”服务的实例。确保您所在的空间就是 {{site.data.keyword.appid_short_notm}} 实例所在的空间。
3. 在“{{site.data.keyword.cloudaccesstrailshort}}”仪表板中，单击**管理**选项卡。
4. 在下拉列表中选择以下配置以搜索 {{site.data.keyword.appid_short_notm}} 生成的任何事件。
<table>
  <tr>
    <th> 字段 </th>
    <th> 配置</th>
  </tr>
  <tr>
    <td>查看日志</td>
    <td>空间日志</td>
  </tr>
  <tr>
    <td>搜索 </td>
    <td>target.name</td>
  </tr>
  <tr>
    <td>过滤器</td>
    <td>appid</td>
  </tr>
</table>
5. 单击**过滤器**。

查看[{{site.data.keyword.cloudaccesstrailshort}}文档](/docs/services/cloud-activity-tracker/index.html)以了解有关该服务工作方式的更多信息。

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
