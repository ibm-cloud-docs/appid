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

# 疑難排解：SAML
{: #troubleshooting-idp}

如果您在配置 SAML 使用 {{site.data.keyword.appid_full}} 時發生問題，請考慮使用這些技術來進行疑難排解並取得協助。
{: shortdesc}


## 一般配置問題
{: #ts-common-saml}

SAML 架構支援多個設定檔、流程及配置，這表示身分提供者配置務必要正確地配置。請參閱下列主題，以協助解決使用 SAML 時可能遇到的一些常見問題。
{: shortdesc}


對於來自您身分提供者且在這個頁面上看不到的特定錯誤碼和訊息，搜尋 [SAML 規格](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html)以取得詳細說明可能很有用。如果您找不到想要的內容，您可以洽詢身分提供者的管理者，以取得相關資訊。
{: note}



### 遺漏 `RelayState` 參數
{: #ts-saml-relaystate}

**發生情況**

鑑別回應遺漏 `RelayState` 參數。


**發生原因**

{{site.data.keyword.appid_short_notm}} 在鑑別要求之中會傳送一個不透明參數，稱為 `RelayState`。如果您未在回應中看到該參數，則表示您的身分提供者可能未配置成正確地傳回該參數。`RelayState` 採用下列格式。

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

**如何修正**

請驗證已配置您的 SAML 提供者，將 `RelayState` 參數傳回給 {{site.data.keyword.appid_short_notm}}，而未以任何方式修改。


### NameID 欄位遺漏或不正確
{: #ts-saml-nameid}

**發生情況**

傳送鑑別要求時，您收到有關 `NameID` 的錯誤。

**發生原因**

{{site.data.keyword.appid_short_notm}} 作為服務提供者，定義了服務及身分提供者識別使用者的方式。使用 {{site.data.keyword.appid_short_notm}}，使用者會在 `NameID` 鑑別要求的 `名稱 ID` 欄位中識別，如下列範例所示。

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**如何修正**

若要解決此問題，身分提供者 `NameID` 務必要格式化為電子郵件位址。驗證身分提供者登錄中的所有使用者，都具有有效的電子郵件位址格式。然後，驗證已適當地定義 `NameID` 欄位，以便一律會傳回有效的電子郵件－即使您登錄中的使用者有多個電子郵件也是如此。



### 回應簽章失敗
{: #ts-saml-response-sign-fail}

**發生情況**

當您傳送鑑別要求時，收到下列錯誤訊息：

```
Could not verify SAML assertion signature. Ensure {{site.data.keyword.appid_short_notm}} is configurated with your SAML provider's signing certificate.
```
{: screen}

**發生原因**

{{site.data.keyword.appid_short_notm}} 預期會簽署回應中的所有 SAML 主張。如果服務在回應中找不到簽章或無法驗證簽章，則會傳回錯誤。

**如何修正**

若要解決此問題，請確定：

* 您已從身分提供者 meta 資料 XML 檔擷取簽署憑證。請務必搭配使用金鑰和 `<KeyDescriptor use="signing">`。
* 您已將回應簽章演算法設為 XXX。 





### 無法將回應解密
{: #ts-saml-decrypt-fail}

**發生情況**

您收到下列其中一則錯誤訊息，以回應您的鑑別要求。

錯誤訊息 1：

```
Unexpectedly received an encrypted assertion. Please enable response encryption in your {{site.data.keyword.appid_short_notm}} SAML configuration.
```
{: screen}

錯誤訊息 2： 

```
Could not decrypt SAML assertion. Ensure your SAML provider is configured with the {{site.data.keyword.appid_short_notm}} encryption 
```
{: screen}


**發生原因**

如果您的身分提供者配置為要加密，則必須配置 {{site.data.keyword.appid_short_notm}} 來簽署 SAML 鑑別要求 (AuthnRequest)。然後，您的身分提供者必須配置為預期對應的配置。由於下列其中一個原因，您可能會收到這些錯誤：

- {{site.data.keyword.appid_short_notm}} 未配置為預期身分提供者 SAML 回應已加密。
- {{site.data.keyword.appid_short_notm}} 無法正確地將您的主張解密。


**如何修正**

如果收到錯誤訊息 1，請驗證 SAML 配置已設為預期回應已加密。依預設，{{site.data.keyword.appid_short_notm}} 不會預期回應要加密。若要配置加密，請使用 [API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) 將 `encryptResponse` 參數設為 **true**。

如果收到錯誤訊息 2，請確定您的憑證正確。您可以從 {{site.data.keyword.appid_short_notm}} meta 資料 XML 檔取得簽署憑證。請務必搭配使用金鑰和 `<KeyDescriptor use="signing">`。請驗證身分提供者已配置成使用 `` 作為簽章的簽署演算法。 


### 回應者錯誤碼
{: #ts-saml-responder}

**發生情況**

當您傳送鑑別要求時，收到下列一般錯誤訊息：

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**發生原因**

雖然 {{site.data.keyword.appid_short_notm}} 會傳送起始鑑別要求，但身分提供者必須執行使用者鑑別並傳回回應。有數個原因可能會導致您的身分提供者擲出此錯誤訊息。

如果您的身分提供者有下列情形，您可能會看到訊息： 

* 找不到或無法驗證使用者名稱。
* 不支援在鑑別要求 (`AuthnRequest`) 中定義的 `NameID` 格式。
* 不支援鑑別環境定義。
* 需要簽署鑑別要求，或在簽章中使用特定的演算法。

**如何修正**

若要解決此問題，請驗證您的配置及使用者名稱。請確認您已定義正確的鑑別環境定義和變數。請檢查您的要求是否需要以特定方式簽署。




### 不受支援的鑑別要求
{: #ts-saml-unsupported-request}

**發生情況**

您收到關於不受支援之鑑別要求的訊息。

**發生原因**

當 {{site.data.keyword.appid_short_notm}} 產生鑑別要求時，它可以使用鑑別環境定義來要求鑑別和 SAML 主張的品質。

**如何修正**

若要解決此問題，您可以更新鑑別環境定義。依預設，{{site.data.keyword.appid_short_notm}} 會使用鑑別類別 `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` 和比較 `exact`。您可以使用 API 更新環境定義參數，以符合您的使用案例。




### SAML 要求簽署失敗
{: #ts-saml-request-sign-fail}

**發生情況**

您收到一個錯誤，指出無法驗證鑑別要求。

**發生原因**

{{site.data.keyword.appid_short_notm}} 可以配置為簽署 SAML 鑑別要求 (`AuthnRequest`)，但您的身分提供者必須配置為預期對應的配置。

**如何修正**

若要解決此問題，請執行下列動作：

* 驗證 {{site.data.keyword.cloud_notm}} 已配置為簽署鑑別要求，方法是使用 [set SAML IdP API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)，將 `signRequest` 參數設為 `true`。您可以查看要求 URL 來檢查是否已簽署您的鑑別要求。簽章已包含為查詢參數。例如：`https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* 驗證您的身分提供者已使用正確的憑證進行配置。若要取得簽署憑證，請檢查從 {{site.data.keyword.cloud_notm}} 儀表板下載的 {{site.data.keyword.cloud_notm}} meta 資料 XML 檔案。請務必搭配使用金鑰和 `<KeyDescriptor use="signing">`。

* 驗證身分提供者已配置成使用 `` 作為簽署演算法。



## 連線除錯
{: #ts-saml-debug-connection}

配置正確但仍然有錯誤？請查看下列一些有助於 SAML 連線除錯的有用提示。
{: shortdesc}


### 如何擷取 SAML 鑑別要求及回應？
{: #ts-saml-capture}

有一些瀏覽器外掛程式的選項，例如 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) 和 [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en)，可用來擷取 SAML 要求和回應。不想使用外掛程式？沒有問題。Atlassian 提供更為[手動擷取方法](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html)的指示。


### 我不瞭解這些訊息！如何解碼？
{: #ts-saml-decode-messages}

如果您在使用 SAML 除錯工具之後仍有問題，請嘗試使用 [SAML 開發人員工具](https://www.samltool.com/online_tools.php)來進一步協助將訊息解碼。切記！視您截取 SAML 訊息的位置而定，您的要求可能是 [URL 編碼](https://www.samltool.com/online_tools.php)、[以 base 64 編碼且已壓縮](https://www.samltool.com/decode.php)，或是[已加密](https://www.samltool.com/decrypt.php)。

請勿使用線上工具來解密 SAML 訊息，例如您的 SAML 回應。工具需要存取加密私密金鑰，才能將資訊解密。金鑰應該保持私密並且控制其存取。本節所提及的解密工具，應該僅用於除錯。
{: important}

