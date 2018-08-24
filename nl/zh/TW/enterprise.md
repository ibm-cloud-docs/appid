---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# 配置企業身分提供者
{: #enterprise}

如果您已有現有的使用者儲存庫及認證的方法，來向內部系統鑑別使用者，則您可以將 {{site.data.keyword.appid_full}} 服務配置為使用企業識別提供者。
{: shortdesc}

## 瞭解 SAML
{: #saml}

SAML 是一種開放式標準，可在主張使用者身分的身分提供者與取用使用者身分資訊的服務提供者之間交換鑑別及授權資料。
{: shortdesc}

運作方式？

{{site.data.keyword.appid_short_notm}} 可充當服務提供者，並對協力廠商提供者（例如 Active Directory Federation Services）起始 Single Sign On (SSO) 登入。<a href="http://saml.xml.org/saml-specifications" target="_blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 通訊協定支援不同的設定檔和連結選項。{{site.data.keyword.appid_short_notm}} 支援 Web 瀏覽器 SSO 設定檔，以及 HTTP Post 連結。

### SAML 主張及身分記號宣告

SAML 主張是包含一個以上陳述式的資訊套件。主張包含授權決策，且可能包含關於使用者的識別資訊。

當使用者利用身分提供者來登入時，該提供者會將主張傳送至 {{site.data.keyword.appid_short_notm}}。{{site.data.keyword.appid_short_notm}} 會將 SAML 主張中傳回的使用者身分資訊傳送至您的應用程式，作為 OIDC 記號宣告。SAML 屬性必須對應於要新增至身分記號的下列 OIDC 宣告 1。

可以新增下列宣告：
* `name `
* `email`
* `locale`
* `picture`

其餘未對應於任何標準名稱的 SAML 屬性元素都會被忽略。請注意，如果提供者端的其中一個或多個值變更，則只有在使用者重新登入之後才會提供新的值。

## 配置應用程式以使用外部 SAML 身分提供者
{: #configuring-saml}

您可以將 {{site.data.keyword.appid_short_notm}} 服務配置為使用「安全主張標記語言 (SAML) 」身分提供者。
{: shortdesc}

如需如何使用特定 SAML 身分提供者的步驟，請查看有關下列作業的這些部落格文章：使用 [Ping One ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/)、[Azure Active Directory ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) 或 [Active Directory Federation Service ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/) 來設定 {{site.data.keyword.appid_short_notm}}。
{: tip}

### 提供 meta 資料給您的身分提供者

若要配置您的應用程式，您需要提供資訊給 SAML 相容身分提供者。此資訊是透過 meta 資料 XML 檔案進行交換，該檔案還包含用來建立信任的配置資料。

1. 在 {{site.data.keyword.appid_short_notm}} 儀表板的**管理**標籤中，將 **SAML 2.0** 設為**開啟**。然後，按一下**編輯**以配置 SAML 設定。
2. 按一下**下載 SAML Meta 資料檔**。您的身分提供者預期來自檔案的下列資訊。
  <table>
    <tr>
      <th> 變數</th>
      <th> 說明</th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>讓身分提供者知道 {{site.data.keyword.appid_short_notm}} 已發出 SAML 要求的 ID。</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>身分提供者在順利鑑別使用者之後傳送 SAML 主張的位置。</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>身分提供者應該如何傳送 SAML 回應的指示。</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>身分提供者知道在主張主旨中需要傳送哪種 ID 格式的方式。{{site.data.keyword.appid_short_notm}} 識別使用者的方式。</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>身分提供者檢查以查看是否需要簽署主張的方式。服務會預期主張已簽署，但不支援加密主張。</td>
    </tr>
  </table>

3. 提供資料給您的身分提供者。如果您的身分提供者支援上傳 meta 資料檔，則您可以這麼做。若非如此，請手動配置內容。並非每個身分提供者都將使用相同的內容，因此，如果您未使用它們全部，也沒關係。

身分提供者之間的內容名稱可能不同。
{: tip}

### 提供 meta 資料給 {{site.data.keyword.appid_short_notm}}

您將需要從身分提供者取得資料，並提供給 {{site.data.keyword.appid_short_notm}}。

1. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的 **SAML 2.0** 標籤。在**提供來自 SAML IdP 的 meta 資料**區段中，輸入您從身分提供者取得的下列 meta 資料。
  <table>
    <tr>
      <th> 變數</th>
      <th> 說明</th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>將使用者重新導向以進行鑑別的 URL。它是由您的 SAML 身分提供者進行管理。</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>SAML 身分提供者的廣域唯一名稱。</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>SAML 身分提供者所發出的憑證。它用於簽署及驗證 SAML 主張。所有提供者都不同，但您可能可以從身分提供者下載簽署憑證。憑證必須為 <code>.pem</code> 格式。</td>
    </tr>
  </table>

2. 選用項目：提供在主要憑證上簽章驗證失敗時所使用的**次要憑證**。如果簽署金鑰保持相同，則 {{site.data.keyword.appid_short_notm}} 不會封鎖過期憑證的鑑別。

3. 更新**提供者名稱**，然後按一下**儲存**。預設名稱為 SAML。


### 測試您的配置

您可以測試「SAML 身分提供者」與 {{site.data.keyword.appid_short_notm}} 之間的配置。

1. 確定您已儲存配置。
2. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的 **SAML 2.0** 標籤，然後按一下**測試**。即會開啟新標籤。
3. 以身分提供者已鑑別的使用者身分登入。
4. 完成表單之後，系統會將您重新導向至另一個頁面。
  * 成功鑑別：{{site.data.keyword.appid_short_notm}} 與「身分提供者」之間的連線正確運作。頁面會顯示有效的[存取及身分記號](/docs/services/appid/authorization.html#key-concepts)。
  * 失敗鑑別：連線已中斷。頁面會顯示錯誤及 SAML 回應 XML 檔。
