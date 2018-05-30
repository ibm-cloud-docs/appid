---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# 常見問題

此常見問題提供 {{site.data.keyword.appid_full}} 服務常見問題的回答。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} 如何計算定價？
{: #pricing}

搭配 {{site.data.keyword.appid_short_notm}}，您可以花費更少的錢，而使用更多的資源。
{: shortdesc}

累進層級方案包括兩個部分：鑑別事件的數目及授權使用者的數目。根據這兩個部分的摘要，每個月向您收取費用。總價是每個使用層級的累計費用，其計算方式為您的數量乘以該層級的單位價格。

### 鑑別事件

發出新的 {{site.data.keyword.appid_short_notm}} 記號時，即會發生鑑別事件。若為已識別的使用者，每一個新的記號，其有效時間為 1 小時。匿名記號的有效期限為 1 個月。在記號到期之後，您必須建立新的記號，才能存取受保護資源。當您使用 {{site.data.keyword.appid_short_notm}} 進行行動鑑別時，使用者記號會儲存在 `key-store/key-chain` 中，並新增至每個未來要求。您可以使用 {{site.data.keyword.appid_short_notm}} Android 或 iOS Swift SDK 存取這些記號。當您使用服務進行 Web 鑑別時，請<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">將使用者記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 儲存在階段作業 Cookie 中。

### 授權使用者

授權使用者是使用您的服務登入（無論是直接或間接）的唯一使用者。每次新的使用者從每一個身分提供者登入（包括匿名使用者），都會向您收取一個授權使用者的費用。比方說，如果使用者藉由 Facebook 登入，而且稍後使用 Google 登入，他們會被視為兩個不同的授權使用者。

如需累進層級定價的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} 定價文件](/docs/billing-usage/how_charged.html#services)。

</br>

## {{site.data.keyword.appid_short_notm}} 監視哪種類型的活動？
{: #activity-monitor}

您可以追蹤在連結至服務實例的應用程式內產生的活動。您也可以使用 {{site.data.keyword.cloudaccesstrailshort}} 服務，監視 {{site.data.keyword.appid_short_notm}} 中所進行的管理活動。

若要檢視應用程式所產生的活動，請執行下列動作：

1. 登入您的 {{site.data.keyword.Bluemix_notm}} 帳戶。
2. 從儀表板中，選取您的 {{site.data.keyword.appid_short_notm}} 實例。
3. 按一下**概觀**標籤。
4. 檢視**活動日誌**中所列出的活動。

</br>
若要監視管理活動，請執行下列動作：

1. 登入您的 {{site.data.keyword.Bluemix_notm}} 帳戶。導覽至在其中佈建 {{site.data.keyword.appid_short_notm}} 實例的組織及空間。
2. 從型錄中，佈建 {{site.data.keyword.cloudaccesstrailshort}} 服務的實例。請確定您位在與 {{site.data.keyword.appid_short_notm}} 實例相同的空間中。
3. 在 {{site.data.keyword.cloudaccesstrailshort}} 儀表板中，按一下**管理**標籤。
4. 從下拉清單中，選取下列配置，以搜尋 {{site.data.keyword.appid_short_notm}} 所產生的任何事件。
<table>
  <tr>
    <th> 欄位</th>
    <th> 配置</th>
  </tr>
  <tr>
    <td>檢視日誌</td>
    <td>空間日誌</td>
  </tr>
  <tr>
    <td>搜尋</td>
    <td>target.name</td>
  </tr>
  <tr>
    <td>過濾</td>
    <td>appid</td>
  </tr>
</table>
5. 按一下**過濾**。

如需服務運作方式的相關資訊，請查看 [{{site.data.keyword.cloudaccesstrailshort}} 文件](/docs/services/cloud-activity-tracker/index.html)。

</br>

## {{site.data.keyword.appid_short_notm}} 預期 SAML 主張看起來像什麼？
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

</br>

## SAML 簽章支援哪種類型的演算法
{: #saml-signatures}

您可以使用下列任何演算法來處理 XML 數位簽章。

<table>
  <tr>
    <th> 演算法的類型</th>
    <th> 演算法選項</th>
  </tr>
  <tr>
    <td>具有及沒有註解的標準化和轉換演算法</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">標準化 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">具有及沒有註解的專用標準化 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">封裝的簽章轉換 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li></ul></td>
  </tr>
  <tr>
    <td>雜湊演算法</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">SHA1 摘要 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">SHA256 摘要 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">SHA512 摘要 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li></ul></td>
  </tr>
  <tr>
    <td>簽章演算法</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></li></ul></td>
  </tr>
</table>

如需使用 SAML 身分提供者的相關資訊，請參閱[配置企業識別提供者](enterprise.html)。
