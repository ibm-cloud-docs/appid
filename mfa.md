---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Multi-Factor Authentication
{: #mfa}

Multi-Factor Authentication (MFA) is a method of confirming a user's identity by requiring them to use something that they have in addition to something that they know to verify they are who they say they are. For example, with {{site.data.keyword.appid_full}} you can have a user input a one-time code that is sent to their email after entering their email and password.
{: shortdesc}

MFA is available only for Cloud Directory users.  If you are using enterprise sign-in with SAML 2.0 or social login, you can enable MFA in the identity provider you are using.
{: note}

When MFA is enabled, the login widget requires MFA each time a new user attempts to sign in. After the user has successfully entered their credentials, a one-time passcode is sent to their email address that they registered when they created their account. Each code is six-characters with an expiration of five minutes. If a user does not receive their code, they can request that another code is sent, but the expiration time is not reset. After a code expires a user is forced to repeat the entire login process.

If a user email has not already been confirmed through either the management APIs or through email verification on sign-up, it is confirmed when an MFA code verification is successful. If you need to change a user's email address, an administrator can use the [management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser).

MFA is available for those instances of {{site.data.keyword.appid_short_notm}} that are on the [graduated tier pricing plan](faq.html#pricing).
{: note}

## Understanding the flow
{: #understanding}



1. The app user is shown {{site.data.keyword.appid_short_notm}}'s default sign in UI.

2. The user inputs their Cloud Directory user credentials, such as their email or username and their password.

3. The credentials are validated and the MFA form is returned. The form asks the user to paste the code sent via email.

4. The user receives a one-time passcode to their email address and enters it into the default MFA UI.

5. The MFA code is validated and redirected to the client app with the authorization code to continue the OAuth 2 flow.


</br>

## Configuring MFA
{: #configuration}

{{site.data.keyword.appid_short_notm}} MFA is supported as part of the OAuth 2.0 authorization code flow for Cloud Directory users through the login widget.
{: shortdesc}

To configure MFA through the GUI, check out [Cloud Directory](cloud-directory.html).
{: note}

### Configuring with the API

You can configure MFA by using the management APIs.
{: shortdesc}

**Before you begin**

Be sure that you have the following prerequisites:

* Your {{site.data.keyword.appid_short_notm}} instance's tenant ID. This can be found in the **Service Credentials** section of the dashboard.
* Your Identity and Access Management (IAM) token. For help obtaining an IAM token, check out the [IAM docs](/docs/iam/apikey_iamtoken.html).


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

2. Enable your MFA channel by making a PUT request to the `/mfa/channels/{channelType}` endpoint with your MFA configuration. When `isActive` is set to `true`, your MFA channel is enabled.

  Header:
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channelType}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3>Supported Channel Types</th>
    </thead>
    <tbody>
      <tr>
        <td>`email`</td>
      </tr>
    </tbody>
  </table>

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
    '{management-url}/management/v4/{tenantId}/mfa/channels/{channelType}'
  ```
  {: screen}

</br>
