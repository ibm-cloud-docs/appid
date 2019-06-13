---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

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

# SAML
{: #enterprise}

當您具有以 SAML 為基礎的身分提供者時，您可以將 {{site.data.keyword.appid_short_notm}} 配置為充當服務提供者，對協力廠商提供者起始單一登入 (SSO) 的登入作業。在登入流程期間，您的使用者可以輕鬆地通過鑑別，且能夠取得 {{site.data.keyword.appid_short_notm}} 安全記號，讓他們可以存取您的應用程式和受保護的 API。
{: shortdesc}

 
使用特定的 SAML 身分提供者嗎？請參閱下列部落格文章之一，以了解如何使用 [Ping One ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-ping-one)、[Azure Active Directory ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory) 或 [Active Directory Federation Service ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service) 來設定 {{site.data.keyword.appid_short_notm}}。
{: tip}


## 瞭解 SAML
{: #saml-understanding}

「安全主張標記語言 (SAML)」是一種開放式標準，可在主張使用者身分的身分提供者與取用使用者身分資訊的服務提供者之間交換鑑別及授權資料。
{: shortdesc}

<a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 通訊協定支援不同的設定檔和連結選項。{{site.data.keyword.appid_short_notm}} 支援 Web 瀏覽器 SSO 設定檔，以及 HTTP Post 連結。

### 流程的技術基準為何？
{: #saml-tech-basis}

SAML 2.0 是鑑別及授權標準最受公認的架構之一。它是服務提供者 ({{site.data.keyword.appid_short_notm}}) 及身分提供者之間以 XML 為基礎的通訊協定。身分提供者鑑別使用者時，它會建立 SAML 記號，其中包含關於使用者的主張或聲明。聲明可能包含：

- 鑑別資訊，例如鑑別使用者的方式－密碼、MFA 等等…
- 與使用者相關聯的屬性－他們所屬的群組。
- 授權決策，指出是否容許使用者對特定資源執行特定動作。

當主張傳回給 {{site.data.keyword.appid_short_notm}} 時，該服務會聯合使用者身分，且會產生適當的記號。如果 SAML 主張對應於下列其中一個 OIDC 宣告，它會自動新增至身分記號。如果這些值有一個以上已在提供者端變更，則只有在使用者再次登入之後，新值才可供使用。

 * `name `
 * `email`
 * `locale`
 * `picture`

依預設，會忽略未對應至任何標準名稱的主張，但如果您的 SAML 提供者傳回其他主張，則在使用者登入時可能會取得此資訊。藉由建立您要使用的主張陣列，您可以[將此資訊注入記號中](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)。但是，請務必不要將非必要資訊新增至記號中。記號通常會以 HTTP 標頭傳送，且標頭有大小限制。
{: tip}

### 流程具有怎樣的外觀？
{: #saml-flow}

雖然 {{site.data.keyword.appid_short_notm}} 和您的身分提供者使用 SAML 架構來鑑別使用者，但 {{site.data.keyword.appid_short_notm}} 仍使用較現代的 OAuth 2.0/ OIDC 架構來與應用程式交換安全記號。請參閱下列影像，以查看詳細的資訊流程。

![SAML 企業鑑別流程](/images/ibmid-flow.png)

1. 使用者存取其應用程式上的登入頁面或受限制資源，這會透過 {{site.data.keyword.appid_short_notm}} SDK 或 API，起始對 {{site.data.keyword.appid_short_notm}}`/authorization` 端點的要求。如果使用者未獲授權，則會以重新導向至 {{site.data.keyword.appid_short_notm}} 來開始鑑別流程。
2. {{site.data.keyword.appid_short_notm}} 會產生 SAML 鑑別要求 (AuthNRequest)，而瀏覽器會自動將使用者重新導向至 SAML 身分提供者。
3. 身分提供者會剖析 SAML 要求、鑑別使用者，以及產生具有其主張的 SAML 回應。
4. 身分提供者會使用 SAML 回應，將使用者及回應重新導向回 {{site.data.keyword.appid_short_notm}}。
5. 如果鑑別成功，{{site.data.keyword.appid_short_notm}} 會建立代表使用者授權和鑑別的存取權和身分記號，並將它們傳回給應用程式。如果鑑別失敗，{{site.data.keyword.appid_short_notm}} 會將身分提供者錯誤碼傳回給應用程式。
6. 使用者會獲授與對應用程式或受保護資源的存取權。



### SSO 會變更流程嗎？
{: #saml-sso-flow}

{{site.data.keyword.appid_short_notm}} 實作的 Web 瀏覽器 SSO 設定檔是由服務提供者所起始，這表示 {{site.data.keyword.appid_short_notm}} 必須將 SAML 要求傳送給身分提供者，以起始鑑別階段作業。 

{{site.data.keyword.appid_short_notm}} 目前不支援身分提供者起始的流程，且目前不應該與服務搭配使用。
{: note}

如果您的身分提供者支援 SSO，則 SAML 鑑別可能會使用已建立的 SSO 階段作業來鑑別使用者。否則會將使用者重新導向至登入頁面。如果您的身分提供者無法滿足用來建立 SSO 之 {{site.data.keyword.cloud_notm}} 鑑別要求中所定義的鑑別需求，則可能會將使用者重新導向。例如，如果身分提供者使用生物識別技術來建立使用者 SSO 階段作業，則必須變更 {{site.data.keyword.appid_short_notm}} 的預設鑑別環境定義。依預設，{{site.data.keyword.appid_short_notm}} 預期使用者以密碼透過 HTTPS 進行鑑別：`urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`。



## 配置 SAML 以使用 {{site.data.keyword.appid_short_notm}}
{: #saml-configure}

您可以配置 SAML 以便使用 {{site.data.keyword.appid_short_notm}}，方法是將 meta 資料從 {{site.data.keyword.appid_short_notm}} 提供給您的身分提供者，以及將 meta 資料從您的身分提供者提供給 {{site.data.keyword.appid_short_notm}}。



### 提供 meta 資料給您的身分提供者
{: #saml-provide-idp}

若要配置您的應用程式，您需要提供資訊給 SAML 相容身分提供者。此資訊是透過 meta 資料 XML 檔案進行交換，該檔案還包含用來建立信任的配置資料。
{: shortdesc}

要等到您將 SAML 配置為身分提供者之後，您才能啟用 SAML。
{: tip}

1. 在 {{site.data.keyword.appid_short_notm}} 儀表板的**管理**標籤中，按一下 **SAML** 列中的**編輯**來配置您的設定。
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
      <td>身分提供者知道在主張主旨中需要傳送哪種 ID 格式的方式，以及 {{site.data.keyword.appid_short_notm}} 如何識別使用者。ID 應該採用下列格式：<code><saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"/></code></td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>身分提供者檢查以查看是否需要簽署主張的方式。服務會預期主張已簽署，但不支援加密主張。</td>
    </tr>
  </table>

3. 提供資料給您的身分提供者。如果您的身分提供者支援上傳 meta 資料檔，則您可以這麼做。若非如此，請手動配置內容。並非每個身分提供者都使用相同的內容，因此，您可能不會使用全部的內容。

  身分提供者之間的內容名稱可能不同。
  {: tip}

4. 將 **SAML 2.0 聯合**切換至**已啟用**。



### 提供 meta 資料給 {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

您可以從身分提供者取得資料，並將其提供給 {{site.data.keyword.appid_short_notm}}。
{: shortdesc}

**使用 GUI 提供 meta 資料** 

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

想要設定鑑別環境定義嗎？您可以透過 API 這樣做。
{: tip}

</br>

**使用 API 提供 meta 資料**

1. 檢視現行 SAML 配置，包括您的鑑別環境定義和憑證，方法是對 [`/saml` API 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp)提出 GET 要求。

  程式碼範例：
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
  ```
  {: codeblock}

  輸出範例：
  ```
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    }
  }
  ```
  {: screen}

2. 建立 SAML 配置，方法是將下列範例中的值取代為來自提供者的資訊。範例中顯示的值是必要的，但您可以選擇包含更多資訊，如表格中所示。

  ```
  "config": {
    "authnContext": {
        "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
    "displayName": "my saml example",
  }
  ```
  {: codeblock}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> 變數</th>
      <th> 說明</th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>將使用者重新導向以進行鑑別的 URL。它是由您的 SAML 身分提供者進行管理。</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>SAML 身分提供者的廣域唯一名稱。</td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>指派給 SAML 配置的名稱。</td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>SAML 身分提供者所發出的憑證。它用於簽署及驗證 SAML 主張。所有提供者都不同，但您可能可以從身分提供者下載簽署憑證。憑證必須為 <code>.pem</code> 格式。</td>
    </tr>
    <tr>
      <td>選用項目：<code>secondary-certificate-example-pem-format</code></td>
      <td>SAML 身分提供者所發出的備份憑證。它用於無法使用主要憑證驗證簽章的情況。<strong>附註</strong>：如果簽署金鑰保持相同，則 {{site.data.keyword.appid_short_notm}} 不會封鎖過期憑證的鑑別。</td>
    </tr>
    <tr>
      <td>選用項目：<code>authnContext</code></td>
      <td>鑑別環境定義是用來驗證鑑別及 SAML 主張的品質。您可以將類別陣列和比較字串新增至您的程式碼，以新增鑑別環境定義。請務必使用您的值同時更新 <code>class</code> 及 <code>comparison</code> 參數。例如，<code>class</code> 參數可能看起來類似 <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code>。</td>
    </tr>
  </table>

3. 對 [`/saml` API 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)提出 PUT 要求，以將您在步驟 2 中建立的配置提供給 {{site.data.keyword.appid_short_notm}}。請查看下列範例，以瞭解要求可能的外觀。

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        ],
      "displayName": "my saml example",
    }
  }
  ```
  {: screen}



## 測試您的配置
{: #saml-testing}

您可以測試「SAML 身分提供者」與 {{site.data.keyword.appid_short_notm}} 之間的配置。

1. 確定您已儲存配置。
2. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的 **SAML 2.0** 標籤，然後按一下**測試**。即會開啟新標籤。
3. 以身分提供者已鑑別的使用者身分登入。
4. 完成表單之後，系統會將您重新導向至另一個頁面。
  * 成功鑑別：{{site.data.keyword.appid_short_notm}} 與「身分提供者」之間的連線正確運作。頁面會顯示有效的[存取及身分記號](/docs/services/appid?topic=appid-tokens#tokens)。
  * 失敗鑑別：連線已中斷。頁面會顯示錯誤及 SAML 回應 XML 檔。


有困難嗎？請參閱[疑難排解：SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp)。
{: tip}




## SAML 常見問題
{: #saml-assertions}

可以使用不同的方式傳回 SAML 主張。請參閱下列範例，以瞭解 {{site.data.keyword.appid_short_notm}} 預期回應格式化的方式。
{: shortdesc}


### {{site.data.keyword.appid_short_notm}} 預期 SAML 主張看起來像什麼？
{: #saml-example}

服務預期 SAML 主張看起來像下列範例。

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}


### {{site.data.keyword.appid_short_notm}} 支援哪些類型的演算法？
{: #saml-signatures}

{{site.data.keyword.appid_short_notm}} 使用 <a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 演算法來處理 XML 數位簽章。

