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

Multi-factor authentication (MFA) requires a user to confirm their identity in two ways. Users are required to provide something that they know - their password and something that they have - an authentication code. For example, with {{site.data.keyword.appid_full}} you can send a one-time code to a user's email when they attempt to sign in as a second form of identity verification.
{: shortdesc}

MFA is available only for Cloud Directory users. If you are using enterprise sign-in with SAML 2.0 or social login, you can enable MFA in the identity provider you are using.
{: note}

With MFA enabled, a user is required to provide two forms of identification when they attempt to sign in. After a user successfully enters their credentials, a one-time passcode is sent to the email address that is associated with their account. Each code is six-characters and is valid for five minutes. If a user does not receive the code, they can request another but the expiration time is not reset. If the code expires before it is entered correctly, the user must start the sign-in process again.

If a user's email is not confirmed, either through the APIs or email verification, it is confirmed with a successful MFA code verification. An administrator can always update or change a user's email if needed by using the [management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser).

MFA is available for instances of {{site.data.keyword.appid_short_notm}} that are on the [graduated tier pricing plan](/docs/services/appid/faq.html#faq-pricing).
{: note}

## Understanding the flow
{: #cd-mfa-understanding}



1. The user is shown {{site.data.keyword.appid_short_notm}}'s default sign in UI.

2. The user inputs their Cloud Directory user credentials, such as their email or user name and their password.

3. The credentials are validated and the MFA form is returned. The form asks the user to paste the code that is sent through email.

4. The user receives a one-time passcode to their email address and enters it into the default MFA UI.

5. The MFA code is validated and redirected to the client app with the authorization code to continue the OAuth 2 flow.


</br>

## Configuring MFA
{: #cd-mfa-configuration}

{{site.data.keyword.appid_short_notm}} MFA is supported as part of the OAuth 2.0 authorization code flow for Cloud Directory users through the Login Widget.
{: shortdesc}

To configure MFA through the GUI, check out [Cloud Directory](/docs/services/appid/cloud-directory.html).
{: note}

### Configuring with the API
{: #cd-mfa-configure-api}

You can configure MFA by using the management APIs.
{: shortdesc}

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
