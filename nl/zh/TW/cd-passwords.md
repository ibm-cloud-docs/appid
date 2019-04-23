---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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

# 定義密碼原則
{: #cd-strength}

您可以設定可與「雲端目錄」搭配使用的密碼需求。透過定義使用者必須遵循的特定需求，您可以確保有更安全的應用程式。
{: shortdesc}

## 原則：密碼強度
{: #cd-password-strength}

高保護性密碼會讓人很難、甚至無法使用手動或自動化方式來猜測密碼。若要設定使用者密碼強度的需求，您可以使用下列步驟。
{: shortdesc}

1. 導覽至「應用程式 ID」儀表板的**密碼原則**標籤。

2. 在**定義密碼強度**方框中，按一下**編輯**。即會顯示畫面。

3. 在**密碼強度**方框中輸入有效的正規表示式字串。

  範例：
    - 必須至少為八個字元。範例正規表示式：`^.{8,}$`
    - 必須包含一個數字、一個小寫字母，以及一個大寫字母。範例正規表示式：`^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
    - 只能包含英文字母及數字。範例正規表示式：`^[A-Za-z0-9]*$`
    - 必須至少有一個唯一字元。範例正規表示式：`^(\w)\w*?(?!\1)\w+$`

4. 按一下**儲存**。

密碼強度可以在「{{site.data.keyword.appid_short_notm}} 主控台」的 Cloud Directory 設定頁面中進行設定，或使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 加以設定。
{: note}


## 進階密碼原則
{: #cd-advanced-password}


您可以藉由強制執行其他密碼限制來加強應用程式的安全。
{: shortdesc}


您可以建立由下列 5 個特性的任何組合所組成的進階密碼原則：

 - 在重複錯誤的認證之後鎖定
 - 避免密碼重複使用
 - 密碼有效期限
 - 密碼變更之間的最短期間
 - 確保密碼不包括使用者名稱


 如果啟用此特性，則會啟動進階安全功能的其他計費。如需相關資訊，請參閱 [{{site.data.keyword.appid_short_notm}} 如何計算定價](/docs/services/appid?topic=appid-faq#faq-pricing)。
 {: important}


### 原則：避免密碼重複使用
{: #cd-avoid-reuse}

當您的使用者變更其密碼時，您可能想要阻止他們選擇最近使用的密碼。
{: shortdesc}

使用 GUI 或 API，您可以選擇使用者在可以重複先前使用的密碼之前必須具有的密碼數目。您可以選取 1 - 10 範圍內的任何整數值。

如果開啟這個選項，使用者就無法使用他們最近使用過的密碼。如果他們嘗試將其密碼設為最近使用過的密碼，則在預設「登入小組件」GUI 中會顯示錯誤，並提示他們輸入不同的密碼。

安全地儲存先前的密碼，其儲存方式與使用者現行密碼的儲存方式相同。
{: note}


### 原則：在重複錯誤認證之後鎖定
{: #cd-lockout}

您可能想要在偵測到可疑行為時（例如使用不正確的密碼連續多次嘗試登入）暫時封鎖登入功能，藉此來保護您的使用者。此措施有助於阻止惡意一方藉由猜測使用者的密碼來取得使用者帳戶的存取權。
{: shortdesc}

使用 GUI 或 API，您可以設定在暫時鎖定使用者的帳戶之前，使用者可以進行的不成功登入嘗試次數上限。您也可以設定帳戶的鎖定時間量。您具有下列選項：

* 嘗試次數：1 - 10 的任何整數值。
* 鎖定期間：在 1 分鐘到 1440 分鐘（24 小時）範圍內指定的任何整數值（分鐘）。

如果帳戶遭到鎖定，則使用者無法登入或執行任何其他自助作業（例如變更其密碼），直到過了指定的鎖定週期為止。鎖定期間結束時，即會自動解除鎖定使用者。

您可以在鎖定期間結束之前解除鎖定使用者。若要查看他們是否遭到鎖定，請查看`作用中`欄位是否設為 `false`。您也可以查看其在服務儀表板之**使用者**標籤上的狀態是否設為`已停用`。若要解除鎖定使用者，您必須使用 [API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser)，將 `active` 欄位設為 `true`。


### 原則：密碼變更之間的最短期間
{: #cd-minimum-time}

您可能想要防止使用者快速切換密碼，方法是設定使用者在密碼變更之間必須等待的最短時間。
{: shortdesc}

此特性在與「避免密碼重複使用」原則一起使用時特別有用。若沒有這項限制，使用者就可以快速連續變更其密碼多次，以規避重複使用最近密碼的限制。您可以選取介於 1 小時與 30 天之間的任何值，以小時為單位指定。


### 原則：密碼有效期限
{: #cd-expiration}

基於安全考量，您可能要強制執行密碼輪替原則，讓使用者在一段時間之後必須變更其密碼。
{: shortdesc}

使用 GUI 或 API，您可以設定使用者密碼將保留有效的時段。在使用者密碼到期之後，於下次登入時，就會強制使用者重設其密碼。您可以選取介於 1 與 90 之間的任意完整天數。

您可以使用提供的預設 GUI，快速開始使用「登入小組件」。在登入完成之前，會指引使用者提供新密碼。

如果您是使用自訂登入體驗，則當使用者嘗試使用過期密碼登入時，即會觸發錯誤。您應負責配置您的應用程式，以提供必要的使用者體驗。您可以呼叫變更密碼 API，來設定新密碼。

記號端點回應與下列內容類似：

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

此選項第一次設為開啟時，所有現有使用者密碼都沒有到期日。當那些使用者的密碼變更時，其有效期限即會開始。在將此特性設為開啟之後，您可能想要鼓勵使用者更新其密碼。
{: note}


### 原則：確保密碼不包含使用者名稱
{: #cd-no-username}

如需更高保護性密碼，您可能要防止密碼包含其使用者名稱，或其電子郵件位址的第一個部分。
{: shortdesc}

此限制不區分大小寫，這表示使用者不能為了使用個人資訊而變更部分或全部字元的大小寫。若要配置此選項，請將開關切換至**開啟**。

