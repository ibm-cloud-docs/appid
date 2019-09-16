---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-16"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# Managing users
{: #cd-users}

With Cloud Directory, you can manage your users in a scalable registry by using pre-built functionality that enhances security and self-service.
{: shortdesc}

A Cloud Directory user is not the same thing as an {{site.data.keyword.appid_short_notm}} user. Users can sign up for your app by using different the identity provider options that you configured, or you can add them to your directory. The users that are mentioned on this page are those that are associated with Cloud Directory as an identity provider.
{: note}

## Viewing user information
{: #cd-user-info}

You can see all of the information that is known about all of your Cloud Directory users as a JSON object by using the APIs or by using the dashboard. 
{: shortdesc}


### With the GUI

You can use the {{site.data.keyword.appid_short_notm}} dashboard to view details about your app users. 

1. Navigate to the **Cloud Directory > Users** tab of your {{site.data.keyword.appid_short_notm}} instance.

2. Look through the table or search by using an email address to find the user that you want to see the information for. The search term must be exact.

3. In the overflow menu in the user's row, click **View user details**. A page opens that contains the user's information. Check out the following table to see what information you can see.

<table>
  <caption>Table 1. The details that you can see about your users by looking in the {{site.data.keyword.appid_short_notm}} dashboard</caption>
  <tr>
    <th>Detail</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>User identifier</td>
    <td>The user identifier is dependant upon the type of user sign-up that you configured. If you have an email and password flow configured, the identifier is the user's email. If you use the user name and password flow, the identifier is the user name that is given at sign-up.</td>
  </tr>
  <tr>
    <td>Email</td>
    <td>The primary email address that is attached to the user.</td>
  </tr>
    <tr>
    <td>First and surname</td>
    <td>Your user's first and surname as they provided during the sign-up process.</td>
  </tr>
  <tr>
    <td>Last Login</td>
    <td>The time stamp of the last time that the user logged in to your application. Note: If you added your user through the dashboard, the login is blank until the user themselves signs in to your app. When sign-in occurs, they also become an App ID user.</td>
  </tr>
  <tr>
    <td>ID</td>
    <td>The ID that is assigned to the user by {{site.data.keyword.appid_short_notm}}. In the UI, it isn't shown but you can copy the value and paste it in a text editor to see the value.</td>
  </tr>
  <tr>
    <td>Predefined attributes</td>
    <td>Predefined attributes are things that are known about a user based on SCIM.</td>
  </tr>
  <tr>
    <td>Custom attributes</td>
    <td>Custom attributes are additional information that is added to their profile or that is learned about the user's as they interact with your application.</td>
  </tr>
  <tr>
    <td>Summary</td>
    <td>All of the attributes are compiled to form one profile that gives you a complete overview of your Cloud Directory user. For more information, see [user profiles](/docs/services/appid?topic=appid-profiles).</td>
  </tr>
</table>

</br>

### With the API

You can use the {{site.data.keyword.appid_short_notm}} API to view details about your app users. 

1. Obtain your tenant ID from your instance of the service.

2. Search your App ID users with an identifying query, such as an email address, to find the user ID.

  ```
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/cloud_directory/Users?query=<identifying-search-query>" \
   -H "accept: application/json" \
   -H "authorization: Bearer <token>"
  ```
  {: codeblock}

  Example:

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=user@domain.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. By using the ID that you obtained in the previous step, make a GET request to the `cloud_directory/users` endpoint to see their full user profile.

  ```
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/cloud_directory/Users/<user-ID>" \
  -H "accept: application/json" \
  -H "authorization: Bearer <token>"
  ```
  {: codeblock}

  Example response:

  ```
  {
    sub: "c155c0ff-337a-46d3-a22a-a8f2cca08995",
    name: "Test User",
    email: "testuser@test.com",
    identities: [
      {
        provider: "cloud_directory",
        id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
        idpUserInfo: {
          displayName: "Test User",
          active: true,
          mfaContext: {},
          emails: [
            {
              value: "testuser@test.com",
              primary: true
            }
          ],
          meta: {
            lastLogin: "2019-05-20T16:33:20.699Z",
            created: "2019-05-20T16:25:13.019Z",
            location: "/v1/6b8ab644-1d4a-4b3e-bcd9-777ba8430a51/Users/f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            lastModified: "2019-05-20T16:33:20.707Z",
            resourceType: "User"
          },
          scemas: [
            "urn:ietf:params:scim:schemas:core:2.0:User"
          ],
          name: {
            givenName: "Test",
            familyName: "User",
            formatted: "Test User"
            },
          id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
          status: "CONFIRMED",
          idpType: "cloud_directory"
        }
      }
    ]
  }
  ```
  {: screen}

  To see the full user data set that {{site.data.keyword.appid_short_notm}} supports, check out [the SCIM core schema](https://tools.ietf.org/html/rfc7643#section-8.2).
  {: tip}




## Adding users
{: #add-users}

When a user signs up for your application, they are added as a user. For test purposes, you can add a user through the {{site.data.keyword.appid_short_notm}} dashboard or by using the API.
{: shortdesc}

When a user signs up for your application, they do so through a self-service workflow that automatically triggers emails such as a welcome or verification request. When you, as an administrator, add a user to your app a self-service workflow is not initiated, which means that users do not receive any emails from your application. If you want your users to still be notified that they're added, you can trigger the messaging flows through the [App ID management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher){: external}.

If you disable self-service sign-up or add a user on their behalf, the user does not receive a welcome or verification email when they're added.
{: tip}


### Adding a user with the GUI
{: #add-user-gui}

1. Go to the **Cloud Directory > Users** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Click **Add user**. A form opens.

3. Enter a **First name**, **Last name**, **Email**, and **Password**. Be sure that the email that you try to register is not already taken by another user. To be sure that you typed your password correctly, confirm it by entering it in the **Reenter Password** field.

4. Click **Save**. A Cloud Directory user is created.

</br>



### Adding a user with the API
{: #add-user-api}


1. Obtain your tenant ID from your application or service credentials.

2. Obtain an {{site.data.keyword.cloud_notm}} IAM token.

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. Run the following user to create a new user and a profile at the same time.

  ```
  curl -X POST "https://<region>.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/sign_up?shouldCreateProfile=true&language=en" \
  -H "accept: application/json" \
  -H "Content-Type: application/json" \
  -H "authorization: Bearer <token>" \
  -d "{ \"active\": true, \"emails\": [ { \"value\": \"<user@domain.com>\", \"primary\": true } ], \"userName\": \"<myUserName>\", \"password\": \"<userPassword>\"}"
  ```
  {: codeblock}



## Deleting users
{: #delete-users}

If you want to remove a user from your directory, you can delete the user from the GUI or by using the APIs.
{: shortdesc}

### Deleting a user through the GUI
{: #delete-user-gui}

1. Go to the **Cloud Directory > Users** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Click the check box next to the user that you want to delete. A box opens.

3. In the box, click **Delete**. A screen opens.

4. Confirm that you understand that deleting a user cannot be undone by clicking **Delete**. If the action was a mistake, you can add the user to your directory again, but any information about that user is no longer available.



### Deleting a user by using the API
{: #delete-user-api}

1. Obtain your tenant ID.

2. Obtain an {{site.data.keyword.cloud_notm}} IAM token.

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" \
  -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. By using the email that is attached to the user, search your directory to find the user's ID.

  ```
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user@domain.com>" \
  -H "accept: application/json"
  ```
  {: codeblock}

4. Delete the user.

  ```
  curl -X DELETE "https://<region>.appid.test.cloud.ibm.com/management/v4/<tenant-ID>/cloud_directory/remove/<user-ID>" \
  -H "accept: application/json" \
  -H "authorization: Bearer <token>"
  ```
  {: codeblock}


## Migrating users
{: #user-migration}

Occasionally, you might need to add an instance of {{site.data.keyword.appid_short_notm}}. When you're working with Cloud Directory, your users must be migrated to the new instance. To help with the migration, you can use the management APIs.
{: shortdesc}


You must be assigned the `Manager` [IAM role](/docs/iam?topic=iam-getstarted#getstarted) for both instances of {{site.data.keyword.appid_short_notm}}.
{: note}


### Exporting
{: #cd-export}

Before you can add your users to the new instance, you need to export them from your current instance. To do so, you can use the [export management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport){: external}.


Example cURL command:

```
curl -X GET ’https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/cloud_directory/export?encryption_secret=<mySecret>' \
-H ‘Accept: application/json’ \
-H ‘Authorization: Bearer <iam-token>'
```
{: codeblock}

<table>
  <caption>Table 2. Descriptions of the parameters that need to be provided in the export request</caption>
  <tr>
    <th>Parameters</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>A custom string that is used to encrypt and decrypt a user's hashed password.</td>
  </tr>
  <tr>
    <td><code>tenantID</code></td>
    <td>The service tenant ID can be found in your service credentials. You can find your service credentials in the {{site.data.keyword.appid_short_notm}} dashboard.</td>
  </tr>
</table>

Only your Cloud Directory users and their profiles are returned. Users from other identity providers are not.
{: note}


### Importing
{: #cd-import}

Now that you have your users ready to go, you can import their information into the new instance. To do so, you can use the [import management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport){: external}.

Example cURL command:

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=mySecret’
```
{: codeblock}



### Migration script
{: #cd-migration-script}

{{site.data.keyword.appid_short_notm}} provides a migration script that you can use through the CLI that can help speed up the migration process.

Before you get started, be sure that you have the following parameter information:

<table>
  <caption>Table 3. Descriptions of the parameters that need to be provided to run the migration script</caption>
  <tr>
    <th>Parameter</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>The tenant ID of the instance of {{site.data.keyword.appid_short_notm}} that you plan to export users from.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>The tenant ID of the instance of {{site.data.keyword.appid_short_notm}} that you plan to import users to.</td>
  </tr>
  <tr>
    <td>Region</td>
    <td>Region options include: <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code>, and <code>us-south</code>.</td>
  </tr>
  <tr>
    <td>IAM token</td>
    <td>Be sure that you have <code>manager</code> permissions before you obtain the token. For help with obtaining an IAM token, check out <a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">the docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</td>
  </tr>
</table>

</br>

1. Clone the [repository](https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users){: external}.

  ```
  git clone https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users.git
  ```
  {: codeblock}

2. In terminal, change to the folder that you cloned the repo into.
3. Run the following command.

  ```
  npm install
  ```
  {: codeblock}

4. With your parameters, run the following command.

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  Example command:

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: screen}
