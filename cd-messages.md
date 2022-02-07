---

copyright:
  years: 2017, 2022
lastupdated: "2022-02-07"

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
{:beta: .beta}
{:term: .term}
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
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}
{:release-note: data-hd-content-type='release-note'}

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

7. Click **Save** to enable your configuration.


#### Configuring a custom provider with the API
{: #cd-messages-configure-custom-api}

You can use the Cloud Directory [management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher){: external} to configure your custom email sender.

To see an example, check out the blog [Using your own provider for mail that is sent with {{site.data.keyword.appid_short_notm}}](https://www.ibm.com/cloud/blog/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users){: external}.
{: tip}


1. Configure an extension point that can listen for a POST request. The endpoint must be able to:
   * Read the payload that comes from {{site.data.keyword.appid_short_notm}}.
   * Send the email from your custom provider.
   * Optionally, [validate](/docs/appid?topic=appid-token-validation#local-validation) the JSON payload that is returned by {{site.data.keyword.appid_short_notm}} was not altered by a third party in any way. A string that is formatted as `{"jws": "jws-format-string"}` is returned that contains your tenant ID, the issuer of your JWS token, the timestamp of when the message was sent, a unique transaction ID, and the actual message information that includes your sender details and email body content. 

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
      const tenantId = '{TENANT-ID}';

      // Send request to {{site.data.keyword.appid_short_notm}}'s public keys endpoint
      const keysOptions = {
      method: 'GET',
      url: `https://{REGION}.appid.cloud.ibm.com/oauth/v4/${tenantId}/publickeys`
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
   curl -X PUT https://{region}.appid.cloud.ibm.com/management/v4/{tenant_ID}/config/cloud_directory/email_dispatcher' \
   --header 'Accept: application/json' \
   --header 'Authorization: Bearer {IAM_token}' \
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

3. Verify that your configuration is correctly set up by testing your email dispatcher. Use the [test API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test){: external} to trigger a request to your configured custom email sender.


## Email templates
{: #cd-messages}

When you send messages to your users, you can use any combination of the following templates. Or, you can edit the templates to customize your message.
{: shortdesc}

In addition to the following message types, you can also take advantage of the [MFA](/docs/appid?topic=appid-cd-mfa) templates.
{: tip}

For further customization, you can use parameters in your messages. Check out the following table to see the parameters that you can use in all the message types.

| Parameter | Description | 
|-----|----| 
| `%{display.logo}` | Displays the image that you configured for your Login Widget. | 
| `%{user.displayName}` | Displays the screen name a user chose to use when interacting with the app. |
| `%{user.email}` | Displays the user's registered email address. |
| `%{user.username}` | Displays the user's specified username when the authentication method is set to username and password. |
| `%{user.firstName}` | Displays the user's specified given name. | 
| `%{user.formattedName}` | Displays the user's full name. |
| `%{user.lastName}` | Displays the user's specified surname. |
{: caption="Table 1. The parameters that you can use in your messages to users" caption-side="top"}


### Email: Welcome
{: #cd-messages-welcome}

When a user signs up for your application, you might want to send them a message that welcomes them to your app. 
{: shortdesc}

1. Go to the **Cloud Directory > Email templates > Welcome email** tab of the service dashboard.

2. Set **Welcome email** to **Enabled**.

3. Customize the content of your message. You can add parameters and insert images by using the UI. To change the [language](/docs/appid?topic=appid-cd-types#cd-languages) of the message, you can use [the APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization){: external} to set the language. However, you are responsible for the content and conversion of the message. Check out the following table to see the list of tables that you can use in this message and all the other messages that you can send. If a user does not supply the information that is pulled by the parameter, it appears blank.

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

   | Parameter | Description | 
   | --------- | ----------- |
   | `%{linkExpiration.hours}` | Displays the number of hours the link is valid. |
   | `%{linkExpiration.minutes}` |  Displays the number of minutes the link is valid. |
   | `%{verify.code}` | Displays a one-time verification URL. |
   | `%{verify.link}` | Displays the action URL that you specified in settings. |
   {: caption="Table 2. Parameters that you can use in messages that are related to verification" caption-side="top"}

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

3. Customize the content of your message. You can add parameters and insert images by using the UI. To change the [language](/docs/appid?topic=appid-cd-types#cd-languages) of the message, you can use [the APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization){: external} to set the language. However, you are responsible for the content and conversion of the message. Check out the following table to see the different parameters that you can use in your message. If a user does not supply the information that is pulled by the parameter, it appears blank.

   | Parameter | Description |
   | --------- | ----------- |
   | `%{linkExpiration.hours}` | Displays the number of hours that the link is valid. |
   | `%{linkExpiration.minutes}` | Displays the number of minutes that the link is valid. |
   | `%{resetPassword.code}` | Displays a one-time passcode as part of the URL. This means that each person would have a different code. Example: `https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478` |
   | `%{resetPassword.link}` | Displays the link that a user clicks to reset their password. | 
   {: caption="Table 3. Parameters that you can use in messages that are related to forgotten passwords" caption-side="top"}

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

   | Parameter | Description |
   | --------- | ----------- |
   | `%{passwordChangeInfo.time}` | Displays the time at which a new password went into effect. |
   | `%{passwordChangeInfo.ipAddress}` | Displays the IP address from which the password change was requested. |
   {: caption="Table 4. Parameters that you can use in messages that are related to changing a password" caption-side="top"}

   You can also use the message parameters that are listed in the [Welcome message](/docs/appid?topic=appid-cd-types#cd-messages-welcome) section.
   {: tip}

4. Click **Save**.


## Supported languages
{: #cd-languages}

You can use [the language management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization){: external} to set the language in which your user communication can be written. However, only English is available out of the box. You are responsible for the conversion of the messages. After you set the configuration with the API, the GUI updates so that you are able to change the template text.
{: shortdesc}


| Code | Language | Region |
|-----|----| ------ |
| `af-ZA` | Afrikaans | South Africa |
| `sq-AL` | Albanian | Albania |
| `am-ET` | Amharic | Ethiopia |
| `ar-DZ` | Arabic | Algeria | 
| `ar-BH` | Arabic | Bahrain| 
| `ar-EG` | Arabic | Egypt |
| `ar-IQ` | Arabic | Iraq | 
| `ar-JO` | Arabic | Jordan | 
| `ar-KW` | Arabic | Kuwait | 
| `ar-LB` | Arabic | Lebanon |
| `ar-LY` | Arabic | Libya |
| `ar-MR` | Arabic | Mauritania | 
| `ar-MA` | Arabic | Morocco | 
| `ar-OM` | Arabic | Oman | 
| `ar-QA` | Arabic | Qatar |
| `ar-SA` | Arabic | Saudi Arabia | 
| `ar-SY` | Arabic | Syria | 
| `ar-YE` | Arabic | Tunisia | 
| `ar-AE` | Arabic | United Arab Emirates |
| `ar-YE` | Arabic | Yemen | 
| `hy-AM` | Armenian | Armenia | 
| `as-IN` | Assamese | India | 
| `az-AZ` | Azerbaijani | Azerbaijan | 
| `eu-ES` | Basque | Spain | 
| `be-BY`| Belarusian | Belarus | 
| `bn-BD` | Bengali | Bangladesh | 
| `be-BY` | Belarusian | Belarus | 
| `bn-BD` | Bengali | Bangladesh | 
| `bn-IN` | Bengali | India | 
| `bs-Latn-BA` | Bosnian | Bosnia | 
| `bg-BG` | Bulgarian | Bulgaria | 
| `my-MM` | Burmese | Myanmar | 
| `ca-ES` | Catalan | Spain | 
| `zh-Hans-CN` | Chinese-simplified | China | 
| `zh-Hans-SG` | Chinese-simplified | Singapore | 
| `zh-Hant-HK` | Chinese-traditional | Hong Kong S.A.R. of China | 
| `zh-Hant-MO` | Chinese-traditional | Macao S.A.R. of the PRC| 
| `zh-Hant-TW` | Chinese-traditional | Taiwan | 
| `hr-HR` | Croatian | Croatia | 
| `cs-CZ` | Czech | Czech Republic | 
| `da-DK` | Danish | Denmark | 
| `nl-BE` | Dutch | Belgium | 
| `nl-NL` | Dutch | The Netherlands | 
| `en-AU` | English | Australia | 
| `eu-BE` | English | Belgium |
| `en-CM` | English | Cameroon | 
| `eu-CA` | English | Canada | 
| `en-GH` | English | Ghana | 
| `eu-HK` | English | Hong Kong S.A.R. of China | 
| `en-IN` | English | India | 
| `en-IE` | English | Ireland | 
| `en-KE` | English | Kenya | 
| `en-MU` | English | Mauritius | 
| `en-NZ` | English | New Zealand |
| `en-NG` | English | Nigeria | 
| `en-PH` | English | Philippines | 
| `en-SG` | English | Singapore |
| `en-ZA` | English | South Africa | 
| `en-TZ` | English | Tanzania |
| `en-GB` | English | United Kingdom | 
| `en-US` | English | United States |
| `en-ZM` | English | Zambia | 
| `en` | English | |
| `et-EE` | Estonian | Estonia |
| `fil-PH` | Filipino | Philippines | 
| `fi-FI` | Finnish | Finland | 
| `fr-DZ` | French | Algeria | 
| `fr-CM` | French | Cameroon | 
| `fr-CD` | French | Democratic Republic of the Congo |
| `fr-BE` | French | Belgium | 
| `fr-CA` | French | Canada | 
| `fr-FR` | French | France | 
| `fr-CI` | French | Ivory Coast (Côte d’Ivoire) |
| `fr-LU` | French | Luxembourg | 
| `fr-MR` | French | Mauritania | 
| `fr-MU` | French | Mauritius | 
| `fr-MA` | French | Morocco |
| `fr-SN` | French | Senegal | 
| `fr-CH` | French | Switzerland | 
| `fr-TN` | French | Tunisia | 
| `gl-ES` | Galician | Spain |
| `lg-UG` | Ganda | Uganda | 
| `ka-GE` | Georgian | Georgia | 
| `de-AT` | German | Austria
| `de-DE` | German | Germany |
| `de-LU` | German | Luxembourg | 
| `de-CH` | German | Switzerland |
| `el-GR` | Greek | Greece | 
| `gu-IN` | Gujarati | India | 
| `ha-NG` | Hausa | Nigeria | 
| `he-IL` | Hebrew | Israel | 
| `hi-IN` | Hindi | India | 
|`hu-HU` | Hungarian | Hungary |
| `is-IS` | Icelandic | Iceland | 
| `ig-NG` | Igbo | Nigeria | 
| `id-ID` | Indonesian | Indonesia | 
| `it-IT` | Italian | Italy | 
| `it-CH` | Italian | Switzerland | 
| `ja-JP` | Japanese | Japan | 
| `kn-IN` | Kannada | India | 
| `kk-KZ` | Kazakh | Kazakhstan | 
| `km-KH` | Khmer | Cambodia | 
| `rw-RW` | Kinyarwanda | Rwanda | 
| `kok-IN` | Konkani | India | 
| `ko-KR` | Korean | South Korea | 
| `lo-LA` | Lithuanian | Lithuania | 
| `lv-LV` | Latvian | Latvia | 
| `lt-LT` | Khmer | Cambodia | 
| `mk-MK` | Macedonian | Macedonia | 
| `ms-Latn-MY` | Malay-Latin | Malaysia | 
| `ml-IN` | Malayalam | India | 
| `mt-MT` | Maltese | Malta |
| `mr-IN` | Marathi | India | 
| `mn-Cyrl-MN` | Mongolian-Cyrillic | Mongolia | 
| `ne-IN` | Nepali | India | 
| `ne-NP` | Nepali | Nepal | 
| `nb-NO` | Norwegian Bokmål | Norway | 
| `nn-NO` | Norwegian Nynorsk | Norway | 
| `or-IN` | Oriya (Odia) | India | 
| `om-ET` | Oromo | Ethiopia | 
| `pl-PL` | Polish | Poland | 
| `pt-AO` | Portuguese | Angola | 
| `pt-BR` | Portuguese | Brazil |
| `pt-MO` | Portuguese | Macao S.A.R. of the PRC| 
| `pt-MZ` | Portuguese | Mozambique | 
| `pt-PT` | Portuguese | Portugal | 
| `pa-IN` | Punjabi | India | 
| `ro-RO` | Romanian | Romania | 
| `ru-RU` | Russian | Russia | 
| `sr-Cyrl-RS` | Serbian-Cyrillic | Serbia | 
| `sr-Latn-ME` | Serbian-Latin | Montenegro | 
| `sr-Latn-RS` | Serbian-Latin | Serbia | 
| `si-LK` | Sinhala | Sri Lanka | 
| `sk-SK` | Slovak | Slovakia | 
| `sl-SI` | Slovenian | Slovenia | 
| `es-AR` | Spanish | Argentina | 
| `es-BO` | Spanish | Bolivia | 
| `es-CL` | Spanish | Chile | 
| `es-CO` | Spanish | Colombia | 
| `es-CR` | Spanish | Costa Rica | 
| `es-DO` | Spanish | Dominican Republic | 
| `es-EC` | Spanish | Ecuador | 
| `es-SV` | Spanish | El Salvador | 
| `es-GT` | Spanish | Guatemala| 
| `es-HN` | Spanish | Honduras | 
| `es-MX` | Spanish | Mexico | 
| `es-NI` | Spanish | Nicaragua | 
| `es-PA` | Spanish | Panama | 
| `es-PY` | Spanish | Paraguay | 
| `es-PE` | Spanish | Peru | 
| `es-PR` | Spanish | Puerto Rico | 
| `es-ES` | Spanish | Spain |
| `es-US` | Spanish | United States | 
| `es-UY` | Spanish | Uruguay | 
| `es-VE` | Spanish | Venezuela | 
| `sw-KE` | Swahili | Kenya | 
| `sw-TZ` | Swahili | Tanzania | 
| `sv-SE` | Swedish | Sweden | 
| `ta-IN` | Tamil | India | 
| `te-IN` | Telugu | India | 
| `th-TH` | Thai | Thailand | 
| `tr-TR` | Turkish | Turkey | 
| `uk-UA` | Ukrainian | Ukraine | 
| `ur-IN` | Urdu | India |
| `ur-PK` | Urdu| Pakistan |
| `uz-Cyrl-UZ` | Uzbek-Cyrillic | Uzbekistan
| `uz-Latn-UZ` | Uzbek-Latin | Uzbekistan |
| `vi-VN` | Vietnamese | Vietnam |
| `cy-GB` | Welsh | United Kingdom |
| `yo-NG` | Yoruba | Nigeria | 
| `zu-ZA` | Zulu | South Africa |
{: caption="Table 6. Languages that are supported" caption-side="top"}

