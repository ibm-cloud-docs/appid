---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# 一般故障诊断
{: #troubleshooting}

在使用 {{site.data.keyword.appid_full}} 时，如果遇到问题，可以考虑使用下列方法进行故障诊断和获取帮助。
{: shortdesc}

## 获取帮助和支持
{: #gettinghelp}

您可以通过搜索信息或通过论坛提问来获取帮助。您还可以开具支持凭单。在使用论坛提问时，请标记您的问题，以便 {{site.data.keyword.Bluemix_notm}} 开发
团队能看到您的问题。
  * 如果有关于 {{site.data.keyword.appid_short_notm}} 的技术问题，请在 <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 上发帖提问，并使用“ibm-appid”标记您的问题。
  * 有关服务和入门指示信息的问题，请使用 <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 论坛。包含 `appid` 标记。

有关获取支持的更多信息，请参阅[如何获得我需要的支持](/docs/get-support/howtogetsupport.html#getting-customer-support)。

</br>

## 定制 URL 被拒绝
{: #ts-custom-url}


{: tsSymptoms}
输入使用定制 URL 方案的 Web 重定向 URL 时，{{site.data.keyword.appid_short_notm}} 控制台拒绝了该 URL。

{: tsCauses}
URL 可能由于以下原因而被拒绝：

* URL 未遵循 `http` 或 `https` 方案
* URL 以 `://` 结尾
* URL 中存在拼写错误

出于安全目的，落实了这些限制。

{: tsResolve}
要解决此问题，请验证 URL 是否正确。如果 URL 不满足需求，可以在应用程序中创建 HTTPS 端点，以将收到的授权代码重定向到定制 URL。在 {{site.data.keyword.appid_short_notm}} 控制台中将已创建的端点指定为重定向 URL。

</br>
