---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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

「安全主張標記語言 (SAML)」是一種開放式標準，可在主張使用者身分的身分提供者與取用使用者身分資訊的服務提供者之間交換鑑別及授權資料。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 可充當服務提供者，並對協力廠商提供者（例如 Active Directory Federation Services）起始單一登入 (SSO) 的登入作業。<a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 通訊協定支援不同的設定檔和連結選項。{{site.data.keyword.appid_short_notm}} 支援 Web 瀏覽器 SSO 設定檔，以及 HTTP Post 連結。

如需如何使用特定 SAML 身分提供者的步驟，請查看有關下列作業的這些部落格文章：使用 [Ping One ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/)、[Azure Active Directory ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) 或 [Active Directory Federation Service ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/) 來設定 {{site.data.keyword.appid_short_notm}}。
{: tip}



## 瞭解主張
{: #saml-assertions}

SAML 主張類似於[使用者屬性](/docs/services/appid?topic=appid-user-profile#user-profile)。它是使用者順利登入應用程式時，由身分提供者傳回給 {{site.data.keyword.appid_short_notm}} 之使用者的相關聲明或一部分資訊。視您的應用程式配置及您使用的身分提供者而定，此資訊可能包含使用者名稱、電子郵件或您要求指定的其他欄位。
{: shortdesc}

當主張傳回給 {{site.data.keyword.appid_short_notm}} 時，該服務會聯合使用者身分。如果 SAML 主張對應於下列其中一個 OIDC 宣告，它會自動新增至身分記號。如果這些值有一個以上已在提供者端變更，則只有在使用者再次登入之後，新值才可供使用。

 * `name `
 * `email`
 * `locale`
 * `picture`

依預設，會忽略未對應至任何標準名稱的主張，但如果您的 SAML 提供者傳回其他主張，則在使用者登入時可能會取得此資訊。藉由建立您要使用的主張陣列，您可以[將此資訊注入記號中](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)。但是，請務必不要將非必要資訊新增至記號中。記號通常會以 HTTP 標頭傳送，且標頭有大小限制。
{: tip}

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




## 提供 meta 資料給您的身分提供者
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
      <td>身分提供者知道在主張主旨中需要傳送哪種 ID 格式的方式。{{site.data.keyword.appid_short_notm}} 識別使用者的方式。</td>
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

## 提供 meta 資料給 {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

您可以從身分提供者取得資料，並將其提供給 {{site.data.keyword.appid_short_notm}}。
{: shortdesc}

### 使用 GUI 提供 meta 資料
{: #saml-provide-gui}

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


### 使用 API 提供 meta 資料
{: #saml-provide-api}

1. 對 [/getSamlMetadata API 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp) 提出 GET 要求，以取得 SAML meta 資料。

  程式碼範例：
  ```
  <?xml version="1.0"?>
  <getSamlMetadata>
    <?xml version="1.0"?> <EntityDescriptor> <SPSSODescriptor> <NameIDFormat> </NameIDFormat> <AssertionConsumerService /> </SPSSODescriptor>
   </EntityDescriptor>
    </getSamlMetadata>
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
    },
    "validation_data": {
      "certificates": [
        {
          "certificate_index": 0,
          "expiration_timestamp": 1674473996,
          "warning": "Your certificate will expire in 18 days."
        }
      ]
    }
  }
  ```
  {: screen}

2. 對 [/set_saml_idp API 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)配置您的 POST 要求。

  1. 在下列 meta 資料範例中，將變數取代為您自己的資訊。

    ```
    Put {Management URI}/config/idps/saml
    Content-Type: application/json
    {
      "isActive": true,
      "config": {
        "entityID": "https://example.com/saml2/metadata/706634",
        "signInUrl": "https://example.com/saml2/sso-redirect/706634",
        "certificates": [
          "primary-certificate-example-pem-format"
        ],
        "displayName": "my saml example"
      }
    }
    ```
    {: codeblock}

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

  2. 選用項目：將次要憑證新增至憑證陣列中的主要認證之後。如果無法使用主要憑證驗證簽章，則會使用次要憑證。如果簽署金鑰保持相同，則 {{site.data.keyword.appid_short_notm}} 不會封鎖過期憑證的鑑別。

    範例：
    ```
    {
      "isActive": true,
      "config": {
        ...
        "certificates": [
          "primary-certificate-example-pem-format",
          "secondary-certificate-example-pem-format"
        ],
        ...
      }
    }
    ```
    {: screen}
  {: #configuring-saml-new}
  3. 選用項目：將類別陣列和比較字串新增至您的程式碼，以新增鑑別環境定義。請務必使用您的值同時更新 `class` 及 `comparison` 參數。鑑別環境定義是用來驗證鑑別及 SAML 主張的品質。

    範例：
    ```
    {
      "isActive": true,
      "config": {
        ...
        "authnContext": {
          "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
          "comparison": "sampleComparisonValue"
        }
      }
    }
    ```
    {: screen}

3. 提出要求。如果您選擇新增選用值，您的要求看起來應該與下列範例類似。

  ```
  Put {Management URI}/config/idps/saml
  Content-Type: application/json
  {
    "isActive": true,
    "config": {
      ...
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
        "comparison": "sampleComparisonValue"
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
      "displayName": "my saml example"
    }
  }
  ```
  {: codeblock}


## 測試您的配置
{: #saml-testing}

您可以測試「SAML 身分提供者」與 {{site.data.keyword.appid_short_notm}} 之間的配置。

1. 確定您已儲存配置。
2. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的 **SAML 2.0** 標籤，然後按一下**測試**。即會開啟新標籤。
3. 以身分提供者已鑑別的使用者身分登入。
4. 完成表單之後，系統會將您重新導向至另一個頁面。
  * 成功鑑別：{{site.data.keyword.appid_short_notm}} 與「身分提供者」之間的連線正確運作。頁面會顯示有效的[存取及身分記號](/docs/services/appid?topic=appid-tokens#tokens)。
  * 失敗鑑別：連線已中斷。頁面會顯示錯誤及 SAML 回應 XML 檔。


有困難嗎？請參閱[身分提供者配置的疑難排解](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp)。
{: tip}
