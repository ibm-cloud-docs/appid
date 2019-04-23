---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# 身份提供者配置
{: #troubleshooting-idp}

在配置身份提供者以使用 {{site.data.keyword.appid_full}} 时，如果遇到问题，请考虑使用下列方法进行故障诊断和获取帮助。
{: shortdesc}


## 用户没有重定向到身份提供者
{: #ts-saml-redirect}

{: tsSymptoms}
用户尝试登录到应用程序，但提示时不显示登录页面。

{: tsCauses}
身份提供者可能由于多种原因而失败：

* 您配置的重定向 URL 不正确。
* 身份提供者无法识别认证请求。
* 身份提供者需要 HTTP-POST 绑定。
* 身份提供者需要已签名的认证请求。

{: tsResolve}
您可以尝试以下某些解决方案：

* 更新登录 URL。此 URL 作为认证请求的一部分发送，并且必须是完全一致。
* 请确保在身份提供者设置中正确设置了 {{site.data.keyword.appid_short_notm}} 元数据。
* 将身份提供者配置为接受 HTTP 重定向中的认证请求。
* {{site.data.keyword.appid_short_notm}} 不支持签名的认证请求。

如果解决方案都不起作用，那么可能是您的连接存在问题。
{: tip}


## 常见 SAML 问题
{: #ts-common-saml}

请查看下表以获取使用 SAML 时遇到的最常见问题的说明和解决方法。

<table summary="从左向右阅读每一个表格，集群状态在第 1 列，描述在第 2 列。">
  <thead>
    <th>消息</th>
    <th>描述</th>
  </thead>
  <tbody>
    <tr>
      <td><code>无法解析断言 XML。</code></td>
      <td>来自 SAML 的响应格式不正确。</td>
    </tr>
    <tr>
      <td><code>属性无效，没有名称。请与身份提供者管理员联系。</code></td>
      <td>有一个 <code>&lt;saml:Attribute&gt;</code> 没有定义值。请与身份提供者管理员联系。</td>
    </tr>
    <tr>
      <td><code>SAML 响应主体必须包含 RelayState 参数。</code></td>
      <td>SAML 响应主体中不包含该参数。{{site.data.keyword.appid_short_notm}} 将参数作为请求的一部分向身份提供者提供，响应中必须返回具体的参数。如果已修改该参数，那么可以与身份提供者管理员联系。</td>
    </tr>
    <tr>
      <td><code>SAML 配置必须具有 IdP 的证书、entityID 和 signInUrl。</code></td>
      <td>未<a href="/docs/services/appid?topic=appid-enterprise#enterprise" target="_blank">正确配置</a> SAML 身份提供者。验证您的配置。</td>
    </tr>
    <tr>
      <td><code>断言验证时出错。SAML 断言签名检查失败！证书 ..可能无效。</code></td>
      <td>必须在断言中包含有效的签名和摘要。必须使用与 SAML 配置中提供的证书相关联的专用密钥来创建签名；可以使用辅助密钥或主密钥。<strong>注</strong>:{{site.data.keyword.appid_short_notm}} 不支持加密断言。如果身份提供者会加密 SAML 断言，请禁用加密。</td>
    </tr>
  </tbody>
</table>



## SAML 响应验证错误
{: #ts-saml-response}

{{site.data.keyword.appid_short_notm}} 对断言实施了以下有效性需求。除非另外指定，否则所有属性都是必需的 SAML 响应 XML 节点。
{: shortdesc}


<table summary="每个表行应从左向右阅读，其中第 1 列是响应元素，第 2 列是描述。">
  <thead>
    <th>响应元素</th>
    <th>描述</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>响应元素必须包含在响应 XML 中。</td>
    </tr>
    <tr>
      <td><code>SAML 版本</code></td>
      <td>{{site.data.keyword.appid_short_notm}} 仅接受 <code>SAML V2.0</code>。</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>{{site.data.keyword.appid_short_notm}} 验证断言中返回的响应元素 <code>InResponseTo</code> 是否与来自 SAML 请求的已保存请求标识相匹配。</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>在断言中指定的颁发者必须与 {{site.data.keyword.appid_short_notm}} 身份提供者配置中指定的颁发者相匹配。</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>必须在断言中包含有效的签名和摘要。必须使用与 SAML 配置中提供的证书相关联的专用密钥来创建签名。摘要使用指定的 <code>CanonicalizationMethod</code> 和 <code>Transforms</code> 进行验证。<strong>注</strong>：{{site.data.keyword.appid_short_notm}} 不会验证证书到期时间。要获取有关管理证书的帮助，请试用 [Certificate Manager](/docs/services/certificate-manager?topic=certificate-manager-getting-started#getting-started)。</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>断言的主题或 <code>name_id</code> 必须是用户的联合电子邮件。</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>断言某些属性与特定的已认证的用户相关联。</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>可选</strong>：断言中包含条件语句时，该条件语句还必须包含有效的时间戳记。{{site.data.keyword.appid_short_notm}} 会采用断言中指定的有效期。为了进行验证，服务会查找必须定义且有效的 <code>NotBefore</code> 和 <code>NotOnOrAfter</code> 约束。</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}} 不支持加密的断言。如果身份提供者设置为加密断言，请禁用此加密。断言必须为未加密格式。
{: tip}
