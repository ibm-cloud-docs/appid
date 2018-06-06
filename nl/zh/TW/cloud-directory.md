---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 配置雲端目錄
{: #cd}

您可以將 {{site.data.keyword.appid_short_notm}} 配置為使用雲端目錄作為身分提供者。使用者可以使用電子郵件及密碼來註冊與登入行動及 Web 應用程式。雲端目錄是雲端中所維護的使用者登錄。使用者利用其電子郵件及密碼來註冊應用程式時，即會將他們新增至使用者目錄。使用此特性之後，一般使用者可以在應用程式內自由管理自己的帳戶。
{: shortdesc}

</br>

## 管理目錄設定
{: #cd-settings}

您可以針對應用程式配置通知及使用者控制層次。設定雲端目錄可以快速完成，如下圖所示。隨時可以從服務儀表板中更新這些設定。
{: shortdesc}

![配置雲端目錄](/images/cloud-directory.png)

1. 確定以身分提供者身分來開啟雲端目錄，並將**容許使用者註冊及重設其密碼**設為**開啟**。當設為**關閉**時，您仍然可以透過主控台新增使用者，但僅基於開發目的。
2. 配置寄件者詳細資料。指定訊息的來源電子郵件位址、寄件者，以及您的使用者可以回覆給誰。
  **附註**：當配置動作 URL，請確定您提供足夠時間，可讓使用者按一下鏈結。使用者必須驗證其電子郵件具有特定選項，例如能夠要求重設其密碼。
3. 判斷使用者接收的電子郵件類型及寄件者資訊。
4. 使用提供的範本，利用品牌或個人化訊息來自訂訊息。如需相關資訊，請參閱[管理訊息](/docs/services/appid/cloud-directory.html#cd-messages)。
5. 在 GUI 的**使用者**標籤中，查看應用程式的註冊人員。

</br>

## 管理訊息
{: #cd-messages}

範本是您可以傳送至使用者之電子郵件訊息的範例。您可以更新訊息的內容及佈置來自訂範本。您可以在目錄設定標籤中將這些訊息設為**開啟**或**關閉**。
{: shortdesc}

1. 選取**訊息類型**。
2. 變更訊息的內容及設計來自訂訊息。您可以使用參數來個人化訊息。請不要忘記儲存您的變更！

### 訊息類型

有數種可傳送給使用者的訊息類型。您可以選擇傳送透過程式設計方式編寫至使用者介面的範例訊息，或自訂更個人的應用程式體驗的內容。

<dl>
  <dt>歡迎使用</dt>
    <dd><p>在使用者完成登錄之後，您可以歡迎使用者使用您的應用程式。若要歡迎並留住您的使用者，請讓您的訊息儘可能吸引人。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/>可在任何類型之訊息中使用的參數</th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> 顯示您已針對登入小組件配置的影像。</td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> 顯示使用者已選擇要在與應用程式互動時使用的畫面名稱。</td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> 顯示使用者的已登錄電子郵件位址。</td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> 顯示使用者的指定名字。</td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> 顯示使用者的完整名稱。</td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> 顯示使用者的指定姓氏。</td>
        </tr>
      </tbody>
    </table>
    <p>**附註**：如果使用者未提供參數所取回的資訊，則它會出現空白。</p></dd>
  <dt>忘記密碼</dt>
    <dd><p>如果使用者忘記或基於任何原因而需要更新其密碼，使用者可以要求重設該密碼。您可以自訂對其要求的電子郵件回應。當使用者要求變更時，其密碼會保持不變，直到他們按一下此電子郵件中的鏈結。

    </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 密碼變更參數</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 顯示鏈結有效的時數。</td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 顯示鏈結有效的分鐘數。</td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> 將一次性通行碼顯示為 URL 的一部分。這將表示每一個人員都將具有不同的通行碼。範例：<code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> 顯示使用者按一下即可重設其密碼的鏈結。</td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>驗證</dt>
    <dd><p>您可以透過電子郵件要求使用者驗證其帳戶。藉由要求驗證，您可以限制可以登入您應用程式之偽造帳戶的數目。您可以限制應用程式的存取，直到使用者已驗證其電子郵件，或使用它作為管理您可以為哪些使用者建立設定檔的方法。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 驗證訊息參數</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 顯示鏈結有效的時數。</td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 顯示鏈結有效的分鐘數。</td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> 顯示一次性驗證 URL。</td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> 顯示您已在設定中指定的動作 URL。</td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>密碼變更</dt>
    <dd><p>您可以讓使用者知道其密碼何時已更新。如果他們並未要求變更其密碼，此舉很有用。他們可以採取適當的步驟來重新保護其帳戶的安全。

    </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 密碼變更參數</th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> 顯示新密碼生效的時間。</td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> 顯示從中要求密碼變更的 IP 位址。</td>
        </tr>
      </tbody>
    </table>
    </dd>
</dl>
</br>
**附註**：{{site.data.keyword.appid_short_notm}} 使用 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 作為郵件傳送服務。所有電子郵件都是使用單一 SendGrid 帳戶所傳送。

</br>
## 後續步驟
既然您已配置雲端目錄，就已準備好將 loginwidget 的程式碼新增至應用程式碼。按一下下圖中的 SDK 語言圖示，以查看您需要執行的作業。
{: shortdesc}

<img usemap="#options-map" border="0" class="image" id="options" src="images/options.png" width="750" alt="按一下 SDK 語言圖示，以在應用程式中開始使用雲端目錄。" style="width:750px;" />
<map name="options-map" id="options-map">
<area href="branded.html#branded-ui-android" alt="使用 Android SDK 管理登入體驗" shape="rect" coords="187, 6, 305, 120" />
<area href="branded.html#branded-ui-ios-swift" alt="使用 iOS Swift SDK 管理登入體驗。" shape="rect" coords="333, 6, 448, 125" />
<area href="branded.html#branded-ui-nodejs" alt="使用 Node.js SDK 管理登入體驗。" shape="rect" coords="472, 7, 590, 121" />
</map>
