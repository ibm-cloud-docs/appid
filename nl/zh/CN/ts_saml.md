---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

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

# 故障诊断：SAML
{: #troubleshooting-idp}

在配置 SAML 以使用 {{site.data.keyword.appid_full}} 时，如果遇到问题，请考虑使用下列方法进行故障诊断和获取帮助。
{: shortdesc}


## 常见配置问题
{: #ts-common-saml}

SAML 框架支持多个概要文件、流程和配置，这意味着对身份提供者配置进行正确配置至关重要。请查看以下主题，以帮助解决使用 SAML 时可能会遇到的一些常见问题。
{: shortdesc}


有关在此页面上未显示的身份提供者生成的特定错误代码和消息，请搜索 [SAML 规范](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html)以获取详细说明，这会非常有用。如果找不到要查找的内容，可以联系身份提供者管理员以获取更多信息。
{: note}



### 缺少 `RelayState` 参数
{: #ts-saml-relaystate}

**问题描述**

认证响应中缺少 `RelayState` 参数。


**问题原因**

{{site.data.keyword.appid_short_notm}} 会在认证请求中发送名为 `RelayState` 的不透明参数。如果未在响应中看到此参数，说明可能未将身份提供者正确配置为返回此参数。`RelayState` 采用以下格式。

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

**解决方法**

验证 SAML 提供者是否已配置为将 `RelayState` 参数不作任何修改就返回到 {{site.data.keyword.appid_short_notm}}。


### 缺少 NameID 字段或此字段不正确
{: #ts-saml-nameid}

**问题描述**

发送认证请求时，收到有关 `NameID` 的错误。

**问题原因**

{{site.data.keyword.appid_short_notm}} 作为服务提供者，定义了服务和身份提供者标识用户的方式。使用 {{site.data.keyword.appid_short_notm}} 时，用户在 `NameID` 字段的 `NameID` 认证请求中进行标识，如以下示例中所示。

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**解决方法**

要解决此问题，请确保身份提供者 `NameID` 的格式设置为电子邮件地址。验证身份提供者注册表中的所有用户是否都具有有效的电子邮件地址格式。然后，验证 `NameID` 字段是否已正确定义，以便始终返回有效的电子邮件 - 即使注册表中的用户有多个电子邮件。



### 响应签名失败
{: #ts-saml-response-sign-fail}

**问题描述**

发送认证请求时，收到以下错误消息：

```
无法验证 SAML 断言签名。请确保 {{site.data.keyword.appid_short_notm}} 配置为使用 SAML 提供者的签名证书。
```
{: screen}

**问题原因**

{{site.data.keyword.appid_short_notm}} 需要响应中的所有 SAML 断言都已签名。如果该服务在响应中找不到签名或无法验证签名，那么会返回错误。

**解决方法**

要解决此问题，请确保：

* 已从身份提供者元数据 XML 文件中抽取签名证书。确保将密钥用于 `<KeyDescriptor use="signing">`。
* 已将响应签名算法设置为 XXX。 





### 解密响应失败
{: #ts-saml-decrypt-fail}

**问题描述**

响应认证请求时，收到下列其中一条错误消息。

错误消息 1：

```
意外收到加密的断言。请在 {{site.data.keyword.appid_short_notm}} SAML 配置中启用响应加密。
```
{: screen}

错误消息 2： 

```
无法解密 SAML 断言。确保 SAML 提供者配置为使用 {{site.data.keyword.appid_short_notm}} 加密。
```
{: screen}


**问题原因**

如果身份提供者配置为使用加密，那么 {{site.data.keyword.appid_short_notm}} 必须配置为对 SAML 认证请求 (AuthnRequest) 签名。然后，身份提供者必须配置为需要相应的配置。出于下列其中一个原因，可能会收到这些错误：

- {{site.data.keyword.appid_short_notm}} 未配置为需要加密身份提供者 SAML 响应。
- {{site.data.keyword.appid_short_notm}} 无法正确解密断言。


**解决方法**

如果收到错误消息 1，请验证 SAML 配置是否设置为需要加密响应。缺省情况下，{{site.data.keyword.appid_short_notm}} 不需要加密响应。要配置加密，请使用 [API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) 将 `encryptResponse` 参数设置为 **true**。

如果收到错误消息 2，请确保证书正确。可以从 {{site.data.keyword.appid_short_notm}} 元数据 XML 文件获取签名证书。确保将密钥用于 `<KeyDescriptor use="signing">`。验证身份提供者是否配置为使用 `` 作为签名的签名算法。 


### 响应者错误代码
{: #ts-saml-responder}

**问题描述**

发送认证请求时，收到以下通用错误消息：

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**问题原因**

虽然 {{site.data.keyword.appid_short_notm}} 发送的是初始认证请求，但身份提供者必须执行用户认证并返回响应。有多种原因可能导致身份提供者抛出此错误消息。

如果身份提供者发生以下情况，那么您可能会看到此消息： 

* 找不到用户名或无法验证用户名。
* 不支持认证请求 (`AuthnRequest`) 中定义的 `NameID` 格式。
* 不支持认证上下文。
* 需要认证请求进行签名，或者在签名中使用特定算法。

**解决方法**

要解决此问题，请验证配置和用户名。验证是否定义了正确的认证上下文和变量。检查以确定请求是否需要以特定方式进行签名。




### 不支持的认证请求
{: #ts-saml-unsupported-request}

**问题描述**

您收到有关不支持认证请求的消息。

**问题原因**

{{site.data.keyword.appid_short_notm}} 生成认证请求时，可以使用认证上下文来请求认证和 SAML 断言的质量。

**解决方法**

要解决此问题，可以更新认证上下文。缺省情况下，{{site.data.keyword.appid_short_notm}} 使用认证类 `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` 和比较 `exact`。可以使用 API 来更新上下文参数以适合您的用例。




### SAML 请求签名失败
{: #ts-saml-request-sign-fail}

**问题描述**

您收到错误，声明无法验证认证请求。

**问题原因**

{{site.data.keyword.appid_short_notm}} 可以配置为对 SAML 认证请求 (`AuthNRequest`) 签名，但身份提供者必须配置为需要相应的配置。

**解决方法**

要解决此问题，请执行以下操作：

* 通过使用[设置 SAML IdP API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) 将 `signRequest` 参数设置为 `true`，验证 {{site.data.keyword.cloud_notm}} 是否配置为对认证请求签名。您可以通过查看请求 URL 来检查以确定是否对认证请求进行了签名。签名会作为查询参数包含在 URL 中。例如：`https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* 验证身份提供者是否配置为使用正确的证书。要获取签名证书，请检查从 {{site.data.keyword.cloud_notm}}“仪表板”下载的 {{site.data.keyword.cloud_notm}} 元数据 XML 文件。确保将密钥用于 `<KeyDescriptor use="signing">`。

* 验证身份提供者是否配置为使用 `` 作为签名算法。



## 调试连接
{: #ts-saml-debug-connection}

配置正确，但仍有错误？请查看以下用于调试 SAML 连接的一些有用提示。
{: shortdesc}


### 如何捕获 SAML 认证请求和响应？
{: #ts-saml-capture}

对于 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) 和 [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) 等浏览器的插件，有多种选项可用于捕获 SAML 请求和响应。不想使用插件？没问题。Atlassian 提供了有关更为[手动的抽取方法](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html)的指示信息。


### 我看不懂消息！如何对其进行解码？
{: #ts-saml-decode-messages}

如果使用 SAML 调试工具后仍然发生问题，请尝试使用 [SAML 开发者工具](https://www.samltool.com/online_tools.php)来获取有关对消息解码的更多帮助。请牢记！根据拦截 SAML 消息的位置，可能会对请求进行 [URL 编码](https://www.samltool.com/online_tools.php)、[Base64 编码和压缩](https://www.samltool.com/decode.php)或[加密](https://www.samltool.com/decrypt.php)。

不要使用联机工具来解密 SAML 消息（如 SAML 响应）。工具需要访问加密专用密钥才能解密信息。该密钥应该保密并通过访问控制进行保护。本部分中提到的解密工具应该仅用于调试目的。
{: important}

