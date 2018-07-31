

## Signing up users in advance
{: #overview}

With {{site.data.keyword.appid_full}}, you can start building a profile for users that haven't signed in to your application yet. This way, if you already know who is accessing your app, you can preregister your users by associating specific attributes with each person.
{: shortdesc}

**Why would I want to add someone to my app before they sign in for the first time?**

There are times in which you might want to authorize users that you already know by using {{site.data.keyword.appid_short_notm}}. For example: Consider an application where you use {{site.data.keyword.appid_short_notm}} to federate existing users from your SAML identity provider. You might want certain users to have `admin` access immediately upon signing into the application for the first time. To make this happen, you can use the preregistration endpoint to set a custom `admin` attribute for those users which grants them access to the administration console without any further action on your part.

**How are users identified?**

You can identify your users by using one of the following:

* The user's unique ID, called the **GUID**, in the identity provider. Although this identifier always exists and is guaranteed to be unique, it is not always readily available or easy to understand. For instance, Cloud Directory uses a random 16 byte random GUID.
* If available, the user's **email** or **username**.

**How do I know which identity provider gives what information?**

Check out the following table to see which type of identity information that you can use.


<table>
  <thead>
    <tr>
      <th>Identity provider</th>
      <th>GUID</th>
      <th>Email</th>
      <th>Username</th>
      <th>Sub</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cloud Directory</td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Custom</td>
      <td> </td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td> </td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td> </td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td> </td>
      <td> </td>
    </tr>
    <tr>
      <td>IBMID</td>
      <td> </td>
      <td> </td>
      <td> </td>
      <td> </td>
    </tr>
  </tbody>
</table>


**Is there anything different about working with Cloud Directory?**

During the registration flow, a user provides an email or username only. During the registration flow, {{site.data.keyword.appid_short_notm}} enforces this restriction in addition to `email` and custom `username` formatting requirements.

Prior to registering users, you can switch between email and username in the service instance dashboard or by using the <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Identity_Providers/set_cloud_directory_idp" target="____blank">Management APIs<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

**Is there anything special that I need to do when I'm using a custom identity provider?**

When you add a user to your application in advance, you can use any unique identifier that is provided by the authentication flow. The identifier must _exactly_ match the `sub` of the signed JSON Web Token that is sent during the authorization request. If the identifier does not match, then the profile that you want to add is not linked successfully.


## Security considerations
{: security}

Unlike the predefined attributes, custom attributes are modifiable by default and can be updated using an {{site.data.keyword.appid_short_notm}} access token from a client application. This means that without taking proper precautions either the user or the application can update custom attributes immediately following the first user login, potentially leading to unintended consequences. For example, a user could potentially change their role from user to admin exposing administrative privileges to malicious users.

Every user profile contains two types of user information that can be retrieved by the `/profile` endpoint:

* The claims that are directly obtained from the identity provider and cannot be modified by the developer or the app.
* Custom attributes that are explicitly set. The attributes can be set by the developer or the application by using a valid access token.

During preregistration, you set custom attributes.

If you are setting administrative or another read-only attribute, you _must_ disable `User Profiles` attribute modification from the dashboard to prevent clients from modifying their access rights.
{: tip}


## Tutorial: Adding users to your app

Now that you've learned about preregistration and considered your security implications, try preregistering a user.

**Before you begin:**

To preregister custom attributes for a specific user by using the [/users Management API endpoint](link to endpoint or swagger), you must know the following information:

* Which identity provider that the user with authenticate with.
* The user's unique identifier that is provided by the identity provider.

When a user signs into your app for the first time, {{site.data.keyword.appid_short_notm}} searches the database of preregistered users. If found, the user inherits the  identity that you assigned as part of preregistration. If the user is not found, then a new user is created based on the information provided by the identity provider.


**To preregister users:**

1. Log into IBM Cloud.
  ```
  ibmcloud login
  ```
  {: pre}

2. Find your IAM token by running the following command.
  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. Make a POST request to the `/users` endpoint that contains a description of the user and the attributes that you want to set as a JSON object.

  Header:
  ```
  POST /<tenantId>/users HTTP/1.1
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  Body:
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes": {}
       }
   }
  ```
  {: pre}

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
        <td>The preregistered user's profile containing the custom attribute JSON mapping.</td>
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

Keep in mind that a user's identity provider attributes are empty until their first authentication, but they are for all intents and purposes a fully authenticated user. You can use their unique ID just as you would someone who had already signed in. For instance, you can modify, search, or delete the profile.

Now that you have nominated your users, try setting up a custom sign in page to streamline their experience!
