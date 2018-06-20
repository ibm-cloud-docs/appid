---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configuring cloud directory
{: #cd}

Users can sign up and sign in to your mobile and web apps by using an email and a password. A cloud directory is a user registry that is maintained in the cloud. When a user signs up for your app with an email and a password, they're added to your directory of users. With this feature, users have the freedom to manage their own account within your app.
{: shortdesc}

</br>

## Managing directory settings
{: #cd-settings}

You can configure the notifications and level of user control for your app. Setting up your cloud directory can be done quickly, as shown in the following image. These settings can be updated at any time from the service dashboard.
{: shortdesc}

![Configuring cloud directory](/images/cloud-directory.png)

1. Be sure that cloud directory is turned on as an identity provider and set **Allow users to sign up and reset their password** to **On**. If set to **Off**, you can still add users through the console for development purposes.
2. Configure your sender details. Specify the email address from which your messages appear to be from, the sender, and to whom your users can reply.
  When you configure your action URL, be sure that you give enough time for a user to click the link. A user must verify their email to have certain options, such as the ability to request a reset of their password.
  {: tip}
3. Determine the types of emails a user receives and the sender information.
4. With the templates provided, customize your messages with your brand or personalized messages. For more information, see [Managing messages](/docs/services/appid/cloud-directory.html#cd-messages).
5. See who's signed-up for your app in the **Users** tab of the GUI.

</br>

## Managing messages
{: #cd-messages}

A template is an example of an email message that you might send to your users. You can customize the template by updating the content and layout of the message.
{: shortdesc}

1. In the **Identity Providers > Cloud Directory > Settings** tab of the dashboard, set the messages that you want to send to **On** .

2. *Optional*: Use the API to set another language that you want to use in your messages. For a list of supported language codes, see [Supported languages](#languages).

3. Select a **Message type**.

4. Customize your message by changing the content and design of the message. You can use parameters to personalize your messages. Don't forget to save your changes!



### Types of messages

You can send several types of messages to your users. You can choose to send the example message that it programmed into the UI or you can customize the content for a more personal app experience.

<dl>
  <dt>Welcome</dt>
    <dd><p>After they've registered, you can welcome a user to your application via email. To welcome and retain your users, make your message as engaging as possible.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/> All message parameters </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Displays the image that you configured for your login widget. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> Displays the screen name a user chose to use when interacting with the app. </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> Displays the user's registered email address. </td>
        </tr>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> Displays the user's specified given name. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Displays the user's full name. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Displays the user's specified surname. </td>
        </tr>
      </tbody>
    </table>
    <p>**Note**: If a user does not supply the information pulled by the parameter, it appears blank.</p></dd>
  <dt>Forgot password</dt>
    <dd><p>A user can ask to have their password reset if they forget it or need to update it for any reason. You can customize the email response to their request. When a user requests a change, their password remains unchanged until they click the link in this email.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/> Password change parameters </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Displays the number of hours the link is valid. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Displays the number of minutes the link is valid. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> Displays a one-time passcode as part of the URL. This means that each person would have a different code. Example: <code>https://appid-wfm.bluemix.net/verify/6574839563478</code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Displays the link that a user clicks to reset their password. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Verification</dt>
    <dd><p>You can request that a user verifies their account via email. By requesting a verification, you limit the number of fake accounts that can sign up for your app. You can restrict access to your app until a user has verified their email, or use it as a way to manage which users you create profiles for.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/> Verification message parameters </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Displays the number of hours the link is valid. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Displays the number of minutes the link is valid. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> Displays a one-time verification URL. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> Displays the action URL that you specified in settings. </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>Password change</dt>
    <dd><p>You can let a user know when their password has been updated. This is helpful if they did not request that their password be changed. They can take the proper steps to re-secure their account.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/> Password change parameters </th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> Displays the time at which a new password went into effect. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Displays the IP address from which the password change was requested. </td>
        </tr>
      </tbody>
    </table>
    </dd>
</dl>
</br>
**NOTE**: {{site.data.keyword.appid_short_notm}} uses <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> as a mail delivery service. All emails are sent with a single SendGrid account.


</br>

## Managing password strength
{: #strength}

You can set the requirements for the passwords that can be used with Cloud Directory.
{: shortdesc}

A strong password makes it difficult, or even improbable for someone to guess the password through in either a manual or automated way. Password strength is set as a regex string.

Some common password strength examples:

- Must be at least 8 characters. Example regex: `^.{8,}$`
- Must contain 1 number, 1 lower case letter, and 1 capital letter. Example regex: `^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Must contain only English letters and numbers. Example regex: `^[A-Za-z0-9]*$`
- Must be at least 1 unique character. Example regex: `^(\w)\w*?(?!\1)\w+$`

To set the requirements, you must use <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">the API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

</br>

## Supported languages
{: #languages}

You can use the API to set the language in which your user communication can be written. You are responsible for the translation of the messages.
{: shortdesc}

<table>
  <col width="20%">
  <col width="30%">
  <col width="0%">
  <col width="20%">
  <col width="30%">
  <tr>
    <th>Code</th>
    <th>Language and region</th>
    <th> </th>
    <th>Code</th>
    <th>Language and region</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>Afrikaans (South Africa)</td>
    <td> </td>
    <td><code>sq-AL</code></td>
    <td>Albanian (Albania)</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>Amharic (Ethiopia)</td>
    <td> </td>
    <td><code>ar-DZ</code></td>
    <td>Arabic (Algeria)</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>Arabic (Bahrain)</td>
    <td> </td>
    <td><code>ar-EG</code></td>
    <td>Arabic (Egypt)</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>Arabic (Iraq)</td>
    <td> </td>
    <td><code>ar-JO</code></td>
    <td>Arabic (Jordan)</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>Arabic (Kuwait)</td>
    <td> </td>
    <td><code>ar-LB</code></td>
    <td>Arabic (Lebanon)</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>Arabic (Libya)</td>
    <td> </td>
    <td><code>ar-MR</code></td>
    <td>Arabic (Mauritania)</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>Arabic (Morroco)</td>
    <td> </td>
    <td><code>ar-OM</code></td>
    <td>Arabic (Oman)</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>Arabic (Qatar)</td>
    <td> </td>
    <td><code>ar-SA</code></td>
    <td>Arabic (Saudi Arabia)</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>Arabic (Syria)</td>
    <td> </td>
    <td><code>ar-YE</code></td>
    <td>Arabic (Tunisia)</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>Arabic (United Arab Emirates)</td>
    <td> </td>
    <td><code>ar-YE</code></td>
    <td>Arabic (Yemen)</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>Armenian (Armenia)</td>
    <td> </td>
    <td><code>as-IN</code></td>
    <td>Assamese (India)</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>Azerbaijani (Azerbaijan)</td>
    <td> </td>
    <td><code>eu-ES</code></td>
    <td>Basque (Spain)</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Belarusian (Belarus)</td>
    <td> </td>
    <td><code>bn-BD</code></td>
    <td>Bengali (Bangladesh)</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Belarusian (Belarus)</td>
    <td> </td>
    <td><code>bn-BD</code></td>
    <td>Bengali (Bangladesh)</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>Bengali (India)</td>
    <td> </td>
    <td><code>bs-Latn-BA</code></td>
    <td>Bosnian (Bosnia)</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>Bulgarian (Bulgaria)</td>
    <td> </td>
    <td><code>my-MM</code></td>
    <td>Burmese (Myanmar)</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>Catalan (Spain)</td>
    <td> </td>
    <td><code>zh-Hans-CN</code></td>
    <td>Chinese-simplified (China)</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>Chinese-simplified (Singapore)</td>
    <td> </td>
    <td><code>zh-Hant-HK</code></td>
    <td>Chinese-traditional (Hong Kong S.A.R. of China)</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>Chinese-traditional (Macao)</td>
    <td> </td>
    <td><code>zh-Hant-TW</code></td>
    <td>Chinese-traditional (Taiwan)</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>Croatian (Croatia)</td>
    <td> </td>
    <td><code>cs-CZ</code></td>
    <td>Czech (Czech Republic)</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>Danish (Denmark)</td>
    <td> </td>
    <td><code>nl-BE</code></td>
    <td>Dutch (Belgium)</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>Dutch (The Netherlands)</td>
    <td> </td>
    <td><code>en-AU</code></td>
    <td>English (Australia)</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>English (Belgium)</td>
    <td> </td>
    <td><code>en-CM</code></td>
    <td>English (Cameroon)</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>English (Canada)</td>
    <td> </td>
    <td><code>en-GH</code></td>
    <td>English (Ghana)</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>English (Hong Kong S.A.R. of China)</td>
    <td> </td>
    <td><code>en-IN</code></td>
    <td>English (India)</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>English (Ireland)</td>
    <td> </td>
    <td><code>en-KE</code></td>
    <td>English (Kenya)</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>English (Mauritius)</td>
    <td> </td>
    <td><code>en-NZ</code></td>
    <td>English (New Zealand)</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>English (Nigeria)</td>
    <td> </td>
    <td><code>en-PH</code></td>
    <td>English (Philippines)</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>English (Singapore)</td>
    <td> </td>
    <td><code>en-ZA</code></td>
    <td>English (South Africa)</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>English (Tanzania)</td>
    <td> </td>
    <td><code>en-GB</code></td>
    <td>English (United Kingdom)</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>English (United States)</td>
    <td> </td>
    <td><code>en-ZM</code></td>
    <td>English (Zambia)</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>English</td>
    <td> </td>
    <td><code>et-EE</code></td>
    <td>Estonian (Estonia)</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>Filipino (Philippines)</td>
    <td> </td>
    <td><code>fi-FI</code></td>
    <td>Finnish (Finland)</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>French (Algeria)</td>
    <td> </td>
    <td><code>fr-CM</code></td>
    <td>French (Cameroon)</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>French (Democratic Republic of the Congo)</td>
    <td> </td>
    <td><code>fr-BE</code></td>
    <td>French (Belgium)</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>French (Canada)</td>
    <td> </td>
    <td><code>fr-FR</code></td>
    <td>French (France)</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>French (Ivory Coast [Côte d’Ivoire])</td>
    <td> </td>
    <td><code>fr-LU</code></td>
    <td>French (Luxembourg)</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>French (Mauritania)</td>
    <td> </td>
    <td><code>fr-MU</code></td>
    <td>French (Mauritius)</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>French (Morocco)</td>
    <td> </td>
    <td><code>fr-SN</code></td>
    <td>French (Senegal)</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>French (Switzerland)</td>
    <td> </td>
    <td><code>fr-TN</code></td>
    <td>French (Tunisia)</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>Galician (Spain)</td>
    <td> </td>
    <td><code>lg-UG</code></td>
    <td>Ganda (Uganda)</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>Georgian (Georgia)</td>
    <td> </td>
    <td><code>de-AT</code></td>
    <td>German (Austria)</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>German (Germany)</td>
    <td> </td>
    <td><code>de-LU</code></td>
    <td>German (Luxembourg)</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>German (Switzerland)</td>
    <td> </td>
    <td><code>el-GR</code></td>
    <td>Greek (Greece)</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>Gujarati (India)</td>
    <td> </td>
    <td><code>ha-NG</code></td>
    <td>Hausa (Nigeria)</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>Hebrew (Israel)</td>
    <td> </td>
    <td><code>hi-IN</code></td>
    <td>Hindi (India)</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>Hungarian (Hungary)</td>
    <td> </td>
    <td><code>is-IS</code></td>
    <td>Icelandic (Iceland)</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>Igbo (Nigeria)</td>
    <td> </td>
    <td><code>id-ID</code></td>
    <td>Indonesian (Indonesia)</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>Italian (Italy)</td>
    <td> </td>
    <td><code>it-CH</code></td>
    <td>Italian (Switzerland)</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>Japanese (Japan)</td>
    <td> </td>
    <td><code>kn-IN</code></td>
    <td>Kannada (India)</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>Kazakh (Kazakhstan)</td>
    <td> </td>
    <td><code>km-KH</code></td>
    <td>Khmer (Cambodia)</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>Kinyarwanda (Rwanda)</td>
    <td> </td>
    <td><code>kok-IN</code></td>
    <td>Konkani (India)</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>Korean (Korea, South)</td>
    <td> </td>
    <td><code>lo-LA</code></td>
    <td>Lithuanian (Lithuania)</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>Latvian (Latvia)</td>
    <td> </td>
    <td><code>lt-LT</code></td>
    <td>Khmer (Cambodia)</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>Macedonian (Macedonia)</td>
    <td> </td>
    <td><code>ms-Latn-MY</code></td>
    <td>Malay-Latin (Malaysia)</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>Malayalam (India)</td>
    <td> </td>
    <td><code>mt-MT</code></td>
    <td>Maltese (Malta)</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>Marathi (India)</td>
    <td> </td>
    <td><code>mn-Cyrl-MN</code></td>
    <td>Mongolian-Cyrillic (Mongolia)</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>Nepali (India)</td>
    <td> </td>
    <td><code>ne-NP</code></td>
    <td>Nepali (Nepal)</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>Norwegian Bokmål (Norway)</td>
    <td> </td>
    <td><code>nn-NO</code></td>
    <td>Norwegian Nynorsk (Norway)</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>Oriya [aka, Odia] (India)</td>
    <td> </td>
    <td><code>om-ET</code></td>
    <td>Oromo (Ethiopia)</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>Polish (Poland)</td>
    <td> </td>
    <td><code>pt-AO</code></td>
    <td>Portuguese (Angola)</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>Portuguese (Brazil)</td>
    <td> </td>
    <td><code>pt-MO</code></td>
    <td>Portuguese (Macao)</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>Portuguese (Mozambique)</td>
    <td> </td>
    <td><code>pt-PT</code></td>
    <td>Portuguese (Portugal)</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>Punjabi (India)</td>
    <td> </td>
    <td><code>ro-RO</code></td>
    <td>Romanian (Romania)</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>Russian (Russia)</td>
    <td> </td>
    <td><code>sr-Cyrl-RS</code></td>
    <td>Serbian-Cyrillic (Serbia)</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>Serbian-Latin (Montenegro)</td>
    <td> </td>
    <td><code>sr-Latn-RS</code></td>
    <td>Serbian-Latin (Serbia)</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>Sinhala (Sri Lanka)</td>
    <td> </td>
    <td><code>sk-SK</code></td>
    <td>Slovak (Slovakia)</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>Slovenian (Slovenia)</td>
    <td> </td>
    <td><code>es-AR</code></td>
    <td>Spanish (Argentina)</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>Spanish (Bolivia)</td>
    <td> </td>
    <td><code>es-CL</code></td>
    <td>Spanish (Chile)</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>Spanish (Colombia)</td>
    <td> </td>
    <td><code>es-CR</code></td>
    <td>Spanish (Costa Rica)</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>Spanish (Dominican Republic)</td>
    <td> </td>
    <td><code>es-EC</code></td>
    <td>Spanish (Ecuador)</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>Spanish (El Salvador)</td>
    <td> </td>
    <td><code>es-GT</code></td>
    <td>Spanish (Guatemala)</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>Spanish (Honduras)</td>
    <td> </td>
    <td><code>es-MX</code></td>
    <td>Spanish (Mexico)</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>Spanish (Nicaragua)</td>
    <td> </td>
    <td><code>es-PA</code></td>
    <td>Spanish (Panama)</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>Spanish (Paraguay)</td>
    <td> </td>
    <td><code>es-PE</code></td>
    <td>Spanish (Peru)</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>Spanish (Puerto Rico)</td>
    <td> </td>
    <td><code>es-ES</code></td>
    <td>Spanish (Spain)</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>Spanish (United States)</td>
    <td> </td>
    <td><code>es-UY</code></td>
    <td>Spanish (Uruguay)</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>Spanish (Venezuela)</td>
    <td> </td>
    <td><code>sw-KE</code></td>
    <td>Swahili (Kenya)</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>Swahili (Tanzania)</td>
    <td> </td>
    <td><code>sv-SE</code></td>
    <td>Swedish (Sweden)</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>Tamil (India)</td>
    <td> </td>
    <td><code>te-IN</code></td>
    <td>Telugu (India)</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>Thai (Thailand)</td>
    <td> </td>
    <td><code>tr-TR</code></td>
    <td>Turkish (Turkey)</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>Ukrainian (Ukraine)</td>
    <td> </td>
    <td><code>ur-IN</code></td>
    <td>Urdu (India)</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>Urdu (Pakistan)</td>
    <td> </td>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>Uzbek-Cyrillic (Uzbekistan)</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>Uzbek-Latin (Uzbekistan)</td>
    <td> </td>
    <td><code>vi-VN</code></td>
    <td>Vietnamese (Vietnam)</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>Welsh (United Kingdom)</td>
    <td> </td>
    <td><code>yo-NG</code></td>
    <td>Yoruba (Nigeria)</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>Zulu (South Africa)</td>
    <td> </td>
    <td> </td>
    <td> </td>
  </tr>

</table>



## Next steps
Now that you've configured cloud directory, you're ready to add the code for the login widget into your app code. Click an SDK language icon in the following image to see what you need to do.
{: shortdesc}

<img usemap="#options-map" border="0" class="image" id="options" src="images/options.png" width="750" alt="Click an SDK language icon to get started with cloud directory in your apps." style="width:750px;" />
<map name="options-map" id="options-map">
<area href="login-widget.html#branded-ui-android" alt="Managing the sign in experience with the Android SDK" shape="rect" coords="187, 6, 305, 120" />
<area href="login-widget.html#branded-ui-ios-swift" alt="Managing the sign in experience with the iOS Swift SDK." shape="rect" coords="333, 6, 448, 125" />
<area href="login-widget.html#branded-ui-nodejs" alt="Managing the sign in experience with the Node.js SDK." shape="rect" coords="472, 7, 590, 121" />
</map>
