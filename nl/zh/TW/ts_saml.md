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

# 身分提供者配置
{: #troubleshooting-idp}

如果您在配置身分提供者使用 {{site.data.keyword.appid_full}} 時發生問題，請考慮使用這些技術來進行疑難排解並取得協助。
{: shortdesc}


## 使用者未重新導向至身分提供者
{: #ts-saml-redirect}

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


## 一般 SAML 問題
{: #ts-common-saml}

檢閱下表，以取得使用 SAML 時最常發生之問題的說明及解決方案。

<table summary="每個表格列都應該從左到右閱讀，第一欄為叢集狀態，第二欄則為說明。">
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
      <td>有一個 <code>&lt;saml:Attribute&gt;</code> 沒有定義的值。請聯絡身分提供者管理者。</td>
    </tr>
    <tr>
      <td><code>SAML 回應內文必須包含 RelayState 參數。</code></td>
      <td>此參數未內含在 SAML 回應內文中。{{site.data.keyword.appid_short_notm}} 提供參數給身分提供者作為要求的一部分，而且必須在回應中傳回確切的參數。如果已修改參數，則您可以聯絡身分提供者管理者。</td>
    </tr>
    <tr>
      <td><code>「SAML 配置」必須具有 IdP 的憑證、entityID 及 signInUrl。</code></td>
      <td>未<a href="/docs/services/appid?topic=appid-enterprise#enterprise" target="_blank">正確配置</a> SAML 身分提供者。請驗證您的配置。</td>
    </tr>
    <tr>
      <td><code>在驗證主張時發生錯誤。「SAML 主張」簽章檢查失敗！憑證 .. 可能無效。</code></td>
      <td>主張中必須內含有效的簽章及摘要。必須使用與 SAML 配置中提供的憑證相關聯的私密金鑰來建立簽章，可以使用次要或主要。<strong>附註</strong>：{{site.data.keyword.appid_short_notm}} 不支援加密主張。如果您的身分提供者加密您的 SAML 主張，請停用加密。</td>
    </tr>
  </tbody>
</table>



## SAML 回應驗證錯誤
{: #ts-saml-response}

{{site.data.keyword.appid_short_notm}} 會強制主張的下列有效性需求。除非另有指定，否則所有屬性都是必要的 SAML 回應 XML 節點。
{: shortdesc}


<table summary="應該由左至右讀取每個表格列，其中回應元素位於直欄 1，而說明位於直欄 2。">
  <thead>
    <th>回應元素</th>
    <th>說明</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>回應元素必須內含在「回應 XML」中。</td>
    </tr>
    <tr>
      <td><code>SAML 版本</code></td>
      <td>{{site.data.keyword.appid_short_notm}} 僅接受 <code>SAML 2.0 版</code>。</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>{{site.data.keyword.appid_short_notm}} 會驗證主張中所傳回的回應元素 <code>InResponseTo</code> 符合 SAML 要求中的已儲存要求 ID。</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>主張中指定的發證者必須符合 {{site.data.keyword.appid_short_notm}} 身分提供者配置中指定的發證者。</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>主張中必須內含有效的簽章及摘要。必須使用與 SAML 配置中提供的憑證相關聯的私密金鑰來建立簽章。使用指定的 <code>CanonicalizationMethod</code> 及 <code>Transforms</code> 來驗證摘要。<strong>附註</strong>：{{site.data.keyword.appid_short_notm}} 未驗證憑證有效期限。如需管理憑證的協助，請試用[憑證管理程式](/docs/services/certificate-manager?topic=certificate-manager-getting-started#getting-started)。</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>主張的主旨或 <code>name_id</code> 必須是使用者的「聯合電子郵件」。</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>主張特定屬性與特定已鑑別使用者相關聯。</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>選用</strong>：在主張中包括條件陳述式時，必須同時包含有效的時間戳記。{{site.data.keyword.appid_short_notm}} 允許主張中指定的有效性期間。若要驗證，服務會尋找必須定義且有效的 <code>NotBefore</code> 及 <code>NotOnOrAfter</code> 限制項。</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}} 不支援加密主張。如果您的身分提供者設為加密主張，請予以停用。主張必須採用未加密格式。
{: tip}
