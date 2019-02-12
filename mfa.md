---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Multi-factor authentication
{: #cd-mfa}


Multi-factor increases the security of user authentication by requiring the user to prove who they say they are through multiple factors. The first factor is the Cloud Directory’s user password, which they normally use to login. A second authentication factor is a one-time code that {{site.data.keyword.appid_full}} sends to the user either as an SMS or email.  {{site.data.keyword.appid_short_notm}} uses a combination of both factors to verify the identity of a user.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} MFA is supported as part of the OAuth 2.0 authorization code flow for Cloud Directory users through the Login Widget. If you're using enterprise sign-in with SAML 2.0 or social login,
you can enable MFA through that identity provider.
{: note}

When MFA is enabled, the {{site.data.keyword.appid_short_notm}} Login Widget requires a second form of verification (second authentication factor) every time a user attempts to sign in. After a user has successfully entered their credentials, a one-time code is sent to the email or phone number that is registered to their account.

Check out the following diagram to see how the MFA flow works.

![MFA flow](images/mfa.png)

1. A user is shown {{site.data.keyword.appid_short_notm}}'s Login Widget and inputs their Cloud Directory user credentials, such as their email or user name and their password. The Cloud Director user credentials form the first authentication factor.

2. The credentials are validated and the MFA screen for second factor verification is returned. Based on the second factor configuration, the user receives either an email or an SMS with a one-time code and enters it into the verification screen.

3. If the MFA code is validated, the user is redirected back to the application and is signed in.



## Understanding MFA
{: #cd-mfa-understanding}


MFA is a method of confirming a user's identity by requiring them to use multiple factors to prove that they are who they say that they are. These factors can be something that they have in addition to something that they know or something that they are.
{: shortdesc}

The first time that MFA is enabled, it is set to use email by default. You can change the setting to use SMS, but you cannot configure both at the same time. For both email and SMS, there are a few settings that are configured for you and cannot be changed.


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

<p>Defined in SCIM as a <a href="https://tools.ietf.org/html/rfc7643#section-2.4" target="_blank">multi-valued attribute <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, a Cloud Directory user's email or phone number can contain the following:
<ul>
<li>Value: The actual attribute value such as email address or phone number.</li>
<li>Primary: A Boolean value that indicates the preferred value for the attribute. The primary attribute value <code>true</code> can occur once and only once. If not specified, the value of <code>primary</code> is assumed to be <code>false</code>.</li>
</ul>For example attributes, check out the [Cloud Directory docs](/docs/services/appid/cloud-directory.html#cloud-directory).</p>


### Email registration
{: #cd-mfa-email-registration}

When email is enabled, {{site.data.keyword.appid_short_notm}} automatically registers the primary email attached to the Cloud Directory user's profile. If a user's email has not already been confirmed, through either the [management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/) or through email verification on sign-up, they are confirmed when an MFA code verification is successful.

### SMS registration
{: #cd-mfa-sms-registration}

When SMS is enabled, {{site.data.keyword.appid_short_notm}} automatically tries to register the first primary phone number found on the Cloud Directory user's profile if found in a [valid format](https://en.wikipedia.org/wiki/E.164). A valid format follows the E.164 international numbering format (e.g. USA number, +1 999 888 7777). You must specify both the country code, starting with a + symbol and the national subscriber number.

If the number is invalid or no phone number is found on the user's profile, then a registration widget is displayed for the user to add a new number. This number is automatically added to the user's profile and, after validation, becomes the default number that is used for MFA.




## Configuring MFA to work with Email
{: #cd-mfa-configure-email}

Before you get started, be sure that your instance of {{site.data.keyword.appid_short_notm}} is on the [graduated tier pricing plan](/docs/services/appid/faq.html#faq-pricing).

### With the GUI
{: #cd-mfa-configure-email-gui}

To configure MFA with the GUI, check out [Cloud Directory](/docs/services/appid/cloud-directory.html).
{: note}

1. In the *Identity Provider* tab of the {{site.data.keyword.appid_short_notm}} dashboard, click *Cloud Directory*.

2. Go to the *Multi-factor authentication* tab.

3. Enable MFA. By default, turning on MFA enables email as the second authentication factor.


### With the APIs
{: #cd-mfa-configure-email-apis}

**Before you begin**

Be sure that you have the following prerequisites:

* Your {{site.data.keyword.appid_short_notm}} instance's tenant ID. This ID can be found in the **Service Credentials** section of the dashboard.
* Your Identity and Access Management (IAM) token. For help with obtaining an IAM token, check out the [IAM docs](/docs/iam/apikey_iamtoken.html).


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


  If your {{site.data.keyword.appid_short_notm}} Cloud Directory instance is configured to work with a custom email dispatcher then MFA uses the same dispatcher to send the one-time code. For more information on setting up a custom dispatcher, refer to the [Cloud Directory](/docs/services/appid?topic=appid-cd#custom-email) docs.
  {: note}


## Configuring MFA to work with SMS
{: #cd-mfa-configure-sms}

**Before you begin**

{{site.data.keyword.appid_short_notm}} uses [Nexmo](https://www.nexmo.com/products/sms) to send MFA SMS one-time codes. Before you get started, be sure that you have an instance of {{site.data.keyword.appid_short_notm}} that is on the [graduated tier pricing plan](/docs/services/appid/faq.html#faq-pricing) and the following Nexmo information.

 - Obtain your Nexmo API key and secret. You can find the Nexmo API key and secret in your account settings page on the Nexmo dashboard. Check out the [Nexmo documentation](https://developer.nexmo.com/concepts/guides/authentication#api-key-and-secret) for further information on how to obtain your credentials.

 - Register your sender ID or the `from` number with Nexmo. This `from` number is what appears on your user's phone to show who the SMS is from. For more information, check out the [Nexmo documentation](https://help.nexmo.com/hc/en-us/articles/217571017-What-is-a-Sender-ID).


### With the GUI
{: #cd-mfa-configure-sms-gui}

To configure MFA with the GUI, check out [Cloud Directory](/docs/services/appid/cloud-directory.html).
{: note}

1. In the *Identity Provider* tab of the {{site.data.keyword.appid_short_notm}} dashboard, click *Cloud Directory*.

2. Go to the *Multi-factor authentication* tab.

3. Enable MFA.

4. Select SMS as the preferred second authentication factor.

5. Configure your Nexmo account information, including your API key, secret, and the [sender's number](https://help.nexmo.com/hc/en-us/articles/217571017-What-is-a-Sender-ID).

### With the APIs
{: #cd-mfa-configure-sms-api}

**Before you begin**

Be sure that you have the following prerequisites:

* Your {{site.data.keyword.appid_short_notm}} instance's tenant ID. This ID can be found in the **Service Credentials** section of the dashboard.
* Your Identity and Access Management (IAM) token. For help with obtaining an IAM token, check out the [IAM docs](/docs/iam/apikey_iamtoken.html).


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
The `config` takes in the Nexmo API key and secret as well as the `from` number.

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
        "phone_number": "+1 999 999 9999"
      }'
  '{management-url}/management/v4/{tenantId}/config/cloud_directory/sms_dispatcher/test'
  ```
  {: screen}

  </br>
