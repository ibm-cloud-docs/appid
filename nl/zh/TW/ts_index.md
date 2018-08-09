---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# 疑難排解
{: #troubleshooting}

如果您在使用 {{site.data.keyword.appid_full}} 時發生問題，請考慮使用這些技術來進行疑難排解及取得協助。
{: shortdesc}


## 取得協助及支援
{: #gettinghelp}

您可以搜尋資訊或透過討論區提問來取得協助。您也可以開立支援問題單。當您使用討論區提問時，請標記您的問題，以便 {{site.data.keyword.Bluemix_notm}} 開發團隊能看到它。
  * 如果您有 {{site.data.keyword.appid_short_notm}} 的相關技術問題，請將問題張貼在 <a href="http://stackoverflow.com/search?q=ibm+" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，並使用 "ibm-appid" 來標記問題。
  * 若為服務及開始使用指示的相關問題，請使用 <a href="https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=appid%20[bluemix]" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 討論區。請包括 `appid` 標籤。

如需取得支援的相關資訊，請參閱[如何取得所需的支援？](/docs/get-support/howtogetsupport.html#getting-customer-support)。

</br>

## 在登入之後沒有重新導向至應用程式
{: #signin-fail}

{: tsSymptoms}
使用者透過身分提供者的登入頁面來登入應用程式，但是沒有發生任何情況或登入失敗。

{: tsCauses}
登入可能由於下列原因而失敗：

* 您的重新導向 URL 未適當地新增至[白名單](identity-providers.html#redirect)。
* 使用者未獲授權。
* 使用者嘗試使用錯誤的認證登入。

{: tsResolve}
對於發生的重新導向，請：

* 驗證您的重新導向 URL 正確無誤。它必須完全一樣，重新導向才能運作。
* 確定您的使用者使用正確的認證登入
* 確認它們是在身分提供者使用者設定中配置的。

</br>

## 使用 SAML 時的常見問題
{: #common-saml}

檢閱下表，以取得使用 SAML 時最常發生之問題的說明及解決方案。

<table summary="應該由左至右讀取每個表格列，其中叢集狀態位於直欄 1，而說明位於直欄 2。">
  <thead>
    <th>訊息</th>
    <th>說明</th>
  </thead>
  <tbody>
    <tr>
      <td><code>無法剖析主張 XML。</code></td>
      <td>來自 SAML 的回應形態異常。</td>
    </tr>
    <tr>
      <td><code>屬性無效，沒有名稱。請聯絡身分提供者管理者。</code></td>
      <td>有一個 <code><saml:Attribute> 沒有定義的值。請聯絡身分提供者管理者。</code></td>
    </tr>
    <tr>
      <td><code>SAML 回應內文必須包含 RelayState。</code></td>
      <td>RelayState 參數未內含在 SAML 回應內文中。{{site.data.keyword.appid_short_notm}} 提供參數給身分提供者作為要求的一部分，而且必須在回應中傳回確切的參數。如果已修改參數，則您可以聯絡身分提供者管理者。</td>
    </tr>
    <tr>
      <td><code>「SAML 配置」必須具有 IdP 的憑證、entityID 及 signInUrl。</code></td>
      <td>未正確配置 SAML 身分提供者。請驗證您的配置。如需相關說明，請參閱<a href="enterprise.html#configuring-saml" target="_blank">配置應用程式以使用外部 SAML 身分提供者。</a></td>
    </tr>
    <tr>
      <td><code>在驗證主張時發生錯誤。「SAML 主張」簽章檢查失敗！憑證 .. 可能無效。</code></td>
      <td>主張中必須內含有效的簽章及摘要。必須使用與 SAML 配置中提供的憑證相關聯的私密金鑰來建立簽章；可以使用次要或主要。<em>附註</em>：{{site.data.keyword.appid_short_notm}} 不支援加密主張。如果您的身分提供者對您的 SAML 主張執行此動作，請停用加密。</td>
    </tr>
  </tbody>
</table>


## 使用 SAML 時，沒有重新導向至身分提供者
{: #saml-redirect}

{: tsSymptoms}
使用者嘗試登入您的應用程式，但在提示時未顯示登入頁面。

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

如果這些解決方案都沒有作用，則可能是您發生連線問題。

</br>

## 使用 SAML 時，屬性顯示錯誤值
{: #saml-attribute}

{: tsSymptoms}
屬性值存在於使用者設定檔中，但未連接至正確屬性。

{: tsCauses}
未正確對映「使用者設定檔屬性」。

{: tsResolve}
對映身分提供者設定中的屬性。{{site.data.keyword.appid_short_notm}} 預期下列屬性：
* `name `
* `email`
* `locale`
* `picture`
