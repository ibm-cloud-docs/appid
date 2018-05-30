---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}


# 访问用户属性
{: #user-profile}

用户属性是由 {{site.data.keyword.appid_full}} 存储并维护的实体中的信息段。概要文件包含由身份提供者管理的用户属性和身份，也可以是匿名的。您可以使用这些概要文件为每个用户创建个性化的应用程序体验。
{:shortdesc}


{{site.data.keyword.appid_short_notm}} 提供用于登录的 API，可以匿名登录，也可以使用 OpenId Connect (OIDC) [身份提供者](/docs/services/appid/identity-providers.html)进行认证。用户概要文件属性 API 端点是通过在登录和授权过程中由 {{site.data.keyword.appid_short_notm}} 生成的访问令牌保护的资源。


## 存储、读取和删除用户属性
{: #storing-data}

{{site.data.keyword.appid_short_notm}} 提供 <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，用于对用户属性执行创建、检索、更新和删除操作。该服务还为 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 和 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 移动客户端提供 SDK。

## 使用 Android SDK 访问用户属性
{: #accessing}

获取访问令牌时，还可获取对用户保护的属性端点的访问权。您可以使用以下 API 方法来获取访问权。

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

未显式传递访问令牌时，{{site.data.keyword.appid_short_notm}} 会使用最后一次收到的令牌。

例如，可以调用以下代码来设置新属性，或者覆盖现有属性。

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//attributes received in JSON format on successful response
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Exception occurred
		}
	});
  ```
  {: pre}

### 匿名登录
{: #anonymous notoc}

通过 {{site.data.keyword.appid_short_notm}}，您可以[匿名](/docs/services/appid/user-profile.html#anonymous)登录。

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
		}

		@Override
		public void onAuthorizationCanceled() {
			//Authentication canceled by the user
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
			//User authenticated
		}
	});
  ```
  {: pre}

### 渐进式认证
{: #progressive notoc}

用户持有匿名访问令牌时，可以通过将令牌传递到 `loginWidget.launch` 方法来得到识别。

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {: pre}

匿名登录后，会执行渐进式认证，即便在未传递访问令牌的情况下调用了登录窗口小部件时也是如此，因为服务使用的是最后一次收到的令牌。如果要清除存储的令牌，请运行以下命令。

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {: pre}


## 使用 iOS SDK 访问用户属性
{: #accessing}

通过以下 API 方法传递访问令牌来访问用户属性。
{: shortdesc}

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

未显式传递访问令牌时，{{site.data.keyword.appid_short_notm}} 会使用最后一次收到的令牌。

例如，可以调用以下代码来设置新属性，或者覆盖现有属性。

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributes recieved as a Dictionary
      } else {
          // An error has occurred
      }
  })
  ```
  {: pre}


### 匿名登录

通过 {{site.data.keyword.appid_short_notm}}，您可以[匿名](/docs/services/appid/user-profile.html#anonymous)登录。

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Error occurred
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {: pre}

### 渐进式认证

持有匿名访问令牌时，用户可以通过将令牌传递到 `loginWidget.launch` 方法来成为已识别用户。

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {: pre}

匿名登录后，会执行渐进式认证，即便在未传递访问令牌的情况下调用了登录窗口小部件时也是如此，因为服务使用的是最后一次收到的令牌。如果要清除存储的令牌，请运行以下命令。

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {: pre}

## 数据分隔和加密
{: #data}

{{site.data.keyword.appid_short_notm}} 存储并加密用户概要文件属性。作为多租户服务，每个租户都具有指定的加密密钥，并且每个租户中的用户数据只使用该租户的密钥进行加密。

{{site.data.keyword.appid_short_notm}} 确保私有信息在加密后才进行存储。
