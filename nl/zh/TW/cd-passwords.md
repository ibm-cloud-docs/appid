---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

subcollection: appid

---

{:external: target="_blank" .external}
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

1. 移至 {{site.data.keyword.appid_short_notm}} 儀表板的**密碼原則**標籤。

2. 在**定義密碼強度**方框中，按一下**編輯**。即會開啟畫面。

3. 在**密碼強度**方框中輸入有效的正規表示式字串。

  範例：
    - 必須至少為 8 個字元。(`^.{8,}$`)
    - 必須具有一個數字、一個小寫字母，以及一個大寫字母。(`^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`)
    - 只能具有英文字母和數字。(`^[A-Za-z0-9]*$`)
    - 必須至少具有一個唯一的字元。(`^(\w)\w*?(?!\1)\w+$`)

4. 按一下**儲存**。

密碼強度可以在「{{site.data.keyword.appid_short_notm}} 主控台」的 Cloud Directory 設定頁面中進行設定，或使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 加以設定。
{: note}


## 進階密碼原則
{: #cd-advanced-password}


您可以透過強制執行密碼限制來加強應用程式的安全。
{: shortdesc}


您可以建立由下列五項特性之任何組合所構成的進階密碼原則：

 - 在重複錯誤的認證之後鎖定
 - 避免密碼重複使用
 - 密碼有效期限
 - 密碼變更之間的最短期間
 - 確定密碼不包含使用者名稱


 當您啟用此特性時，會啟動進階安全功能的額外計費。如需相關資訊，請參閱[如何執行{{site.data.keyword.appid_short_notm}}計算定價](/docs/services/appid?topic=appid-faq#faq-pricing)。
 {: important}


### 原則：避免密碼重複使用
{: #cd-avoid-reuse}

當您的使用者變更其密碼時，您可能想要阻止他們選擇最近使用的密碼。
{: shortdesc}

透過使用 GUI 或 API，您可以選擇使用者在可以重複先前使用的密碼之前必須具有的密碼數目。設定選項包括 1 - 10 範圍內的任何整數值。

如果開啟這個選項，使用者就無法使用他們最近使用過的密碼。如果他們嘗試將其密碼設為最近使用過的密碼，則會在預設「登入小組件」GUI 中顯示錯誤，並提示使用者輸入其他選項。

安全地儲存先前的密碼，其儲存方式與使用者現行密碼的儲存方式相同。
{: note}


### 原則：在重複錯誤認證之後鎖定
{: #cd-lockout}

您可能想要在偵測到可疑行為時（例如使用不正確的密碼連續多次嘗試登入）暫時封鎖登入功能，藉此來保護使用者的帳戶。此措施有助於阻止惡意一方透過猜測使用者的密碼來取得使用者帳戶的存取權。
{: shortdesc}

透過使用 GUI 或 API，您可以設定暫時鎖定使用者的帳戶之前，使用者可以進行的不成功登入嘗試次數上限。您也可以定義鎖定帳戶的時間量。您具有下列選項：

* 嘗試次數：1 - 10 的任何整數值。
* 鎖定期間：在 1 分鐘到 1440 分鐘（24 小時）範圍內指定的任何整數值（分鐘）。

如果帳戶遭到鎖定，則使用者無法登入或完成任何其他自助作業（例如變更其密碼），直到過了指定的鎖定期間為止。鎖定期間結束時，即會自動將使用者解除鎖定。

您可以在鎖定期間結束之前解除鎖定使用者。若要查看他們是否遭到鎖定，請查看`作用中`欄位是否設為 `false`。您也可以查看其在服務儀表板之**使用者**標籤上的狀態是否設為`已停用`。若要解除鎖定使用者，您必須使用 [API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser)，將 `active` 欄位設為 `true`。


### 原則：密碼變更之間的最短期間
{: #cd-minimum-time}

建議您防止使用者快速切換密碼，方法是設定使用者在兩次密碼變更之間必須等待的最短時間。
{: shortdesc}

此特性在與「避免密碼重複使用」原則一起使用時特別有用。若沒有這項限制，使用者只需快速連續多次變更密碼，就可規避重複使用最近的密碼的限制。您可以選取 1 到 720 小時（30 天）範圍內的任何值。此欄位是以小時為單位來指定。


### 原則：密碼有效期限
{: #cd-expiration}

基於安全考量，建議您強制執行密碼輪替原則，讓使用者在指定的時間量之後就必須變更其密碼。
{: shortdesc}

透過使用 GUI 或 API，您可以設定使用者密碼將保留有效的時段。在使用者密碼到期之後，就會強制使用者在下次登入時重設其密碼。您可以選取範圍 1 到 90 之間的任意完整天數。

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

這個選項第一次設為開啟時，所有現有的使用者密碼都沒有到期日。當那些使用者的密碼變更時，其有效期限即會開始。在將此特性設為開啟之後，您可能想要鼓勵使用者更新其密碼。
{: note}


### 原則：確定密碼不包含使用者名稱
{: #cd-no-username}

如需更強保護性的密碼，您可能要防止使用者使用的密碼包含其使用者名稱，或其電子郵件位址的第一個部分。
{: shortdesc}

此限制不區分大小寫。使用者無法變更部分或所有字元的大小寫，以便使用個人資訊。若要配置此選項，請將開關切換至**開啟**。
{: note}

