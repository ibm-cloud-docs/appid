---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configuring cloud directory
{: #cd}

Users can sign up and sign in to your mobile and web apps by using an email and a password. A cloud directory is a user registry that is maintained in the cloud. When a user signs up for your app they're added to your directory of users. With this feature, users have the freedom to manage their own account within your app.
{: shortdesc}

</br>

## Managing directory settings
{: #cd-settings}

You can configure the notifications and level of user control for your app. Setting up your cloud directory can be done quickly, as shown in the following image. These settings can be updated at any time from the service dashboard.
{: shortdesc}

![Configuring cloud directory](/images/cloud-directory.png)

1. Be sure that cloud directory is turned on as an identity provider and set **Allow users to sign up and reset their password** to **On**. If set to **Off**, you can still add users through the console for development purposes.
3. Configure your sender details. Specify the email address from which your messages appear to be from, the sender, and to whom your users can reply.
  When you configure your action URL, be sure that you give enough time for a user to click the link. A user must verify their email to have certain options, such as the ability to request a reset of their password.
  {: tip}
4. Determine the types of emails a user receives and the sender information.
5. With the templates provided, customize your messages with your brand or personalized messages. For more information, see [Managing messages](/docs/services/appid/cloud-directory.html#cd-messages).
6. See who's signed-up for your app in the **Users** tab of the GUI.

</br>

## Managing messages
{: #cd-messages}

A template is an example of an email message that you might send to your users. You can customize the template by updating the content and layout of the message.
{: shortdesc}

1. In the **Identity Providers > Cloud Directory > Settings** tab of the dashboard, set the messages that you want to send to **On** .

2. *Optional*: Use <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">the language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to set another language that you want to use in your message templates. For a list of supported language codes, see [Supported languages](#languages).

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

You can use <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">the language management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to set the language in which your user communication can be written. You are responsible for the translation of the messages.
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



## Next steps
{: #next}

Now that you've configured cloud directory, you're ready to add the code for the login widget into your app code. Click an SDK language icon in the following image to see what you need to do.
{: shortdesc}

<img usemap="#options-map" border="0" class="image" id="options" src="images/options.png" width="750" alt="Click an SDK language icon to get started with cloud directory in your apps." style="width:750px;" />
<map name="options-map" id="options-map">
<area href="login-widget.html#branded-ui-android" alt="Managing the sign in experience with the Android SDK" shape="rect" coords="187, 6, 305, 120" />
<area href="login-widget.html#branded-ui-ios-swift" alt="Managing the sign in experience with the iOS Swift SDK." shape="rect" coords="333, 6, 448, 125" />
<area href="login-widget.html#branded-ui-nodejs" alt="Managing the sign in experience with the Node.js SDK." shape="rect" coords="472, 7, 590, 121" />
</map>
