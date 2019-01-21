---

copyright:
  years: 2014, 2019
lastupdated: "2019-01-21"

---

{:new_window: target="blank"}
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

## Audience
{: #audience}

This tutorial is intended for software developers who are working with custom attributes for the first time.
{: shortdesc}

## Time required
{: #time}

45 minutes


## Scenario
{: #scenario}

You are creating an application for a fictional theme park and you need to find a way to manage identity. The app needs to support both standard and admin user permissions, where each type of user has different permissions that limit the capabilities that they can perform. It's essential to you to streamline identity federation and the assignment of capabilities to provide the best user experience possible.
{: shortdesc}

No problem! You can integrate {{site.data.keyword.appid_short_notm}} into your application to create a tailored user experience. Before your users have ever signed in, you can create profiles on their behalf and set their custom attributes, such as user roles. When a user signs in for the first time {{site.data.keyword.appid_short_notm}} uses their verified authentication information to link them with their pre-registered profile, which enables them to inherit all of its accompanying custom attributes.


## Objectives
{: #objectives}

In this tutorial you are going to use {{site.data.keyword.appid_short_notm}} to assign permissions to both a standard user and to an administrator. To accomplish your goal, you will complete the following objectives:
{: shortdesc}

- Configure a sample application
- Pre-register a user with the admin role before he signs in for the first time
- Update a standard user's role after they've signed in
- Insert the roles into a user's token by using a global configuration
- Verify the configuration


## Before you begin
{: before}

Ready? Let's get started!

Be sure that you have the following prerequisites before you begin:
- an instance of the {{site.data.keyword.appid_short_notm}} service
- the **Administrator** IAM platform role
- Node 6.0.0 or higher


## Lesson 1: Configuring the sample app
{: #configure-app}

Before you can start adding roles and scopes for your Cloud Land users, you need to have the app! Download and configure the app to get started.
{: shortdesc}

1. In the {{site.data.keyword.appid_short_notm}} dashboard, click **Download Sample**. You can choose any language that you like, but this tutorial is written for the **Node.js** sample.

2. In **Identity Providers > Manage > Settings**, add http://localhost:3000/* to the list of allowed redirect URIs.

  This URL should not be used in any instances of {{site.data.keyword.appid_short_notm}} that support production level applications for security reasons.
  {: note}

3. In the **Identity Providers** tab of the service dashboard, enable Cloud Directory.

4. In the **Cloud Directory > Email Verification** tab, set **Allow users to sign-in to your app without first verifying their email address** to **No**. When working with custom attributes, you want to be sure that users are able to validate their identity before assuming the attributes that you set.

5. In the **Profiles** tab, set **Change custom attributes from the app** to **Disabled**.

  By default, custom attributes can be changed by anyone with an access token. To ensure application security, you must configure {{site.data.keyword.appid_short_notm}} so custom attributes can be changed only by the administrator of the application. This prevents users from changing their own custom attributes and granting themselves permissions they should not have.
  {: important}

Excellent! Your sample app is created and you're ready to start creating users.


## Lesson 2: Setting roles before user sign in
{: #set-before}

You can assign roles as a way to manage application permissions. Because you know who your application users are, you can assign roles on their behalf before they've signed in for the first time. This process creates an {{site.data.keyword.appid_short_notm}} user and profile but it is not yet associated with a specific Cloud Directory user.
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

3. Make a POST request to create a user profile for the new user that contains the `admin` attribute.

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

  You must use a real email that you have access to and are able to validate.
  {: note}

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

Great job! You preregistered a user for your application. Now, when the preregistered user signs into your app with the credentials that you used, a Cloud Directory user is created and they inherit the {{site.data.keyword.appid_short_notm}} user profile and attributes that you created. Next, learn how to update attributes.

## Lesson 3: Updating user attributes
{: #lesson-update}

In an effort to meet the growing traffic flow of your application, Cloud Land is hiring new employees. This time, you're promoting a standard user of the app to a more prominent position. You need to update their original standard user role to `admin` so that they have the permissions needed to be successful in their new role.
{: shortdesc}

1. Sign up for the sample app by using Cloud Directory, with an email that is different than the one that you used in Lesson 1.

2. View the new user's profile.

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
      }
  }
  ```
  {: screen}

2. Update the developers user profile.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/8<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
        “role”: “admin”
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
          "role": "admin"
      }
  }
  ```
  {: screen}

Great work!


## Lesson 4: Injecting attributes into tokens
{: #lesson-map-claims}

Now that you have so many new employees, you need to limit the number of requests that are made. You can map user profile attributes to your access and identity token claims. This means that you don't have to go to the [/userinfo endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V3/userInfo) or pull custom attributes later, because they're already stored in the tokens!
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

3. As one of the users that you created, log in to the sample app.

4. Click **Sign-up** and fill out the user information for your users.

5. Click **View Token**.

6. In the access token, verify that you see the role is added.

With all of your user information in one place, consider the security implications of using extended expiration times for your tokens. The longer the lifespan of your token, the higher the security risk. You can read more about the risks of using custom attributes in [Security considerations](custom-attributes.html#security).
{: tip}


## Next steps
{: #next }

Nice work! You completed the tutorial. Next, you can try configuring [multi-factor authentication](mfa.html) or setting up [your own branded GUI](branded.html).

</staging>
