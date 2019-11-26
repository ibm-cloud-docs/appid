---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-25"

keywords: Migrating users, multiple service instances, manage service, access, configuration, duplicate, export, app security, identity

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


# Managing service instances
{: #service-instance-management}

There are times when you might need to have more than one instance of {{site.data.keyword.appid_short_notm}} or migrate to a new instance. You might need to have an instance of {{site.data.keyword.appid_short_notm}} in multiple regions or different versions for different types of users. No problem! You can easily export your identity provider configuration. 
{: shortdesc}


## Migrating to another instance
{: #migrate-service}

You can migrate the information in one instance of {{site.data.keyword.appid_short_notm}} to another.
{: shortdesc}

1. Create a new instance of the service.

2. Duplicate your identity provider configuration by using the GUI.

3. Migrate your users. Known users are exported as a JSON object. Anonymous user's cannot be migrated. You can choose to import the entire object into the new instance or break it up and divide the users as you see fit if you have more than one instance.

  For Cloud Directory, see [Migrating users](/docs/services/appid?topic=appid-cd-users#user-migration). For federated identity providers, use the following steps.
  {: note}

  1. Ensure that you are assigned the `Manager` [IAM role](/docs/iam?topic=iam-getstarted#getstarted) for both instances of {{site.data.keyword.appid_short_notm}}.
  2. Export the users from your original instance of the service.

    ```sh
    curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/{tenant-ID}/users/export \
    --header "Accept: application/json" \
    --header "Authorization: Bearer {IAM-token}"
    ```
    {: codeblock}

    <table>
      <caption>User import command variables</caption>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><code>tenantID</code></td>
        <td>The service tenant ID can be found in your service credentials. You can find your service or application credentials in the {{site.data.keyword.appid_short_notm}} dashboard.</td>
      </tr>
      <tr>
        <td><code>iam-token</code></td>
        <td>Your IAM token.</td>
      </tr>
    </table>

    Example response:

    ```json
    {
      "itemsPerPage": 2,
      "totalResults": 2,
      "requestOptions": {},
      "users": [
        {
          "id": "7ae804f3-0ed3-45f0-bc6b-1c6af868e6d6",
          "name": "App ID Google User profile",
          "email": "your@mail.com",
          "identities": [
            {
              "provider": "google",
              "id": "105646725068605084546",
              "idpUserInfo": {
                "id": "105646725068605084546",
                "email": "your@mail.com",
                "picture": "profilePic.jpg"
              }
            }
          ],
          "attributes": {
            "points": 150
          }
        },
        {
          "id": "1439d777-185d-4be1-8f4a-c4e8142b87ea",
          "name": "App ID Facebook User profile",
          "email": "mail@mail.com",
          "identities": [
            {
              "provider": "facebook",
              "id": "100195207128541",
              "picture": {
                "data": {
                  "height": 50,
                  "width": 50,
                  "url": "https://url-to-idp-profile-picture.com"
                }
              },
              "first_name": "AppID",
              "last_name": "Development"
            }
          ],
          "attributes": {
            "points": 250
          }
        }
      ]
    }
    ```
    {: screen}

  3. Import the users to your new instance of the service.

    ```sh
    curl -X POST "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users/import" \
    -H "accept: application/json" \
    -H "Authorization: Bearer {Bearer_Token}" \
    -H "Content-Type: application/json" \
    -d "{ \"itemsPerPage\": 2, \"totalResults\": 2, \"requestOptions\": {}, \"users\": [ { \"id\": \"7ae804f3-0ed3-45f0-bc6b-1c6af868e6d6\", \"name\": \"App ID Google User profile\", \"email\": \"your@mail.com\", \"identities\": [ { \"provider\": \"google\", \"id\": \"105646725068605084546\", \"idpUserInfo\": { \"id\": \"{ID}\", \"email\": \"your@mail.com\", \"picture\": \"{profile.jpg}\" } } ], \"attributes\": { \"points\": 150 } }, { \"id\": \"{userinfo}\", \"name\": \"App ID Facebook User profile\", \"email\": \"mail@mail.com\", \"identities\": [ { \"provider\": \"facebook\", \"id\": \"{id}\", \"picture\": { \"data\": { \"height\": 50, \"width\": 50, \"url\": \"https://{url}.com\" } }, \"first_name\": \"AppID\", \"last_name\": \"Development\" } ], \"attributes\": { \"points\": 250 } } ]}"
    ```
    {: codeblock}
    
    When you import users to an instance of App ID, their Identity Provider identifier remains the same.
    {: note}

4. Create application credentials to invoke the new service instance.

  1. In the service dashboard navigate to the **Applications** tab.

  2. Click **Add Application** and give your application a name. Then, click **Save**.

  3. Click **View credentials** in the table and copy the output.

  4. Paste your new credentials into your application.

5. Update your application to use the new credentials including any URLs. 

6. Depending on your configuration, you might need to redeploy or unbind and rebind your application.

