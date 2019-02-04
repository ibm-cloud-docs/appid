---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Multi-factor authentication
{: #cd-mfa}

Multi-Factor Authentication (MFA) is a method of confirming a user's identity by requiring them to use
something that they have in addition to something that they know to verify they are who they say they are.
For example, with IBM® Cloud App ID you can require a user inputs a one-time code received in an email or
a text message after entering their login credentials to confirm their identity.
{: shortdesc}

MFA is available only for Cloud Directory users. If you are using enterprise sign-in with SAML 2.0 or social login,
you can enable MFA in the identity provider's configuration.
{: note}

When MFA is enabled, the login widget requires MFA each time a new user attempts to sign in.
After the user has successfully entered their credentials, a one-time passcode is sent to the email or phone number registered on their account. User's without a phone number will enroll a new number during thier first SMS MFA flow. Each code is six-characters with an expiration of five minutes.
If a user does not receive their code, they can request that another code is sent, but the expiration time is not reset.
After a code expires a user is forced to repeat the entire login process.

Currently {{site.data.keyword.appid_short_notm}} supports sending the one-time passcode via email or a text message. When MFA is first turned on, the email channel becomes enabled by default. You may configure your instance to deliver codes by either email or SMS, but not both at the same time.

<table>
  <thead>
    <th colspan=3>Supported Channel Types</th>
  </thead>
  <tbody>
    <tr>
      <td>`email`</td>
    </tr>
    <tr>
      <td>`sms`</td>
    </tr>
  </tbody>
</table>

MFA is available for instances of {{site.data.keyword.appid_short_notm}} that are on the [graduated tier pricing plan](/docs/services/appid/faq.html#faq-pricing).
{: note}

## Understanding the flow
{: #cd-mfa-understanding}



1. The user is shown {{site.data.keyword.appid_short_notm}}'s default sign in UI.

2. The user inputs their Cloud Directory user credentials, such as their email or user name and their password.

3. The credentials are validated and the MFA form is returned.

4. Based on the channel configured with MFA, the user will either receive an email or a text message with a one-time passcode
and will enter it into the default MFA UI.

5. The MFA code is validated and redirected to the client app with the authorization code to continue the OAuth 2 flow.

If a user email has not already been confirmed through either the management APIs or through email verification
on sign-up, they are confirmed when an MFA code verification is successful. {: note }


### Email Enrollment

When Email is enabled, {{site.data.keyword.appid_short_notm}} will automatically enroll the primary email found on the user's profile. 

### SMS Enrollment

In order to dispatch text messages, phone numbers must follow the [E.164 international numbering format](https://en.wikipedia.org/wiki/E.164) by specifying both the country code (starting with a +) and the national subscriber number. (e.g. +1 999 888 7777)

When SMS is enabled, {{site.data.keyword.appid_short_notm}} will automatically try to enroll the first primary phone number found on the user's profile if found in a valid format. 

If the number is invalid or no phone number is found on the user's profile, then an enrollment widget is displayed for the user to add a new number. This number will be automatically added to the user's profile and once validated will become the default number used for MFA.

Note (for both Email and SMS): A cloud directory  user's email or phone number value in SCIM is defined as a [multi-valued attribute](https://tools.ietf.org/html/rfc7643#section-2.4) containing:

- value: The attribute's significant value, e.g., email address, phone number.

- primary: A Boolean value indicating the 'primary' or preferred attribute value for this attribute, e.g., the preferred mailing address or the primary email address.  The primary attribute value "true" MUST appear no more than once.  If not specified, the value of "primary" SHALL be assumed to be "false".

Example attribute values can be found [here](/docs/services/appid/cloud-directory.html#cd).

## Configuring MFA
{: #cd-mfa-configuration}

{{site.data.keyword.appid_short_notm}} MFA is supported as part of the OAuth 2.0 authorization code flow for Cloud Directory users through the Login Widget.
{: shortdesc}


To configure MFA through the GUI, check out [Cloud Directory](/docs/services/appid/cloud-directory.html).
{: note}

**Before you begin**

Be sure that you have the following prerequisites:

* Your {{site.data.keyword.appid_short_notm}} instance's tenant ID. This ID can be found in the **Service Credentials** section of the dashboard.
* Your Identity and Access Management (IAM) token. For help with obtaining an IAM token, check out the [IAM docs](/docs/iam/apikey_iamtoken.html).



### Configuring MFA to work with Email
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
  the [Cloud Directory](/docs/services/appid?topic=appid-cd#custom-email) docs.  {: note}

### Configuring MFA to work with SMS
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
