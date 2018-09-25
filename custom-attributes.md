---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-25"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Accessing custom user attributes
{: #custom}

With {{site.data.keyword.appid_full}}, you can save and access your custom attributes through API endpoints.
{: shortdesc}

</br>

## Adding pre sign-in attributes
{: #sign-in}

With {{site.data.keyword.appid_full}}, you can start building a profile for users that you know are going to need access to your app, prior to their initial sign-in.
{: shortdesc}

**Why would I want to add information about a user to my app before they sign in for the first time?**

Consider an application where you use {{site.data.keyword.appid_short_notm}} to federate existing users from your SAML identity provider. You might want certain users to have `admin` access immediately upon signing into the application for the first time. To make this happen, you can use the preregistration endpoint to set a custom `admin` attribute for those users and grant them access to the administration console without any further action on your part. Be sure to consider the [security issues](#security) that can arise by changing the default setting.

**Is there a limit to the amount of information that can be stored for each user?**

You can store 100KB of information for each user.

**How are users identified?**

You can identify your users by using one of the following:

* The user's unique ID, called the **GUID**, in the identity provider. Although this identifier always exists and is guaranteed to be unique, it is not always readily available or easy to understand. For instance, Cloud Directory uses a random 16 byte random GUID.
* If available, the user's **email**.

**How do I know which identity provider gives what information?**

Check out the following table to see which type of identity information that you can use.

<table>
  <thead>
    <tr>
      <th>Identity provider</th>
      <th>GUID</th>
      <th>Email</th>
      <th>Sub</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cloud Directory</td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Custom</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>IBMID</td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td> </td>
    </tr>
  </tbody>
</table>

**Is Cloud Directory handled differently?**

In order to ensure the integrity of the preregistered user attributes,
Cloud Directory places additional requirements on its users.

1. User preregistration can only occur, while set to **email/password** mode. This can be changed from the dashboard or management APIs, see [configuring cloud directory](/cloud-directory.html#cd) for details

2. Users preregistered using their email, must have their email address confirmed. You can confirm a users identity in one of two ways: through email or manually.

  * To verify a users identity through email, set **Email verification** to **On** in the **Cloud Directory** tab of the service dashboard. If a user is added by you and signs in to your app without first verifying their email, the sign in completes successfully, but their predefined attribute is deleted.
  * To verify users manually you must be an administrator and use the [management APIs](https://appid-management.ng.bluemix.net/swagger-ui/).

**Is there anything special that I need to do when using a custom identity provider?**

When you add user information to your application in advance, you can use any unique identifier that is provided by the authentication flow. The identifier must _exactly_ match the `sub` of the signed JSON Web Token that is sent during the authorization request. If the identifier does not match, then the profile that you want to add is not linked successfully.


### Security considerations
{: #security}

Every user profile contains two types of user information that can be retrieve by the `/profile` endpoint:

* Predefined attributes that are directly obtained from the identity provider and cannot be modified by the developer or the app
* Custom attributes that are explicitly set by either the developer or an app with a valid access token

During this process, you set custom attributes. Unlike predefined attributes, custom attributes are modifiable by default and can be updated using an {{site.data.keyword.appid_short_notm}} access token from a client application. This means that without taking proper precautions either the user or the application can update custom attributes immediately following the first user sign in, provided that they have access to an access token. This can potentially lead to unintended consequences. For example, a user could change their role from user to admin which might expose administrative privileges to malicious users.

**What can I do to prevent this?**

To prevent your users from changing the attributes that you give them, set **Change custom attributes from the app** to **Off** on the **Profiles** tab of the {{site.data.keyword.appid_short_notm}} dashboard. By default, **Change custom attributes from the app** is set to **On**



### Adding user information to your app
{: #add}

Now that you've learned about the process and considered your security implications, try adding a user.

**Before you begin:**

To add custom attributes for a specific user by using the [/users](link to endpoint or swagger) Management API endpoint, you must know the following information:

* Which identity provider that the user is going to use to sign in.
* The user's unique identifier that is provided by the identity provider.

When a user signs into your app for the first time, {{site.data.keyword.appid_short_notm}} searches for the user. If found, the user inherits the identity that you assigned. If the user is not found, then a new user is created based on the information that is provided by the identity provider.

**To add a user:**

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

Now that you have associated a user with specific attributes, try setting up a [custom sign in page](custom.html) to streamline their experience!


</br>

## Accessing attributes

{{site.data.keyword.appid_short_notm}} provides a <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> that allows log in, either anonymously or by authenticating, with a supported [identity provider](/docs/services/appid/identity-providers.html). The API endpoint is a resource that is protected by the access token that is generated by {{site.data.keyword.appid_short_notm}} during the login and authorization process.
{: shortdesc}

### Accessing with the iOS SDK
{: #ios}

 You can access custom attributes by passing an access token through the following API methods.

  ```swift
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {: pre}

When an access token is not explicitly passed, {{site.data.keyword.appid_short_notm}} uses the last received token.

For example, you can call the following code to set a new attribute, or override an existing one.

  ```swift
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // an error has occurred
		}
		// attributes recieved as a Dictionary
	})
  ```
  {: pre}

  For more information about working in iOS Swift, check out the <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
  {: tip}

</br>


### Accessing with the Android SDK
{: #android}

You can access custom attributes by passing an access token through the following API methods.

```java
void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

void getAllAttributes(@NonNull UserAttributeResponseListener listener);
void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
```
{: pre}

When an access token is not explicitly passed, {{site.data.keyword.appid_short_notm}} uses the last received token.

For example, you can call the following code to set a new attribute, or override an existing one.

```java
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
{: pre}

For more information about working in Android, check out the <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{: tip}

</br>

### Accessing with the Swift Server SDK
{: #swift}

You can access custom attributes by passing an access token through the following API methods.

  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  Example usage:

  ```swift

	let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

	userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
			return // an error has occurred
		}
		// attributes recieved as a Dictionary
	}
  ```

  {: pre}

  For more information about working in Swift Server Sdk, check out the <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
  {: tip}

</br>

### Accessing with the Node.js Server SDK
{: #node}

You can access custom attributes by passing an access token through the following API methods.

  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  Example usage:

  ```javascript

	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: pre}

  For more information about working in Node.js Server Sdk, check out the <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
  {: tip}



