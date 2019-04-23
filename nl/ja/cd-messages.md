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

# E メールのカスタマイズ
{: #cd-types}

ユーザーがアプリケーションと対話するときに、ユーザーに応答を送信したい場合や、検証を求めたい場合があります。{{site.data.keyword.appid_short_notm}} には、対話に使用できるデフォルトのテンプレートが用意されています。これらのテンプレートをガイドとして使用して、ブランドに合わせてメッセージングをカスタマイズすることもできます。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} は <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> をメール配信サービスとして使用します。 すべての E メールは、単一の SendGrid アカウントを使用して送信されます。
{: note}

## E メール・テンプレート
{: #cd-messages}

ユーザーにメッセージを送信する場合、以下のテンプレートの任意の組み合わせを使用できます。あるいは、テンプレートを編集してメッセージをカスタマイズすることもできます。
{: shortdesc}

以下のメッセージ・タイプに加えて、[SSO](/docs/services/appid?topic=appid-cd-sso#cd-sso) 用テンプレートと [MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) 用テンプレートを利用することもできます。
{: tip}

メッセージをさらにカスタマイズするために、メッセージ内でパラメーターを使用できます。次の表を参照して、すべてのメッセージ・タイプで使用できるパラメーターを確認してください。

<table>
  <tr>
    <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> すべてのメッセージ・パラメーター </th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> ログイン・ウィジェットのために構成したイメージを表示します。</td>
  </tr>
  <tr>
    <td><code>%{user.displayName}</code></td>
    <td> アプリとやり取りするときに使用する、ユーザーが選択した画面名を表示します。</td>
  </tr>
  <tr>
    <td><code>%{user.email}</code></td>
    <td> ユーザーが登録した E メール・アドレスを表示します。</td>
  </tr>
  <tr>
    <td><code>%{user.username}</code></td>
    <td> 認証方式がユーザー名とパスワードに設定されているとき、ユーザーが指定したユーザー名を表示します。 </td>
  </tr>
  <tr>
    <td><code>%{user.firstName}</code></td>
    <td> ユーザーが指定した名を表示します。 </td>
  </tr>
  <tr>
    <td><code>%{user.formattedName}</code></td>
    <td> ユーザーのフルネームを表示します。 </td>
  </tr>
  <tr>
    <td><code>%{user.lastName}</code></td>
    <td> ユーザーが指定した姓を表示します。 </td>
  </tr>
</table>


### E メール: ようこそ
{: #cd-messages-welcome}

ユーザーがアプリケーションに登録するときに、アプリのウェルカム・メッセージをユーザーに送信したい場合があります。
{: shortdesc}

1. サービス・ダッシュボードの**「ワークフロー・テンプレート (Workflow templates)」>「ようこそ E メール (Welcome email)」**タブにナビゲートします。

2. **「ようこそ E メール (Welcome email)」**を**「有効」**に設定します。

3. メッセージの内容をカスタマイズします。UI を使用して、パラメーターを追加したり、画像を挿入したりできます。メッセージの[言語](/docs/services/appid?topic=appid-cd-messages#cd-languages)を変更するには、<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して言語を設定します。ただし、メッセージの内容と翻訳については、ご自身の責任になります。次の表を参照して、このメッセージで使用できる表および送信できる他のすべてのメッセージのリストを確認してください。パラメーターによってプルされた情報をユーザーが指定していない場合は、ブランクとして表示されます。

4. **「保存」**をクリックします。


### E メール: 検証
{: #cd-messages-verification}

ユーザーが E メールを使用してアプリケーションに登録するとき、アイデンティティーの確認を求める E メールをユーザーに送信できます。検証を要求することで、アプリに登録されるおそれのある偽アカウントの数を抑制します。 ユーザーが E メールを検証するまでアプリへのアクセスを制限したり、プロファイルを作成する対象ユーザーを管理する手段として利用したりできます。 なお、{{site.data.keyword.appid_short_notm}} ダッシュボードまたはユーザー作成 API を使用して手動で追加されたユーザーは、この E メールを自動受信しません。
{: shortdesc}


1. サービス・ダッシュボードの**「ワークフロー・テンプレート (Workflow templates)」>「E メール検証 (Email verification)」**タブにナビゲートします。

2. **「E メール検証 (Email verification)」**を**「有効」**に設定します。

3. **「最初にユーザーの E メール・アドレスを検証せずに、ユーザーがアプリケーションにサインインできるようにする」**を**「はい」**に設定します。 「はい」に設定すると、ユーザーは登録後、E メール・アドレスを検証する前に、アプリケーションと対話できるようになります。デフォルト設定は「いいえ」です。

4. メッセージの内容をカスタマイズします。UI を使用して、パラメーターを追加したり、画像を挿入したりできます。メッセージの[言語](/docs/services/appid?topic=appid-cd-messages#cd-languages)を変更するには、<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して言語を設定します。ただし、メッセージの内容と翻訳については、ご自身の責任になります。次の表を参照して、メッセージで使用できるさまざまなパラメーターを確認してください。パラメーターによってプルされた情報をユーザーが指定していない場合は、ブランクとして表示されます。

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> 検証メッセージ・パラメーター</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> リンクが有効な時間数を表示します。 </td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td> リンクが有効な分数を表示します。 </td>
    </tr>
    <tr>
      <td><code>%{verify.code}</code></td>
      <td> ワンタイム検証 URL を表示します。 </td>
    </tr>
    <tr>
      <td><code>%{verify.link}</code></td>
      <td> 設定で指定したアクション URL を表示します。 </td>
    </tr>
  </table>

  [ウェルカム・メッセージ](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome)のセクションにリストされているメッセージ・パラメーターを使用することもできます。
  {: tip}

5. アクション URL の有効期限時間を定義します。URL の有効期限は分単位の時間であり、ユーザーはこの時間内にアクションを完了する必要があります。この時間が経過すると、検証リンクが期限切れになります。この設定は、パスワード再設定リンクが有効である時間にも影響します。
 
6. E メールをユーザーが検証した後に表示するページの URL を、**「Thank you ページの URL (Thank you page URL)」**ボックスに入力します。このフィールドをブランクのままにしておくことを選択した場合は、{{site.data.keyword.appid_short_notm}} のデフォルト・ページが表示されます。

7. **「保存」**をクリックします。 


### E メール: パスワードの再設定
{: #cd-messages-reset}

ユーザーは、アプリと対話するときに、パスワードを忘れている場合や、それとは別にパスワードを更新する必要がある場合があります。その要求に対する E メール応答をカスタマイズすることができます。ユーザーがパスワードの変更を要求しても、ユーザーがこの E メール内のリンクをクリックするまでパスワードは変更されません。
{: shortdesc}


1. サービス・ダッシュボードの**「ワークフロー・テンプレート (Workflow templates)」>「パスワードのリセット」**タブにナビゲートします。

2. **「パスワードを忘れた場合の E メール (Forgot password email)」**を**「有効」**に設定します。

3. メッセージの内容をカスタマイズします。UI を使用して、パラメーターを追加したり、画像を挿入したりできます。メッセージの[言語](/docs/services/appid?topic=appid-cd-messages#cd-languages)を変更するには、<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して言語を設定します。ただし、メッセージの内容と翻訳については、ご自身の責任になります。次の表を参照して、メッセージで使用できるさまざまなパラメーターを確認してください。パラメーターによってプルされた情報をユーザーが指定していない場合は、ブランクとして表示されます。

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> パスワード再設定パラメーター</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> リンクが有効な時間数を表示します。</td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td>リンクが有効な分数を表示します。</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.code}</code></td>
      <td> URL の一部としてワンタイム・パスコードを表示します。 ユーザーごとに異なるコードになります。 例: <code>https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478</code></td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> パスワードをリセットするためにユーザーがクリックするリンクを表示します。</td>
    </tr>
  </table>

  [ウェルカム・メッセージ](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome)のセクションにリストされているメッセージ・パラメーターを使用することもできます。
  {: tip}

4. アクション URL の有効期限時間を定義します。URL の有効期限は分単位の時間であり、ユーザーはこの時間内にアクションを完了する必要があります。この時間が経過すると、検証リンクが期限切れになります。この設定は、パスワード再設定リンクが有効である時間にも影響します。
 
5. E メールをユーザーが検証した後に表示するページの URL を、**「パスワード再設定ページの URL (Reset password page URL)」**ボックスに入力します。このフィールドをブランクのままにしておくことを選択した場合は、{{site.data.keyword.appid_short_notm}} のデフォルト・ページが表示されます。

6. **「保存」**をクリックします。


### E メール: パスワードの変更
{: #cd-messages-password-change}

パスワードが更新されたときにユーザーに通知することができます。 これは、ユーザーがパスワードの変更を要求しなかった場合に役立ちます。 ユーザーは適切な手順に沿って、アカウントを再びセキュアにすることができます。
{: shortdesc}

1. サービス・ダッシュボードの**「ワークフロー・テンプレート (Workflow templates)」>「パスワードの変更 (Password change)」**タブにナビゲートします。

2. **「パスワードが変更された場合の E メール (Password changed email)」**を**「有効」**に設定します。

3. メッセージの内容をカスタマイズします。UI を使用して、パラメーターを追加したり、画像を挿入したりできます。メッセージの[言語](/docs/services/appid?topic=appid-cd-messages#cd-languages)を変更するには、<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して言語を設定します。ただし、メッセージの内容と翻訳については、ご自身の責任になります。次の表を参照して、メッセージで使用できるさまざまなパラメーターを確認してください。パラメーターによってプルされた情報をユーザーが指定していない場合は、ブランクとして表示されます。

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> パスワード変更パラメーター</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> 新規パスワードが有効になった時刻を表示します。 </td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> パスワード変更の要求元となった IP アドレスを表示します。 </td>
    </tr>
  </table>

  [ウェルカム・メッセージ](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome)のセクションにリストされているメッセージ・パラメーターを使用することもできます。
  {: tip}

4. **「保存」**をクリックします。




## カスタム E メール送信者の使用
{: #cd-custom-email}

{{site.data.keyword.appid_short_notm}} では、クラウド・ディレクトリーの E メール・メッセージを送信するためのカスタム拡張ポイントを定義できます。 拡張ポイントを定義することにより、E メールの送信方法を自由に制御でき、独自のドメイン・ネームを使用できます。 デフォルトでは、{{site.data.keyword.appid_short_notm}} は <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> をメール配信サービスとして使用します。
 {: shortdesc}

以下の理由で、カスタム E メール送信者を使用したい場合があります。

- **個別設定ドメイン**
カスタム E メール・ディスパッチャーを構成すると、E メール・メッセージの送信方法を自由に制御できます。 例えば、E メール・ドメインをカスタマイズすることで、E メールがスパムとしてフィルタリングされる可能性を少なくすることができます。 アプリ・ユーザーのブランド・エクスペリエンスをさらに向上させることもできます。

- **洞察とトラブルシューティング**
E メール・プロバイダーから洞察が得られます。例えば、E メールを開封したユーザーの数や、配信されなかったメッセージを特定できます。 個々のメッセージを追跡し、全般的な統計を確認できるので、問題の解決に役立ちます。

拡張ポイントを構成した後は、E メール・メッセージを送信する必要が生じるたびに、{{site.data.keyword.appid_short_notm}} によって拡張ポイントが呼び出されます。 この拡張ポイントには、メッセージに関するすべての情報 (E メール本文の最後のコンテンツを含む) が格納されます。



### カスタム送信者の構成
{: #cd-messages-configure-custom-sender}

カスタム E メール送信者を構成するには、Cloud Directory の<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher" target="_blank">管理 API</a> を使用する必要があります。


1. URL を指定します。また、許可情報を指定することもできます。 サポートされる許可タイプは、`Basic authorization` または `constant authorization header value` です。

  有効な構成例を以下に示します。
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

2. POST 要求を listen できる拡張ポイントを構成します。 このエンドポイントは、{{site.data.keyword.appid_short_notm}} からのペイロードを読み取り、カスタム E メール送信者で E メールを送信することができるものでなければなりません。

3. {{site.data.keyword.appid_short_notm}} から送信される本体の形式は、`{"jws": "jws-format-string"}` です。 ペイロードをデコードして確認した後のコンテンツは JSON 文字列です。

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
      <th>変数</th>
      <th>説明</th>
    </tr>
    <tr>
      <td><code> tenant </code></td>
      <td>{{site.data.keyword.appid_short_notm}} インスタンスのテナント ID。</td>
    </tr>
    <tr>
      <td><code> iat </code></td>
      <td>メッセージが送信されたときのタイム・スタンプ。</td>
    </tr>
    <tr>
      <td><code>jss</code></td>
      <td>JWS トークンを発行した原則。</td>
    </tr>
    <tr>
      <td><code>jti</code></td>
      <td>固有トランザクション ID。</td>
    </tr>
    <tr>
      <td><code>message: to</code></td>
      <td>メッセージの受信者の E メール・アドレス。</td>
    </tr>
    <tr>
      <td><code>message: from</code></br><code>name</code></br><code>address</code></td>
      <td></br>メッセージの送信者の名前。</br>送信者の E メール・アドレス。</td>
    </tr>
    <tr>
      <td><code>オプション: message: reply to</code></br><code>name</code></br><code>address</code></td>
      <td></br>応答 E メール・アドレスに付加する名前。</br>ユーザーの応答先になる E メール・アドレス。</td>
    </tr>
  </table>

  応答状況コードを調べて、要求が成功したことを確認できます。 200 から 299 の範囲の応答はすべて、成功と見なされます。 他の応答を受け取った場合は、要求を再試行してください。
  {: tip}

4. {{site.data.keyword.appid_short_notm}} から送信されるすべての HTTP ペイロードは、非対称鍵ペアを使用して、JWS 標準に従って自動的に署名されます。
{{site.data.keyword.appid_short_notm}} インスタンスごとに、他のインスタンスとの間で共有されない秘密鍵と公開鍵が生成されます。 秘密鍵は、HTTP ペイロードに署名するために使用されます。公開鍵は、ペイロードが {{site.data.keyword.appid_short_notm}} によって生成されたこと、およびサード・パーティーの<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys" target="_blank">公開鍵エンドポイント</a>によって変更されていないことを確認するために使用できます。

5. 拡張ポイントのサンプル・コード (JavaScript) を以下に示します。
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

6. E メール・ディスパッチャーをテストして、構成が正しくセットアップされていることを確認します。 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">テスト API</a> を使用して、構成済みのカスタム E メール送信者への要求をトリガーしてください。

操作の例全体については、<a href="https://www.ibm.com/blogs/bluemix/2018/10/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users/" target="_blank">Use your own provider for mail sent with {{site.data.keyword.appid_full}}</a> を参照してください。



## サポートされる言語
{: #cd-languages}

<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">言語管理 API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して、ユーザー通信を記述するための言語を設定できます。 ただし、すぐに使用できるのは英語だけです。 メッセージの翻訳については、お客様の責任となります。 API を使用して構成を設定した後、テンプレート・テキストを変更できるように GUI が更新されます。
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>コード</th>
    <th>言語</th>
    <th>地域</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>アフリカーンス語</td>
    <td>南アフリカ</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>アルバニア語</td>
    <td>アルバニア</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>アムハラ語</td>
    <td>エチオピア</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>アラビア語</td>
    <td>アルジェリア</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>アラビア語</td>
    <td>バーレーン</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>アラビア語</td>
    <td>エジプト</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>アラビア語</td>
    <td>イラク</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>アラビア語</td>
    <td>ヨルダン</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>アラビア語</td>
    <td>クウェート</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>アラビア語</td>
    <td>レバノン</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>アラビア語</td>
    <td>リビア</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>アラビア語</td>
    <td>モーリタニア</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>アラビア語</td>
    <td>モロッコ</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>アラビア語</td>
    <td>オマーン</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>アラビア語</td>
    <td>カタール</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>アラビア語</td>
    <td>サウジアラビア</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>アラビア語</td>
    <td>シリア</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>アラビア語</td>
    <td>チュニジア</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>アラビア語</td>
    <td>アラブ首長国連邦</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>アラビア語</td>
    <td>イエメン</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>アルメニア語</td>
    <td>アルメニア</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>アッサム語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>アゼルバイジャン語</td>
    <td>アゼルバイジャン</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>バスク語</td>
    <td>スペイン</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>ベラルーシ語</td>
    <td>ベラルーシ</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>ベンガル語</td>
    <td>バングラデシュ</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>ベラルーシ語</td>
    <td>ベラルーシ</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>ベンガル語</td>
    <td>バングラデシュ</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>ベンガル語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>ボスニア語</td>
    <td>ボスニア</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>ブルガリア語</td>
    <td>ブルガリア</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>ビルマ語</td>
    <td>ミャンマー</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>カタロニア語</td>
    <td>スペイン</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>中国語 (簡体字)</td>
    <td>中国</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>中国語 (簡体字)</td>
    <td>シンガポール</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>中国語 (繁体字)</td>
    <td>中華人民共和国香港特別行政区</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>中国語 (繁体字)</td>
    <td>中華人民共和国マカオ特別行政区</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>中国語 (繁体字)</td>
    <td>台湾</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>クロアチア語</td>
    <td>クロアチア</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>チェコ語</td>
    <td>チェコ共和国</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>デンマーク語</td>
    <td>デンマーク</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>オランダ語</td>
    <td>ベルギー</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>オランダ語</td>
    <td>オランダ</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>英語</td>
    <td>オーストラリア</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>英語</td>
    <td>ベルギー</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>英語</td>
    <td>カメルーン</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>英語</td>
    <td>カナダ</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>英語</td>
    <td>ガーナ</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>英語</td>
    <td>中華人民共和国香港特別行政区</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>英語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>英語</td>
    <td>アイルランド</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>英語</td>
    <td>ケニア</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>英語</td>
    <td>モーリシャス</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>英語</td>
    <td>ニュージーランド</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>英語</td>
    <td>ナイジェリア</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>英語</td>
    <td>フィリピン</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>英語</td>
    <td>シンガポール</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>英語</td>
    <td>南アフリカ</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>英語</td>
    <td>タンザニア</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>英語</td>
    <td>英国</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>英語</td>
    <td>米国</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>英語</td>
    <td>ザンビア</td>
  </tr>
  <tr>
    <td><code>     en
    </code></td>
    <td>英語</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>エストニア語</td>
    <td>エストニア</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>フィリピン語</td>
    <td>フィリピン</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>フィンランド語</td>
    <td>フィンランド</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>フランス語</td>
    <td>アルジェリア</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>フランス語</td>
    <td>カメルーン</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>フランス語</td>
    <td>コンゴ民主共和国</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>フランス語</td>
    <td>ベルギー</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>フランス語</td>
    <td>カナダ</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>フランス語</td>
    <td>フランス</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>フランス語</td>
    <td>象牙海岸 (コートジボアール)</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>フランス語</td>
    <td>ルクセンブルグ</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>フランス語</td>
    <td>モーリタニア</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>フランス語</td>
    <td>モーリシャス</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>フランス語</td>
    <td>モロッコ</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>フランス語</td>
    <td>セネガル</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>フランス語</td>
    <td>スイス</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>フランス語</td>
    <td>チュニジア</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>ガリシア語</td>
    <td>スペイン</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>ガンダ語</td>
    <td>ウガンダ</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>ジョージア語</td>
    <td>ジョージア</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>ドイツ語</td>
    <td>オーストリア</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>ドイツ語</td>
    <td>ドイツ</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>ドイツ語</td>
    <td>ルクセンブルグ</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>ドイツ語</td>
    <td>スイス</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>ギリシャ語</td>
    <td>ギリシャ</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>グジャラート語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>ハウサ語</td>
    <td>ナイジェリア</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>ヘブライ語</td>
    <td>イスラエル</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>ヒンディ語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>ハンガリー語</td>
    <td>ハンガリー</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>アイスランド語</td>
    <td>アイスランド</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>イボ語</td>
    <td>ナイジェリア</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>インドネシア語</td>
    <td>インドネシア</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>イタリア語</td>
    <td>イタリア</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>イタリア語</td>
    <td>スイス</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>日本語</td>
    <td>日本</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>カンナダ語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>カザフ語</td>
    <td>カザフスタン</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>クメール語</td>
    <td>カンボジア</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>キンヤルワンダ語</td>
    <td>ルワンダ</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>コンカニー語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>韓国語</td>
    <td>韓国</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>リトアニア語</td>
    <td>リトアニア</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>ラトビア語</td>
    <td>ラトビア</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>クメール語</td>
    <td>カンボジア</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>マケドニア語</td>
    <td>マケドニア</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>マレー語ローマ字</td>
    <td>マレーシア</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>マラヤーラム語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>マルタ語</td>
    <td>マルタ</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>マラーティー語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>モンゴル語キリル文字</td>
    <td>モンゴル</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>ネパール語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>ネパール語</td>
    <td>ネパール</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>ノルウェー語ブークモール</td>
    <td>ノルウェー</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>ノルウェー語ニーノシュク</td>
    <td>ノルウェー</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>オリヤー語 (オディア語)</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>オロモ語</td>
    <td>エチオピア</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>ポーランド語</td>
    <td>ポーランド</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>ポルトガル語</td>
    <td>アンゴラ</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>ポルトガル語</td>
    <td>ブラジル</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>ポルトガル語</td>
    <td>中華人民共和国マカオ特別行政区</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>ポルトガル語</td>
    <td>モザンビーク</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>ポルトガル語</td>
    <td>ポルトガル</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>パンジャブ語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>ルーマニア語</td>
    <td>ルーマニア</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>ロシア語</td>
    <td>ロシア</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>セルビア語キリル文字</td>
    <td>セルビア</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>セルビア語ローマ字</td>
    <td>モンテネグロ</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>セルビア語ローマ字</td>
    <td>セルビア</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>シンハラ語</td>
    <td>スリランカ</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>スロバキア語</td>
    <td>スロバキア</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>スロベニア語</td>
    <td>スロベニア</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>スペイン語</td>
    <td>アルゼンチン</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>スペイン語</td>
    <td>ボリビア</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>スペイン語</td>
    <td>チリ</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>スペイン語</td>
    <td>コロンビア</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>スペイン語</td>
    <td>コスタリカ</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>スペイン語</td>
    <td>ドミニカ共和国</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>スペイン語</td>
    <td>エクアドル</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>スペイン語</td>
    <td>エルサルバドル</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>スペイン語</td>
    <td>グアテマラ</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>スペイン語</td>
    <td>ホンジュラス</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>スペイン語</td>
    <td>メキシコ</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>スペイン語</td>
    <td>ニカラグア</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>スペイン語</td>
    <td>パナマ</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>スペイン語</td>
    <td>パラグアイ</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>スペイン語</td>
    <td>ペルー</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>スペイン語</td>
    <td>プエルトリコ</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>スペイン語</td>
    <td>スペイン</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>スペイン語</td>
    <td>米国</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>スペイン語</td>
    <td>ウルグアイ</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>スペイン語</td>
    <td>ベネズエラ</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>スワヒリ語</td>
    <td>ケニア</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>スワヒリ語</td>
    <td>タンザニア</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>スウェーデン語</td>
    <td>スウェーデン</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>タミール語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>テルグ語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>タイ語</td>
    <td>タイ</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>トルコ語</td>
    <td>トルコ</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>ウクライナ語</td>
    <td>ウクライナ</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>ウルドゥー語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>ウルドゥー語</td>
    <td>パキスタン</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>ウズベク語キリル文字</td>
    <td>ウズベキスタン</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>ウズベク語ローマ字</td>
    <td>ウズベキスタン</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>ベトナム語</td>
    <td>ベトナム</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>ウェールズ語</td>
    <td>英国</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>ヨルバ語</td>
    <td>ナイジェリア</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>ズールー語</td>
    <td>南アフリカ</td>
  </tr>
</table>
