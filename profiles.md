---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-19"

keywords: authentication, authorization, identity, app security, secure, attributes, user information, storing, accessing

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
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}



# Storing and accessing profiles
{: #profiles}


With {{site.data.keyword.appid_full}}, you can compile information about the individual users of your application into a profile. The information in the profile can be learned about your users by the way that they interact with your app or added by you on their behalf. By storing the information, you can access it to help create personalized experiences of your app for your users.
{: shortdesc}

Looking for information about your Cloud Directory users? Check out [managing users](/docs/services/appid?topic=appid-cd-users).
{: tip}

## Understanding profiles
{: #profile-understand}

A user profile is all of the information that is known about a specific user - compiled into one JSON object and stored by {{site.data.keyword.appid_short_notm}}. There are two types of information, or attributes, that can be obtained and stored in a profile: `predefined` and `custom`. Predefined attributes are specific to the identity of your user and are returned by an identity provider when your user signs in to your app and can include information such as their name or age. Custom attributes are used to store additional information about your users. They can be set by you or learned about the user as they interact with your app. Custom attributes might include an assigned role, a food preference, or a preferred aisle seat on an airplane.

![{{site.data.keyword.appid_short_notm}} user profiles](images/user-profile-makeup.png){: caption="Figure 1. User profile information flow" caption-side="bottom"}


You can store up to 100 KB of information for each user.
{: note}

### How do I get the user profile information?
{: #profile-endpoint}

There are several different ways in which you can access user information, as well as several different reasons why you would want to. The endpoint that you choose to call can vary depending on your use case.

Not sure which one works best? Join our [Slack channel](https://www.ibm.com/cloud/blog/announcements/get-help-with-ibm-cloud-app-id-related-questions-on-slack){: external} and get advice directly from our development team.
{: tip}



If you need to work with an API, check out the following image and corresponding information to see how the information is pulled.

![{{site.data.keyword.appid_short_notm}} user profile endpoint options](images/user-profile-endpoints.png){: caption="Figure 2. Endpoint options that can be used to access user information" caption-side="bottom"}

<dl>
  <dt><code>/oauth/v4/{tenantId}/token</code></dt>
    <dd>After a successful authentication, you receive access and identity tokens that contain the most common user information - a name, picture, or email for example. If you want to add additional information, you can use [custom claims-mapping](/docs/services/appid?topic=appid-customizing-tokens) to configure App ID to inject the information to the token before it is returned to you.</dd>
  <dt><code>/management/v4/{tenantId}/userinfo</code></dt>
    <dd>If you need to see an in-depth view of the user profile information that is returned by an identity provider, you can call the [<code>/userinfo</code> endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo). It's recommended to use this endpoint only if the information cannot be mapped to the token as it requires extra network roundtrips.</dd>
  <dt><code>/api/v1/attributes</code></dt>
    <dd>If your application requires reading and updating custom profile attributes for a currently logged in user, then you can use the /attributes endpoint. For example, the user wants to update a food preference.</dd>
  <dt><code>/management/v4/{tenantId}/users</code></dt>
    <dd>If you're building administrative interfaces or processes that might apply to multiple users, you can use the App ID management API. Specifically, you can use the <code>/users</code> endpoint.</dd>
</dl>

The easiest ways to work with user information are by using the GUI or an SDK. With those options, all of the API calls are done behind the scenes for you.
{: tip}


## Viewing user profiles as an administrator
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


## Accessing attributes at runtime
{: profile-access-runtime}

After successful user authentication, your app receives access and identity tokens from {{site.data.keyword.appid_short_notm}}. The service automatically injects a subset of attributes into your access and identity tokens. If the information isn't in the token, you can use any of the following endpoints to find the information. 

### Accessing the `/userinfo` endpoint with an SDK
{: #profile-predefined-access}

To see the information about your users that is provided by your configured identity providers, you can access your predefined attributes.
{: shortdesc}

iOS Swift
{: ph data-hd-programlang='swift'}

If new tokens are not explicitly passed to the SDK, {{site.data.keyword.appid_short_notm}} uses the last received tokens to retrieve and validate the response. For example, you can run the following code after a successful authentication and the SDK retrieves additional information about the user.
{: ph data-hd-programlang='swift'}

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}
```
{: codeblock}
{: ph data-hd-programlang='swift'}

Alternatively, you can explicitly pass access and identity tokens. The identity token is optional, but when passed, it is used to validate the response.
{: ph data-hd-programlang='swift'}

```
AppID.sharedInstance.userProfileManager.getUserInfo(accessToken: String, identityToken: String?) { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}
```
{: codeblock}
{: ph data-hd-programlang='swift'}

Android Java
{: ph data-hd-programlang='java'}

If new tokens are not explicitly passed to the SDK, {{site.data.keyword.appid_short_notm}} uses the last received tokens to retrieve and validate the response. For example, you can run the following code after a successful authentication and the SDK retrieves additional information about the user.
{: ph data-hd-programlang='java'}

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		// retrieved user info successfully
	}

	@Override
	public void onFailure(UserInfoException e) {
		// exception occurred
	}
});
```
{: codeblock}
{: ph data-hd-programlang='java'}

Alternatively, you can explicitly pass access and identity tokens. The identity token is optional. But when passed, it is used to validate the response.
{: ph data-hd-programlang='java'}

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(accessToken, identityToken, new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		// retrieved attribute "name" successfully
	}

	@Override
	public void onFailure(UserInfoException e) {
		// exception occurred
	}
});
```
{: codeblock}
{: ph data-hd-programlang='java'}

Node.js
{: ph data-hd-programlang='javascript'}

By using a server-side SDK, you can retrieve additional information about your users. You can call the following method by using the stored access and identity tokens, or you can explicitly pass the tokens. The identity token is optional, but when passed, it's used to validate the response.
{: ph data-hd-programlang='javascript'}

```javascript
let userProfileManager = UserProfileManager(options: options)

let accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;
let identityToken = req.session[WebAppStrategy.AUTH_CONTEXT].identityToken;


// Retrieve user info and validate against the given identity token
userProfileManager.getUserInfo(accessToken, identityToken).then(function (profile) {
	// retrieved user info successfully
});

// Retrieve user info without validation
userProfileManager.getUserInfo(accessToken).then(function (profile) {
	// retrieved user info successfully
});
```
{: codeblock}
{: ph data-hd-programlang='javascript'}


Server-side Swift
{: ph data-hd-programlang='swift'}

By using a server-side SDK, you can retrieve additional information about your users. You can call the following method by using the stored access and identity tokens, or you can explicitly pass the tokens. The identity token is optional, but when passed, it's used to validate the response.
{: ph data-hd-programlang='swift'}


```swift
let userProfileManager = UserProfileManager(options: options)

let accessToken = "<access_token>"
let identityToken = "<identity_token>"

// If identity token is provided (recommended approach), response is validated against the identity token
userProfileManager.getUserInfo(accessToken: accessToken, identityToken: identityToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}

// Retrieve the UserInfo without any validation
userProfileManager.getUserInfo(accessToken: accessToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}
```
{: codeblock}
{: ph data-hd-programlang='swift'}


### Accessing the `/userinfo` endpoint with the API
{: #profile-predefined-api}


You can view additional information through the `/userinfo` endpoint.

1. Be sure that you have a valid access token with an `openid` scope. You can verify that your token is valid by using the `/introspect` endpoint.

2. Make a request to the [`/userinfo` endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo){: external}.
  ```
  GET https://<region>.appid.cloud.ibm.com/v4/<tenant_ID>/userinfo
  Authorization: 'Bearer <access_token>'
  ```
  {: codeblock}

  Example output:
  ```
  "sub": "cad9f1d4-e23b-3683-b81b-d1c4c4fd7d4c",
  "name": "John Doe",
  "email": "john.doe@gmail.com",
  "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
  "gender": "male",
  "locale": "en",
  "identities": [
      {
          "provider": "google",
          "id": "104560903311317789798",
          "profile": {
              "id": "104560903311317789798",
              "email": "john.doe@gmail.com",
              "verified_email": true,
              "name": "John Doe",
              "given_name": "John",
              "family_name": "Doe",
              "link": "https://plus.google.com/104560903311317789798",
              "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
              "gender": "male",
              "locale": "en",
              "idpType": "google"
          }
      }
  ]
  ```
  {: screen}

3. Verify that the `sub` claim exactly matches the `sub` claim in the identity token. If these do not match, do not use the returned information. To learn more about token substitution, see the <a href="https://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">OIDC specification <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

If changes are made by an external identity provider, you can get the updated information when your users log in again. Your new tokens retrieve the most up-to-date data.
{: tip}



### Accessing the `/attributes` endpoint
{: #profile-attributes-access}

Depending on your configuration, attributes are encrypted and saved as part of a user profile when a user interacts with your application. The interaction might be a user signing in or setting a preference in your app. To access the attributes, pass an access token through an API method.
{: shortdesc}

  iOS Swift
  {: ph data-hd-programlang='swift'}

  ```
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  Server-side swift
  {: ph data-hd-programlang='swift'}

  ```
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  Android Java
  {: ph data-hd-programlang='java'}

  ```
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {: codeblock}
  {: ph data-hd-programlang='java'}

  Node.js
  {: ph data-hd-programlang='javascript'}

  ```
  function getAllAttributes(accessTokenString) {}
  function getAttribute(accessTokenString, key) {}
  function setAttribute(accessTokenString, key, value) {}
  function deleteAttribute(accessTokenString, name) {}
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}


## Setting custom attributes
{: #profile-set-custom}

You can add information about your users to their profile such as a role or preference, by setting a custom attribute.
{: shortdesc}

By default, custom attributes are modifiable and can be updated by using an {{site.data.keyword.appid_short_notm}} access token from a client application. This means that without taking proper precautions either the user or the application can update custom attributes immediately following the first user sign-in, if they have an access token. This can potentially lead to unintended consequences. For example, a user might change their role from user to admin, which might expose administrative privileges to malicious users.
{: important}

### With the GUI
{: #profile-attribute-gui}

You can set and update custom attributes for your users in the {{site.data.keyword.appid_short_notm}} dashboard.

1. Go to the **User profiles > Settings** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Toggle custom attributes to **Enabled**.

3. Click **View profile** in the overflow menu of the row for the user that you want set the attribute for.

4. In the **Custom attributes** section, click **Edit**.

5. Enter the attributes that you want to add as a JSON object. For example: `{"role":"admin"}`.


### With an SDK
{: #profile-attribute-sdk}

You can add the following code to your application to allow a user to update their attributes from your app.

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

4. By using the `attributes` endpoint, make a PUT request.

    iOS Swift
    {: ph data-hd-programlang='swift'}

    ```
    AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
      guard let result = result, error == nil else {
          return // an error has occurred
      }
      // attributes recieved as a Dictionary
    })
    ```
    {: codeblock}
    {: ph data-hd-programlang='swift'}

    Android Java
    {: ph data-hd-programlang='java'}

    ```
    appId.getUserProfileManager().setAttribute(name, value, useThisToken, new UserProfileResponseListener() {
      @Override
      public void onSuccess(JSONObject attributes) {
        // attributes received in JSON format on successful response
      }

      @Override
      public void onFailure(UserAttributesException e) {
        // exception occurred
      }
    });
    ```
    {: codeblock}
    {: ph data-hd-programlang='java'}

    Node.js
    {: ph data-hd-programlang='javascript'}

    ```
    const userProfileManager = require("ibmcloud-appid").UserProfileManager;
    userProfileManager.init();

    var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

    userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
      // attributes returned as dictionary
    });
    ```
    {: codeblock}
    {: ph data-hd-programlang='javascript'}

    Server-side Swift
    {: ph data-hd-programlang='swift'}

    ```
    let userProfileManager = UserProfileManager(options: options)
    let accesstoken = "access token"

    userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
      guard let response = response, error == error else {
        return // an error has occurred
      }
      // attributes received as a Dictionary
    }
    ```
    {: codeblock}
    {: ph data-hd-programlang='swift'}

### With the API
{: #profile-attribute-api}


If you're an administrator, you can use the `/users` endpoint. If you want to configure self-service for your users at runtime, use the `/attributes` endpoint. To set custom attributes before a user signs in to your application, see [preregistering future users](/docs/services/appid?topic=appid-preregister).

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

4. Make a PUT request to either the `/users` or `/attributes` endpoint.

  * To call the `/users` endpoint, use the following example to format your command.

    ```
    curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant-ID>/users/<user-id>/profile" \
      -H "accept: application/json" \
      -H "Content-Type: application/json" \
      -H "authorization: Bearer <token>"
      -d "{ \"attributes\": { \"points\": \"150\" }}"
    ```
    {: codeblock}

  * To call the `/attributes` endpoint, use the following example to format your command.

    ```
    curl -X PUT "https://<region>.appid.cloud.ibm.com/api/v1/attributes/<attribute_name>" \
    -H "Authorization: Bearer <token>" \
    -d "<attribute_value>" 
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

