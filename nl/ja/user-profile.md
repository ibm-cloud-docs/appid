---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# ユーザー属性へのアクセス
{: #user-profile}

個人別設定の可能なアプリ操作環境の構築に使用できるエンド・ユーザー・データを管理できます。
{:shortdesc}

ユーザー属性は、{{site.data.keyword.appid_full}} によって保管され保守されるエンティティー内の情報のセグメントです。 プロファイルには、ユーザーの属性と ID が入ります。プロファイルは、匿名にすることも、ID プロバイダーによって管理されている ID にリンクすることもできます。

{{site.data.keyword.appid_short_notm}} には、匿名ログインまたは OpenId Connect (OIDC) [ID プロバイダー](/docs/services/appid/identity-providers.html)による認証を使用したログインのための API が用意されています。 ユーザー・プロファイル属性 API エンドポイントは、ログインと許可のプロセス中に {{site.data.keyword.appid_short_notm}} が生成するアクセス・トークンによって保護されるリソースです。


## ユーザー属性の保管、読み取り、削除
{: #storing-data}

{{site.data.keyword.appid_short_notm}} には、ユーザーの属性に対する操作を作成、検索、更新、および削除するための <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> が用意されています。 このサービスには、<a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> および <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> モバイル・クライアント用の SDK も用意されています。

## Android SDK を使用したユーザー属性へのアクセス
{: #accessing}

アクセス・トークンを取得すれば、ユーザーの保護された属性のエンドポイントにアクセスできます。 以下の API メソッドを使用してアクセスできます。

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
  {: codeblock}

アクセス・トークンを明示的に渡さないと、{{site.data.keyword.appid_short_notm}} は最後に受け取ったトークンを使用します。

例えば、以下のコードを呼び出して、新しい属性を設定したり既存の属性をオーバーライドしたりできます。

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//正常な応答から受け取った JSON 形式の属性
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//例外の発生
		}
	});
  ```
  {: codeblock}

### 匿名ログイン
{: #anonymous notoc}

{{site.data.keyword.appid_short_notm}} では、[匿名](/docs/services/appid/user-profile.html#anonymous)ログインが可能です。

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//例外の発生
		}

		@Override
		public void onAuthorizationCanceled() {
			//ユーザーによる認証の取り消し
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//ユーザーの認証
		}
	});
  ```
  {: codeblock}

### 段階的な認証
{: #progressive notoc}

匿名のアクセス・トークンを保持しているユーザーは、そのトークンを `loginWidget.launch` メソッドに渡すと、識別済みユーザーとなることができます。

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {: codeblock}

匿名ログインの後には、アクセス・トークンを渡さずにログイン・ウィジェットを呼び出した場合であっても段階的な認証が行われます。最後に受け取ったトークンがサービスで使用されるからです。 保管されているトークンをクリアする場合は、以下のコマンドを実行します。

  ```java
  	appIDAuthorizationManager = new
    AppIDAuthorizationManager(this.appId);
    appIDAuthorizationManager.clearAuthorizationData();
  ```
  {: codeblock}


## iOS SDK を使用したユーザー属性へのアクセス
{: #accessing}

アクセス・トークンを取得すれば、ユーザーの保護された属性のエンドポイントにアクセスできます。 以下の API メソッドを使用すると、アクセスできるようになります。

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
  {: codeblock}

アクセス・トークンを明示的に渡さないと、{{site.data.keyword.appid_short_notm}} は最後に受け取ったトークンを使用します。

例えば、以下のコードを呼び出して、新しい属性を設定したり既存の属性をオーバーライドしたりできます。

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributes recieved as a Dictionary
      } else {
          // An error has occurred
      }
  })
  ```
  {: codeblock}


### 匿名ログイン
{: #anonymous notoc}

{{site.data.keyword.appid_short_notm}} では、[匿名](/docs/services/appid/user-profile.html#anonymous)ログインが可能です。

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //ユーザーの認証
      }

      public func onAuthorizationCanceled() {
          //ユーザーによる認証の取り消し
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //エラーの発生
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {: codeblock}

### 段階的な認証
{: #progressive notoc}

匿名のアクセス・トークンを保持している場合、このトークンを `loginWidget.launch` メソッドに渡すと、ユーザーを識別済みのユーザーにすることができます。

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {: codeblock}

匿名ログインの後には、アクセス・トークンを渡さずにログイン・ウィジェットを呼び出した場合であっても段階的な認証が行われます。最後に受け取ったトークンがサービスで使用されるからです。 保管されているトークンをクリアする場合は、以下のコマンドを実行します。

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {: codeblock}

## データ分離と暗号化
{: #data}

{{site.data.keyword.appid_short_notm}} は、ユーザー・プロファイル属性を保管して暗号化します。 マルチテナント・サービスでは、すべてのテナントには指定された暗号鍵がありそれぞれのテナントのユーザー・データはそのテナントの鍵だけで暗号化されます。

{{site.data.keyword.appid_short_notm}} は必ず、プライベートな資料を暗号化してから保管します。
