---

copyright:
  years: 2017, 2020
lastupdated: "2020-07-09"

keywords: emails, verification, templates, sendgrid, welcome, password reset, password change, change details, verification, supported languages, registry, cloud directory, 

subcollection: appid

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}


# Customizing emails
{: #cd-types}

When a user interacts with your application, you might want to send a reply or ask for verification. {{site.data.keyword.appid_short_notm}} provides default templates that you can use for the interactions. You can also use the templates as a guide and customize your messaging to fit your brand.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} uses [SendGrid](https://sendgrid.com/){: external} as a mail delivery service. All emails are sent with a single SendGrid account.
{: note}


## Configuring email settings
{: #cd-email-settings}

With {{site.data.keyword.appid_short_notm}}, you can choose to use {{site.data.keyword.appid_short_notm}} default [SendGrid](https://sendgrid.com/){: external} credentials, add your own SendGrid account, or configure your own custom webhook to send email messages in Cloud Directory.
{: shortdesc}


### Using the IBM default email provider
{: #cd-default-email}

By default, {{site.data.keyword.appid_short_notm}} uses [SendGrid](https://sendgrid.com/){: external} as an email delivery service for Cloud Directory.

As of 30 April 2020, email content and sender details are no longer editable if you’re using the {{site.data.keyword.appid_short_notm}} default email provider. To customize your user communication, add your own SendGrid account or custom email provider.
{: important}

1. Go to the **Cloud Directory > Email templates > Email settings** page of the service dashboard.

2. Select **Default**. The information that you need to input appears.

3. Configure your **Sender details**.

  1. In **From**, enter the email address that you want users to receive your emails from.

  2. In **Sender name**, enter the name that you want associated with the "From" email.

  3. In **Reply-to**, enter the email address where you want to receive any replies that someone might have to the email.

4. Click **Test** to try your configuration with a test email.

5. Click **Save** to enable your configuration.


### Adding your own SendGrid account
{: #cd-add-sendgrid-account}

By using your own SendGrid account to send your Cloud Directory emails, you have full control. You can decide how the emails are sent, use your own domain name, and define your sender details. With custom email settings, you can reduce the chances of an email getting filtered as spam while also furthering brand recognition for your application.

A direct connection to your email provider can help you to get information about individual messages such as the number of people that open the emails and which messages were not delivered. You can also see overall statistics that you can use to better manage your email campaigns.


Don't have a SendGrid account? [Sign up](https://signup.sendgrid.com/){: external}.
{: tip}

1. Go to the **Cloud Directory > Email templates > Email settings** page of the service dashboard.

2. Select **SendGrid**. The information that you need to input appears.

3. In **SendGrid API key**, enter your API key.

4. Configure your **Sender details**.

  1. In **From**, enter the email address that you want users to receive your emails from.

  2. In **Sender name**, enter the name that you want associated with the "From" email.

  3. In **Reply-to**, enter the email address where you want to receive any replies that someone might have to the email.

5. Click **Test** to try your configuration with a test email.

6. Click **Save** to enable your configuration.


### Customizing your email provider
{: #cd-custom-email}

By defining your own custom extension point to send your Cloud Directory emails, you have full control. You can decide how the emails are sent, use your own domain name, and define your sender details. With custom email settings, you can reduce the chances of an email getting filtered as spam while also furthering brand recognition for your application.

A direct connection to your email provider can help you to get information about individual messages such as the number of people that open the emails and which messages were not delivered. You can also see overall statistics that you can use to better manage your email campaigns.


#### Configuring a custom provider with the GUI
{: #cd-messages-configure-custom-gui}

You can use the service dashboard to configure your custom provider.

1. Go to the **Cloud Directory > Email templates > Email settings** page of the service dashboard.

2. Select **Custom**. The information that you need to input appears.

3. In **Webhook**, enter your custom extension URL.

4. Select an **Authorization type**. You can choose from the following options:

  * **None**: The webhook endpoint or URL, does not require an authorization header.

  * **Basic**: The webhook endpoint requires an HTTP authorization header with every request in the form of a username and password.
  
  * **Authorization headers**: The webhook request requires that you pass the authorization information for your endpoint in an HTTP authorization. For example, you might pass an OAuth 2.0 token: `Authorization: Bearer eyJraWQiOiIyMDIwMDEyNTE2MzMiLCJhbGciOiJSUzI1NiJ9.eyJpYW1faWQiOiJJ`.

5. Configure your **Sender details**.

  1. In **From**, enter the email address that you want users to receive your emails from.

  2. In **Sender name**, enter the name that you want associated with the "From" email.

  3. In **Reply-to**, enter the email address where you want to receive any replies to the email.

6. Click **Test** to try your configuration with a test email.

6. Click **Save** to enable your configuration.


#### Configuring a custom provider with the API
{: #cd-messages-configure-custom-api}

You can use the Cloud Directory [management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher){: external} to configure your custom email sender.

To see an example, check out the blog <a href="https://www.ibm.com/cloud/blog/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users" target="_blank">Using your own provider for mail that is sent with {{site.data.keyword.appid_full}}</a>.
{: tip}

1. Configure an extension point that can listen for a POST request. The endpoint must be able to:
  * Read the payload that comes from {{site.data.keyword.appid_short_notm}}.
  * Send the email from your custom provider.
  * Optionally, [validate](/docs/appid?topic=appid-token-validation#local-validation) the JSON payload that is returned by {{site.data.keyword.appid_short_notm}} has not been altered by a third party in any way. A string that is formatted as `{"jws": "jws-format-string"}` is returned that contains your tenant ID, the issuer of your JWS token, the time stamp of when the message was sent, a unique transaction ID, and the actual message information including your sender details and email body content. 

  Your extension point might look similar to the following example:

  ```javascript
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

2. Make a PUT request to the `/management/v4/{tenantId}/config/cloud_directory/email_dispatcher` to provide your webhook URL. Optionally, you can provide authorization information. Supported authorization types include: `Basic authorization` and `constant authorization header value`.

  ```sh
  curl -X PUT https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/config/cloud_directory/email_dispatcher' \
  --header 'Accept: application/json' \
  --header 'Authorization: Bearer <IAM_token>' \
  -d '{
    "provider": "custom",
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "basic",
        "username": "username",
        "password": "password"
        }
      }
    }'
  ```
  {: codeblock}

3. Verify that your configuration is correctly set up by testing your email dispatcher. Use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">test API</a> to trigger a request to your configured custom email sender.



## Email templates
{: #cd-messages}

When you send messages to your users, you can use any combination of the following templates. Or, you can edit the templates to customize your message.
{: shortdesc}

In addition to the following message types, you can also take advantage of the [MFA](/docs/appid?topic=appid-cd-mfa) templates.
{: tip}

For further customization, you can use parameters in your messages. Check out the following table to see the parameters that you can use in all of the message types.

<table>
  <caption>Table 1. The parameters that you can use in your messages to users</caption>
  <tr>
    <th>Parameter</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> Displays the image that you configured for your Login Widget.</td>
  </tr>
  <tr>
    <td><code>%{user.displayName}</code></td>
    <td> Displays the screen name a user chose to use when interacting with the app.</td>
  </tr>
  <tr>
    <td><code>%{user.email}</code></td>
    <td> Displays the user's registered email address.</td>
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
</table>


### Email: Welcome
{: #cd-messages-welcome}

When a user signs up for your application, you might want to send them a message that welcomes them to your app. 
{: shortdesc}

1. Go to the **Cloud Directory > Email templates > Welcome email** tab of the service dashboard.

2. Set **Welcome email** to **Enabled**.

3. Customize the content of your message. You can add parameters and insert images by using the UI. To change the [language](/docs/appid?topic=appid-cd-types#cd-languages) of the message, you can use [the APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization){: external} to set the language. However, you are responsible for the content and conversion of the message. Check out the following table to see the list of tables that you can use in this message and all of the other messages that you can send. If a user does not supply the information that is pulled by the parameter, it appears blank.

4. Click **Save**.


### Email: Verification
{: #cd-messages-verification}

When a user signs up for your application by using their email, you can send them an email that asks them to confirm their identity. By requesting a verification, you limit the number of fake accounts that can sign up for your app. You can restrict access to your app until a user verifies their email, or use it as a way to manage which users you create profiles for.
{: shortdesc}

Users who are manually added via the {{site.data.keyword.appid_short_notm}} dashboard or the create user API do not automatically receive this email.
{: note}


1. Go to the **Cloud Directory > Email templates > Email verification** tab of the service dashboard.

2. Set **Email verification** to **Enabled**.

3. Set **Allow users to sign in to your app without first verifying their email address** to **Yes**. When set to yes, users are able to interact with your application after they sign up, but before they verify their email address. The default setting is no.

4. Customize the content of your message. You can add parameters and insert images by using the UI. To change the [language](/docs/appid?topic=appid-cd-types#cd-languages) of the message, you can use [the APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization){: external} to set the language. However, you are responsible for the content and conversion of the message. Check out the following table to see the different parameters that you can use in your message. If a user does not supply the information that is pulled by the parameter, it appears blank.

  <table>
    <caption>Table 2. Parameters that you can use in messages that are related to verification</caption>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
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
  </table>

  You can also use the message parameters that are listed in the [Welcome message](/docs/appid?topic=appid-cd-types#cd-messages-welcome) section.
  {: tip}

5. Define an expiration time for the action URL. The URL expiration is the amount of time, in minutes, that a user must complete the action before the verification link expires. This setting also affects the amount of time that your reset password link is valid.
 
6. Enter a URL for the page that you want to display after a user verifies their email in the **Thank you page URL** box. If you choose to leave this field blank, an {{site.data.keyword.appid_short_notm}} default page is displayed.

7. Click **Save**. 


### Email: Reset password
{: #cd-messages-reset}

When a user interacts with your app, they might forget their password or need to update it. You can customize the email response to their request. When a user requests a change to their password, the password remains unchanged until they click the link in this email.
{: shortdesc}


1. Go to the **Cloud Directory > Email templates > Reset password** tab of the service dashboard.

2. Set **Forgot password email** to **Enabled**.

3. Customize the content of your message. You can add parameters and insert images by using the UI. To change the [language](/docs/appid?topic=appid-cd-types#cd-languages) of the message, you can use <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">the APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to set the language. However, you are responsible for the content and conversion of the message. Check out the following table to see the different parameters that you can use in your message. If a user does not supply the information that is pulled by the parameter, it appears blank.

  <table>
    <caption>Table 3. Parameters that you can use in messages that are related to forgotten passwords</caption>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
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
      <td> Displays a one-time passcode as part of the URL. This means that each person would have a different code. Example: `https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478`</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> Displays the link that a user clicks to reset their password.</td>
    </tr>
  </table>

  You can also use the message parameters that are listed in the [Welcome message](/docs/appid?topic=appid-cd-types#cd-messages-welcome) section.
  {: tip}

4. Define an expiration time for the action URL. The URL expiration is the amount of time, in minutes, that a user must complete the action before the verification link expires. This setting also affects the amount of time that your reset password link is valid.
 
5. Enter a URL for the page that you want to display after a user verifies their email in the **Reset password page URL** box. If you choose to leave this field blank, an {{site.data.keyword.appid_short_notm}} default page is displayed.

6. Click **Save**.


### Email: Password change
{: #cd-messages-password-change}

You can notify a user when their password is updated. The notification can be helpful if they did not request that their password be changed. They can take the proper steps to resecure their account.
{: shortdesc}

1. Go to the **Cloud Directory > Email templates > Password change** tab of the service dashboard.

2. Set **Password changed email** to **Enabled**.

3. Customize the content of your message. You can add parameters and insert images by using the UI. To change the [language](/docs/appid?topic=appid-cd-types#cd-languages) of the message, you can use [the APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization){: external} to set the language. However, you are responsible for the content and conversion of the message. Check out the following table to see the different parameters that you can use in your message. If a user does not supply the information that is pulled by the parameter, it appears blank.

  <table>
    <caption>Table 4. Parameters that you can use in messages that are related to changing a password</caption>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> Displays the time at which a new password went into effect. </td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> Displays the IP address from which the password change was requested. </td>
    </tr>
  </table>

  You can also use the message parameters that are listed in the [Welcome message](/docs/appid?topic=appid-cd-types#cd-messages-welcome) section.
  {: tip}

4. Click **Save**.



## Supported languages
{: #cd-languages}

You can use [the language management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization){: external} to set the language in which your user communication can be written. However, only English is available out of the box. You are responsible for the conversion of the messages. After you set the configuration with the API, the GUI updates so that you are able to change the template text.
{: shortdesc}

<table>
  <caption>Table 6. Languages that are supported</caption>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Code</th>
    <th>Language</th>
    <th>Region</th>
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
    <td>Morocco</td>
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
    <td>Macao S.A.R. of the PRC</td>
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
    <td>Macao S.A.R. of the PRC</td>
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
