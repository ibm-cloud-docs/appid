---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: authentication, authorization, identity, app security, secure

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
{:faq: data-hd-content-type='faq'}


# 常見問題
{: #faq}

此常見問題提供 {{site.data.keyword.appid_full}} 服務常見問題的回答。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} 如何計算定價？
{: #faq-pricing}
{: faq}

搭配 {{site.data.keyword.appid_short_notm}}，您可以花費更少的錢，而使用更多的資源。
{: shortdesc}

累進層級方案包含三個部分：鑑別事件的數目、一般與進階安全，以及授權使用者的數目。根據這兩個部分的摘要，每個月向您收取費用。總價是每個使用層級的累計費用，其計算方式為您的數量乘以該層級的單位價格。

您每月的前 1000 個鑑別事件及前 1000 個授權使用者免費，但進階安全事件除外。任何進階安全事件都會產生額外費用。

### 鑑別事件
{: #faq-authentication}

發出新的存取記號（一般或匿名）時，即會發生鑑別事件。您可以發出記號，以回應使用者起始的登入要求，或應用程式代表使用者起始的登入要求。依預設，存取記號的有效期限為 1 小時，而匿名記號的有效期限為 30 天。在記號到期之後，您必須建立新的記號，才能存取受保護資源。您可以在服務儀表板的**身分提供者 > 管理 > 鑑別設定**頁面上，更新 {{site.data.keyword.appid_short_notm}} 記號的有效期限。

#### 進階安全特性

進階安全特性可讓您加強應用程式的安全。
{: shortdesc}

<table>
  <tr>
    <th>特性</th>
    <th>好處</th>
  </tr>
  <tr>
    <td>多因子鑑別</td>
    <td>[MFA for Cloud Directory](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) 會確認使用者的身分，方法是要求使用者除了輸入其電子郵件及密碼外，還要輸入傳送至其電子郵件的一次性密碼。</td>
  </tr>
  <tr>
    <td>密碼原則管理</td>
    <td>身為帳戶擁有者，您可以配置一組使用者密碼必須符合的規則，以針對「雲端目錄」強制執行更安全的密碼。範例包括鎖定之前的嘗試登入次數、有效期限、密碼更新之間的時間跨距下限，或密碼不能重複的次數。如需選項及設定資訊的完整清單，請參閱[進階密碼管理](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password)。</td>
  </tr>
</table>

依預設，會停用進階安全特性。如果您開啟 MFA 或密碼原則管理，則會產生額外費用。如果您停用所有進階特性，您的帳戶會回復為較低成本原則。例如，如果您已取得 10,000 個存取記號。然後，您開啟了密碼原則管理，而且又取得了 10,000 個。您將支付 20,000 個鑑別事件及 10,000 個進階安全事件的費用。

這些特性僅適用於累進層級定價方案的實例，以及在 2018 年 3 月 15 日之後建立的實例。
{: note}

### 授權使用者
{: #faq-authorized}

授權使用者是使用您的服務登入（無論是直接或間接）的唯一使用者，包括匿名使用者。每次新的使用者登入應用程式（包括匿名使用者），都會向您收取一個授權使用者的費用。例如，如果使用者藉由 Facebook 登入，而且稍後使用 Google 登入，他們會被視為兩個不同的授權使用者。

對於最新計價資訊，您可以在 [{{site.data.keyword.cloud_notm}} 型錄](https://cloud.ibm.com/catalog/services/app-id)的 {{site.data.keyword.appid_short_notm}} 區段中，按一下**新增至預估**來建立成本預估。
{: tip}



## 為何需要將我的重新導向 URI 列入白名單？
{: #faq-redirect}
{: faq}

重新導向 URI 是應用程式的回呼端點。為了防止網路釣魚攻擊，{{site.data.keyword.appid_short_notm}} 會根據重新導向 URI 的白名單來驗證 URI。發生網路釣魚時，攻擊者有可能會取得您使用者記號的存取權。如需重新導向 URI 的相關資訊，請參閱[新增重新導向 URI](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)。

請不要在您的 URL 中包括任何查詢參數。在驗證處理程序中，會忽略它們。範例 URL：`http://host:[port]/path`
{: tip}



## 加密在 {{site.data.keyword.appid_short_notm}} 中如何運作？
{: #faq-encryption}
{: faq}

請查看下表，以取得加密常見問題的答案。

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>您為何使用加密？</td>
      <td>我們保護使用者資訊的方式是加密靜止中的客戶資料。服務會使用每個承租戶金鑰來加密靜止中的客戶資料。</td>
    </tr>
    <tr>
      <td>您建置過自己的演算法嗎？您在程式碼中使用哪些演算法？</td>
      <td>我們未曾建置自己的演算法，服務會搭配使用 <code>AES</code> 及 <code>SHA-256</code> 與 salt。</td>
    </tr>
    <tr>
      <td>您是否使用公用或開放程式碼加密模組或提供者？您是否曾經公開加密功能？</td>
      <td>此服務使用 <code>javax.crypto</code> Java 程式庫，但絕不會公開加密功能。</td>
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

