---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-14"

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
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}

# Custom user attributes
{: #custom}

With {{site.data.keyword.appid_full}}, you can save, access, and update custom attributes.
{: shortdesc}


## Setting attributes
{: #setting}

You can set roles and scopes known as attributes to a user profile. You can also override existing attributes that might have been pulled from an external identity provider.
{: shortdesc}

**Why would I want to save additional attributes about a user?**

Attributes are pieces of information about your users. By saving them, you can create profiles on your users that allow you to personalize their experience. The more attributes that are added to their profile, the more personalized their app experience can be. Check out this blog to see how creating user profiles can make a difference: <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="blank">Introducing {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

**Is there a limit to the amount of information that can be stored for each user?**

You can store 100KB of information for each user.


**To set an attribute:**

All incoming requests to your app have Authorization header, with `access_token`. You can use `access_token` to make requests to the custom attributes endpoints with one of the provided SDKs or by using [the attributes APIs](https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes).


iOS Swift:
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

Server Swift:
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

</br>

## Accessing custom attributes
{: #accessing}

Depending on your configuration, attributes are encrypted and saved as part of a user profile when a user interacts with your application. The interaction could be a user signing in or setting a preference in your app. To access the attributes, you can pass an access token through an API method. If an access token isn't explicitly passed, {{site.data.keyword.appid_short_notm}} uses the last received token.
{: shortdesc}

iOS Swift:
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

  ```
  function getAllAttributes(accessTokenString) {}
  function getAttribute(accessTokenString, key) {}
  function setAttribute(accessTokenString, key, value) {}
  function deleteAttribute(accessTokenString, name) {}
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

Server side swift:
{: ph data-hd-programlang='swift'}

  ```
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

</br>

## Security considerations
{: #security}

Before you begin working with custom attributes, be sure that you understand the security considerations.

By default, custom attributes are modifiable and can be updated by using an {{site.data.keyword.appid_short_notm}} access token from a client application. This means that without taking proper precautions either the user or the application can update custom attributes immediately following the first user sign in, provided that they have access to an access token. This can potentially lead to unintended consequences. For example, a user could change their role from user to admin which might expose administrative privileges to malicious users.

To prevent your users from changing the attributes that you give them, set **Change custom attributes from the app** to **Off** on the **Profiles** tab of the {{site.data.keyword.appid_short_notm}} dashboard. By default, it is set to **On**.
{: tip}

</br>

## Next steps
{: #next}

For more information about working with a specific language SDK, see the following GitHub repositories:

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">iOS Swift SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">Server Swift SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>


Didn't find an SDK for the language that your app is written in? No problem! You can integrate the service by using the APIs. {{site.data.keyword.appid_short_notm}} provides a <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> that allows log in, either anonymously or by authenticating, with a supported [identity provider](/docs/services/appid/manageidp.html) For help implementing the API in languages such as Python and Go, <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">check out our blogs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{: tip}
