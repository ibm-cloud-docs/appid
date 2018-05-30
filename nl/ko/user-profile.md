---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}


# 사용자 속성 액세스
{: #user-profile}

사용자 속성은 {{site.data.keyword.appid_full}}에서 저장하고 유지보수하는 엔티티에 포함된 정보의 한 부분입니다. 프로파일은 ID 제공자가 관리하는 사용자의 속성 및 ID를 포함하거나 익명일 수 있습니다. 프로파일을 사용하여 각 사용자에 대해 앱의 개인화된 경험을 작성할 수 있습니다.
{:shortdesc}


{{site.data.keyword.appid_short_notm}}는 익명으로 또는 OIDC(OpenId Connect) [ID 제공자](/docs/services/appid/identity-providers.html)로 인증하여 로그인을 위한 API를 제공합니다. 사용자 프로파일 속성 API 엔드포인트는 로그인 및 권한 부여 프로세스 중에 {{site.data.keyword.appid_short_notm}}에서 생성된 액세스 토큰이 보호하는 리소스입니다.


## 사용자 속성 저장, 읽기 및 삭제
{: #storing-data}

{{site.data.keyword.appid_short_notm}}는 사용자의 속성에서 작성, 검색, 업데이트 및 삭제 오퍼레이션을 수행하기 위해 <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 제공합니다. 또한, 서비스는 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 및 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 모바일 클라이언트에 SDK를 제공합니다.

## Android SDK로 사용자 속성 액세스
{: #accessing}

액세스 토큰을 확보할 때 사용자 보호 속성 엔드포인트에 대한 액세스 권한을 얻을 수 있습니다. 다음과 같은 API 메소드를 사용하여 액세스 권한을 얻을 수 있습니다.

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

액세스 토큰이 명시적으로 전달되지 않을 때 {{site.data.keyword.appid_short_notm}}는 마지막으로 수신된 토큰을 사용합니다.

예를 들어, 다음과 같은 코드를 호출하여 새 속성을 설정하거나 기존 속성을 대체할 수 있습니다.

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

### 익명 로그인
{: #anonymous notoc}

{{site.data.keyword.appid_short_notm}}에서 [익명으로](/docs/services/appid/user-profile.html#anonymous) 로그인할 수 있습니다.

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

### 점진적 인증
{: #progressive notoc}

사용자가 익명 액세스 토큰을 보유하고 있는 경우 해당 토큰을 `loginWidget.launch`
메소드에 전달하여 식별된 사용자가 될 수 있습니다.

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {: pre}

익명 로그인 후에는 서비스가 마지막으로 수신된 토큰을 사용했기 때문에 액세스 토큰을 전달하지 않고 로그인 위젯이 호출되는 경우에도 점진적 인증이 발생합니다. 저장된 토큰을 지우려는 경우 다음 명령을 실행하십시오.

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {: pre}


## iOS SDK로 사용자 속성 액세스
{: #accessing}

다음의 API 메소드를 통해 액세스 토큰을 전달하여 사용자 속성에 액세스합니다.
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

액세스 토큰이 명시적으로 전달되지 않을 때 {{site.data.keyword.appid_short_notm}}는 마지막으로 수신된 토큰을 사용합니다.

예를 들어, 다음과 같은 코드를 호출하여 새 속성을 설정하거나 기존 속성을 대체할 수 있습니다.

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


### 익명 로그인

{{site.data.keyword.appid_short_notm}}에서 [익명으로](/docs/services/appid/user-profile.html#anonymous) 로그인할 수 있습니다.

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

### 점진적 인증

익명 액세스 토큰을 보유하고 있는 경우, 사용자는 해당 토큰을 `loginWidget.launch` 메소드에 전달하여 식별된 사용자가 될 수 있습니다.

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {: pre}

익명 로그인 후에는 서비스가 마지막으로 수신된 토큰을 사용했기 때문에 액세스 토큰을 전달하지 않고 로그인 위젯이 호출되는 경우에도 점진적 인증이 발생합니다. 저장된 토큰을 지우려는 경우 다음 명령을 실행하십시오.

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {: pre}

## 데이터 분리 및 암호화
{: #data}

{{site.data.keyword.appid_short_notm}}는 사용자 프로파일 속성을 저장하고 암호화합니다. 다중 테넌트 서비스로서 모든 테넌트에는 지정된 암호화 키가 있으며 각 테넌트의 사용자 데이터는 해당 테넌트의 키로만 암호화됩니다.

{{site.data.keyword.appid_short_notm}}는 개인 정보를 저장하기 전에 암호화되었는지 확인합니다.
