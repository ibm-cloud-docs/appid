---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-17"

keywords: Authentication, authorization, identity, app security, secure, access management, roles, attributes, users

subcollection: appid

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}


# Tutorial: Setting user roles
{: #tutorial-roles}

Ensuring that the correct people, have the approved access, when they need it can be difficult when you are coding your application. To help with that process, you can use {{site.data.keyword.appid_full}} to define a custom attribute such as `role`, which allows you to assign different types of users. Then, you can use your application to enforce varying levels of permissions for each type of user. By using this step-by-step guide that you can learn to set user attributes, update them, and then inject them in to a token by using the {{site.data.keyword.appid_short_notm}} APIs.
{: shortdesc}

New to the APIs? Try them out with this [Postman collection](https://github.com/ibm-cloud-security/appid-postman).
{: tip}

## Scenario
{: #roles-scenario}

You are a developer for a fictional theme park. You're tasked with managing access for the [web application](/docs/services/appid?topic=appid-web-apps), and you feel the easiest way to do so is by setting roles for each type of user. You have several different types of roles such as park staff and visitors that all need different levels of permissions. You want to be able to streamline the process and ensure that your users are assigned the correct role from the first time they sign in to your application.  
{: shortdesc}

No problem! You can use the [custom attributes feature](/docs/services/appid?topic=appid-profiles) of {{site.data.keyword.appid_short_notm}} to store any type of user-related information. So, because you're working with role-based access control, you can create an attribute that is called `role` and assign different values to specify a type of role. For instance, the theme park might have `visitors` or `staff` that can each be different values for the `role` attribute. Then, you can ensure that your application code enforces the access policies and privileges that you assigned.

Although this tutorial is written specifically with web apps and Cloud Directory in mind, attributes can be used in a much broader sense. Custom attributes can be anything that you want them to be. As long as you stay under 100k attributes and you format them as a plain JSON object, you can store all types of information!
{: note}


## Before you begin
{: #roles-before}

Ready? Let's get started!

Be sure that you have the following prerequisites before you begin:
- An instance of the {{site.data.keyword.appid_short_notm}} service
- A set of service credentials
- An email address that you can access and validate


## Step 1: Configuring your {{site.data.keyword.appid_short_notm}} instance
{: #roles-configure-app}

Before you can start adding attributes for your Cloud Land users, you need to configure your instance of {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

1. In the **Identity Providers** tab of the service dashboard, enable **Cloud Directory**. Although this tutorial uses [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), you might also choose to use any of the other IdP's such as [SAML](/docs/services/appid?topic=appid-enterprise), [Facebook](/docs/services/appid?topic=appid-social#facebook), [Google](/docs/services/appid?topic=appid-social#google), or a [custom provider](/docs/services/appid?topic=appid-custom-identity).

2. In the **Cloud Directory > Email Verification** tab, enable verification and set **Allow users to sign-in to your app without first verifying their email address** to **No**. When you use custom attributes to set permissions-related roles, be sure that users must validate their identity before they assume the attributes that you set.

3. In the **Profiles** tab, set **Change custom attributes from the app** to **Disabled**.

  By default, custom attributes can be changed by anyone with an access token. To ensure application security, you must configure {{site.data.keyword.appid_short_notm}} so that custom attributes can be changed only by the administrator or owner of the app. This prevents users from changing their own custom attributes and granting themselves permissions that they should not have.
  {: important}

Excellent! Your dashboard is configured and you're ready to start setting roles.


## Step 2: Setting roles on behalf of another user before sign in
{: #roles-set-before}

Cloud Land has a new staff member! You know all of their information, but they don't start for several days. You can [preregister them](/docs/services/appid?topic=appid-preregister) by creating an {{site.data.keyword.appid_short_notm}} user and profile that contains the attributes such as the `staff` role.
{: shortdesc}

This process does not finish Cloud Directory registration. The user must still sign up for the app to inherit the attribute in the profile that you create.
{: tip}

1. Log in to {{site.data.keyword.cloud_notm}} by using the CLI.

  ```
  ibmcloud login
  ```
  {: codeblock}

2. Obtain an IAM access token.

  ```
  ibmcloud iam oauth-tokens
  ```
  {: codeblock}

3. Make a POST request to create a user profile for the new user that contains the `staff` attribute. Be sure that you can access and validate the email that you use.

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": “user@email.com“,
    "profile": {
      "attributes": {
        “role”: “staff”
      }
    }
  }'
  ```
  {: codeblock}

  Successful response output:

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. Validate that the profile was created with the `staff` role.

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Successful response body:

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

Great job! You preregistered a user for your application. Now, when they sign in to your app with the identifier that you used for preregistration, a Cloud Directory user is created and they inherit the {{site.data.keyword.appid_short_notm}} user profile. Next, learn how to update attributes.


## Step 3: Updating user attributes
{: #roles-update-attributes}

Cloud Land is growing! To keep up with the growth, your company is hiring new people. The `staff` user from step two is now a manager. You can update their profile by [assigning a new role](/docs/services/appid?topic=appid-profiles#profile-set-custom).
{: shortdesc}

1. Update the profile.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
        “role”: “manager”
      }
    }
  }'
  ```
  {: codeblock}

3. View the profile to verify that it was updated correctly.

  ```
  curl --request GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Successful response output:

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

Great work!


## Step 4: Injecting attributes into tokens
{: #roles-map-claims}

Becoming more popular, the theme park continues to grow! With so many new visitors and staff, you want to limit the number of requests that are made. For better performance, you can map user profile attributes to your access and identity token claims. By mapping custom claims, you're able to store the custom attributes in the tokens themselves.
{: shortdesc}

[Token configuration](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens) is global, which means that it applies to every user with a `role` attribute, regardless of the actual role they are assigned.
{: tip}


1. Make a request to the token configuration endpoint.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: codeblock}

  <table>
    <caption>Table 1. Token configuration variables</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td>
      <td>A tenant ID is how your instance of {{site.data.keyword.appid_short_notm}} is identified in the request. You can find your ID in the <em>Service credentials</em> tab of the dashboard. If you don't have a set, you can follow the steps in the GUI to create credentials.</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>For both <code>accessTokenClaim</code> and <code>idTokenClaims</code> set the source to <code>attribute</code>.</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>For both <code>accessTokenClaim</code> and <code>idTokenClaims</code> set the source claim to <code>role</code>.</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>This value applies to each token type and must be set in each request. If you previously set the value in the GUI, and then run this request, then the values in the request override the previously set values. Be sure to set the expiration to the correct value for your configuration.</td>
    </tr>
  </table>

  Successful response output:

  ```
  {
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## Step 5: Viewing the access token
{: #roles-view-token}

Optionally, you can verify that step 4 was successful by viewing an access token.
{: shortdesc}

1. For testing purposes, create a Cloud Directory user by using the {{site.data.keyword.appid_short_notm}} GUI.

  1. In the **Users** tab, click **Add User**. A form displays.
  2. Enter a first and surname, an email, and password.
  3. Click **Save**.

2. Encode your client ID and secret.

  1. In the **Service Credentials** tab of the {{site.data.keyword.appid_short_notm}} GUI, copy your client ID and Secret.
  2. Use a base64 encoder to encode your authorization information.
  3. Copy the output to use in the following command.

4. Sign in by using the APIs to obtain your access token information. The token that is returned is encoded.

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: codeblock}

5. Decode your access token.
  1. Copy the token in the response output from the previous command.
  2. In a browser, navigate to https://jwt.io/.
  3. Paste the token into the box labeled **Encoded**.

6. In the **Decoded** section, verify that you can see the role.

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "role": "manager"
  }
  ```
  {: screen}



## Next steps
{: #roles-next}

Nice work! You completed the tutorial. Next, you can try configuring [multi-factor authentication](/docs/services/appid?topic=appid-cd-mfa) or setting up [your own branded GUI](/docs/services/appid?topic=appid-branded).
