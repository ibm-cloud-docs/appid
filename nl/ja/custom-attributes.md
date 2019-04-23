---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-14"

keywords: authentication, authorization, identity, app security, secure, attributes, user information, storing, accessing

subcollection: appid

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

# カスタム・ユーザー属性
{: #custom-attributes}

{{site.data.keyword.appid_full}} では、カスタム属性を保存し、それにアクセスし、更新することができます。
{: shortdesc}


## 属性の設定
{: #setting-custom-attributes}

属性と呼ばれる役割とスコープをユーザー・プロファイルに設定できます。外部の ID プロバイダーからプルされた可能性のある既存の属性をオーバーライドすることもできます。
{: shortdesc}


属性とは、ユーザーに関する情報の一部分です。 それを保存すると、ユーザーのプロファイルを作成し、それを利用してユーザーの操作環境を個別設定できるようになります。 プロファイルに追加する属性が多いほど、ユーザーのアプリ・エクスペリエンスを細かく個別設定できます。次のブログを参照して、ユーザー・プロファイルを作成する意義を確認してください。<a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="blank">{{site.data.keyword.appid_short_notm}} の紹介 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>。


ユーザーごとに 100 KB の情報を保管できます。
{: note}


**属性を設定するには、以下のようにします。**

アプリに対するすべての着信要求には許可ヘッダーがあり、そこには `access_token` が含まれています。`access_token` を使用し、提供される SDK の 1 つ、または[属性 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes) を使用して、カスタム属性エンドポイントに対する要求を行えます。


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
  		//正常な応答から受け取った JSON 形式の属性
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

サーバー Swift:
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

## カスタム属性へのアクセス
{: #accessing-custom-attributes}

構成に応じて、ユーザーがアプリケーションと対話するときに、属性が暗号化され、ユーザー・プロファイルの一部として保存されます。 この対話には、ユーザーによるアプリでのサインインや設定作業が含まれます。 属性にアクセスするには、API メソッドを介してアクセス・トークンを渡します。アクセス・トークンを明示的に渡さないと、{{site.data.keyword.appid_short_notm}} は最後に受け取ったトークンを使用します。
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

サーバー・サイド swift:
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

## セキュリティーに関する考慮事項
{: #security-custom-attributes}

カスタム属性に関する作業を開始する前に、セキュリティー上の考慮事項を理解しておく必要があります。

デフォルトでは、カスタム属性は変更可能であり、クライアント・アプリケーションから {{site.data.keyword.appid_short_notm}} アクセス・トークンを使用して更新できます。 したがって、適切な予防措置を講じないと、ユーザーまたはアプリケーションは、アクセス・トークンにアクセスできる限り、ユーザーの初回サインインの直後にカスタム属性を更新できます。 このため、意図しない結果が生じる可能性があります。 例えば、ユーザーが役割をユーザーから管理者に変更できてしまうので、管理特権が悪意のあるユーザーに付与される可能性があります。

ユーザーに付与した属性がユーザーによって変更されることがないようにするには、{{site.data.keyword.appid_short_notm}} ダッシュボードの**「プロファイル」**タブで、**「アプリからのカスタム属性の変更」**を**「オフ」**に設定します。 デフォルトでは、**「オン」**に設定されています。
{: tip}

</br>

## 次のステップ
{: #next-custom-attributes}

特定の言語の SDK での作業について詳しくは、以下の GitHub リポジトリーを参照してください。

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android SDK <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">iOS Swift SDK <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">サーバー Swift SDK <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>


アプリの作成に使用した言語の SDK が見つかりませんでしたか? 問題ありません。 API を使用してサービスを統合できます。 {{site.data.keyword.appid_short_notm}} には、サポートされる [ID プロバイダー](/docs/services/appid?topic=appid-managing-idp)を使用した、匿名または認証によるログインを可能にする <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> が用意されています。 Python や Go などの言語で API を実装する際の支援情報については、<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">弊社のブログ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を確認してください。
{: tip}
