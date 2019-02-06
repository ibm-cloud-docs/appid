---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Multi-factor authentication
{: #cd-mfa}

Multi-factor authentication (MFA) can require a user to input a second form of verification to confirm their identity. With {{site.data.keyword.appid_full}}, you can send a one-time code through either an SMS or their email.
{: shortdesc}

MFA is available for Cloud Directory users that are on the [graduated tier pricing plan](/docs/services/appid/faq.html#faq-pricing). If you're using enterprise sign-in with SAML 2.0 or social login,
you can enable MFA through that identity provider.
{: note}

When MFA is enabled, the {{site.data.keyword.appid_short_notm}} Login Widget requires a second form of verification every time a new user attempts to sign in. After a user successfully enters their credentials, a one-time passcode is sent to the email or phone number that is registered to their account.

Check out the following diagram to see how the MFA flow works.

![MFA flow](images/mfa.png)

1. A user is shown {{site.data.keyword.appid_short_notm}}'s Login Widget and inputs their Cloud Directory user credentials, such as their email or user name and their password.

2. The credentials are validated and the MFA validation screen is returned. Based on the channel configuration, the user receives either an email or an SMS with a one-time passcode and enters it into the MFA validation screen.

3. If the MFA code is validated, the user is redirected back to the application and is signed in.



## Understanding MFA
{: #cd-mfa-understanding}


MFA is a method of confirming a user's identity by requiring them to use something that they have in addition to something that they know to verify that they are who they say that they are.
{: shortdesc}

The first time that MDA is enabled, it is set to use email by default. You can change the setting to use SMS, but you cannot configure both at the same time. For both email and SMS, there are a few settings that are configured for you and cannot be changed.


<table>
  <tr>
    <th>Setting</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>Code characters</td>
    <td>Six numeric characters</td>
  </tr>
  <tr>
    <td>Code expiration</td>
    <td>Five minutes </p> If a user does not receive their code, they can request that another code is sent, but the expiration time is not reset. When the code expires a user must repeat the login process from the beginning.</td>
  </tr>
</table>

<p class="important">Defined in SCIM as a <a href="https://tools.ietf.org/html/rfc7643#section-2.4" target="_blank">multi-valued attribute <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, a Cloud Directory user's email or phone number must contain the following:<ul>
<li>Value: The actual attribute value such as email address or phone number.</li>
<li>Primary: A Boolean value that indicates the preferred value for the attribute. The primary attribute value <code>true</code> can occur once and only once. If not specified, the value of <code>primary</code> is assumed to be <code>false</code>.</li>
</ul>For example attributes, check out the [Cloud Directory docs](/docs/services/appid/cloud-directory.html#cloud-directory).</p>


### Email enrollment
{: #cd-mfa-email-enroll}

When email is enabled, {{site.data.keyword.appid_short_notm}} automatically enrolls the primary email attached the user's profile. If a user's email has not already been confirmed through either the management APIs or through email verification on sign-up, they are confirmed when an MFA code verification is successful.

### SMS enrollment
{: #cd-mfa-sms-enroll}

When SMS is enabled, {{site.data.keyword.appid_short_notm}} automatically tries to enroll the first primary phone number found on the user's profile if found in a [valid format](https://en.wikipedia.org/wiki/E.164). A valid format follows the E.164 international numbering format. You must specify both the country code, starting with a + symbol and the national subscriber number. If the number is invalid or no phone number is found on the user's profile, then an enrollment widget is displayed for the user to add a new number. This number is automatically added to the user's profile and once validated will become the default number that is used for MFA.


## Configuring MFA
{: #cd-mfa-configuration}

{{site.data.keyword.appid_short_notm}} MFA is supported as part of the OAuth 2.0 authorization code flow for Cloud Directory users through the Login Widget.
{: shortdesc}


To configure MFA with the GUI, check out [Cloud Directory](/docs/services/appid/cloud-directory.html).
{: note}

**Before you begin**

Be sure that you have the following prerequisites:

* Your {{site.data.keyword.appid_short_notm}} instance's tenant ID. This ID can be found in the **Service Credentials** section of the dashboard.
* Your Identity and Access Management (IAM) token. For help with obtaining an IAM token, check out the [IAM docs](/docs/iam/apikey_iamtoken.html).


### Configuring MFA to work with Email
{: #cd-mfa-configure-email}

1. Enable MFA, by making a PUT request to the `/config/mfa` endpoint with your MFA configuration to set `isActive` to `true`.

  Header:
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  Body:
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  Example request:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. Enable your MFA channel by making a PUT request to the `/mfa/channels/{channel}` endpoint with your MFA configuration. When `isActive` is set to `true`, your MFA channel is enabled.

  Header:
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channel}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  Body:
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  Example request:

  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/mfa/channels/email'
  ```
  {: screen}


  If your {{site.data.keyword.appid_short_notm}} Cloud Directory instance is configured to work with a custom email dispatcher then
  MFA will use the same dispatcher to send the one-time passcode. For more information and setting up a custom dispatcher, refer to
  the [Cloud Directory](/docs/services/appid/cloud-directory.html#custom-email) docs.
  {: note}

### Configuring MFA to work with SMS
{: #cd-mfa-configure-sms}

**Before you begin**

{{site.data.keyword.appid_short_notm}} currently only supports Nexmo as the SMS provider. You'd need your Nexmo API key
and secret to complete the MFA SMS configuration. You can find the Nexmo API key and secret in your account settings page on the
Nexmo dashboard. Check out the [Nexmo documentation](https://developer.nexmo.com/concepts/guides/authentication#api-key-and-secret)
for further information on how to obtain your credentials.

1. Enable MFA, by making a PUT request to the `/config/mfa` endpoint with your MFA configuration to set `isActive` to `true`.

Header:

  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
    Host: <management-server-url>
    Authorization: Bearer <IAM_TOKEN>
    Content-Type: application/json
  ```
  {: pre}

Body:

  ```
  {
   "isActive": true
  }
  ```
  {: pre}


Example request:

  ```
  $ curl -X PUT
  --header 'Content-Type: application/json'
  --header 'Accept: application/json'
  --header 'Authorization: Bearer <IAM_TOKEN>'
  -d '{
       "isActive": true
   }'
  '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. Enable your MFA channel by making a PUT request to the `/mfa/channels/{channel}` endpoint with your MFA configuration. When `isActive` is set to `true`, your MFA channel is enabled.
The `config` takes in the Nexmo API key and secret as well as the `from` number. This `from` number is what appears on your user's phone to show who the SMS is from. This number
has to be registered with Nexmo. Please refer to the [Nexmo documentation](https://developer.nexmo.com/messaging/sms/guides/custom-sender-id) for more details.

Header:

  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channel}
      Host: <management-server-url>
      Authorization: Bearer <IAM_TOKEN>
      Content-Type: application/json
  ```
  {: pre}

Body:

  ```
  {
      "isActive": true,
      "config": {
        "key": "nexmo key",
        "secret": "nexmo secret",
        "from": sender-phoneNumber
      }
  }
  ```
  {: pre}

Example request:

  ```
  $ curl -X PUT
   --header 'Content-Type: application/json'
   --header 'Accept: application/json'
   --header 'Authorization: Bearer <IAM_TOKEN>'
   -d '{
         "isActive": true,
         "config": {
          "key": "key",
          "secret": "secret",
          "from": 12345678900
        }
     }'
   '{management-url}/management/v4/{tenantId}/mfa/channels/nexmo'
  ```
  {: screen}


3. Once the channel is successfully configured, verify your Nexmo configuration and connection is setup
correctly using the test button on the UI or using the management API.

Header:

  ```
  POST /management/v4/{tenantId}/config/cloud_directory/sms_dispatcher/test
     Host: <management-server-url>
     Authorization: Bearer <IAM_TOKEN>
     Content-Type: application/json
  ```
  {: pre}

Body:

  ```
  {
    "phone_number": "phoneNumber-receives-test-message"
  }
  ```
  {: pre}

Example request:

  ```
  $ curl -X POST
  --header 'Content-Type: application/json'
  --header 'Accept: application/json'
  --header 'Authorization: Bearer <IAM_TOKEN>'
  -d '{
        "phone_number": "+1-999-999-9999"
      }'
  '{management-url}/management/v4/{tenantId}/config/cloud_directory/sms_dispatcher/test'
  ```
  {: screen}

  </br>
