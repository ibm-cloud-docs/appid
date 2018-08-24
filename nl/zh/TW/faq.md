---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-01"

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

發出新的存取記號（一般或匿名）時，即會發生鑑別事件。若為已識別的使用者，依預設，每個新存取記號的有效期限為 1 小時（透過實際使用者鑑別或透過重新整理記號進行）。依預設，匿名記號的有效期限為 1 個月。在記號到期之後，您必須建立新的記號，才能存取受保護資源。您可以在 {{site.data.keyword.appid_short_notm}} 儀表板的**登入有效期限**頁面上更新 {{site.data.keyword.appid_short_notm}} 記號的有效期限。

當您在行動應用程式中使用 {{site.data.keyword.appid_short_notm}} 時，記號會儲存在金鑰儲存庫或金鑰鏈中，並新增至每個未來要求。您可以使用 App ID Android 或 iOS SDK 存取這些記號。當您在 Web 應用程式中使用 {{site.data.keyword.appid_short_notm}} 時，建議將記號儲存至應用程式階段作業 Cookie 中。


### 授權使用者

授權使用者是使用您的服務登入（無論是直接或間接）的唯一使用者。每次新的使用者從每一個身分提供者登入（包括匿名使用者），都會向您收取一個授權使用者的費用。比方說，如果使用者藉由 Facebook 登入，而且稍後使用 Google 登入，他們會被視為兩個不同的授權使用者。

如需累進層級定價的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} 定價文件](/docs/billing-usage/how_charged.html#services)。

</br>


## 加密在 {{site.data.keyword.appid_short_notm}} 中如何運作？
{: #encryption}

請查看下表，以取得加密常見問題的答案。

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>您為何使用加密？</td>
      <td>服務會加密靜止中客戶資料。</td>
    </tr>
    <tr>
      <td>您建置過自己的演算法嗎？您在程式碼中使用哪些演算法？</td>
      <td>我們未曾建置自己的演算法，服務會搭配使用 <code>AES</code> 及 <code>SHA-256</code> 與 salt。</td>
    </tr>
    <tr>
      <td>您是否使用公用或開放程式碼加密模組或提供者？您是否曾經公開加密功能？</td>
      <td>服務使用 <code>javax.crypto</code> Java 程式庫，但從未公開過加密功能。</td>
    </tr>
    <tr>
      <td>您如何儲存金鑰？</td>
      <td>使用每個地區特有的主要金鑰加密之後，會產生金鑰，並將其儲存在本端。主要金鑰儲存在 {{site.data.keyword.keymanagementserviceshort}} 中。</td>
    </tr>
    <tr>
      <td>您使用的金鑰強度為何？</td>
      <td>服務使用 16 個位元組。</td>
    </tr>
    <tr>
      <td>您是否呼叫任何公開加密功能的遠端 API？</td>
      <td>否，我們沒有。</td>
    </tr>
  </tbody>
</table>

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
