---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

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

# 定制电子邮件
{: #cd-types}

用户与应用程序进行交互时，有时您可能希望发送回复或请求验证。{{site.data.keyword.appid_short_notm}} 提供了可用于交互的缺省模板。此外，您还可以使用这些模板作为指南，定制消息传递以适合您的品牌。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 使用 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 作为邮件传递服务。所有电子邮件都会使用单个 SendGrid 帐户发送。
{: note}

## 电子邮件模板
{: #cd-messages}

向用户发送消息时，可以使用以下模板的任意组合。或者，可以编辑模板来定制消息。
{: shortdesc}

除了以下消息类型外，还可以利用 [SSO](/docs/services/appid?topic=appid-cd-sso#cd-sso) 和 [MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) 模板。
{: tip}

可以在消息中使用参数，以便进一步定制消息。请查看下表以了解可以在所有消息类型中使用的参数。

<table>
  <tr>
    <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 所有消息参数</th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> 显示为登录窗口小部件配置的图像。</td>
  </tr>
  <tr>
    <td><code>%{user.displayName}</code></td>
    <td> 显示用户所选的在与应用程序交互时要使用的屏幕名称。</td>
  </tr>
  <tr>
    <td><code>%{user.email}</code></td>
    <td> 显示用户的注册电子邮件地址。</td>
  </tr>
  <tr>
    <td><code>%{user.username}</code></td>
    <td> 当认证方法设置为用户名和密码时，显示用户指定的用户名。</td>
  </tr>
  <tr>
    <td><code>%{user.firstName}</code></td>
    <td> 显示用户的指定名字。</td>
  </tr>
  <tr>
    <td><code>%{user.formattedName}</code></td>
    <td> 显示用户的全名。</td>
  </tr>
  <tr>
    <td><code>%{user.lastName}</code></td>
    <td> 显示用户的指定姓氏。</td>
  </tr>
</table>


### 电子邮件：欢迎
{: #cd-messages-welcome}

用户向应用程序注册时，您可能希望向用户发送一条消息，欢迎他们使用您的应用程序。
{: shortdesc}

1. 导航至服务仪表板的**工作流程模板 > 欢迎电子邮件**选项卡。

2. 将**欢迎电子邮件**设置为**已启用**。

3. 定制消息的内容。可以使用 UI 添加参数和插入图像。要更改消息的[语言](/docs/services/appid?topic=appid-cd-messages#cd-languages)，可以使用 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来设置语言。但是，消息的内容和翻译由您自己负责。请查看下表以了解可在此消息中使用的表的列表以及可以发送的其他所有消息。如果用户未提供参数拉出的信息，那么会显示为空。


4. 单击**保存**。


### 电子邮件：验证
{: #cd-messages-verification}

用户使用自己的电子邮件注册应用程序时，您可以向他们发送一封电子邮件，要求他们确认自己的身份。通过请求验证，您可以限制可注册应用程序的伪帐户数。您可以限制为当用户已验证电子邮件后才可访问应用程序，或用于管理您将为哪些用户创建概要文件。请注意，通过 {{site.data.keyword.appid_short_notm}} 仪表板或创建用户 API 手动添加的用户不会自动收到此电子邮件。
{: shortdesc}


1. 导航至服务仪表板的**工作流程模板 > 电子邮件验证**选项卡。

2. 将**电子邮件验证**设置为**已启用**。

3. 将**允许用户在未先验证其电子邮件地址的情况下登录到应用程序**设置为**是**。设置为“是”时，用户向应用程序注册后，但在验证其电子邮件地址之前，能够与应用程序进行交互。缺省设置为“否”。

4. 定制消息的内容。可以使用 UI 添加参数和插入图像。要更改消息的[语言](/docs/services/appid?topic=appid-cd-messages#cd-languages)，可以使用 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来设置语言。但是，消息的内容和翻译由您自己负责。请查看下表以了解可以在消息中使用的不同参数。如果用户未提供参数拉出的信息，那么会显示为空。


  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 验证消息参数</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> 显示链接保持有效的时数。</td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td> 显示链接保持有效的分钟数。</td>
    </tr>
    <tr>
      <td><code>%{verify.code}</code></td>
      <td> 显示一次性验证 URL。</td>
    </tr>
    <tr>
      <td><code>%{verify.link}</code></td>
      <td> 显示在设置中指定的操作 URL。</td>
    </tr>
  </table>

  您还可以使用[欢迎消息](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome)部分中列出的消息参数。
  {: tip}

5. 为操作 URL 定义到期时间。URL 到期时间是以分钟为单位的时间量，用户必须在此时间内完成操作，在此时间后验证链接将到期。此设置还会影响重置密码链接有效的时间量。
 
6. 在**感谢页面 URL** 框中输入在用户验证其电子邮件后要显示的页面的 URL。如果选择将此字段保留为空，那么将显示 {{site.data.keyword.appid_short_notm}} 缺省页面。

7. 单击**保存**。 


### 电子邮件：重置密码
{: #cd-messages-reset}

用户与应用程序进行交互时，可能会忘记自己的密码，或者需要更新密码。您可以定制对这些请求的电子邮件响应。当用户请求更改自己的密码时，在他们单击此电子邮件中的链接之前，其密码仍保持未更改状态。
{: shortdesc}


1. 导航至服务仪表板的**工作流程模板 > 重置密码**选项卡。

2. 将**忘记密码电子邮件**设置为**已启用**。

3. 定制消息的内容。可以使用 UI 添加参数和插入图像。要更改消息的[语言](/docs/services/appid?topic=appid-cd-messages#cd-languages)，可以使用 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来设置语言。但是，消息的内容和翻译由您自己负责。请查看下表以了解可以在消息中使用的不同参数。如果用户未提供参数拉出的信息，那么会显示为空。


  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 忘记密码参数</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> 显示链接保持有效的小时数。</td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td>显示链接保持有效的分钟数。</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.code}</code></td>
      <td> 在 URL 中，显示一次性密码作为其中一部分。这意味着每个人都会收到不同的代码。示例：`https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478`</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> 显示用户单击以重置密码的链接。</td>
    </tr>
  </table>

  您还可以使用[欢迎消息](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome)部分中列出的消息参数。
  {: tip}

4. 为操作 URL 定义到期时间。URL 到期时间是以分钟为单位的时间量，用户必须在此时间内完成操作，在此时间后验证链接将到期。此设置还会影响重置密码链接有效的时间量。
 
5. 在**重置密码页面 URL** 框中输入在用户验证其电子邮件后要显示的页面的 URL。如果选择将此字段保留为空，那么将显示 {{site.data.keyword.appid_short_notm}} 缺省页面。

6. 单击**保存**。


### 电子邮件：密码更改
{: #cd-messages-password-change}

您可以在用户密码进行更新后告知用户。在用户并未请求更改密码时，该功能很有用。他们可以采取适当步骤来重新保护自己帐户的安全。
{: shortdesc}

1. 导航至服务仪表板的**工作流程模板 > 密码更改**选项卡。

2. 将**密码已更改电子邮件**设置为**已启用**。

3. 定制消息的内容。可以使用 UI 添加参数和插入图像。要更改消息的[语言](/docs/services/appid?topic=appid-cd-messages#cd-languages)，可以使用 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来设置语言。但是，消息的内容和翻译由您自己负责。请查看下表以了解可以在消息中使用的不同参数。如果用户未提供参数拉出的信息，那么会显示为空。

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 密码更改参数</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> 显示新密码生效的时间。</td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> 显示请求更改密码的 IP 地址。</td>
    </tr>
  </table>

  您还可以使用[欢迎消息](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome)部分中列出的消息参数。
  {: tip}

4. 单击**保存**。




## 使用定制电子邮件发件人
{: #cd-custom-email}

通过 {{site.data.keyword.appid_short_notm}}，可以定义定制扩展点，以发送 Cloud Directory 电子邮件消息。通过定义扩展点，您可以全面控制电子邮件发送方式，并且可以使用您自己的域名。
 缺省情况下，{{site.data.keyword.appid_short_notm}} 使用 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 作为邮件传递服务。
 {: shortdesc}

出于以下原因，您可能希望使用定制电子邮件发件人：

- **个性化域**
通过配置定制电子邮件分派器，可以全面控制电子邮件发送方式。这包括定制电子邮件域，通过定制，可进一步降低电子邮件被当成垃圾邮件过滤掉的机率。此外，还可以进一步增强应用程序用户的品牌体验。

- **洞察和故障诊断**
通过电子邮件提供者获得洞察，例如：打开电子邮件的人数或哪些消息未传递。由于您可以跟踪各个消息，并且可以查看总体统计信息，因此这可以帮助解决问题。

配置了扩展点之后，每当需要发送电子邮件时，{{site.data.keyword.appid_short_notm}} 都会调用该扩展点。此扩展点包含有关消息的所有信息，包括电子邮件正文的最终内容。



### 配置定制发件人
{: #cd-messages-configure-custom-sender}

要配置定制电子邮件发件人，必须使用 Cloud Directory <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher" target="_blank">管理 API</a>。


1. 提供 URL。此外，还可以提供授权信息。支持的授权类型为：`基本授权`或`常量授权头值`。

  有效配置示例：
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

2. 配置可以侦听发布请求的扩展点。此端点应能够读取来自 {{site.data.keyword.appid_short_notm}} 的有效内容，并通过定制电子邮件发件人发送电子邮件。

3. {{site.data.keyword.appid_short_notm}} 发送的主体采用以下格式：`{"jws": "jws-format-string"}`。解码并验证有效内容后，内容为 JSON 字符串。

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
      <th>变量 </th>
      <th>描述</th>
    </tr>
    <tr>
      <td><code>tenant</code></td>
      <td>{{site.data.keyword.appid_short_notm}} 实例的租户标识。</td>
    </tr>
    <tr>
      <td><code>iat</code></td>
      <td>发送消息时的时间戳记。</td>
    </tr>
    <tr>
      <td><code>iss</code></td>
      <td>发出 JWS 令牌的主体或 {{site.data.keyword.appid_short_notm}} 实例。</td>
    </tr>
    <tr>
      <td><code>jti</code></td>
      <td>唯一事务标识。</td>
    </tr>
    <tr>
      <td><code>message: to</code></td>
      <td>消息收件人的电子邮件地址。</td>
    </tr>
    <tr>
      <td><code>message: from</code></br><code>name</code></br><code>address</code></td>
      <td></br>消息发件人的姓名。</br>发件人的电子邮件地址。</td>
    </tr>
    <tr>
      <td><code>可选：message: reply to</code></br><code>name</code></br><code>address</code></td>
      <td></br>附加到回复电子邮件地址的姓名。</br>用户可以回复的电子邮件地址。</td>
    </tr>
  </table>

  可以通过检查响应状态码来验证请求是否成功。范围在 200 - 299 内的任何状态码都视为成功。如果收到其他任何响应，请重试发出请求。
  {: tip}

4. 对于从 {{site.data.keyword.appid_short_notm}} 发送的每个 HTTP 有效内容，都会使用非对称密钥对根据 JWS 标准自动对其签名。对于每个 {{site.data.keyword.appid_short_notm}} 实例，会生成不在其他实例中共享的专用密钥和公用密钥。专用密钥用于对 HTTP 有效内容签名，并且可以使用公用密钥来验证有效内容是否由 {{site.data.keyword.appid_short_notm}} 生成，并且未被第三方<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys" target="_blank">公用密钥端点</a>变更。

5. 扩展点的示例代码 (JavaScript)。
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

6. 通过测试电子邮件分派器来验证配置是否已正确设置。使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">测试 API</a> 可触发对已配置的定制电子邮件发件人的请求。

有关完整的有效示例，请参阅 <a href="https://www.ibm.com/cloud/blog/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users" target="_blank">Use your own provider for mail sent with {{site.data.keyword.appid_full}}</a>。



## 支持的语言
{: #cd-languages}

您可以使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">语言管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>来设置可编写用户通信的语言。但是，仅英语开箱即用。您负责翻译消息。在使用 API 设置配置后，GUI 将更新，从而使您能够更改模板文本。
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>代码</th>
    <th>语言</th>
    <th>区域</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>南非荷兰语</td>
    <td>南非</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>阿尔巴尼亚语</td>
    <td>阿尔巴尼亚</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>阿姆哈拉语</td>
    <td>埃塞俄比亚</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>阿拉伯语</td>
    <td>阿尔及利亚</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>阿拉伯语</td>
    <td>巴林</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>阿拉伯语</td>
    <td>埃及</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>阿拉伯语</td>
    <td>伊拉克</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>阿拉伯语</td>
    <td>约旦</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>阿拉伯语</td>
    <td>科威特</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>阿拉伯语</td>
    <td>黎巴嫩</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>阿拉伯语</td>
    <td>利比亚</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>阿拉伯语</td>
    <td>毛里塔尼亚</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>阿拉伯语</td>
    <td>摩洛哥</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>阿拉伯语</td>
    <td>阿曼</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>阿拉伯语</td>
    <td>卡塔尔</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>阿拉伯语</td>
    <td>沙特阿拉伯</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>阿拉伯语</td>
    <td>叙利亚</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>阿拉伯语</td>
    <td>突尼斯</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>阿拉伯语</td>
    <td>阿拉伯联合酋长国</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>阿拉伯语</td>
    <td>也门</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>亚美尼亚语</td>
    <td>亚美尼亚</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>阿萨姆语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>阿塞拜疆语</td>
    <td>阿塞拜疆</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>巴斯克语</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>白俄罗斯语</td>
    <td>白俄罗斯</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>孟加拉语</td>
    <td>孟加拉国</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>白俄罗斯语</td>
    <td>白俄罗斯</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>孟加拉语</td>
    <td>孟加拉国</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>孟加拉语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>波斯尼亚语</td>
    <td>波斯尼亚</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>保加利亚语</td>
    <td>保加利亚</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>缅甸语</td>
    <td>缅甸</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>加泰隆尼亚语</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>简体中文</td>
    <td>中国</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>简体中文</td>
    <td>新加坡</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>繁体中文</td>
    <td>中国香港特别行政区</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>繁体中文</td>
    <td>中国澳门特别行政区</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>繁体中文</td>
    <td>台湾</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>克罗地亚语</td>
    <td>克罗地亚</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>捷克语</td>
    <td>捷克共和国</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>丹麦语</td>
    <td>丹麦</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>荷兰语</td>
    <td>比利时</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>荷兰语</td>
    <td>荷兰</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>英语</td>
    <td>澳大利亚</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>英语</td>
    <td>比利时</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>英语</td>
    <td>喀麦隆</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>英语</td>
    <td>加拿大</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>英语</td>
    <td>加纳</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>英语</td>
    <td>中国香港特别行政区</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>英语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>英语</td>
    <td>爱尔兰</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>英语</td>
    <td>肯尼亚</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>英语</td>
    <td>毛里求斯</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>英语</td>
    <td>新西兰</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>英语</td>
    <td>尼日利亚</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>英语</td>
    <td>菲律宾</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>英语</td>
    <td>新加坡</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>英语</td>
    <td>南非</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>英语</td>
    <td>坦桑尼亚</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>英语</td>
    <td>英国</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>英语</td>
    <td>美国</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>英语</td>
    <td>赞比亚</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>英语</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>爱沙尼亚语</td>
    <td>爱沙尼亚</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>菲律宾语</td>
    <td>菲律宾</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>芬兰语</td>
    <td>芬兰</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>法语</td>
    <td>阿尔及利亚</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>法语</td>
    <td>喀麦隆</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>法语</td>
    <td>刚果民主共和国</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>法语</td>
    <td>比利时</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>法语</td>
    <td>加拿大</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>法语</td>
    <td>法国</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>法语</td>
    <td>科特迪瓦</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>法语</td>
    <td>卢森堡</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>法语</td>
    <td>毛里塔尼亚</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>法语</td>
    <td>毛里求斯</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>法语</td>
    <td>摩洛哥</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>法语</td>
    <td>塞内加尔</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>法语</td>
    <td>瑞士</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>法语</td>
    <td>突尼斯</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>加利西亚语</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>干达语</td>
    <td>乌干达</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>格鲁吉亚语</td>
    <td>格鲁吉亚</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>德语</td>
    <td>奥地利</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>德语</td>
    <td>德国</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>德语</td>
    <td>卢森堡</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>德语</td>
    <td>瑞士</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>希腊语</td>
    <td>希腊</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>古吉拉特语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>蒙撒语</td>
    <td>尼日利亚</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>希伯莱语</td>
    <td>以色列</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>印度语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>匈牙利语</td>
    <td>匈牙利</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>冰岛语</td>
    <td>冰岛</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>伊博语</td>
    <td>尼日利亚</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>印度尼西亚语</td>
    <td>印度尼西亚</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>意大利语</td>
    <td>意大利</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>意大利语</td>
    <td>瑞士</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>日语</td>
    <td>日本</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>卡纳达语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>哈萨克语</td>
    <td>哈萨克斯坦</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>高棉语</td>
    <td>柬埔寨</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>卢旺达语</td>
    <td>卢旺达</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>孔卡尼语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>韩语</td>
    <td>韩国</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>立陶宛语</td>
    <td>立陶宛</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>拉脱维亚语</td>
    <td>拉脱维亚</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>高棉语</td>
    <td>柬埔寨</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>马其顿语</td>
    <td>马其顿</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>马来西亚拉丁语</td>
    <td>马来西亚</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>马拉雅拉姆语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>马耳他语</td>
    <td>马耳他</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>马拉地语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>蒙古斯拉夫语</td>
    <td>蒙古</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>尼泊尔语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>尼泊尔语</td>
    <td>尼泊尔</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>挪威语</td>
    <td>挪威</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>西挪威语</td>
    <td>挪威</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>奥里雅语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>奥罗莫语</td>
    <td>埃塞俄比亚</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>波兰语</td>
    <td>波兰</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>葡萄牙语 </td>
    <td>安哥拉</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>葡萄牙语 </td>
    <td>巴西</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>葡萄牙语 </td>
    <td>中国澳门特别行政区</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>葡萄牙语 </td>
    <td>莫桑比克</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>葡萄牙语 </td>
    <td>葡萄牙</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>旁遮普语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>罗马尼亚语</td>
    <td>罗马尼亚</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>俄语</td>
    <td>俄罗斯</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>塞尔维亚西里尔语</td>
    <td>塞尔维亚</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>塞尔维亚拉丁语</td>
    <td>黑山共和国</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>塞尔维亚拉丁语</td>
    <td>塞尔维亚</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>锡兰语</td>
    <td>斯里兰卡</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>斯洛伐克语</td>
    <td>斯洛伐克</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>斯诺文尼亚语</td>
    <td>斯洛文尼亚</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>西班牙语</td>
    <td>阿根廷</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>西班牙语</td>
    <td>玻利维亚</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>西班牙语</td>
    <td>智利</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>西班牙语</td>
    <td>哥伦比亚</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>西班牙语</td>
    <td>哥斯达黎加</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>西班牙语</td>
    <td>多米尼加共和国</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>西班牙语</td>
    <td>厄瓜多尔</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>西班牙语</td>
    <td>萨尔瓦多</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>西班牙语</td>
    <td>危地马拉</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>西班牙语</td>
    <td>洪都拉斯</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>西班牙语</td>
    <td>墨西哥</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>西班牙语</td>
    <td>尼加拉瓜</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>西班牙语</td>
    <td>巴拿马</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>西班牙语</td>
    <td>巴拉圭</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>西班牙语</td>
    <td>秘鲁</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>西班牙语</td>
    <td>波多黎各</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>西班牙语</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>西班牙语</td>
    <td>美国</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>西班牙语</td>
    <td>乌拉圭</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>西班牙语</td>
    <td>委内瑞拉</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>斯瓦希里语</td>
    <td>肯尼亚</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>斯瓦希里语</td>
    <td>坦桑尼亚</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>瑞典语</td>
    <td>瑞典</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>泰米尔语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>泰卢固语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>泰语</td>
    <td>泰国</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>土耳其语</td>
    <td>土耳其</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>乌克兰语</td>
    <td>乌克兰</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>乌尔都语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>乌尔都语</td>
    <td>巴基斯坦</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>乌兹别克西里尔语</td>
    <td>乌兹别克斯坦</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>乌兹别克拉丁语</td>
    <td>乌兹别克斯坦</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>越南语</td>
    <td>越南</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>威尔士语</td>
    <td>英国</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>约鲁巴语</td>
    <td>尼日利亚</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>祖鲁语</td>
    <td>南非</td>
  </tr>
</table>
