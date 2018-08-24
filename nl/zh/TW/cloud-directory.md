---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 配置雲端目錄
{: #cd}

使用者可以使用電子郵件或使用者名稱及密碼來註冊與登入行動及 Web 應用程式。雲端目錄是雲端中所維護的使用者登錄。使用者註冊應用程式時，即會將它們新增至使用者目錄。使用此特性，使用者可以在應用程式內自由管理自己的帳戶。
{: shortdesc}

</br>

## 管理目錄設定
{: #cd-settings}

您可以針對應用程式配置通知及使用者控制層次。設定雲端目錄可以快速完成，如下圖所示。隨時可以從服務儀表板中更新這些設定。
{: shortdesc}


![配置雲端目錄](/images/cloud-directory.png)
圖. Cloud Directory 的配置行程


1. 確定以身分提供者身分來開啟「雲端目錄」，並將**容許使用者註冊及重設其密碼**設為**開啟**。設為**關閉**時，則基於開發目的，您仍然可以透過主控台新增使用者。
2. 選擇是否使用指定的使用者名稱或電子郵件來鑑別使用者。 此欄位用於註冊、登入及忘記密碼流程。如果您容許使用者使用使用者名稱及密碼登入，則使用者名稱必須至少為 8 個字元，而且不能包含空格、逗點或斜線。**附註：**只有在您的「雲端目錄」中沒有使用者時，才能切換選項。
3. 配置寄件者詳細資料。指定訊息的來源電子郵件位址、寄件者，以及您的使用者可以回覆給誰。當您配置動作 URL 時，請確定您提供足夠時間，可讓使用者按一下鏈結。使用者必須驗證其電子郵件具有特定選項，例如能夠要求重設其密碼。
  {: tip}
4. 判斷使用者接收的電子郵件類型及寄件者資訊。
5. 使用提供的範本，搭配特有風格或個人化訊息來自訂訊息。如需相關資訊，請參閱[管理訊息](/docs/services/appid/cloud-directory.html#cd-messages)。
6. 在 GUI 的**使用者**標籤中，查看應用程式的註冊人員。

單一使用者最多可以登入 5 次。如果已嘗試第六次，則會顯示錯誤。
{: tip}

</br>

## 管理訊息
{: #cd-messages}

範本是您可以傳送至使用者之電子郵件訊息的範例。您可以更新訊息的內容及佈置來自訂範本。
{: shortdesc}

1. 在儀表板的**身分提供者 > 雲端目錄 > 設定**標籤中，將您要傳送的訊息設為**開啟**。

2. 選用項目：使用<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">語言管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來設定您要在訊息範本中使用的另一種語言。如需受支援語言碼的清單，請參閱[支援的語言](#languages)。

3. 選取**訊息類型**。

4. 變更訊息的內容及設計來自訂訊息。您可以使用參數來個人化訊息。請不要忘記儲存您的變更！

### 訊息類型

您可將數種類型的訊息傳送給您的使用者。您可以選擇傳送透過程式設計方式編寫至使用者介面的範例訊息，或自訂更個人的應用程式體驗的內容。

<dl>
  <dt>歡迎使用</dt>
    <dd><p>在使用者完成登錄之後，您可以透過電子郵件歡迎使用者使用您的應用程式。若要歡迎並留住您的使用者，請讓您的訊息儘可能吸引人。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 所有訊息參數</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> 顯示您已針對登入小組件配置的影像。</td>
        </tr>
        <tr>
          <td><code>%{user.displayName}</code></td>
          <td> 顯示使用者選擇要在與應用程式互動時使用的畫面名稱。</td>
        </tr>
        <tr>
          <td><code>%{user.email}</code></td>
          <td> 顯示使用者的已登錄電子郵件位址。</td>
        </tr>
        <tr>
          <td><code>%{user.username}</code></td>
          <td> 鑑別方法設為使用者名稱及密碼時，會顯示使用者的指定使用者名稱。 </td>
        </tr>
        <tr>
          <td><code>%{user.firstName}</code></td>
          <td> 顯示使用者的指定名字。</td>
        </tr>
        <tr>
          <td><code>%{user.formattedName}</code></td>
          <td> 顯示使用者的完整名稱。</td>
        </tr>
        <tr>
          <td><code>%{user.lastName}</code></td>
          <td> 顯示使用者的指定暱稱。</td>
        </tr>
      </tbody>
    </table>
    <p>**附註**：如果使用者未提供參數所取回的資訊，則它會出現空白。</p></dd>
  <dt>忘記密碼</dt>
    <dd><p>如果使用者忘記其密碼，或基於任何原因而需要更新其密碼，使用者可以要求重設其密碼。您可以自訂對其要求的電子郵件回應。當使用者要求變更時，其密碼會保持不變，直到他們按一下此電子郵件中的鏈結。

    </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 密碼變更參數</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> 顯示鏈結有效的時數。</td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> 顯示鏈結有效的分鐘數。</td>
        </tr>
        <tr>
          <td><code>%{resetPassword.code}</code></td>
          <td> 將一次性通行碼顯示為 URL 的一部分。這表示每一個人員都將具有不同的通行碼。範例：<code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.link}</code></td>
          <td> 顯示使用者按一下即可重設其密碼的鏈結。</td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>驗證</dt>
    <dd><p>您可以透過電子郵件要求使用者驗證其帳戶。藉由要求驗證，您可以限制可以登入您應用程式之偽造帳戶的數目。您可以限制應用程式的存取，直到使用者已驗證其電子郵件，或使用它作為管理您可以為哪些使用者建立設定檔的方法。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 驗證訊息參數</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> 顯示鏈結有效的時數。</td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> 顯示鏈結有效的分鐘數。</td>
        </tr>
        <tr>
          <td><code>%{verify.code}</code></td>
          <td> 顯示一次性驗證 URL。</td>
        </tr>
        <tr>
          <td><code>%{verify.link}</code></td>
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
        <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 密碼變更參數</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
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

## 管理密碼強度
{: #strength}

您可以設定可與「雲端目錄」搭配使用的密碼需求。
{: shortdesc}

高保護性密碼會讓人很難甚至無法使用手動或自動化方式來猜測密碼。密碼強度設為正規表示式字串。

部分共用密碼強度範例：

- 必須至少為 8 個字元。範例正規表示式：`^.{8,}$`
- 必須包含 1 個數字、1 個小寫字母及 1 個大寫字母。範例正規表示式：`^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- 只能包含英文字母及數字。範例正規表示式：`^[A-Za-z0-9]*$`
- 必須至少為 1 個唯一字元。範例正規表示式：`^(\w)\w*?(?!\1)\w+$`

您必須使用<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 設定需求。

</br>



</br>

## 支援的語言
{: #languages}

您可以使用<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">語言管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 設定可用來寫入使用者通訊的語言。不過，預設只能使用英文。您負責翻譯訊息。使用 API 設定配置之後，就會更新 GUI，讓您能夠變更範本文字。
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>代碼</th>
    <th>語言</th>
    <th>地區</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>南非荷蘭文</td>
    <td>南非</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>阿爾巴尼亞文</td>
    <td>阿爾巴尼亞</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>阿姆哈拉文</td>
    <td>衣索比亞</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>阿拉伯文</td>
    <td>阿爾及利亞</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>阿拉伯文</td>
    <td>巴林</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>阿拉伯文</td>
    <td>埃及</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>阿拉伯文</td>
    <td>伊拉克</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>阿拉伯文</td>
    <td>約旦</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>阿拉伯文</td>
    <td>科威特</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>阿拉伯文</td>
    <td>黎巴嫩</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>阿拉伯文</td>
    <td>利比亞</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>阿拉伯文</td>
    <td>茅利塔尼亞</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>阿拉伯文</td>
    <td>摩洛哥</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>阿拉伯文</td>
    <td>阿曼</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>阿拉伯文</td>
    <td>卡達</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>阿拉伯文</td>
    <td>沙烏地阿拉伯</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>阿拉伯文</td>
    <td>敘利亞</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>阿拉伯文</td>
    <td>突尼西亞</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>阿拉伯文</td>
    <td>阿拉伯聯合大公國</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>阿拉伯文</td>
    <td>葉門</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>亞美尼亞文</td>
    <td>亞美尼亞</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>阿薩姆文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>亞塞拜然文</td>
    <td>亞塞拜然</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>巴斯克文</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>白俄羅斯文</td>
    <td>白俄羅斯</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>孟加拉文</td>
    <td>孟加拉</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>白俄羅斯文</td>
    <td>白俄羅斯</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>孟加拉文</td>
    <td>孟加拉</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>孟加拉文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>波士尼亞文</td>
    <td>波士尼亞</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>保加利亞文</td>
    <td>保加利亞</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>緬甸文</td>
    <td>緬甸</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>加泰蘭文</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>簡體中文</td>
    <td>中國</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>簡體中文</td>
    <td>新加坡</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>繁體中文</td>
    <td>中國香港特別行政區</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>繁體中文</td>
    <td>澳門</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>繁體中文</td>
    <td>台灣</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>克羅埃西亞文</td>
    <td>克羅埃西亞共和國</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>捷克文</td>
    <td>捷克共和國</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>丹麥文</td>
    <td>丹麥</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>荷蘭文</td>
    <td>比利時</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>荷蘭文</td>
    <td>荷蘭</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>英文</td>
    <td>澳洲</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>英文</td>
    <td>比利時</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>英文</td>
    <td>喀麥隆</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>英文</td>
    <td>加拿大</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>英文</td>
    <td>迦納</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>英文</td>
    <td>中國香港特別行政區</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>英文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>英文</td>
    <td>愛爾蘭</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>英文</td>
    <td>肯亞</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>英文</td>
    <td>模里西斯</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>英文</td>
    <td>紐西蘭</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>英文</td>
    <td>奈及利亞</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>英文</td>
    <td>菲律賓</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>英文</td>
    <td>新加坡</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>英文</td>
    <td>南非</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>英文</td>
    <td>坦尚尼亞</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>英文</td>
    <td>英國</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>英文</td>
    <td>美國</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>英文</td>
    <td>尚比亞</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>英文</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>愛沙尼亞文</td>
    <td>愛沙尼亞</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>菲律賓文</td>
    <td>菲律賓</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>芬蘭文</td>
    <td>芬蘭</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>法文</td>
    <td>阿爾及利亞</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>法文</td>
    <td>喀麥隆</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>法文</td>
    <td>剛果民主共和國</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>法文</td>
    <td>比利時</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>法文</td>
    <td>加拿大</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>法文</td>
    <td>法國</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>法文</td>
    <td>象牙海岸（象牙海岸共和國）</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>法文</td>
    <td>盧森堡</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>法文</td>
    <td>茅利塔尼亞</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>法文</td>
    <td>模里西斯</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>法文</td>
    <td>摩洛哥</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>法文</td>
    <td>塞內加爾</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>法文</td>
    <td>瑞士</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>法文</td>
    <td>突尼西亞</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>加利西亞文</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>干達文</td>
    <td>烏干達</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>喬治亞文</td>
    <td>喬治亞共和國</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>德文</td>
    <td>奧地利</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>德文</td>
    <td>德國</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>德文</td>
    <td>盧森堡</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>德文</td>
    <td>瑞士</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>希臘文</td>
    <td>希臘</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>古吉拉特文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>豪薩文</td>
    <td>奈及利亞</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>希伯來文</td>
    <td>以色列</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>北印度文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>匈牙利人</td>
    <td>匈牙利</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>冰島文</td>
    <td>冰島</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>伊博文</td>
    <td>奈及利亞</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>印尼文</td>
    <td>印尼</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>義大利文</td>
    <td>意大利</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>義大利文</td>
    <td>瑞士</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>日文</td>
    <td>日本</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>坎那達文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>哈薩克文</td>
    <td>哈薩克</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>高棉文</td>
    <td>柬埔寨</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>金亞盧安文</td>
    <td>盧安達</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>貢根文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>韓文</td>
    <td>南韓</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>立陶宛文</td>
    <td>立陶宛</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>拉脫維亞文</td>
    <td>拉脫維亞</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>高棉文</td>
    <td>柬埔寨</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>馬其頓文</td>
    <td>馬其頓</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>馬來拉丁文</td>
    <td>馬來西亞</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>馬來亞拉姆文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>馬爾他文</td>
    <td>馬爾他</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>馬拉地文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>蒙古斯拉夫語</td>
    <td>蒙古</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>尼泊爾文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>尼泊爾文</td>
    <td>尼泊爾</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>挪威波克莫爾文</td>
    <td>挪威</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>新挪威文</td>
    <td>挪威</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>奧里亞文（歐迪亞文）</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>奧里亞文</td>
    <td>衣索比亞</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>波蘭文</td>
    <td>波蘭</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>葡萄牙文</td>
    <td>安哥拉</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>葡萄牙文</td>
    <td>巴西</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>葡萄牙文</td>
    <td>澳門</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>葡萄牙文</td>
    <td>莫三比克</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>葡萄牙文</td>
    <td>葡萄牙</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>旁遮普文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>羅馬尼亞文</td>
    <td>羅馬尼亞</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>俄文</td>
    <td>俄羅斯</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>塞爾維亞斯拉夫語</td>
    <td>塞爾維亞</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>塞爾維亞拉丁文</td>
    <td>芒特尼格羅共和國</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>塞爾維亞拉丁文</td>
    <td>塞爾維亞</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>辛哈拉文</td>
    <td>斯里蘭卡</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>斯洛伐克文</td>
    <td>斯洛伐克</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>斯洛維尼亞文</td>
    <td>斯洛維尼亞</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>西班牙文</td>
    <td>阿根廷</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>西班牙文</td>
    <td>玻利維亞</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>西班牙文</td>
    <td>智利</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>西班牙文</td>
    <td>哥倫比亞</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>西班牙文</td>
    <td>哥斯大黎加</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>西班牙文</td>
    <td>多明尼加共和國</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>西班牙文</td>
    <td>厄瓜多爾</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>西班牙文</td>
    <td>薩爾瓦多</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>西班牙文</td>
    <td>瓜地馬拉</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>西班牙文</td>
    <td>宏都拉斯</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>西班牙文</td>
    <td>墨西哥</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>西班牙文</td>
    <td>尼加拉瓜</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>西班牙文</td>
    <td>巴拿馬</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>西班牙文</td>
    <td>巴拉圭</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>西班牙文</td>
    <td>秘魯</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>西班牙文</td>
    <td>波多黎各</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>西班牙文</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>西班牙文</td>
    <td>美國</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>西班牙文</td>
    <td>烏拉圭</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>西班牙文</td>
    <td>委內瑞拉</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>斯華西里文</td>
    <td>肯亞</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>斯華西里文</td>
    <td>坦尚尼亞</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>瑞典文</td>
    <td>瑞典</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>泰米爾文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>泰盧固文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>泰文</td>
    <td>泰國</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>土耳其文</td>
    <td>土耳其</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>烏克蘭文</td>
    <td>烏克蘭</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>烏都文</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>烏都文</td>
    <td>巴基斯坦</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>烏茲別克斯拉夫語</td>
    <td>烏玆別克</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>烏茲別克拉丁文</td>
    <td>烏玆別克</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>越南文</td>
    <td>越南</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>威爾斯文</td>
    <td>英國</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>優魯巴文</td>
    <td>奈及利亞</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>祖魯文</td>
    <td>南非</td>
  </tr>
</table>
