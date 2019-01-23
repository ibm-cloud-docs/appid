---

copyright:
  years: 2014, 2019
lastupdated: "2019-01-23"

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



# Tutorial: Setting user roles
{: #tutorial-roles}

With {{site.data.keyword.appid_full}} you can use custom user attributes to assign roles and preferences in order to create a more personalized user experience. By using this tutorial, you can walk through a step-by-step guide to set user attributes, update them, and then inject them in to a token by using the {{site.data.keyword.appid_short_notm}} APIs.
{: shortdesc}


## Scenario
{: #scenario}

You are a developer for a fictional theme park. You are tasked with managing identity federation for the application. The app must support varying levels of staff and general visitors, and allow for each type of role to have different capabilities.
{: shortdesc}

No problem! You can use the [custom attributes feature](custom-attributes.html) of {{site.data.keyword.appid_short_notm}} to create a tailored experience for each type of user. When you know who your users are going to be, such as park staff, you can create profiles on their behalf and apply custom attributes like a `visitor` or `admin` role. When that user signs in for the first time, {{site.data.keyword.appid_short_notm}} uses their verified authentication information to link them to the preregistered profile which allows for them to inherit all the attributes that are defined in the profile.

You can create custom attributes to be anything that you want them to be. The key to using custom attributes correctly is to ensure that your application clearly defines each attributes meaning. For example, if you're using attributes to control access or user permissions, you must ensure that your application clearly defines which attribute setting a user needs in order to perform each task within your app.

Just trying it out? For an easier way to test the API commands, check out this [PostMan collection]().


## Before you begin
{: before}

Ready? Let's get started!

Be sure that you have the following prerequisites before you begin:
- An instance of the {{site.data.keyword.appid_short_notm}} service
- A set of service credentials
- Node 6.0.0 or higher
- An email address that you can access and validate


## Step 1: Configuring the sample app
{: #configure-app}

Before you can start adding attributes for your Cloud Land users, you need to have the app! Don't have one? Download and configure the app to get started.
{: shortdesc}

1. In the {{site.data.keyword.appid_short_notm}} dashboard, click **Download Sample**. You can choose any language that you like, but this tutorial is written for the **Node.js** sample.

2. In **Identity Providers > Manage > Settings**, add `http://localhost:3000/*` to the list of allowed redirect URIs.

  This URL should not be used in any instances of {{site.data.keyword.appid_short_notm}} that support production level applications for security reasons.
  {: note}

3. In the **Identity Providers** tab of the service dashboard, enable Cloud Directory. Although this tutorial uses Cloud Directory, you could also choose to use any of the other IdP's such as SAML, Facebook, Google, or a custom provider.

4. In the **Cloud Directory > Email Verification** tab, set **Allow users to sign-in to your app without first verifying their email address** to **No**. When working with custom attributes, you want to be sure that users are able to validate their identity before assuming the attributes that you set. Be sure enabled.

5. In the **Profiles** tab, set **Change custom attributes from the app** to **Disabled**.

  By default, custom attributes can be changed by anyone with an access token. To ensure application security, you must configure {{site.data.keyword.appid_short_notm}} so that custom attributes can be changed only by the administrator or owner of the app. This prevents users from changing their own custom attributes and granting themselves permissions they should not have.
  {: important}

Excellent! Your sample app is created and you're ready to start creating users.


## Step 2: Setting roles before user sign in
{: #set-before}

You recently hired a new staff member at Cloud Land. You know all of their information, but they don't start for several days. You can preregister them by creating an {{site.data.keyword.appid_short_notm}} user and profile that contains the attributes such as the `admin` role, that they need to be successful. Note that this process does not finish Cloud Directory registration. The user must still sign up for the app to inherit the attribute in the profile that you created.
{: shortdesc}

1. Log in to IBM Cloud by using the CLI.

  ```
  ibmcloud login
  ```
  {: pre}

2. Obtain an IAM access token. You can use this token for the rest of the tutorial.

  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. Make a POST request to create a user profile for the new user that contains the `admin` attribute. Be sure that you can access and validate the email that you use.

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
        “role”: “admin”
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

6. Validate that the profile was created with the admin role.

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

Great job! You preregistered a user for your application. Now, when they sign in to your app with the credentials that you used for preregistration, a Cloud Directory user is created and they inherit the {{site.data.keyword.appid_short_notm}} user profile. Next, learn how to update attributes.

## Step 3: Updating user attributes
{: #lesson-update}

Cloud Land is growing! Your company is hiring new people all the time. The `admin` user from step 2 has been promoted. In preparation for their new role, you need to update their user profile by assigning a new role.
{: shortdesc}

1. Update the admin's user profile.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/8<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
        “role”: “director”
      }
    }
  }'
  ```
  {: pre}

3. View the updated profile to verify that it was updated correctly.

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
          "role": "director"
      }
  }
  ```
  {: screen}

Great work!


## Step 4: Injecting attributes into tokens
{: #lesson-map-claims}

Becoming more and more popular, the theme park continues to grow! With so many new visitors and staff, you want to limit the number of requests that are made. For better performance, you can map user profile attributes to your access and identity token claims. By mapping custom claims, you're able to store the custom attributes in the tokens themselves.
{: shortdesc}

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

2. Restart the sample app.

3. Log in to the sample app by using the user credentials that you created for this tutorial.

4. Click **Sign-up** and fill out the user information. When you finish, an email with a validation link is sent to your email. Click the link to verify your email address.

5. Click **Login** to

5. Click **View Token**.

6. In the access token, verify that you see the role is added.

With all of your user information in one place, consider the security implications of using extended expiration times for your tokens. The longer the lifespan of your token, the higher the security risk. You can read more about the risks of using custom attributes in [Security considerations](custom-attributes.html#security).
{: tip}


## Next steps
{: #next}

Nice work! You completed the tutorial. Next, you can try configuring [multi-factor authentication](mfa.html) or setting up [your own branded GUI](branded.html).

</staging>
