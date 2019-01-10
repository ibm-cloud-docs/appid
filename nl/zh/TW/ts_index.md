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

# 一般疑難排解
{: #troubleshooting}

如果您在使用 {{site.data.keyword.appid_full}} 時發生問題，請考慮使用這些技術來進行疑難排解及取得協助。
{: shortdesc}

## 取得協助及支援
{: #gettinghelp}

您可以搜尋資訊或透過討論區提問來取得協助。您也可以開立支援問題單。當您使用討論區提問時，請標記您的問題，以便 {{site.data.keyword.Bluemix_notm}} 開發團隊能看到它。
  * 如果您有 {{site.data.keyword.appid_short_notm}} 的相關技術問題，請將問題張貼在 <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，並使用 "ibm-appid" 來標記問題。
  * 若為服務及開始使用指示的相關問題，請使用 <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 討論區。請包括 `appid` 標籤。

如需取得支援的相關資訊，請參閱[如何取得所需的支援](/docs/get-support/howtogetsupport.html#getting-customer-support)。

</br>

## 已拒絕自訂 URL
{: #ts-custom-url}


{: tsSymptoms}
當您輸入使用自訂「URL 架構」的 Web 重新導向 URL 時，{{site.data.keyword.appid_short_notm}} 主控台會拒絕它。

{: tsCauses}
您的 URL 可能會由於下列原因而遭到拒絕：

* URL 未遵循 `http` 或 `https` 架構。
* URL 的結尾為 `://`
* URL 中有拼字錯誤

基於安全用途，而有所限制。

{: tsResolve}
若要解決問題，請驗證 URL 正確。如果 URL 不符合需求，您可以在應用程式中建立 HTTPS 端點，以將接收的授權碼重新導向至自訂 URL。在 {{site.data.keyword.appid_short_notm}} 主控台中，將已建立的端點指定為重新導向 URL。

</br>
