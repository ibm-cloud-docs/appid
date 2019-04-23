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


# 配置 Cloud Directory
{: #cloud-directory}

有了 {{site.data.keyword.appid_full}}，使用者可以使用電子郵件或使用者名稱及密碼來註冊與登入行動及 Web 應用程式。雲端目錄是雲端中所維護的使用者登錄。使用者註冊應用程式時，即會將它們新增至使用者目錄。使用此特性，使用者可以在應用程式內自由管理自己的帳戶。
{: shortdesc}


## 管理目錄設定
{: #cd-settings}

您可以針對應用程式配置通知及使用者控制層次。設定 Cloud Directory 可以快速完成，如下圖所示。可以隨時從服務儀表板更新這些設定，而且這些設定不需任何程式碼變更就會反映在應用程式中。
{: shortdesc}


![配置雲端目錄](images/cloud-directory.png)
圖. Cloud Directory 的配置旅程


1. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的**管理鑑別**標籤，確定 Cloud Directory 是設為**開啟**。

2. 在 **Cloud Directory > 設定**標籤中，將**容許使用者註冊及登入**設為**電子郵件及密碼**或**使用者名稱及密碼**。使用者可以使用他們已擁有的電子郵件登入，或建立使用者與應用程式互動時要使用的使用者名稱。

  您可以在使用者新增至目錄之前切換選項。在新增第一位使用者之後，未來使用者也必須使用相同的配置。
  {: note}

2. 決定是要您的使用者在登入時建立使用者名稱，還是使用其電子郵件。這兩個選項都需要密碼。將使用者新增至目錄之後，就無法再切換這些選項。

3. 按一下密碼準則列中的**編輯**，以指定您要設置的所有需求。密碼準則是以正規表示式提供。如需協助判斷強度或要查看一般範例，請參閱[管理密碼強度](/docs/services/appid?topic=appid-cd-strength#cd-strength)。按一下**儲存**，讓您的需求付諸實踐。

4. 將**容許使用者註冊至您的應用程式**設為**是**。如果它設為**否**，您還是可以透過主控台新增使用者。不過，一般僅基於開發目的而透過主控台新增使用者。

5. 如果您想要使用者能夠重設其密碼、變更其密碼或重設其詳細資料，請將**容許使用者從您的應用程式管理其帳戶**設為**是**。如果您想要限制使用者的自助能力，請將值設為**否**。

6. 配置電子郵件設定。按一下**寄件者詳細資料**列中的**編輯**，以更新您的電子郵件設定。電子郵件設定適用於透過 {{site.data.keyword.appid_short_notm}} 傳送的所有通訊。

    1. 指定應該傳送電子郵件的電子郵件位址。如果您選擇變更預設值，則電子郵件可能會傳送至使用者的垃圾郵件資料夾。

    2. 新增「寄件者」的名稱。

    3. 輸入可用來傳送回應的電子郵件。

    4. 按一下**儲存**。
