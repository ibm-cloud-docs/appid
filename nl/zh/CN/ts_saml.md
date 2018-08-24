---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}

# 身份提供者配置
{: #troubleshooting-idp}

在配置身份提供者以使用 {{site.data.keyword.appid_full}} 时，如果遇到问题，可以考虑使用下列方法进行故障诊断和获取帮助。
{: shortdesc}


## 登录后没有重定向到应用程序
{: #signin-fail}

{: tsSymptoms}
用户通过身份提供者的登录页面登录您的应用程序时，什么也没有发生或者登录失败。

{: tsCauses}
登录可能由于以下原因而失败：

* 您的重定向 URL 未正确添加到[白名单](identity-providers.html#redirect)。
* 用户未经授权。
* 用户登录时尝试使用的凭证有问题。

{: tsResolve}
要进行重定向：

* 请验证您的重定向 URL 是否正确。它必须是具体的 URL，才能真正重定向。
* 请确保您的用户登录时使用的凭证正确
* 请检查这些凭证是否已在您的身份提供者用户设置中进行了配置。


## 使用 SAML 时的常见问题
{: #common-saml}

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
      <td><code>SAML 响应主体必须包含 RelayState。</code></td>
      <td>SAML 响应主体中不包含 RelayState 参数。{{site.data.keyword.appid_short_notm}} 将参数作为请求的一部分向身份提供者提供，响应中必须返回具体的参数。如果已修改该参数，那么可以与身份提供者管理员联系。</td>
    </tr>
    <tr>
      <td><code>SAML 配置必须具有 IdP 的证书、entityID 和 signInUrl。</code></td>
      <td>未正确配置 SAML 身份提供者。验证您的配置。要获取帮助，请参阅<a href="enterprise.html#configuring-saml" target="_blank">配置应用程序以使用外部 SAML 身份提供者。</a></td>
    </tr>
    <tr>
      <td><code>断言验证时出错。SAML 断言签名检查失败！证书 ..可能无效。</code></td>
      <td>必须在断言中包含有效的签名和摘要。必须使用与 SAML 配置中提供的证书相关联的专用密钥来创建签名；可以使用辅助密钥或主密钥。<strong>注</strong>:{{site.data.keyword.appid_short_notm}} 不支持加密断言。如果身份提供者对 SAML 断言执行此操作，请禁用加密。</td>
    </tr>
  </tbody>
</table>


## 没有重定向到身份提供者
{: #saml-redirect}

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

* 更新您的登录 URL。此 URL 作为认证请求的一部分发送，并且必须是完全一致。
* 请确保在身份提供者设置中正确设置了 {{site.data.keyword.appid_short_notm}} 元数据。
* 将身份提供者配置为接受 HTTP 重定向中的认证请求。
* {{site.data.keyword.appid_short_notm}} 不支持签名的认证请求。

如果解决方案都不起作用，那么可能是您的连接存在问题。
{: tip}

## 属性显示了错误值
{: #saml-attribute}

{: tsSymptoms}
属性值存在于用户概要文件中，但它未连接到正确的属性。

{: tsCauses}
未正确映射用户概要文件属性。

{: tsResolve}
请在身份提供者设置中映射该属性。{{site.data.keyword.appid_short_notm}} 需要下列属性：
* `name`
* `email`
* `locale`
* `picture`


