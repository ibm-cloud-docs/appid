---

copyright:
  years: 2017, 2020
lastupdated: "2020-01-29"

keywords: user information, add users, delete users, profile, access, attributes, admin, app security, authentication, authorization

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


# Managing profiles
{: #user-admin}

With {{site.data.keyword.appid_full}}, you can compile information about the individual users of your application into a profile. The information in the profile can be learned about your users by the way that they interact with your app or added by you on their behalf. By storing the information, you can access it to help create personalized experiences of your app for your users.
{: shortdesc}

Looking for information about your Cloud Directory users? Check out [managing users](/docs/services/appid?topic=appid-cd-users).
{: tip}


## Viewing user profiles
{: #profile-view}

You can see all of the information that is known about all of your users as a JSON object by using the APIs or by using the dashboard. 
{: shortdesc}


### With the GUI
{: #profile-gui}

You can use the {{site.data.keyword.appid_short_notm}} dashboard to view details about your app users. 

1. Navigate to the **User Profiles > Profiles** tab of your {{site.data.keyword.appid_short_notm}} instance.

2. Look through the table or search by using an email address to find the user that you want to see the information for. The search term must be exact.

3. In the overflow menu of the user's row, click **View user profile**. A page opens that contains the user's information. Check out the following table to see what information you can see.

  <table>
    <caption>Table 1. User details as shown in the {{site.data.keyword.appid_short_notm}} dashboard</caption>
    <tr>
      <th>Detail</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>IdP identifier</td>
      <td>The IdP identifier is issued by the provider that your user chose to sign in to your application with.</td>
    </tr>
    <tr>
      <td>Email</td>
      <td>The primary email address that is attached to the user.</td>
    </tr>
      <tr>
      <td>Name</td>
      <td>Your user's first and surname as issued by the identity provider.</td>
    </tr>
    <tr>
      <td>Identity provider</td>
      <td>The provider that your user chose to sign in with.</td>
    </tr>
    <tr>
      <td>ID</td>
      <td>The ID that is assigned to the user by {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td>Custom attributes</td>
      <td>Custom attributes are additional information that is added to their profile or that is learned about the user's as they interact with your application.</td>
    </tr>
    <tr>
      <td>Summary</td>
      <td>All of the information that is associated with that user shown as a JSON object.</td>
    </tr>
  </table>

</br>

### With the API
{: #profile-api}

You can use the {{site.data.keyword.appid_short_notm}} API to view details about your app users. 

1. Obtain your tenant ID from your instance of the service. You can find the ID in your service or application credentials. 

2. Search your {{site.data.keyword.appid_short_notm}} users with an identifying query, such as an email address, to find the user ID.

  ```
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/Users?query=<identifying-search-query>" \
  -H "accept: application/json" \
  -H "authorization: Bearer <token>"
  ```
  {: codeblock}

  Example:

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@domain.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. By using the ID that you obtained in the previous step, make a GET request to the `/users` endpoint to see their full user profile.

    ```
    curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/users/<user-id>/profile" \
    -H "accept: application/json" \
    -H "authorization: Bearer <token>"
    ```
    {: codeblock}

    Example response:

    ```
    {
        "id": "a0791903-ed4c-41cf-bd0e-a37957dad820",
        "name": "David Test-user",
        "email": "dave.test@domain.com",
        "picture": "https://platform-lookaside.fbsbx.com/platform/profilepic/?asid=11122233344455566&height=50&width=50&ext=1569429199&hash=AaAaAAAAAaAAAaaA",
        "identities": [
            {
            "provider": "facebook",
            "id": "11122233344455566",
            "idpUserInfo": {
                "id": "11122233344455566",
                "name": "David Test-user",
                "picture": {
                "data": {
                    "height": 50,
                    "is_silhouette": false,
                    "url": "https://platform-lookaside.fbsbx.com/platform/profilepic/?asid=11122233344455566&height=50&width=50&ext=1569429199&hash=AaAaAAAAAaAAAaaA"",
                    "width": 50
                }
                },
                "first_name": "David",
                "last_name": "Test-user",
                "email": "dave.test@domain.com",
                "idpType": "facebook"
            }
            }
        ],
        "attributes": {
            "role": "admin"
        }
    }
    ```
    {: screen}

  To see the full user data set that {{site.data.keyword.appid_short_notm}} supports, check out [the SCIM core schema](https://tools.ietf.org/html/rfc7643#section-8.2){: external}.
  {: tip}



## Setting custom attributes
{: #admin-set-custom}

You can add information about your users to their profile such as a role or preference, by setting a custom attribute.
{: shortdesc}

By default, custom attributes are modifiable and can be updated by using an {{site.data.keyword.appid_short_notm}} access token from a client application. This means that without taking proper precautions either the user or the application can update custom attributes immediately following the first user sign-in, if they have an access token. This can potentially lead to unintended consequences. For example, a user might change their role from user to admin, which might expose administrative privileges to malicious users.
{: important}

### With the GUI
{: #admin-attribute-gui}

You can set and update custom attributes for your users in the {{site.data.keyword.appid_short_notm}} dashboard.

1. Go to the **User profiles > Settings** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Toggle custom attributes to **Enabled**.

3. Click **View profile** in the overflow menu of the row for the user that you want set the attribute for.

4. In the **Custom attributes** section, click **Edit**.

5. Enter the attributes that you want to add as a JSON object. For example: `{"role":"admin"}`.


### With the API
{: #admin-attribute-api}

If you're an administrator, you can use the `/users` endpoint. To set custom attributes before a user signs in to your application for the first time, see [preregistering future users](/docs/services/appid?topic=appid-preregister).

1. Go to the **User profiles > Settings** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Toggle custom attributes to **Enabled**.

3. Obtain an IAM token.

  1. In the {{site.data.keyword.cloud_notm}} dashboard, click **Manage > Access (IAM)**.
  2. Select **{{site.data.keyword.cloud_notm}} API keys**.
  3. Click **Create an {{site.data.keyword.cloud_notm}} API key**.
  4. Give your key a name and describe it. Click Create. A screen displays with your key.
  5. Click **Copy** or **Download** your key. When you close the screen, you can no longer access the key.
  6. Make the following cURL request with the API key that you created.

    ```
    curl -k -X POST \
    --header "Content-Type: application/x-www-form-urlencoded" \
    --header "Accept: application/json" \
    --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
    --data-urlencode "apikey={apikey}" \
    "https://iam.cloud.ibm.com/identity/token"
    ```
    {: codeblock}

4. Make a PUT request to either the `/users` endpoint.

    ```
    curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/users/<user-id>/profile" \
      -H "accept: application/json" \
      -H "Content-Type: application/json" \
      -H "authorization: Bearer <token>"
      -d "{ \"attributes\": { \"points\": \"150\" } { \"role\": \"admin\" }}"
    ```
    {: codeblock}



## Deleting a profile
{: #profile-delete}

To completely delete a profile and remove someone as a user of your application, you must be an administrator.


### With the GUI
{: #profile-delete-gui}

1. Navigate to the **User Profiles > Profiles** tab of your {{site.data.keyword.appid_short_notm}} instance.

2. Look through the table or search by using an email address to find the user that you want to see the information for. The search term must be exact.

3. In the overflow menu of the user's row, click **Delete**. A confirmation screen opens.

4. Verify that you're deleting the correct user by checking their email against the one displayed. If it is the correct user, click **Delete**. This action cannot be undone. The user can be readded but their profile shows that they are a new user as of the date that they're readded.

### With the API
{: #profile-delete-api}

1. Obtain your tenant ID from your instance of the service. You can find the ID in your service or application credentials. 

2. Search your {{site.data.keyword.appid_short_notm}} users with an identifying query, such as an email address, to find the user ID.

  ```
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/Users?query=<identifying-search-query>" \
  -H "accept: application/json" \
  -H "authorization: Bearer <token>"
  ```
  {: codeblock}

  Example:

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@domain.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. By using the ID that you obtained in the previous step, make a `DELETE` request to the `/users` endpoint to see their full user profile.

    ```
    curl -X DELETE "https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/users/<user-id>/profile" \
    -H "accept: application/json" \
    -H "authorization: Bearer <token>"
    ```
    {: codeblock}


## Migrating user profiles
{: #migrating-profiles}

Occasionally, you might need to add an instance of {{site.data.keyword.appid_short_notm}}. To help with migrating to the new instance, you can use the export and import APIs.

You must be assigned the `Manager` [IAM role](/docs/iam?topic=iam-getstarted#getstarted) for both instances of {{site.data.keyword.appid_short_notm}}.
{: note}


### Exporting user profiles
{: #exporting-profiles}

Before you can import your profiles to your new instance, you need to export them from your original instance of the service.

1. Export the profiles from your original instance of the service.

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
        "name": "{{site.data.keyword.appid_short_notm}} Google User profile",
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
        },
        "roles": ["admin"]
      {
        "id": "1439d777-185d-4be1-8f4a-c4e8142b87ea",
        "name": "{{site.data.keyword.appid_short_notm}} Facebook User profile",
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
        },
        "roles": ["admin"]
      }
  }
  ```
  {: screen}

### Importing user profiles
{: #importing-profiles}

Now that you have a list of exported user profiles, you can import them into the new instance.

1. If your users are [assigned roles](/docs/services/appid?topic=appid-access-control), be sure to create the roles and scopes in your new instance of {{site.data.keyword.appid_short_notm}}.

  The roles and scopes must be created exactly as they were in the previous instance with the same spellings.
  {: tip}

2. Import the users to your new instance of the service.

  ```sh
  curl -X POST "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users/import" \
  -H "accept: application/json" \
  -H "Authorization: Bearer {Bearer_Token}" \
  -H "Content-Type: application/json" \
  -d "{ \"itemsPerPage\": 2, \"totalResults\": 2, \"requestOptions\": {}, \"users\": [ { \"id\": \"7ae804f3-0ed3-45f0-bc6b-1c6af868e6d6\", \"name\": \"{{site.data.keyword.appid_short_notm}} Google User profile\", \"email\": \"your@mail.com\", \"identities\": [ { \"provider\": \"google\", \"id\": \"105646725068605084546\", \"idpUserInfo\": { \"id\": \"{ID}\", \"email\": \"your@mail.com\", \"picture\": \"{profile.jpg}\" } } ], \"attributes\": { \"points\": 150 } { \"role\": admin } }, { \"id\": \"{userinfo}\", \"name\": \"{{site.data.keyword.appid_short_notm}} Facebook User profile\", \"email\": \"mail@mail.com\", \"identities\": [ { \"provider\": \"facebook\", \"id\": \"{id}\", \"picture\": { \"data\": { \"height\": 50, \"width\": 50, \"url\": \"https://{url}.com\" } }, \"first_name\": \"AppID\", \"last_name\": \"Development\" } ], \"attributes\": { \"points\": 250 } { \"role\": admin } } ]}"
  ```
  {: codeblock}
  
  When you import users to an instance of {{site.data.keyword.appid_short_notm}}, their Identity Provider identifier remains the same.
  {: note}




