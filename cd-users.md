---
copyright:
  years: 2017, 2023
lastupdated: "2023-11-14"

keywords: manage users, registry, cloud directory, add user, delete user, tokens, attributes, migrating users, identity provider, app security

subcollection: appid
---
 
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}
{:terraform: .ph data-hd-interface='terraform'}
{:release-note: data-hd-content-type='release-note'}

# Managing users
{: #cd-users}

With Cloud Directory, you can manage your users in a scalable registry by using a pre-built functionality that enhances security and self-service.
{: shortdesc}

A Cloud Directory user is not the same thing as an {{site.data.keyword.appid_short_notm}} user. Users can sign up for your app by using the different identity provider options that you configured, or you can add them to your directory. The users that are mentioned in the following sections are the users who are associated with Cloud Directory as an identity provider.
{: note}

## Viewing user information
{: #cd-user-info}

You can see all the information that is known about all your Cloud Directory users as a JSON object by using the APIs or by using the dashboard. 
{: shortdesc}


### Viewing user information with the UI
{: #cd-view-gui}
{: ui}

You can use the {{site.data.keyword.appid_short_notm}} dashboard to view details about your app users. 

1. Go to the **Cloud Directory > Users** tab of your {{site.data.keyword.appid_short_notm}} instance.

2. Look through the table or search by using an email address to find the user that you want to see the information for. The search term must be exact.

3. In the overflow menu in the user's row, click **View user details**. A page opens that contains the user's information. Check out the following table to see what information you can see.

   | Detail | Description | 
   |-----|----| 
   |User identifier | The user identifier is dependant upon the type of user sign-up that you configured. For example, if you have an email and password flow, the identifier is the user's email. If you use the username and password flow, the identifier is the username that is given at sign-up. | 
   | Email | The primary email address that is attached to the user. |
   | First name and surname | Your user's first name and surname as they provided during the sign-up process. |
   | Last Login | The timestamp of the last time that the user logged in to your application. Note: If you added your user through the dashboard, the login is blank until the user themselves signs in to your app. When sign-in occurs, they also become an {{site.data.keyword.appid_short_notm}} user. | 
   | ID | The ID that is assigned to the user by {{site.data.keyword.appid_short_notm}}. In the UI, it isn't shown but you can copy the value and paste it in a text editor to see the value. |
   | Predefined attributes | Predefined attributes are things that are known about a user based on SCIM. |
   | Custom attributes | Custom attributes are additional information that is added to their profile or that is learned about the user's as they interact with your application. |
   | Summary | All the attributes are compiled to form one profile that gives you a complete overview of your Cloud Directory user. For more information, see [user profiles](/docs/appid?topic=appid-profiles). |
   {: caption="Table 1. The details that you can see about your users by looking in the {{site.data.keyword.appid_short_notm}} dashboard" caption-side="top"}


### Viewing user information with the API
{: #cd-view-api}
{: api}

You can use the {{site.data.keyword.appid_short_notm}} API to view details about your app users. 

1. Obtain your tenant ID from your instance of the service.

2. Search your {{site.data.keyword.appid_short_notm}} users with an identifying query, such as an email address, to find the user ID.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/Users?query=<identifyingSearchQuery>" \
   -H "accept: application/json" \
   -H "authorization: Bearer <token>"
   ```
   {: codeblock}

   Example:

   ```sh
   curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=user@domain.com 
   -H "accept: application/json" 
   -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
   ```
   {: screen}

3. By using the ID that you obtained in the previous step, make a GET request to the `cloud_directory/users` endpoint to see their full user profile.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/Users/<userID>" \
   -H "accept: application/json" \
   -H "authorization: Bearer <token>"
   ```
   {: codeblock}

   Example response:

   ```json
   {
      "sub": "c155c0ff-337a-46d3-a22a-a8f2cca08995",
      "name": "Test User",
      "email": "testuser@test.com",
      "identities": [
      {
         "provider": "cloud_directory",
         "id": "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
         "idpUserInfo": {
            "displayName": "Test User",
            "active": true,
            "mfaContext": {},
            "emails": [
            {
               "value": "testuser@test.com",
               "primary": true
            }
            ],
            "meta": {
            "lastLogin": "2019-05-20T16:33:20.699Z",
            "created": "2019-05-20T16:25:13.019Z",
            "location": "/v1/6b8ab644-1d4a-4b3e-bcd9-777ba8430a51/Users/f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            "lastModified": "2019-05-20T16:33:20.707Z",
            "resourceType": "User"
            },
            "schemas": [
            "urn:ietf:params:scim:schemas:core:2.0:User"
            ],
            "name": {
            "givenName": "Test",
            "familyName": "User",
            "formatted": "Test User"
            },
            "id": "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            "status": "CONFIRMED",
            "idpType": "cloud_directory"
         }
      }
      ]
   }
   ```
   {: screen}

   To see the full user data set that {{site.data.keyword.appid_short_notm}} supports, check out [the SCIM core schema](https://datatracker.ietf.org/doc/html/rfc7643#section-8.2).
   {: tip}




## Adding users
{: #add-users}

When a user signs up for your application, they are added as a user. For test purposes, you can add a user through the {{site.data.keyword.appid_short_notm}} dashboard or by using the API.
{: shortdesc}

When a user signs up for your application, they do so through a self-service workflow that automatically triggers emails such as a welcome or verification request. When you, as an administrator, add a user to your app a self-service workflow is not initiated, which means that users do not receive any emails from your application. If you want your users to still be notified that they're added, you can trigger the messaging flows through the [{{site.data.keyword.appid_short_notm}} management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher){: external}.

If you disable self-service sign-up or add a user on their behalf, the user does not receive a welcome or verification email when they're added.
{: tip}


### Adding users with the UI
{: #add-user-gui}
{: ui}

1. Go to the **Cloud Directory > Users** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Click **Add user**. A form opens.

3. Enter a **First name**, **Last name**, **Email**, and **Password**. Be sure that the email that you try to register is not already taken by another user. To be sure that you typed your password correctly, confirm it by entering it in the **Reenter Password** field.

4. Click **Save**. A Cloud Directory user is created.



### Adding users with the API
{: #add-user-api}
{: api}


1. Obtain your tenant ID from your application or service credentials.

2. Obtain an {{site.data.keyword.cloud_notm}} IAM token.

   ```sh
   curl -X GET "https://iam.cloud.ibm.com/oidc/token" \
   -H "accept: application/x-www-form-urlencoded"
   ```
   {: codeblock}

3. Run the following command to create a new user and a profile at the same time.

   ```sh
   curl -X POST "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/sign_up?shouldCreateProfile=true&language=en" \
   -H "accept: application/json" \
   -H "Content-Type: application/json" \
   -H "authorization: Bearer <token>" \
   -d "{ \"active\": true, \"emails\": [ { \"value\": \"<user@domain.com>\", \"primary\": true } ], \"userName\": \"<userName>\", \"password\": \"<userPassword>\"}"
   ```
   {: codeblock}



## Deleting users
{: #delete-users}

If you want to remove a user from your directory, you can delete the user from the UI or by using the APIs.
{: shortdesc}

### Deleting a single user with the UI
{: #delete-user-gui}
{: ui}

1. Go to the **Cloud Directory > Users** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Click the checkbox next to the user that you want to delete. A box opens.

3. In the box, click **Delete**. A screen opens.

4. Confirm that you understand that deleting a user cannot be undone by clicking **Delete**. If the action was a mistake, you can add the user to your directory again, but any information about that user is no longer available.


### Deleting a single user with the API
{: #delete-single-user-api}
{: api}

1. Obtain your tenant ID.

2. Obtain an {{site.data.keyword.cloud_notm}} IAM token.

   ```sh
   curl -X GET "https://iam.cloud.ibm.com/oidc/token" \
   -H "accept: application/x-www-form-urlencoded"
   ```
   {: codeblock}

3. By using the email that is attached to the user, search your directory to find the user's ID.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/users?email=<user@domain.com>" \
   -H "accept: application/json"
   ```
   {: codeblock}

4. Delete the user.

   ```sh
   curl -X DELETE "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/remove/<userID>" \
   -H "accept: application/json" \
   -H "authorization: Bearer <token>"
   ```
   {: codeblock}
   

### Deleting multiple users with the API
{: #delete-multiple-user-api}
{: api}

You can also bulk delete cloud directory users and their corresponding profiles by using the bulk delete API.

You can delete up to 100 users per request.
{: note}

1. Obtain your tenant ID.

2. Obtain an {{site.data.keyword.cloud_notm}} IAM token.

   ```sh
   curl -X GET "https://iam.cloud.ibm.com/oidc/token" \
   -H "accept: application/x-www-form-urlencoded"
   ```
   {: codeblock}

3. Delete the users by running the following command with a list of user ID's.

   ```sh
   curl -X POST "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/bulk_remove" \
   -H "accept: application/json" \
   -H "authorization: Bearer <token>"
   -d '{
   "ids": [
     "fed2634a-7a6c-4f6a-855d-8e3c73a5b5cc",
     "9380158c-19c9-4303-9111-a91743f4bad8"
     ]
   }'
   ```
   {: codeblock}
   


## Migrating users
{: #user-migration}

Occasionally, you might need to add an instance of {{site.data.keyword.appid_short_notm}}. To help with migrating to the new instance, you can use the export and import APIs for smaller migrations. If you are migrating a large number of users (16,000 or more), you can [export all of them](/docs/appid?topic=appid-cd-users#cd-export-all) or [import all of them](/docs/appid?topic=appid-cd-users#cd-import-all) with a single API request to improve your efficiency.

You must be assigned the `Manager` [IAM role](/docs/account?topic=account-access-getstarted) for both instances of {{site.data.keyword.appid_short_notm}}.
{: note}


### Exporting all users
{: #cd-export-all}

Before you can import your profiles to your new instance, you need to export them from your original instance of the service.

If you are exporting many users (16,000 or more), you can use the `export/all` API endpoint. 

1. Export all the users from your original instance of the service.

   ```sh
   curl -X POST 'https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/export/all' \
      --header 'Content-Type: application/json' \
      --header 'Authorization: Bearer <IAMToken>' \
      --data-raw '{"encryptionSecret" : "<encryptionSecret>",  
   "emailAddress" : "jdoe@example.com"}'
   ```
   {: codeblock}

2. Get the status of your request, as needed. 

   ```sh
   curl -X GET 'https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/export/status?id=<id>' --header 'Accept: application/json' \
      --header 'Content-Type: application/json' \
      --header 'Authorization: Bearer <IAMToken>'
   ```
   {: codeblock}

3. When the export is ready or if the request fails, an email is sent to the email address provided. To download the export, use the [export/download](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryDownloadExport){: external} API. 

   ```sh
   curl -X GET 'https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/export/download?id=<id>' \
      --header 'Content-Type: application/json' \
      --header 'Authorization: Bearer <IAMToken>'

   ```
   {: codeblock}

   An export file is created only when the export request is successful. If the request fails, to reduce your vulnerability risk, the data that is gathered is deleted. 
   The export is automatically deleted after 7 days or the number of days that you specify in the body of the request (in the range of 1 - 30 days). You can choose to manually delete the export by sending a request to the [delete](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryDownloadExportDelete){: external} API.
   {: note}


   | Parameters | Description |
   | ---------- | ----------- |
   | `encryptionSecret` | A custom string that is used to encrypt and decrypt a user's hashed password. Retain the encryption secret as you need it to use the [import/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImportAll){:external} API. IBM does not store the secret so if the secret is lost, you can't access the exported data. |
   | `emailAddress` | An email address to which an email is sent when the export is ready or if the request fails. |
   | `expires` | An integer that you can set (1 ≤ value ≤ 30) to specify the number of days after which the export must be deleted. The default value is 7. |
   | `tenantID` | The service tenant ID can be found in your service credentials. You can find or create your service credentials in the {{site.data.keyword.appid_short_notm}} dashboard. |
   {: caption="Table 3. Descriptions of the parameters that need to be provided in the export/all request" caption-side="top"}



### Exporting users in smaller batches
{: #cd-exporting-profiles}

The export endpoint is reserved for smaller exports of approximately less than 16,000 users. To export all your Cloud Directory users who are associated with a specific tenant ID, use the [export/all](/docs/appid?topic=appid-cd-users#cd-export-all) API endpoint.

1. Export the users from your original instance of the service.

   ```sh
   curl -X GET 'https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/export?encryption_secret=mySecret' \
   -H 'Accept: application/json' \
   -H 'Authorization: Bearer <IAMToken>'
   ```
   {: codeblock}

   | Parameters | Description |
   | ---------- | ----------- |
   | `encryptionSecret` | A custom string that is used to encrypt and decrypt a user's hashed password. |
   | `tenantID` | The service tenant ID can be found in your service credentials. You can find your service credentials in the {{site.data.keyword.appid_short_notm}} dashboard. |
   {: caption="Table 2. Descriptions of the parameters that need to be provided in the export request" caption-side="top"}

   Only your Cloud Directory users and their profiles are returned. Users from other identity providers are not.
   {: note}


### Importing all users
{: #cd-import-all}

Now that you have a list of exported Cloud Directory users, you can import them into the new instance. You can use the import-all API endpoint to import a large number of users (16,000 or more) with a single request. 

1. Import the list of exported users that you downloaded. 

   ```sh
   curl -X POST 'https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/import/all' \
   --header 'Content-Type: multipart/form-data' \
   --header 'Authorization: Bearer <IAMToken>' \
   --form 'file=@<User/desktop/myfolder/user_list.json>' \
   --form 'encryptionSecret=mySecret' \
   --form 'emailAddress=jdoe@example.com'
   ```
   {: codeblock}

2. Get the status of your request, as needed.

   ```sh
   curl -X GET 'https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/import/status?id=<id>' \
   --header 'Accept: application/json' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: Bearer <IAMToken>'
   ```
   {: codeblock}

   | Parameters | Description |
   | ---------- | ----------- |
   | `encryptionSecret` | A custom string that is used to encrypt and decrypt a user's hashed password. The encryption secret is the same secret that you attached to the [export/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExportAll){: external} API. IBM does not store the secret so if the secret is lost, you can't access the exported data. |
   | `emailAddress` | An email address to which an email is sent when the export is ready or if the request fails. |
   | `tenantID` | The service tenant ID can be found in your service credentials. You can find or create your service credentials in the {{site.data.keyword.appid_short_notm}} dashboard. |
   | `file`| The output from the [export/download](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryDownloadExport){: external} endpoint. |
   {: caption="Table 4. Descriptions of the parameters that need to be provided in the import/all request" caption-side="top"}


### Importing users in smaller batches
{: #cd-import}

You can use the import API endpoint to import small groups of users. You can add up to only 50 users per request with the import API endpoint. To add all your users through a single request, use the [import/all](/docs/appid?topic=appid-cd-users#cd-import-all) API endpoint.

1. If your users are [assigned roles](/docs/appid?topic=appid-access-control), be sure to create the roles and scopes in your new instance of {{site.data.keyword.appid_short_notm}}.

   The roles and scopes must be created exactly as they were in the previous instance with the same spellings.
   {: tip}

2. Users are imported with a new Cloud Directory identifier. If your app references the Cloud Directory identifier in any way, you can choose to create a custom attribute and adjust your application to call the attribute instead of the identifier directly. 

3. Import the users to your new instance of the service.

   ```sh
   curl -X POST 'https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/cloud_directory/import?encryption_secret=mySecret'
   --header 'Content-Type: application/json' 
   --header 'Accept: application/json' 
   --header 'Authorization: Bearer <IAMToken>' 
   -d '{"users": [
      {
         "scimUser": {
            "originalId": "3f3f6779-7978-4383-926f-a43aef3b724b",
            "name": {
            "givenName": "John",
            "familyName": "Doe",
            "formatted": "John Doe"
            },
            "displayName": "John Doe",
            "emails": [
            {
               "value": "user@example.com",
               "primary": true
            }
            ],
            "status": "PENDING"
         },
         "displayName": "Jane-Doe",
         "emails": [
            {
            "value": "jdoe@example.com",
            "primary": true
            }
         ],
         "status": "PENDING"
      },
      "passwordHash": "<passwordHashHere>",
      "passwordHashAlg": <passwordHashAlgorithm>,
      "profile": {
         "attributes": {}
      },
      "roles": []
      }
   ]}' 
   ```
   {: codeblock}


### Migration script for smaller exports and imports
{: #cd-migration-script}

{{site.data.keyword.appid_short_notm}} provides a migration script that you can use through the CLI that can help speed up the migration process when you use the export or import API endpoints. Alternatively, to make the migration process even more efficient, you can use the [export/all](/docs/appid?topic=appid-cd-users#cd-export-all) and [import/all](/docs/appid?topic=appid-cd-users#cd-import-all) API endpoints.

1.  Clone the [repository](https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users){: external}.

   ```sh
   git clone https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users.git
   ```
   {: codeblock}

2. In terminal, change to the folder that you cloned the repo into.
3. Run the following command.

   ```sh
   npm install
   ```
   {: codeblock}

4. With your parameters, run the following command.

   ```sh
   users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
   ```
   {: codeblock}

   | Parameter | Description |
   | --------- | ----------- |
   | `sourceTenantId` | The tenant ID of the instance of {{site.data.keyword.appid_short_notm}} that you plan to export users from. |
   | `destinationTenantId` | The tenant ID of the instance of {{site.data.keyword.appid_short_notm}} that you plan to import users to. |
   | `region` | Learn more about the [available regions](/docs/appid?topic=appid-regions-endpoints). | 
   | `IAM token` | For help with obtaining an IAM token, check out [the docs](/docs/account?topic=account-iamtoken_from_apikey#iamtoken_from_apikey). | 
   {: caption="Table 3. Parameter descriptions" caption-side="top"}

   Example command:

   ```sh
   users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
   ```
   {: screen}
