---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

subcollection: appid

---

{:external: target="_blank" .external}
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

# 故障诊断：常规
{: #troubleshooting}

在使用 {{site.data.keyword.appid_full}} 时，如果遇到问题，可以考虑使用下列方法进行故障诊断和获取帮助。
{: shortdesc}

## 获取帮助和支持
{: #ts-gettinghelp}

您可以通过搜索信息或通过论坛提问来获取帮助。您还可以开具支持凭单。在使用论坛提问时，请标记您的问题，以便 {{site.data.keyword.cloud_notm}} 开发
团队能看到您的问题。
  * 如果有关于 {{site.data.keyword.appid_short_notm}} 的技术问题，请在 <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 上发帖提问，并使用“ibm-appid”标记您的问题。
  * 有关服务和入门指示信息的问题，请使用 <a href="https://developer.ibm.com/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 论坛。包含 `appid` 标记。

有关获取支持的更多信息，请参阅[如何获得我需要的支持](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support)。


## 用户登录后没有重定向到应用程序
{: #ts-signin-fail}

{: tsSymptoms}
用户通过身份提供者的登录页面登录到应用程序时，什么也没有发生或者登录失败。

{: tsCauses}
登录可能由于以下原因而失败：

* 您的重定向 URL 未正确添加到[白名单](/docs/services/appid?topic=appid-faq#faq-redirect)。
* 用户未经授权。
* 用户登录时尝试使用的凭证有问题。

{: tsResolve}
要进行重定向：

* 请验证您的重定向 URL 是否正确。它必须是具体的 URL，才能真正重定向。
* 请确保您的用户登录时使用的凭证正确
* 请检查这些凭证是否已在您的身份提供者用户设置中进行了配置。



## 定制 URI 被拒绝
{: #ts-custom-uri}

{: tsSymptoms}
输入使用定制 URL 方案的 Web 重定向 URL 时，{{site.data.keyword.appid_short_notm}} 控制台拒绝了该 URL。

{: tsCauses}
URL 可能由于以下原因而被拒绝：

* URL 未遵循 `http` 或 `https` 方案
* URL 以 `://` 结尾
* URL 中存在拼写错误

出于安全目的，落实了这些限制。

{: tsResolve}
要解决此问题，请验证 URL 是否正确。如果 URL 不满足需求，可以在应用程序中创建 HTTPS 端点，以将收到的授权代码重定向到定制 URL。在 {{site.data.keyword.appid_short_notm}} 控制台中将已创建的端点指定为重定向 URL。有关重定向 URI 的更多信息，请参阅[添加重定向 URI](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)

## 用户没有重定向到身份提供者
{: #ts-redirect}

{: tsSymptoms}
用户尝试登录到应用程序，但提示时不显示登录页面。

{: tsCauses}
身份提供者可能由于多种原因而失败：

* 您配置的重定向 URL 不正确。
* 身份提供者无法识别认证请求。
* 身份提供者需要 HTTP-POST 绑定。
* 身份提供者需要已签名的 AuthnRequest。

{: tsResolve}
您可以尝试以下某些解决方案：

* 更新登录 URL。此 URL 作为 AuthnRequest 的一部分发送，并且必须是完全一致的。
* 请确保在身份提供者设置中正确设置了 {{site.data.keyword.appid_short_notm}} 元数据。
* 将身份提供者配置为接受 HTTP-Redirect 中的 AuthnRequest。
* {{site.data.keyword.appid_short_notm}} 不支持对 AuthnRequest 进行签名。

如果解决方案都不起作用，那么可能是您的连接存在问题。
{: tip}


## 属性显示了错误值
{: #ts-saml-attribute}

{: tsSymptoms}
某个属性值存在于用户概要文件中，但未与正确的属性相关联。

{: tsCauses}
未正确映射用户概要文件属性。

{: tsResolve}
请在身份提供者设置中映射该属性。{{site.data.keyword.appid_short_notm}} 需要下列属性：
* `name`
* `email`
* `locale`
* `picture`



## 错误：请求太多
{: #ts-requests}

{: tsSymptoms}
您尝试查看应用程序的主页，但收到以下错误：

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
如果您是仅使用一个虚拟用户执行自动测试，那么可能会收到“请求太多”错误。每个用户的登录尝试次数限制为一分钟时间范围内五次。限制登录尝试次数可防止暴力 DDoS 和其他类型的类似攻击。

{: tsResolve}
要解决此问题，您可能需要在执行测试时使用多个虚拟用户。
</br>
