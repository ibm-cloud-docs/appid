---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

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

# 疑難排解：一般
{: #troubleshooting}

如果您在使用 {{site.data.keyword.appid_full}} 時發生問題，請考慮使用這些技術來進行疑難排解及取得協助。
{: shortdesc}

## 取得協助及支援
{: #ts-gettinghelp}

您可以搜尋資訊或透過討論區提問來取得協助。您也可以開立支援問題單。當您使用討論區提問時，請標記您的問題，以便 {{site.data.keyword.cloud_notm}} 開發團隊能看到它。
  * 如果您有 {{site.data.keyword.appid_short_notm}} 的相關技術問題，請將問題張貼在 <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，並使用 "ibm-appid" 來標記問題。
  * 若為服務及開始使用指示的相關問題，請使用 <a href="https://developer.ibm.com/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 討論區。請包括 `appid` 標籤。

如需取得支援的相關資訊，請參閱[如何取得所需的支援](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support)。


## 使用者在登入之後未重新導向至應用程式
{: #ts-signin-fail}

{: tsSymptoms}
使用者透過身分提供者的登入頁面來登入應用程式，但是未執行任何動作，或者登入失敗。

{: tsCauses}
登入可能由於下列原因而失敗：

* 您的重新導向 URL 未適當地新增至[白名單](/docs/services/appid?topic=appid-faq#faq-redirect)。
* 使用者未獲授權。
* 使用者嘗試使用錯誤的認證登入。

{: tsResolve}
對於發生的重新導向，請：

* 驗證您的重新導向 URL 正確無誤。它必須完全一樣，重新導向才能運作。
* 確定您的使用者使用正確的認證登入
* 確認它們是在身分提供者使用者設定中配置的。



## 自訂 URI 遭到拒絕
{: #ts-custom-uri}

{: tsSymptoms}
當您輸入使用自訂「URL 架構」的 Web 重新導向 URL 時，它被 {{site.data.keyword.appid_short_notm}} 主控台拒絕。

{: tsCauses}
您的 URL 可能是因為下列原因而被拒絕：

* URL 未遵循 `http` 或 `https` 架構
* URL 的結尾為 `://`
* URL 中有拼字錯誤

基於安全用途，而有所限制。

{: tsResolve}
若要解決問題，請驗證 URL 正確無誤。如果 URL 不符合需求，您可以在應用程式中建立 HTTPS 端點，以將接收的授權碼重新導向至自訂 URL。在 {{site.data.keyword.appid_short_notm}} 主控台中，將已建立的端點指定為重新導向 URL。如需重新導向 URI 的相關資訊，請參閱[新增重新導向 URI](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)

## 使用者未重新導向至身分提供者
{: #ts-redirect}

{: tsSymptoms}
使用者嘗試登入您的應用程式，但系統提示時未顯示登入頁面。

{: tsCauses}
身分提供者可能由於數個原因而失敗：

* 配置的重新導向 URL 不正確。
* 身分提供者無法辨識鑑別要求。
* 身分提供者預期 HTTP-POST 連結。
* 身分提供者預期已簽署的 authnRequest。

{: tsResolve}
您可以嘗試下列部分解決方案：

* 更新您的登入 URL。此 URL 會當作 authnRequest 的一部分傳送，而且必須完全一樣。
* 確定已在您的身分提供者設定中正確設定您的 {{site.data.keyword.appid_short_notm}} meta 資料。
* 將您的身分提供者配置為接受 HTTP-Redirect 中的 authnRequest。
* {{site.data.keyword.appid_short_notm}} 不支援簽署 authnRequest。

如果解決方案未作用，則可能是您發生連線問題。
{: tip}


## 屬性顯示錯誤值
{: #ts-saml-attribute}

{: tsSymptoms}
屬性值存在於使用者設定檔中，但未與正確的屬性相關聯。

{: tsCauses}
未正確對映使用者設定檔屬性。

{: tsResolve}
對映身分提供者設定中的屬性。{{site.data.keyword.appid_short_notm}} 預期下列屬性：
* `name `
* `email`
* `locale`
* `picture`



## 錯誤：要求太多
{: #ts-requests}

{: tsSymptoms}
您嘗試檢視應用程式的首頁，但收到下列錯誤：

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
如果您僅以一個虛擬使用者來執行自動化測試，可能會收到「要求太多」錯誤。每一位使用者在 1 分鐘的時間跨距內僅限於五次登入嘗試。登入嘗試受到限制，是為了以避免強制入侵 DDOS 及其他類型的類似攻擊。

{: tsResolve}
若要解決此問題，您可以在執行測試時使用多個虛擬使用者。
</br>
