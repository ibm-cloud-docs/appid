---

copyright:
  years: 2017
lastupdated: "2017-12-12"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# 常見問題

此常見問題提供 {{site.data.keyword.appid_full}} 服務常見問題的回答。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} 如何計算定價？
{: #pricing}

搭配 {{site.data.keyword.appid_short_notm}}，您可以花費更少的錢，而使用更多的資源。
{: shortdesc}

累進層級方案包括兩個部分：鑑別事件的數目及授權使用者的數目。根據這兩個部分的摘要，每個月向您收取費用。總價是每個使用層級的累計費用，其計算方式為您的數量乘以該層級的單位價格。

### 鑑別事件

發出新的 {{site.data.keyword.appid_short_notm}} 記號時，即會發生鑑別事件。若為已識別的使用者，每一個新的記號，其有效時間為一小時。若為匿名使用者，記號有效時間為一個月。在記號到期之後，您必須建立新的記號，才能存取受保護資源。當您使用應用程式 ID 進行行動鑑別時，使用者記號會儲存在 `key-store/key-chain` 中，並新增至每個未來要求。您可以使用 {{site.data.keyword.appid_short_notm}} Android 或 iOS Swift SDK 存取這些記號。當您使用服務進行 Web 鑑別時，請<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">將使用者記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 儲存在階段作業 Cookie 中。

### 授權使用者

授權使用者是使用您的服務登入（無論是直接或間接）的唯一使用者。每次新的使用者從每一個身分提供者登入（包括匿名使用者），都會向您收取一個授權使用者的費用。比方說，如果使用者藉由 Facebook 登入，而且稍後使用 Google 登入，他們會被視為兩個不同的授權使用者。


如需累進層級定價的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} 定價文件](/docs/pricing/index.html#pricing)。
