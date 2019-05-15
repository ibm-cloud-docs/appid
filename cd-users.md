---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

subcollection: appid

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


# Managing users
{: #cd-users}

Cloud Directory provides you with a user registry for your apps that scales with your user base and includes simple ways to authenticate users to your apps using email and password. Cloud Directory has pre-built functionality for enhanced security and self service, like email verification, and password reset.
{: shortdesc}


A Cloud Directory user is not the same thing as an {{site.data.keyword.appid_short_notm}} user. Users can sign up for your app by using different the identity provider options that you configured, or you can add them to your directory. The users that are mentioned in this topic are those that are associated with Cloud Directory as an identity provider.
{: note}





## Adding and deleting users
{: #add-delete-users}

You can manage your Cloud Directory users through the {{site.data.keyword.appid_short_notm}} dashboard or by using the APIs.
{: shortdesc}

When a user signs up for your application, they do so through a self-service workflow that automatically triggers emails such as a welcome or verification request. When you, as an administrator, add a user to your app a self-service workflow is not initiated, which means that users do not receive any emails from your application. If you want your users to still be notified that they've been added, you can trigger the messaging workflows through the [App ID management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher).


### Adding users
{: #add-users}

When a user signs up for your application, they are added as a user. For test purposes, you can add a user through the {{site.data.keyword.appid_short_notm}} dashboard or by using the API. When you add a user to Cloud Directory, they are not added until 

If you disable self-service sign up or add a user on their behalf, the user does not receive a welcome or verification email when they're added.
{: tip}


**To add a new user with the GUI:**

1. Navigate to the **Cloud Directory > Users** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Click **Add user**. A form displays.

3. Enter a **First name**, **Last name**, **Email**, and **Password**. Be sure that the email that you try to register is not already taken by another user. To be sure that you typed your password correctly, confirm it by entering it in the **Re-enter Password** field.

4. Click **Save**. A Cloud Directory user is created.



Now that you have a new user, try adding [custom attributes](/docs/services/appid?topic=appid-custom-attributes).
{: tip}
</br>

### Deleting users
{: #delete-users}

If you want to remove a user from your directory, you can delete the user from the GUI or by using the APIs.
{: shortdesc}

**To delete a user through the GUI:**

1. Navigate to the **Cloud Directory > Users** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Click the check box next to the user that you want to delete. A box displays.

3. In the box, click **Delete**. A screen displays.

4. Confirm that you understand that deleting a user cannot be undone by clicking **Delete**. If the action was a mistake, you can add the user to your directory again, but any information about that user is no longer available.




## Migrating users
{: #user-migration}

Occasionally you might need to set up a new instance of {{site.data.keyword.appid_short_notm}}. If you're using Cloud Directory this means that your users must be migrated to the new instance. You can use the management APIs to help with the migration.
{: shortdesc}


You must be assigned the `Manager` [IAM role](/docs/iam?topic=iam-getstarted#getstarted) for both instances of {{site.data.keyword.appid_short_notm}}.
{: note}


### Exporting
{: cd-export}

Before you can add your users to the new instance, you need to export them from your current instance. To do so, you can use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">export management API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

Example cURL command:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>Variable</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>A custom string that is used to encrypt and decrypt a users hashed password.</td>
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

Now that you have your users ready to go, you can import their information into the new instance. To do so, you can use the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">import management API<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.


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
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}



### Migration script
{: cd-migration-script}

{{site.data.keyword.appid_short_notm}} provides a migration script that you can use through the CLI that can help speed up the migration process.

Before you get started, be sure that you have the following parameter information:

<table>
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
    <td>Be sure that you have <code>manager</code> permissions before you obtain the token. For help obtaining an IAM token, check out <a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">the docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</td>
  </tr>
</table>

To run the script:

1. Clone the <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Open terminal and navigate to the folder that you cloned the repo into.
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
  {: codeblock}
