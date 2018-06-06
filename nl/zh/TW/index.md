---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 入門指導教學
{: #gettingstarted}

{{site.data.keyword.appid_full}} 可協助您新增對行動及 Web 應用程式的鑑別，並且會保護您的後端資源。
{: shortdesc}

## 建立服務實例
{: #create}

建立 {{site.data.keyword.appid_short_notm}} 實例以開始。
{: shortdesc}

1. 在 {{site.data.keyword.Bluemix}} 型錄中，選取 {{site.data.keyword.appid_short_notm}}。即會開啟服務配置畫面。
2. 提供服務實例的名稱，或使用預設名稱。
3. 若要連結實例，請從**連接至**功能表中選取應用程式。如果您選取**維持不連結**，可於稍後連結服務實例。
4. 選取定價方案，然後按一下**建立**。

## 配置範例應用程式
{: #sample-app}

您可以使用其中一個預先配置的範例應用程式來熟悉如何使用服務。
{: shortdesc}

根據預設，範例應用程式已配置兩個身分提供者，而且可以檢閱鑑別。您也可以使用登入小組件特性來自訂登入頁面，以及查看在應用程式中顯示您進行的更新的速度。

若要從 GUI 配置範例應用程式，請執行下列動作：

1. 在您建立服務實例之後，可以選擇使用您覺得適合處理的語言的範例應用程式。您可以從 iOS Swift、Android、Node.js 及 Java 中進行選擇。不使用 SDK 嗎？請查看部落格上的<a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">搭配使用 {{site.data.keyword.appid_short_notm}} 與其他語言（例如 Python）<img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
2. 遵循 GUI 中的步驟，以**建置並執行**範例應用程式。每一種語言的配置略有不同，因此，請務必選取您已從下拉清單下載的應用程式語言。配置應用程式之後，即可在瀏覽器中進行開啟，並使用您的認證登入。
  **附註**：確定您已安裝要使用之語言的必要條件。
  <dl>
    <dt> Android</dt>
      <dd><ul><li> Android API 25 或更高版本</li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools 25.0.2 版 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods（1.1.0 版或更高版本）</li><li> iOS 9 或更高版本</li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> Cloud Foundry CLI </li></ul></dd>
    <dt> Java

</dt>
      <dd><ul><li> Cloud Foundry CLI </li><li> Maven </li></ul></dd>
  </dl>
3. 按一下**檢閱活動**，查看已發生的鑑別事件。如果您已登入，則應該至少看到一個事件。
4. 自訂登入體驗。您可以選取影像（例如您的標誌及標頭顏色）。您可以選取其中一個顏色選項，或插入十六進位值。當您滿意預覽結果時，請按一下**儲存變更**。您可以在下圖中看到範例登入體驗範例。
5. 在瀏覽器中，重新整理登入頁面。即可看到您在前一個步驟中進行的變更。
