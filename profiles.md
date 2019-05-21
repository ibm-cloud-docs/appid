
  </tbody>
</table>

### Preregistering a user

Now that you've learned about the process and considered your security implications, try adding a user.

**Before you begin:**

To add custom attributes for a specific user with the [/users Management API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.users_search_user_profile), you must know the following information:

* Which identity provider that the user is going to use to sign in.
* The user's unique identifier that is provided by the identity provider.

When a user signs into your app for the first time, {{site.data.keyword.appid_short_notm}} searches for the user. If found, the user inherits the identity that you assigned. If the user is not found, then a new user is created based on the information that is provided by the identity provider.

**To add a user:**

1. Log in to IBM Cloud.
  ```
  ibmcloud login
  ```
  {: codeblock}

2. Find your IAM token by running the following command.
  ```
  ibmcloud iam oauth-tokens
  ```
  {: codeblock}

3. Make a POST request to the `/users` endpoint that contains a description of the user and the attributes that you want to set as a JSON object.

  Header:
  ```
  POST {management-url}/management/v4/{tenantId}/users
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: codeblock}

  Body:
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes": {
             "mealPreference":"vegeterian"
           }
       }
   }
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the components</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>idp</em></code></td>
        <td>The identity provider that the user will authenticate with. Options include: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid`.</td>
      </tr>
      <tr>
        <td><code><em>idp-identity</em></code></td>
        <td>The unique identifier provided by the identity provider.</td>
      </tr>
      <tr>
        <td><code><em>profile</em></code></td>
        <td>The user's profile containing the custom attribute JSON mapping.</td>
      </tr>
    </tbody>
  </table>

  Example request:
  ```
  $ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
  ```
  {: screen}

3. Verify that registration was successful in one of the following ways:
  * Check for the user ID in the response.
    ```
    {
        "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
    }
    ```
    {: screen}
  * Check for the user profile that was created.

Keep in mind that a user's predefined attributes are empty until their first authentication, but the user is, for all intents and purposes, a fully authenticated user. You can use their unique ID just as you would someone who had already signed in. For instance, you can modify, search, or delete the profile.


## Next steps
{: #next-custom-attributes}

For more information about working with a specific language SDK, see the following GitHub repositories:

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">iOS Swift SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">Server Swift SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>


Didn't find an SDK for the language that your app is written in? No problem! You can integrate the service by using the APIs. {{site.data.keyword.appid_short_notm}} provides a <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> that allows log in, either anonymously or by authenticating, with a supported [identity provider](/docs/services/appid?topic=appid-managing-idp). For help implementing the API in languages such as Python and Go, <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">check out our blogs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{: tip}


</staging>