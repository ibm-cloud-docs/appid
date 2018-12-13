---

copyright:
  years: 2018, 2018
  lastupdated: "2018-12-13"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


## Multi-Factor Authentication
{: #mfa}

Multi-Factor Authentication (MFA) is a method of confirming a user's identity by requiring them to use something that they have in addition to something that they know to verify they are who they say they are. For example, they might have to input a code that is sent to their email in addition to signing in with their email and password.
{: shortdesc}

MFA is available only for Cloud Directory users

### Understanding the flow
{: #understanding}

**What is MFA and when why would I use it?**

MFA confirms a user’s identity by requiring multiple types of credentials. Rather than just asking for a email and password, MFA requires additional types of authentication. For example, having a user input a one-time code that is sent to a their email account or phone. Poor password management policies by users and companies alike can leave applications susceptible to exploitation by malicious actors. MFA supplements basic password based security by adding additional factors that are based on possession to establish a user's identity with greater certainty.





**How does {{site.data.keyword.appid_short_notm}} MFA work?**

![{{site.data.keyword.appid_short_notm}} mfa flow](images/mfa-flow.png)

1. A user initiates the authorization flow by sending a request to the /authorization endpoint via the App ID SDK or API.

2. The login widget in the users browser.

3. The user inputs their Cloud Directory user credentials.

4. The credentials are validated and the MFA widget is returned.

5. The user receives a one-time passcode to their primary email address and enters it into the MFA widget.

6. The MFA code is validated and redirected to the client app with the authorization code to continue the OAuth 2 flow.

MFA is a part of the graduated tier pricing plan. For more information on what that means see [the docs](/docs/services/appid/faq.html#pricing).
{:tip}

</br>

## Account Lockout
{: #account-lockout}

One-time MFA codes are entered after the first authentication which makes incorrect codes rare. If incorrect codes are used, they are treated suspiciously.
{: shortdesc}

With each incorrect MFA code entered, it is increasingly likely the account is being accessed by an unauthorized user. After three incorrect attempts, a user fails the authentication flow and is unable to sign in for 30 minutes.

</br>

## Configuring MFA
{: #configuration}

{{site.data.keyword.appid_short_notm}} MFA is supported as part of the OAuth 2.0 authorization code flow for Cloud Directory users through the login widget.
{: shortdesc}

When enabled, the login widget requires MFA each time a new user attempts to sign in. After the user has successfully entered their credentials, a one-time passcode is sent to their email address that they registered when they created their account. Each code is six-characters with an expiration of five minutes. If a user does not receive their code, they can request that another code is sent, but the expiration time is not reset. After a code expires a user is forced to repeat the entire login process.

If an MFA code is entered incorrectly multiple times, then an account is locked. For more information about account lockout, see [account lockout](#advanced-lockout).

If a user email has not already been confirmed through either the management APIs or through email verification on sign-up, it is confirmed when an MFA code verification is successful. If you need to change a user's email address, an administrator can use the [management APIs](https://appid-management.stage1.eu-gb.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser).

To configure MFA through the GUI, check out [Cloud Directory](cloud-directory.html).
{: note}

### Configuring MFA with the APIs
{: #mfa-api}

You can configure MFA by using the management APIs.

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
