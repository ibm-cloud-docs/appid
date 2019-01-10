---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:faq: data-hd-content-type='faq'}


# 常見問題
{: #faq}

此常見問題提供 {{site.data.keyword.appid_full}} 服務常見問題的回答。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} 如何計算定價？
{: #pricing}
{: faq}

搭配 {{site.data.keyword.appid_short_notm}}，您可以花費更少的錢，而使用更多的資源。
{: shortdesc}

累進層級方案包括三個部分：鑑別事件的數目、一般進階與安全，以及授權使用者的數目。根據這兩個部分的摘要，每個月向您收取費用。總價是每個使用層級的累計費用，其計算方式為您的數量乘以該層級的單位價格。

您的前 1000 個鑑別事件及前 1000 個授權使用者每個月都是免費的，但任何進階安全事件除外。任何進階安全事件都會產生額外的費用。

### 鑑別事件

發出新的存取記號（一般或匿名）時，即會發生鑑別事件。您可以發出記號，以回應使用者起始的登入要求，或應用程式代表使用者起始的登入要求。依預設，存取記號的有效期限為 1 小時，而匿名記號的有效期限為 30 天。在記號到期之後，您必須建立新的記號，才能存取受保護資源。您可以在服務儀表板的**登入有效期限**頁面上，更新 {{site.data.keyword.appid_short_notm}} 記號的有效期限。

#### 進階安全功能

進階安全功能可讓您加強應用程式的安全。
{: shortdesc}

<table>
  <tr>
    <th>功能</th>
    <th>好處</th>
  </tr>
  <tr>
    <td>多因子鑑別</td>
    <td>[MFA for Cloud Directory](mfa.html) 會確認使用者的身分，方法是要求使用者除了輸入其電子郵件及密碼外，還需要輸入傳送至其電子郵件的一次性通行碼。</td>
  </tr>
  <tr>
    <td>密碼原則管理</td>
    <td>身為帳戶擁有者，您可以配置一組使用者密碼必須符合的規則，以針對「雲端目錄」強制執行更安全的密碼。範例包括鎖定之前的已嘗試登入次數、有效期限、密碼更新之間的時間跨距下限，或密碼不能重複的次數。如需選項的完整清單，以及設定資訊，請參閱[進階密碼管理](cloud-directory.html#advanced-password)。</td>
  </tr>
</table>

依預設，會停用進階安全功能。如果您開啟「多因子鑑別」或密碼原則管理，則會產生額外的費用。如果停用所有進階功能，您的帳戶將回復為較低成本原則。比方說，如果您已取得 10,000 個存取記號。然後，開啟 MFA 及密碼原則管理，並再取得 10,000 個。您將支付 20,000 個鑑別事件及 10,000 個進階安全事件的費用。

這些功能僅適用於累進層級定價方案上的實例，以及在 2018 年 3 月 15 日之後建立的實例。
{: note}

### 授權使用者

授權使用者是使用您的服務登入（無論是直接或間接）的唯一使用者，包括匿名使用者。每次新的使用者登入應用程式（包括匿名使用者），都會向您收取一個授權使用者的費用。比方說，如果使用者藉由 Facebook 登入，而且稍後使用 Google 登入，他們會被視為兩個不同的授權使用者。

如需 {{site.data.keyword.appid_short_notm}} 的最新定價資訊，請參閱[定價計算機](https://console.cloud.ibm.com/pricing/configure/service/AdvancedMobileAccess-d6aece47-d840-45b0-8ab9-ad15354deeea)。
{: important}

</br>


## 為何需要將我的重新導向 URL 列入白名單？
{: #redirect}
{: faq}

重新導向 URL 是應用程式的回呼端點。為了防止網路釣魚攻擊，{{site.data.keyword.appid_short_notm}} 會根據重新導向 URL 的白名單來驗證 URL。發生網路釣魚時，攻擊者有可能取得您的使用者記號的存取權。

若要將您的 URL 新增至白名單，請執行下列動作：

1. 導覽至**身分提供者 > 管理**。
2. 在**新增 Web 重新導向 URL** 欄位中，鍵入 URL ，然後按一下 **+**。

請不要在您的 URL 中包括任何查詢參數。在驗證處理程序中，會忽略它們。範例 URL：`http://host:[port]/path`
{: tip}

</br>

## 加密在 {{site.data.keyword.appid_short_notm}} 中如何運作？
{: #encryption}
{: faq}

請查看下表，以取得加密常見問題的答案。

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>您為何使用加密？</td>
      <td>我們保護使用者資訊的方式是加密靜止中的客戶資料。服務會使用每個承租戶金鑰加密靜止中的客戶資料。</td>
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
      <td>系統會產生金鑰，並以每一個地區特定的主要金鑰進行加密，然後儲存在本端。主要金鑰儲存在 {{site.data.keyword.keymanagementserviceshort}} 中。在儲存空間及中介軟體層次上，有一個服務水準加密，表示所有客戶都有一個金鑰。在應用程式層次上，每一個客戶都有自己的加密金鑰。</td>
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
{: faq}

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
{: faq}

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
