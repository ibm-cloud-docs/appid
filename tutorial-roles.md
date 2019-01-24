---

copyright:
  years: 2014, 2019
lastupdated: "2019-01-24"

---

{:new_window: target="_blank"}
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



# Tutorial: Setting custom attributes
{: #tutorial-roles}

With {{site.data.keyword.appid_full}} you can use custom user attributes to assign roles and preferences in order to create a more personalized user experience. By using this tutorial, you can walk through a step-by-step guide to set user attributes, update them, and then inject them in to a token by using the {{site.data.keyword.appid_short_notm}} APIs.
{: shortdesc}

New to the APIs? Try them out with this [Postman collection](https://github.com/ibm-cloud-security/appid-postman).
{: tip}


## Scenario
{: #scenario}

You are a developer for a fictional theme park. You are tasked with managing identity federation for the [web application](web-apps.html). The app must support varying levels of staff and general visitors, and allow for each type of role to have different capabilities.
{: shortdesc}

No problem! You can use the [custom attributes feature](custom-attributes.html) of {{site.data.keyword.appid_short_notm}} to create a tailored experience for each type of user. When you know who your users are going to be, you can create profiles on their behalf and apply custom attributes like a `staff` role. When that user signs in for the first time, {{site.data.keyword.appid_short_notm}} uses their verified authentication information to link them to the preregistered profile which allows for them to inherit all the attributes that are defined in the profile.

Custom attributes can be anything that you want them to be. The key to using them correctly is to ensure that your application clearly defines each attributes meaning. For example, if you're using [attributes](user-profile.html) to control access or user permissions, you must ensure that your application clearly defines which attribute setting a user needs in order to perform each task within your app.


## Before you begin
{: before}

Ready? Let's get started!

Be sure that you have the following prerequisites before you begin:
- An instance of the {{site.data.keyword.appid_short_notm}} service
- A set of service credentials
- An email address that you can access and validate


## Step 1: Configuring your {{site.data.keyword.appid_short_notm}} instance
{: #configure-app}

Before you can start adding attributes for your Cloud Land users, you need to configure your instance of {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

1. In the **Identity Providers** tab of the service dashboard, enable **Cloud Directory**. Although this tutorial uses [Cloud Directory](cloud-directory.html), you could also choose to use any of the other IdP's such as [SAML](enterprise.html), [Facebook](identity-providers.html#facebook), [Google](identity-providers.html#google), or a [custom provider](custom.html).

2. In the **Cloud Directory > Email Verification** tab, enable verification and set **Allow users to sign-in to your app without first verifying their email address** to **No**. When you use custom attributes to set permissions related roles, be sure that users must validate their identity before assuming the attributes that you set.

3. In the **Profiles** tab, set **Change custom attributes from the app** to **Disabled**.

  By default, custom attributes can be changed by anyone with an access token. To ensure application security, you must configure {{site.data.keyword.appid_short_notm}} so that custom attributes can be changed only by the administrator or owner of the app. This prevents users from changing their own custom attributes and granting themselves permissions they should not have.
  {: important}

Excellent! Your sample app is created and you're ready to start creating users.


## Step 2: Setting roles before user sign in
{: #set-before}

You recently hired a new staff member at Cloud Land. You know all of their information, but they don't start for several days. You can [preregister them](pre-sign-in.html) by creating an {{site.data.keyword.appid_short_notm}} user and profile that contains the attributes such as the `staff` role. Note that this process does not finish Cloud Directory registration. The user must still sign up for the app to inherit the attribute in the profile that you create.
{: shortdesc}

1. Log in to {{site.data.keyword.cloud_notm}} by using the CLI.

  ```
  ibmcloud login
  ```
  {: pre}

2. Obtain an IAM access token.

  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. Make a POST request to create a user profile for the new user that contains the `staff` attribute. Be sure that you can access and validate the email that you use.

  ```
  curl --request POST \
  https://us-south.appid.ibm.cloud.com/management/v4/{{APPID_TENANT_ID}}/users \
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
  {: pre}

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
  https://us-south.appid.ibm.cloud.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

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
{: #lesson-update}

Cloud Land is growing! To keep up with the growth, your company is hiring new people. The `staff` user from step two is now a manager. You can update their profile by [assigning a new role](custom-attributes.html).
{: shortdesc}

1. Update the profile.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/8<tenant-id>/users/<user-id>/profile \
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
  {: pre}

3. View the profile to verify that it was updated correctly.

  ```
  curl --request POST \
  GET https://us-south.appid.ibm.cloud.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

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
{: #lesson-map-claims}

Becoming more and more popular, the theme park continues to grow! With so many new visitors and staff, you want to limit the number of requests that are made. For better performance, you can map user profile attributes to your access and identity token claims. By mapping custom claims, you're able to store the custom attributes in the tokens themselves.
{: shortdesc}

[Token configuration](customizing-tokens.html) is global, which means that it applies to every user with a `role` attribute, regardless of the actual role they are assigned.
{: tip}


1. Make a request to the token configuration endpoint.

  ```
  curl --request PUT \
  https://us-south.appid.ibm.cloud.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
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
  {: pre}

  <table>
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
      <td>For both your <code>accessTokenClaim</code> and your <code>idTokenClaims</code> the source should be set to <code>attribute</code>.</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>For both your <code>accessTokenClaim</code> and your <code>idTokenClaims</code> the source claim should be set to <code>role</code>.</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>This value applies to each token type and must be set in each request. If you previously set the value in the GUI, and then run this request, then the values in the request override the previously set values. Be sure to use the expiration to the correct value for your configuration.</td>
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


## Try it out
{: #trying}

Now that your token contains all of your information, try signing in and viewing the access token.
{: shortdesc}

1. For testing purposes, create a Cloud Directory user by using the {{site.data.keyword.appid_short_notm}} GUI.

  1. In the **Users** tab, click **Add User**. A form displays.
  2. Enter a first and last name, an email, and password.
  3. Click **Save**.

2. Encode your client ID and secret.

  1. In the **Service Credentials** tab of the {{site.data.keyword.appid_short_notm}} GUI, copy your client ID and Secret.
  2. Use a base64 encoder to encode your authorization information.
  3. Copy the output to use in the following command.

4. Sign in by using the APIs to obtain your access token information. The token returned is encoded.

  ```
  curl --request PUT \
  https://appid.ibm.cloud.com/oauth/v3/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: pre}

5. Decode your access token.
  1. Copy the token in the response output from the previous command.
  2. In a browser, navigate to https://jwt.io/.
  3. Paste the token into the box labeled **Encoded**.

6. In the **Decoded** section, verify that you can see the role.

  ```
  {
      iss: "appid-oauth.ng.bluemix.net",
      exp: "1548103508",
      aud: "a3b87400-f03b-4956-844e-a52103ef26ba",
      sub: "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      amr: [
            "cloud_directory"
      ],
      iat: "1548099908",
      tenant: "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      scope: "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
      role: "manager"
  }
  ```
  {: screen}

With all of your user information in one place, consider the security implications of using extended expiration times for your tokens. The longer the lifespan of your token, the higher the security risk. You can read more about the risks of using custom attributes in [Security considerations](custom-attributes.html#security).
{: tip}


## Next steps
{: #next}

Nice work! You completed the tutorial. Next, you can try configuring [multi-factor authentication](mfa.html) or setting up [your own branded GUI](branded.html).

</staging>
