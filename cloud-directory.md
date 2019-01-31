---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Cloud Directory
{: #cd}

With {{site.data.keyword.appid_full}}, users can sign up and sign in to your mobile and web apps by using an email or username and a password. A cloud directory is a user registry that is maintained in the cloud. When a user signs up for your app, they're added to your directory of users. With this feature, users have the freedom to manage their own account within your app.
{: shortdesc}

</br>

## Managing directory settings
{: #cd-settings}

You can configure the notifications and level of user control for your app. Setting up cloud directory can be done quickly, as shown in the following image. These settings can be updated at any time from the service dashboard.
{: shortdesc}


![Configuring cloud directory](images/cloud-directory.png)
Figure. The configuration journey for Cloud Directory

1. In the **Manage** tab of the {{site.data.keyword.appid_short_notm}} dashboard, be sure that Cloud Directory is set to **On**.

2. Configure your general settings.
  1. Decide whether you want your users to create a username or use their email when they sign in. Both options require a password. After users have been added to your directory, you can no longer toggle between the options.
  2. Click **Edit** in the password criteria row to specify any requirements that you want to put in place. Password criteria is given as regex. For help determining strength or to see common examples see, [Managing password strength](/docs/services/appid//cloud-directory.html#strength). Click **Save** to put your requirements into action.
  3. Set **Allow users to sign up to your app** to **Yes**. You can still add users through the console if it's set to **No**. However, you should add users through the console only for development purposes.
  4. Set **Allow users to manage their account from your app** to **Yes** if you want your users to be able to reset their password, change their password, or reset their details. If you want to limit your users self-service, set the value to **No**.
  5. Click **Edit** in the **Sender details** row to update your email settings. The email settings apply for all of the communication that is sent through {{site.data.keyword.appid_short_notm}}. Specify the email address that should send the email, their name, and leave a separate email for users to send a response.
  6. Enable **Advanced password policy** to create limitations and time requirements for your passwords. This feature requires additional billing. For more information about your options, see [Advanced password policy](/docs/services/appid/cloud-directory.html#advanced-password).
  6. Click **Save**.

3. Configure your verification email settings.
  1. To have your users verify their email address set **Email verification** to **On**. When a user signs up for your application, they receive an email that asks them to confirm that they've signed up for the app.
  2. If you've decided that you want your users to verify their email, your next decision is whether you want to allow users into your application before them verifying their email address. Depending on your preference, set **Allow users to sign in to your app without first verifying their email address** to **Yes** or **No**.
  3. Customize the content and design the appearance of your message. There is a template for the message, but you can update the text with your own message. You can use a [language](/docs/services/appid/cloud-directory.html#languages) other than English, but you are responsible for the translation of the text. To choose another language, use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#//Config/updateLocalization" target="_blank">language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
  4. Give the verification URL an expiration time limit, specified as minutes.  When this time is set here, it also affects the length of time that your reset password link is valid for.
  5. Enter your own verification page URL if you have a specific page that you want your users to see when they click the link. If you leave the **Custom verification page URL** field blank, a default verification page is provided by {{site.data.keyword.appid_short_notm}}.
  6. Click **Save**.

4. Configure your welcome email settings.
  1. To welcome users through email when they sign up for your app, set **Welcome email** to **On**.
  2. Customize the content and design the appearance of your message. There is an example message that you can use, but you can update the text with your own message. You can use a [language](/docs/services/appid/cloud-directory.html#languages) other than English, but you are responsible for the translation of the text. To choose another language, use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization" target="_blank">language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
  3. Click **Save**.

5. Configure your password reset settings.
  1. To allow users to request a reset of their password, set **Forgot password email** to **On**. **Note**: A user must have validated their email before reseting their password. This means that you must require email verification to allow password resets.
  2. Customize the content and design the appearance of your message. There is an example message that you can use, but you can update the text with your own message. You can use a [language](/docs/services/appid/cloud-directory.html#languages) other than English, but you are responsible for the translation of the text. To choose another language, use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization" target="_blank">language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
  3. Give the reset password URL an expiration time limit, specified as minutes. When this time is set here, it also affects the length of time that your email verification link is valid for.
  4. Enter your own password reset URL if you have a specific page that you want your users to see when they click the link. If you leave the **Reset password page URL** field blank, a default reset password page is provided by {{site.data.keyword.appid_short_notm}}.
  5. Click **Save**.

6. Configure your change password settings.
  1. To notify users about any changes made to their password, set **Password changed email** to **On**.
  2. Customize the content and design the appearance of your message. There is an example message that you can use, but you can update the text with your own message. You can use a [language](/docs/services/appid/cloud-directory.html#languages) other than English, but you are responsible for the translation of the text. To choose another language, use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization" target="_blank">language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
  3. Click **Save**.

7. Configure multifactor authentication.
  1. To require multifactor authentication on user sign in, set **Enable Email Multi-Factor Authentication** to **On**.
  2. Customize the content and design of your email using the template below. You can use a [language](/docs/services/appid/cloud-directory.html#languages) other than English, but you are responsible for the translation of the text. To choose another language, use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization" target="_blank">language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
  3. Click **Save**.

8. In the **Users** tab you can see who has signed-up for your app. Note: A single user can attempt to sign in up to 5 times in 60 seconds. If a sixth attempt is made, an error is displayed.

</br>
</br>

## Types of messages
{: #types}

You can send several types of messages to your users. You can choose to send the example message that is provided by the service or you can customize the content for a more personal app experience. {{site.data.keyword.appid_short_notm}} uses <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> as a mail delivery service. All emails are sent with a single SendGrid account.
{: shortdesc}

If a user does not supply the information pulled by the parameter, it appears blank.
{: tip}

<dl>
  <dt>Welcome</dt>
    <dd><p>After they've registered, you can welcome a user to your application via email. To welcome and retain your users, make your message as engaging as possible.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/> All message parameters </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> Displays the image that you configured for your login widget. </td>
        </tr>
        <tr>
          <td><code>%{user.displayName}</code></td>
          <td> Displays the screen name a user chose to use when interacting with the app. </td>
        </tr>
        <tr>
          <td><code>%{user.email}</code></td>
          <td> Displays the user's registered email address. </td>
        </tr>
        <tr>
          <td><code>%{user.username}</code></td>
          <td> Displays the user's specified username when the authentication method is set to username and password. </td>
        </tr>
        <tr>
          <td><code>%{user.firstName}</code></td>
          <td> Displays the user's specified given name. </td>
        </tr>
        <tr>
          <td><code>%{user.formattedName}</code></td>
          <td> Displays the user's full name. </td>
        </tr>
        <tr>
          <td><code>%{user.lastName}</code></td>
          <td> Displays the user's specified surname. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt>Forgot password</dt>
    <dd><p>A user can ask to have their password reset if they forget it or need to update it for any reason. You can customize the email response to their request. When a user requests a change, their password remains unchanged until they click the link in this email.</p>
    <table>
      <tr>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/> Forgot password parameters </th>
      </tr>
      <tr>
        <td><code>%{linkExpiration.hours}</code></td>
        <td> Displays the number of hours that the link is valid.</td>
      </tr>
      <tr>
        <td><code>%{linkExpiration.minutes}</code></td>
        <td>Displays the number of minutes that the link is valid.</td>
      </tr>
      <tr>
        <td><code>%{resetPassword.code}</code></td>
        <td> Displays a one-time passcode as part of the URL. This means that each person would have a different code. Example: <code>https://appid.cloud.ibm.com/wfm/verify/6574839563478</code> </td>
      </tr>
      <tr>
        <td><code>%{resetPassword.link}</code></td>
        <td> Displays the link that a user clicks to reset their password. </td>
      </tr>
     </tbody>
  </table></dd>
  <dt>Verification</dt>
    <dd><p>You can request that a user verifies their account via email. By requesting a verification, you limit the number of fake accounts that can sign up for your app. You can restrict access to your app until a user has verified their email, or use it as a way to manage which users you create profiles for. Note that users who are manually added via the {{site.data.keyword.appid_short_notm}} dashboard or the create user API do not automatically receive this email.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/> Verification message parameters </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> Displays the number of hours the link is valid. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> Displays the number of minutes the link is valid. </td>
        </tr>
        <tr>
          <td><code>%{verify.code}</code></td>
          <td> Displays a one-time verification URL. </td>
        </tr>
        <tr>
          <td><code>%{verify.link}</code></td>
          <td> Displays the action URL that you specified in settings. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt>Password change</dt>
    <dd><p>You can let a user know when their password has been updated. This is helpful if they did not request that their password be changed. They can take the proper steps to re-secure their account.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/> Password change parameters</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
          <td> Displays the time at which a new password went into effect. </td>
        </tr>
        <tr>
          <td><code>%{passwordChangeInfo.ipAddress}</code></td>
          <td> Displays the IP address from which the password change was requested. </td>
        </tr>
      </tbody>
    </table></dd>
    </dd>
    <dt>MFA Verification Code</dt>
      <dd><p>When multifactor authentication is enabled, users can receive challenge codes as a secondary means of authentication.</p>
      <table>
        <thead>
          <th colspan=2><img src="images/idea.png" alt="More information icon"/> All message parameters </th>
        </thead>
        <tbody>
          <tr>
            <td><code>%{mfa.code}</code></td>
            <td> Displays a one-time MFA verification code. </td>
          </tr>
        </tbody>
      </table></dd></dl>

</br>
</br>

## Managing password strength
{: #strength}

You can set the requirements for the passwords that can be used with Cloud Directory.
{: shortdesc}

A strong password makes it difficult, or even improbable for someone to guess the password in either a manual or automated way. Password strength is set as a regex string.

Some common password strength examples:

- Must be at least eight characters. Example regex: `^.{8,}$`
- Must contain one number, one lowercase letter, and one capital letter. Example regex: `^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Must contain only English letters and numbers. Example regex: `^[A-Za-z0-9]*$`
- Must be at least one unique character. Example regex: `^(\w)\w*?(?!\1)\w+$`

Password strength can be set in the Cloud Directory settings page in App ID Console, or by using <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/set_cloud_directory_password_regex" target="_blank">the management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

</br>


## Advanced password policy
{: #advanced-password}


You can enhance the security of your application by enforcing additional password constraints.
{: shortdesc}


Advanced password policy consists of 5 features that can each be toggled separately.

 - Lockout after repeated wrong credentials
 - Avoid password reuse
 - Password expiration
 - Minimum period between password changes
 - Ensure password does not include username


 If you enable this feature, additional billing for advanced security capabilities is activated. For more information see the [Pricing Calculator](/docs/services/appid/faq.html#pricing).

</br>

### Avoid Password Reuse
{: #avoid-reuse}

When your users are changing their password, you might want to prevent them from choosing a recently used password.
{: shortdesc}

By using the GUI or the API, you can choose the number of passwords that a user must have before they can repeat a previously used password. You can select any whole value between 1 and 10.

If this option is turned on, and one of your users attempts to set their password to one that was recently used by them, they are shown an error in the default sign in widget UI and are prompted to enter a different password.

Previous passwords are securely stored in the same way that a user's current password is stored.

</br>

### Lockout after repeated wrong credentials
{: #lockout}

You may want to protect your users' accounts by temporarily blocking the ability to sign in when a suspicious behavior is detected, such as multiples consecutive sign in attempts with an incorrect password. This measure can help to prevent a malicious party from gaining access to a user's account by guessing a user's password.
{: shortdesc}

By using the GUI or the API, you can set the maximum number of unsuccessful sign in attempts that a user can make before their account is temporarily locked. You can also set the amount of time that the account is locked for. You have the following options:

* Number of attempts: Any whole value between 1 and 10.
* Lockout period: Any whole value between 1 minute and 24 hours, specified in minutes.

If an account is locked, users are unable to sign in or perform any other self service operations, such as changing their password until the the specified lockout period has elapsed. When the lockout period has ended, the user is automatically unlocked.

You can unlock a user before the lockout period is over. To see if they are locked out look to see if the `active` field is set to `false`. You can also check to see if their status on the **Users** tab of the service dashboard is set to `disabled`. To unlock a user, you must use [the API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) to set the `active` field to `true`.

</br>

### Minimum period between password changes
{: #minimum-time}

You might want to prevent your users from quickly switching between passwords by setting a minimum period of time that a user must wait between password changes.
{: shortdesc}

This feature is especially useful when used in conjunction with the "Avoid password re-use" policy. Without this limitation, a user could simply change their password multiple times in quick succession to circumvent the limitation of re-using recent passwords. You can select any value between 1 hour and 30 days, specified in hours.

</br>

### Password expiration
{: #expiration}

For security reasons, you might want to enforce a password rotation policy, such that your users must change their password after a period of time.
{: shortdesc}

By using the GUI or the API, you can set a time period for which your user's passwords will remain valid. After a user's password expires, they are forced to reset their password on the next sign in. You can select any number of full days between 1 and 90.

The service provides a default GUI and experience out of the box with the login widget. The user is directed to supply a new password before the sign in is complete.

If you're using a custom sign in experience, an error is triggered when a user attempts to sign in with an expired password. It is your responsibility to configure your application to provide the necessary user experience. You can call the change password API to set the new password.

The token endpoint response looks similar to the following:

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

When this option is first set to on, any existing user passwords will not have an expiration date. The expiration period begins for those user's when their password is changed. You might want to encourage users to update their password after you set this feature to on.
{: note}

</br>

### Ensure password does not include username
{: #no-username}

For stronger passwords, you might want to prevent users that contain their username or the first part of their email address.
{: shortdesc}

This constraint is not case-sensitive which means that users are not able to alter the case of some or all of the characters in order to use the personal information. To configure this option, toggle the switch to **on**.

</br>

## Using a custom email sender
{: #custom-email}

With {{site.data.keyword.appid_short_notm}}, you can define a custom extension point to send your Cloud Directory email messages. By defining an extension point, you have full control of how the emails are sent and you can use your own domain name.
 {: shortdesc}

**Why would I want to use a custom email sender?**

By default, {{site.data.keyword.appid_short_notm}} uses SendGrid to deliver messages on your behalf. By configuring your own custom email sender, you can further enhance the branded experience for your app users.

Some more specific examples:
- **Personalized domain**
By configuring a custom email dispatcher, you have full control over how the email messages are sent. This includes customizing the email domain which might further reduce the chances of emails being filtered as spam.
- **Insights and troubleshooting**
Gain insights from your email provider, such as: the number of people that opened the emails or which messages were not delivered. Because you can track individual messages, and see overall statistics, this can help solve issues.

</br>

**How does it work?**

After the extension point is configured, it is called by {{site.data.keyword.appid_short_notm}} whenever an email message needs to be sent. The extension point contains all of the information about the message, including the final content of the email body.

</br>

**To create a custom email sender:**

1. In order to configure the {{site.data.keyword.appid_short_notm}} instance to use custom dispatcher, use <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/set_cloud_directory_email_dispatcher" target="_blank">the management API </a>.</br>
You must provide the URL. Additionally you can provide authorization information. The supported authorization types are: `Basic authorization` or a `constant authorization header value`.

  Valid configuration examples:
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

2. Configure an extension point that can listen to post request. This endpoint should be able to read the payload that comes from {{site.data.keyword.appid_short_notm}} and send the email with your custom email sender.

3. The body sent from {{site.data.keyword.appid_short_notm}} is in the following format: `{"jws": "jws-format-string"}`. </br> After you decode and verify the payload, the content is a JSON string.</br>
  ```
    {
      "tenant": "tenant-id",
      "iss" : "appid-oauth.ng.bluemix.net",
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

  - tenant: App ID instance tenantId
  - iat: timestamp of when the message was sent
  - iss: identifies principal that issued the JWS.
  - jti: uniq transaction ID
  - message: message to send, consists of the following fields:
    - to: recepiance email address
    - from: sender information, consists of the following fields:
      - name: optional, sender name
      - address: sender address
    - reply to: optional, consists of the following fields:
      - name: optional, sender name
      - address: optional, sender address
    - subject: email subject
    - body: email body, in html format

  You can verify that your request was successful by checking the response status code. Anything in the range of 200 - 299 is considered a success. If you receive any other response, try to make your request again.
  {: tip}

4. Every HTTP payload that is sent from {{site.data.keyword.appid_short_notm}} is automatically signed according to the JWS standard by using an asymmetric key pair.
For every {{site.data.keyword.appid_short_notm}} instance, a private and a public key is generated that are not shared across other instances. The private key is used to sign the HTTP payload, and you can use the public key to verify that the payload is generated by {{site.data.keyword.appid_short_notm}} and is not altered by a third party, <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V3/publicKeys" target="_blank">Public keys endpoint </a>.

5. Example code for the extension point (JavaScript)
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// Your App ID instance tenant ID
  	const tenantId = '<TENANT-ID>';

  	// Send request to App ID's public keys endpoint
  	const keysOptions = {
  		method: 'GET',
  		url: `https://<REGION>.appid.cloud.ibm.com/oauth/v3/${tenantId}/publickeys`
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
  {: codeblock}

6. Verify that your configuration is correctly set up by testing your email dispatcher. Use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">test API</a> to trigger a request to your configured custom email sender.

For full working example, see <a href="https://www.ibm.com/blogs/bluemix/2018/10/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users/" target="_blank">Use your own provider for mail sent with {{site.data.keyword.appid_full}}</a>.

</br>
</br>


## Migrating users
{: #user-migration}

Occasionally you might need to set up a new instance of {{site.data.keyword.appid_short_notm}}. If you're using Cloud Directory this means that your users must be migrated to the new instance. You can use the management APIs to help with the migration.
{: shortdesc}

### Before you begin

You must be assigned the `Manager` [IAM role](/docs/iam/quickstart.html) for both instances of {{site.data.keyword.appid_short_notm}}.

</br>

**Exporting**

Before you can add your users to the new instance, you need to export them from your current instance. To do so, you can use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/cloudDirectoryExport" target="_blank">export management API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

Example cURL command:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://eu-gb.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>Variable</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>A custom string that is used to encrypt and decrypt a users hashed password.</td>
  </tr>
  <tr>
    <td><code>tenantID</code></td>
    <td>The service tenant ID can be found in your service credentials. You can find your service credentials in the App ID dashboard.</td>
  </tr>
</table>

Only your Cloud Directory users and their profiles are returned. Users from other identity provider's are not.
{: note}

</br>

**Importing**

Now that you have your users ready to go, you can import their information into the new instance. To do so, you can use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/cloudDirectoryImport" target="_blank">import management API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

Example cURL command:

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://eu-gb.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}

</br>

### Using the migration script

{{site.data.keyword.appid_short_notm}} provides a migration script that you can use through the CLI that can help speed up the migration process.

Before you get started, be sure you have the following parameter information:

<table>
  <tr>
    <th>Parameter</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>The tenant ID of the instance of {{site.data.keyword.appid_short_notm}} that you plan to export users from.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>The tenant ID of the instance of {{site.data.keyword.appid_short_notm}} that you plan to import users to.</td>
  </tr>
  <tr>
    <td>Region</td>
    <td>Current options include: US-South: <code>ng</code>, London: <code>eu-gb</code>,  Sydney: <code>au-syd</code>, Washington: <code>us-east</code>, and Germany: <code>eu-de</code>.</td>
  </tr>
  <tr>
    <td>IAM token</td>
    <td>Be sure that you have <code>manager</code> permissions before you obtain the token. For help obtaining an IAM token, check out <a href="https://console.cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">the docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</td>
  </tr>
</table>

To run the script:

1. Clone the <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Open terminal and navigate to the folder that you cloned the repo into.
3. Run the following command.

  ```
  npm install
  ```
  {: codeblock}

4. With your parameters, run the following command.

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  Example command:

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwMFQ2RlMiLCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNzE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}

</br>
</br>


## Supported languages
{: #languages}

You can use <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization" target="_blank">the language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to set the language in which your user communication can be written. However, only English is available out of the box. You are responsible for the translation of the messages. After you set the configuration with the API, the GUI updates so that you are able to change the template text.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Code</th>
    <th>Language</th>
    <th>region</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>Afrikaans</td>
    <td>South Africa</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>Albanian</td>
    <td>Albania</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>Amharic</td>
    <td>Ethiopia</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>Arabic</td>
    <td>Algeria</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>Arabic</td>
    <td>Bahrain</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>Arabic</td>
    <td>Egypt</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>Arabic</td>
    <td>Iraq</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>Arabic</td>
    <td>Jordan</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>Arabic</td>
    <td>Kuwait</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>Arabic</td>
    <td>Lebanon</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>Arabic</td>
    <td>Libya</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>Arabic</td>
    <td>Mauritania</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>Arabic</td>
    <td>Morroco</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>Arabic</td>
    <td>Oman</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>Arabic</td>
    <td>Qatar</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>Arabic</td>
    <td>Saudi Arabia</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>Arabic</td>
    <td>Syria</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Arabic</td>
    <td>Tunisia</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>Arabic</td>
    <td>United Arab Emirates</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Arabic</td>
    <td>Yemen</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>Armenian</td>
    <td>Armenia</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>Assamese</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>Azerbaijani</td>
    <td>Azerbaijan</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>Basque</td>
    <td>Spain</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Belarusian</td>
    <td>Belarus</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengali</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Belarusian</td>
    <td>Belarus</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengali</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>Bengali</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>Bosnian</td>
    <td>Bosnia</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>Bulgarian</td>
    <td>Bulgaria</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>Burmese</td>
    <td>Myanmar</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>Catalan</td>
    <td>Spain</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>Chinese-simplified</td>
    <td>China</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>Chinese-simplified</td>
    <td>Singapore</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>Chinese-traditional</td>
    <td>Hong Kong S.A.R. of China</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>Chinese-traditional</td>
    <td>Macao</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>Chinese-traditional</td>
    <td>Taiwan</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>Croatian</td>
    <td>Croatia</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>Czech</td>
    <td>Czech Republic</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>Danish</td>
    <td>Denmark</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>Dutch</td>
    <td>Belgium</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>Dutch</td>
    <td>The Netherlands</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>English</td>
    <td>Australia</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>English</td>
    <td>Belgium</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>English</td>
    <td>Cameroon</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>English</td>
    <td>Canada</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>English</td>
    <td>Ghana</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>English</td>
    <td>Hong Kong S.A.R. of China</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>English</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>English</td>
    <td>Ireland</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>English</td>
    <td>Kenya</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>English</td>
    <td>Mauritius</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>English</td>
    <td>New Zealand</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>English</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>English</td>
    <td>Philippines</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>English</td>
    <td>Singapore</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>English</td>
    <td>South Africa</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>English</td>
    <td>Tanzania</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>English</td>
    <td>United Kingdom</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>English</td>
    <td>United States</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>English</td>
    <td>Zambia</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>English</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>Estonian</td>
    <td>Estonia</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>Filipino</td>
    <td>Philippines</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>Finnish</td>
    <td>Finland</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>French</td>
    <td>Algeria</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>French</td>
    <td>Cameroon</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>French</td>
    <td>Democratic Republic of the Congo</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>French</td>
    <td>Belgium</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>French</td>
    <td>Canada</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>French</td>
    <td>France</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>French</td>
    <td>Ivory Coast (Côte d’Ivoire)</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>French</td>
    <td>Luxembourg</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>French</td>
    <td>Mauritania</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>French</td>
    <td>Mauritius</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>French</td>
    <td>Morocco</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>French</td>
    <td>Senegal</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>French</td>
    <td>Switzerland</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>French</td>
    <td>Tunisia</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>Galician</td>
    <td>Spain</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>Ganda</td>
    <td>Uganda</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>Georgian</td>
    <td>Georgia</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>German</td>
    <td>Austria</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>German</td>
    <td>Germany</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>German</td>
    <td>Luxembourg</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>German</td>
    <td>Switzerland</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>Greek</td>
    <td>Greece</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>Gujarati</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>Hausa</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>Hebrew</td>
    <td>Israel</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>Hindi</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>Hungarian</td>
    <td>Hungary</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>Icelandic</td>
    <td>Iceland</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>Igbo</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>Indonesian</td>
    <td>Indonesia</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>Italian</td>
    <td>Italy</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>Italian</td>
    <td>Switzerland</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>Japanese</td>
    <td>Japan</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>Kannada</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>Kazakh</td>
    <td>Kazakhstan</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>Khmer</td>
    <td>Cambodia</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>Kinyarwanda</td>
    <td>Rwanda</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>Konkani</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>Korean</td>
    <td>South Korea</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>Lithuanian</td>
    <td>Lithuania</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>Latvian</td>
    <td>Latvia</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>Khmer</td>
    <td>Cambodia</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>Macedonian</td>
    <td>Macedonia</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>Malay-Latin</td>
    <td>Malaysia</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>Malayalam</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>Maltese</td>
    <td>Malta</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>Marathi</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>Mongolian-Cyrillic</td>
    <td>Mongolia</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>Nepali</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>Nepali</td>
    <td>Nepal</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>Norwegian Bokmål</td>
    <td>Norway</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>Norwegian Nynorsk</td>
    <td>Norway</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>Oriya (Odia)</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>Oromo</td>
    <td>Ethiopia</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>Polish</td>
    <td>Poland</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>Portuguese</td>
    <td>Angola</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>Portuguese</td>
    <td>Brazil</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>Portuguese</td>
    <td>Macao</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>Portuguese</td>
    <td>Mozambique</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>Portuguese</td>
    <td>Portugal</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>Punjabi</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>Romanian</td>
    <td>Romania</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>Russian</td>
    <td>Russia</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>Serbian-Cyrillic</td>
    <td>Serbia</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>Serbian-Latin</td>
    <td>Montenegro</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>Serbian-Latin</td>
    <td>Serbia</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>Sinhala</td>
    <td>Sri Lanka</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>Slovak</td>
    <td>Slovakia</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>Slovenian</td>
    <td>Slovenia</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>Spanish</td>
    <td>Argentina</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>Spanish</td>
    <td>Bolivia</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>Spanish</td>
    <td>Chile</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>Spanish</td>
    <td>Colombia</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>Spanish</td>
    <td>Costa Rica</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>Spanish</td>
    <td>Dominican Republic</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>Spanish</td>
    <td>Ecuador</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>Spanish</td>
    <td>El Salvador</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>Spanish</td>
    <td>Guatemala</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>Spanish</td>
    <td>Honduras</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>Spanish</td>
    <td>Mexico</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>Spanish</td>
    <td>Nicaragua</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>Spanish</td>
    <td>Panama</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>Spanish</td>
    <td>Paraguay</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>Spanish</td>
    <td>Peru</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>Spanish</td>
    <td>Puerto Rico</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>Spanish</td>
    <td>Spain</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>Spanish</td>
    <td>United States</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>Spanish</td>
    <td>Uruguay</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>Spanish</td>
    <td>Venezuela</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>Swahili</td>
    <td>Kenya</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>Swahili</td>
    <td>Tanzania</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>Swedish</td>
    <td>Sweden</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>Tamil</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>Telugu</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>Thai</td>
    <td>Thailand</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>Turkish</td>
    <td>Turkey</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>Ukrainian</td>
    <td>Ukraine</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>Urdu</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>Urdu</td>
    <td>Pakistan</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>Uzbek-Cyrillic</td>
    <td>Uzbekistan</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>Uzbek-Latin</td>
    <td>Uzbekistan</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>Vietnamese</td>
    <td>Vietnam</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>Welsh</td>
    <td>United Kingdom</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>Yoruba</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>Zulu</td>
    <td>South Africa</td>
  </tr>
</table>
