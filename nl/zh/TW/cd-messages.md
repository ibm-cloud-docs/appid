---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

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

# 自訂電子郵件
{: #cd-types}

當使用者與您的應用程式互動時，有時候您可能想要傳送回覆或要求驗證。{{site.data.keyword.appid_short_notm}} 提供您可用於互動的預設範本。您也可以使用範本作為指引，並自訂傳訊以符合您的品牌。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 使用 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 作為郵件傳送服務。所有電子郵件都是使用單一 SendGrid 帳戶所傳送。
{: note}

## 電子郵件範本
{: #cd-messages}

將訊息傳送給使用者時，您可以使用下列範本的任何組合。或者，您可以編輯範本來自訂訊息。
{: shortdesc}

除了下列訊息類型之外，您還可以利用 [SSO](/docs/services/appid?topic=appid-cd-sso#cd-sso) 及 [MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) 範本。
{: tip}

您可以在訊息中使用參數，以進一步自訂訊息。請參閱下表，以查看您可以在所有訊息類型中使用的參數。

<table>
  <tr>
    <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 所有訊息參數</th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> 顯示您為「登入小組件」配置的影像。</td>
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
</table>


### 電子郵件：歡迎使用
{: #cd-messages-welcome}

當使用者註冊您的應用程式時，您可能想要傳送一則訊息給他們，來歡迎他們使用您的應用程式。
{: shortdesc}

1. 導覽至服務儀表板的**工作流程範本 > 歡迎使用電子郵件**標籤。

2. 將**歡迎使用電子郵件**設為**已啟用**。

3. 自訂訊息的內容。您可以透過使用者介面來新增參數及插入影像。若要變更訊息的[語言](/docs/services/appid?topic=appid-cd-messages#cd-languages)，您可以利用 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來設定語言。不過，您要負責訊息的內容及翻譯。請參閱下表，以查看您可以在此訊息中使用的表格清單，以及您可以傳送的所有其他訊息。如果使用者未提供參數所取回的資訊，則它會出現空白。

4. 按一下**儲存**。


### 電子郵件：驗證
{: #cd-messages-verification}

當使用者透過其電子郵件來註冊您的應用程式時，您可以傳送電子郵件給他們，要求他們確認其身分。藉由要求驗證，您可以限制可以登入您應用程式之偽造帳戶的數目。您可以限制應用程式的存取，直到使用者已驗證其電子郵件，或使用它作為管理您可以為哪些使用者建立設定檔的方法。請注意，透過 {{site.data.keyword.appid_short_notm}} 儀表板或建立使用者 API 手動新增的使用者，不會自動收到此電子郵件。
{: shortdesc}


1. 導覽至服務儀表板的**工作流程範本 > 電子郵件驗證**標籤。

2. 將**電子郵件驗證**設為**已啟用**。

3. 將**容許使用者登入您的應用程式，而不需要先驗證其電子郵件位址**設為**是**。若設為「是」，使用者可以在註冊之後但在驗證其電子郵件位址之前，與您的應用程式互動。預設值為「否」。

4. 自訂訊息的內容。您可以透過使用者介面來新增參數及插入影像。若要變更訊息的[語言](/docs/services/appid?topic=appid-cd-messages#cd-languages)，您可以利用 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來設定語言。不過，您要負責訊息的內容及翻譯。請參閱下表，以查看您可以在訊息中使用的不同參數。如果使用者未提供參數所取回的資訊，則它會出現空白。

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 驗證訊息參數</th>
    </tr>
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
  </table>

  您也可以使用[歡迎使用訊息](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome)區段中所列出的訊息參數。
  {: tip}

5. 定義動作 URL 的有效期限。URL 有效期限是使用者在驗證鏈結到期之前必須完成動作的時間量（分鐘）。此設定也會影響重設密碼鏈結有效的時間量。
 
6. 輸入當使用者在**感謝您頁面 URL** 方框中驗證其電子郵件之後您想要顯示的頁面 URL。如果您選擇將此欄位保留空白，則會顯示 {{site.data.keyword.appid_short_notm}} 預設頁面。

7. 按一下**儲存**。 


### 電子郵件：重設密碼
{: #cd-messages-reset}

當使用者與您的應用程式互動時，他們可能會忘記其密碼，或另有需要來更新它。您可以自訂對其要求的電子郵件回應。當使用者要求變更其密碼時，密碼會保持不變，直到他們按一下此電子郵件中的鏈結為止。
{: shortdesc}


1. 導覽至服務儀表板的**工作流程範本 > 重設密碼**標籤。

2. 將**忘記密碼電子郵件**設為**已啟用**。

3. 自訂訊息的內容。您可以透過使用者介面來新增參數及插入影像。若要變更訊息的[語言](/docs/services/appid?topic=appid-cd-messages#cd-languages)，您可以利用 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來設定語言。不過，您要負責訊息的內容及翻譯。請參閱下表，以查看您可以在訊息中使用的不同參數。如果使用者未提供參數所取回的資訊，則它會出現空白。

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 忘記密碼參數</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> 顯示鏈結有效的時數。</td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td>顯示鏈結有效的分鐘數。</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.code}</code></td>
      <td> 將一次性通行碼顯示為 URL 的一部分。這表示每一個人員都將具有不同的通行碼。範例：<code>https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478</code></td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> 顯示使用者按一下即可重設其密碼的鏈結。</td>
    </tr>
  </table>

  您也可以使用[歡迎使用訊息](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome)區段中所列出的訊息參數。
  {: tip}

4. 定義動作 URL 的有效期限。URL 有效期限是使用者在驗證鏈結到期之前必須完成動作的時間量（分鐘）。此設定也會影響重設密碼鏈結有效的時間量。
 
5. 輸入當使用者在**重設密碼頁面 URL** 方框中驗證其電子郵件之後您想要顯示的頁面 URL。如果您選擇將此欄位保留空白，則會顯示 {{site.data.keyword.appid_short_notm}} 預設頁面。

6. 按一下**儲存**。


### 電子郵件：密碼變更
{: #cd-messages-password-change}

您可以讓使用者知道其密碼何時已更新。如果他們並未要求變更其密碼，此舉很有用。他們可以採取適當的步驟來重新保護其帳戶的安全。
{: shortdesc}

1. 導覽至服務儀表板的**工作流程範本 > 密碼變更**標籤。

2. 將**密碼變更電子郵件**設為**已啟用**。

3. 自訂訊息的內容。您可以透過使用者介面來新增參數及插入影像。若要變更訊息的[語言](/docs/services/appid?topic=appid-cd-messages#cd-languages)，您可以利用 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來設定語言。不過，您要負責訊息的內容及翻譯。請參閱下表，以查看您可以在訊息中使用的不同參數。如果使用者未提供參數所取回的資訊，則它會出現空白。

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 密碼變更參數</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> 顯示新密碼生效的時間。</td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> 顯示從中要求密碼變更的 IP 位址。</td>
    </tr>
  </table>

  您也可以使用[歡迎使用訊息](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome)區段中所列出的訊息參數。
  {: tip}

4. 按一下**儲存**。




## 使用自訂電子郵件寄件者
{: #cd-custom-email}

使用 {{site.data.keyword.appid_short_notm}}，您可以定義自訂延伸點來傳送「雲端目錄」電子郵件訊息。定義延伸點，您可以完全控制電子郵件的傳送方式，而且您可以使用自己的網域名稱。依預設，{{site.data.keyword.appid_short_notm}} 會使用 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 作為郵件傳送服務。
 {: shortdesc}

您可能基於下列原因而想要使用自訂電子郵件寄件者：

- **個人化網域**
配置自訂電子郵件分派器，您可以完全控制電子郵件訊息的傳送方式。這包括自訂電子郵件網域，如此可進一步降低電子郵件被過濾為垃圾郵件的機會。您也可以進一步加強應用程式使用者的品牌體驗。

- **見解與疑難排解**
從電子郵件提供者獲得見解，例如：已開啟電子郵件的人員數目或哪些訊息尚未遞送。因為您可以追蹤個別訊息，並查看整體統計資料，所以這可以協助解決問題。

在配置延伸點之後，每當需要傳送電子郵件訊息時，{{site.data.keyword.appid_short_notm}} 都會呼叫它。延伸點包含訊息的所有相關資訊，包括電子郵件內文的最終內容。



### 配置自訂寄件者
{: #cd-messages-configure-custom-sender}

若要配置自訂電子郵件寄件者，您必須使用 Cloud Directory <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher" target="_blank">管理 API</a>。


1. 提供 URL。此外，您還可以提供授權資訊。支援的授權類型如下：`基本授權`或`固定授權標頭值`。

  有效的配置範例：
  ```
  {
    "custom": {
      "url": "https://example.com/send_mail"
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "basic",
        "username": "username",
        "password": "password"
      }
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "value",
        "value": "myApiKey"
      }
    }
  }
  ```
  {: screen}

2. 配置可以接聽 POST 要求的延伸點。此端點應該能夠讀取來自 {{site.data.keyword.appid_short_notm}} 的有效負載，並使用您的自訂電子郵件寄件者來傳送電子郵件。

3. 來自 {{site.data.keyword.appid_short_notm}} 的內文採用下列格式：`{"jws": "jws-format-string"}`。在您解碼並驗證有效負載之後，內容是一個 JSON 字串。

  ```
    {
      "tenant": "tenant-id",
      "iss" : "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "iat": 1539173126,
      "jti": "uniq-id",
      "message": {
          "to": "your@mail.com",
          "from": {
              "name": "My Awesome Service",
              "address": "no-reply@company.com"
          },
          "replyTo": {
              "name": "My Awesome Service",
              "address": "yes-reply@company.com"
          },
          "subject": "Welcome to My Awesome Service",
          "body": "<p>Hello<p><br/><p>Thanks for signing up John Doe</p>"
      }
    }
  ```
  {: screen}

  <table>
    <tr>
      <th>變數</th>
      <th>說明</th>
    </tr>
    <tr>
      <td><code>tenant</code></td>
      <td>{{site.data.keyword.appid_short_notm}} 實例的承租戶 ID。</td>
    </tr>
    <tr>
      <td><code> iat </code> </td>
      <td>已傳送訊息的時間戳記。</td>
    </tr>
    <tr>
      <td><code>jss</code></td>
      <td>發出 JWS 記號的原則。</td>
    </tr>
    <tr>
      <td><code>jti</code></td>
      <td>唯一交易 ID。</td>
    </tr>
    <tr>
      <td><code>message: to</code></td>
      <td>訊息收件者的電子郵件位址。</td>
    </tr>
    <tr>
      <td><code>message: from</code></br><code>name</code></br><code>address</code></td>
      <td></br>訊息寄件者的名稱。</br>寄件者的電子郵件位址。</td>
    </tr>
    <tr>
      <td><code>Optional: message: reply to</code></br><code>name</code></br><code>address</code></td>
      <td></br>附加至回覆電子郵件位址的名稱。</br>使用者可以回覆的電子郵件位址。</td>
    </tr>
  </table>

  您可以檢查回應狀態碼，以驗證您的要求已成功。在 200 - 299 範圍內的任何回應都視為成功。如果您收到任何其他回應，請嘗試重新提出要求。{: tip}

4. 從 {{site.data.keyword.appid_short_notm}} 傳送的每個 HTTP 有效負載都會使用非對稱金鑰配對，根據 JWS 標準自動簽署。對於每個 {{site.data.keyword.appid_short_notm}} 實例，會產生一個私密金鑰及一個公開金鑰，而這兩個金鑰不會在其他實例之中共用。私密金鑰是用來簽署 HTTP 有效負載，而且您可以使用公開金鑰來驗證有效負載是由 {{site.data.keyword.appid_short_notm}} 產生，且不是由第三方（<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys" target="_blank">公開金鑰端點</a>）變更。

5. 延伸點的程式碼範例 (JavaScript)。
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// Your {{site.data.keyword.appid_short_notm}} instance tenant ID
  	const tenantId = '<TENANT-ID>';

  	// Send request to {{site.data.keyword.appid_short_notm}}'s public keys endpoint
  	const keysOptions = {
  		method: 'GET',
  		url: `https://<REGION>.appid.cloud.ibm.com/oauth/v4/${tenantId}/publickeys`
  	};
  	const keysResponse = await request(keysOptions);
  	return JSON.parse(keysResponse.body).keys;
  }

  async function verifySignature(keysArray, kid, jws) {
  	const keyJson = keysArray.find(key => key.kid === kid);
  	if (keyJson) {
  		const pem = jwkToPem(keyJson);
  		await jwtVerify(jws, pem);
  		return;
  	}
  	throw new Error ("Unable to verify signature");
  }

  async function verifyAndSendMail(jws) {
  	// The API key for Sendgrid
  	const sgApiKey = '<SENDGRID-API-KEY>';

  	// Init Sendgrind
  	sgMail.setApiKey(sgApiKey);

  	// Decode message to get information
  	const data = jwtDecode(jws, {complete: true});

  	// Extract kid from header
  	const kid = data.header.kid;

  	const keysArray = await obtainPublicKeys();

  	// Verify the signature of the payload with the public keys
  	await verifySignature(keysArray, kid ,jws);

  	// Send the email with Your Sendgrid account
  	const message = data.payload.message;
  	const msg = {
  		to: message.to,
  		from: message.from.address,
  		subject: message.subject,
  		html: message.body,
  	};
  	console.log(`Sending email to ${message.to}`);
  	let sendgridResponse = await sgMail.send(msg);

  	return {result : 'email_sent',sendgridResponse};
  }
  ```
  {: screen}

6. 測試電子郵件分派器，驗證配置已正確設定。請使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">測試 API</a>，對您配置的自訂電子郵件寄件者觸發要求。

如需完整運作範例，請參閱 <a href="https://www.ibm.com/blogs/bluemix/2018/10/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users/" target="_blank">Use your own provider for mail sent with {{site.data.keyword.appid_full}}</a>。



## 支援的語言
{: #cd-languages}

您可以使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">語言管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 設定可用來寫入使用者通訊的語言。不過，預設只能使用英文。您負責翻譯訊息。使用 API 設定配置之後，就會更新 GUI，讓您能夠變更範本文字。
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
    <td>中華人民共和國澳門特別行政區</td>
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
    <td>匈牙利文</td>
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
    <td>中華人民共和國澳門特別行政區</td>
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
