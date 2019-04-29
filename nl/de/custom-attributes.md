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

# Angepasste Benutzerattribute
{: #custom-attributes}

Mit {{site.data.keyword.appid_full}} können Sie angepasste Attribute speichern, auf diese Attribute zugreifen und sie aktualisieren.
{: shortdesc}


## Attribute festlegen
{: #setting-custom-attributes}

Sie können Rollen und Bereiche festlegen, die als Attribute für ein Benutzerprofil bezeichnet werden. Sie können vorhandene Attribute, die möglicherweise von einem externen Identitätsprovider extrahiert wurden, auch überschreiben.
{: shortdesc}


Bei den Attributen handelt es sich um Angaben über die Benutzer. Indem Sie sie speichern, können Sie Profile für Ihre Benutzer erstellen, um deren Benutzererlebnis zu personalisieren. Je mehr Attribute zu diesem Profil hinzugefügt werden, umso mehr kann die App für die Benutzer personalisiert werden. Informieren Sie sich in diesem Blog, um zu erfahren, welche Vorteile sich durch das Erstellen von Benutzerprofilen ergeben: <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="blank">Einführung in {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.


Sie können für jeden Benutzer 100 KB an Informationen speichern.
{: note}


**Gehen Sie wie folgt vor, um ein Attribut festzulegen:**

Alle eingehenden Anforderungen an Ihre App haben Berechtigungsheader mit der Angabe `access_token`. Sie können `access_token` verwenden, um mit einem der bereitgestellten SDKs oder mit den [APIs für Attribute](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes) Anforderungen an die Endpunkte der angepassten Attribute abzusetzen.


iOS Swift:
{: ph data-hd-programlang='swift'}

  ```
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // Ein Fehler ist aufgetreten.
		}
		// Attribute als Verzeichnis empfangen.
	})
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  ```
  appId.getUserProfileManager().setAttribute(name, value, useThisToken, new UserProfileResponseListener() {
  	@Override
		public void onSuccess(JSONObject attributes) {
  		// Attribute im JSON-Format nach erfolgreicher Antwort empfangen.
		}

  	@Override
		public void onFailure(UserAttributesException e) {
  		// Eine Ausnahmebedingung ist aufgetreten.
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
		// Attribute als Verzeichnis zurückgegeben.
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
      return // Ein Fehler ist aufgetreten.
		}
    // Attribute als Verzeichnis empfangen
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

</br>

## Auf angepasste Attribute zugreifen
{: #accessing-custom-attributes}

Abhängig von Ihrer Konfiguration werden Attribute verschlüsselt und als Teil eines Benutzerprofils gespeichert, wenn ein Benutzer mit Ihrer Anwendung interagiert. Die Interaktion könnte durch einen Benutzer erfolgen, der sich anmeldet oder eine Benutzervorgabe in Ihrer App festlegt. Um auf die Attribute zugreifen zu können, können Sie ein Zugriffstoken über eine API-Methode übergeben. Wenn ein Zugriffstoken nicht explizit übergeben wird, verwendet {{site.data.keyword.appid_short_notm}} das zuletzt empfangene Token.
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

Serverseitiges Swift:
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

## Sicherheitsaspekte
{: #security-custom-attributes}

Bevor Sie mit angepassten Attributen arbeiten können, müssen Sie sich mit den Sicherheitsaspekten vertraut machen.

Angepasste Attribute können standardmäßig geändert werden und können mit einem {{site.data.keyword.appid_short_notm}}-Zugriffstoken von einer Clientanwendung aus aktualisiert werden. Dies bedeutet, dass der Benutzer oder die Anwendung ohne besondere Vorsichtsmaßnahmen die angepassten Attribute unmittelbar nach der ersten Anmeldung aktualisieren kann, vorausgesetzt, es besteht Zugriff auf ein Zugriffstoken. Dies kann unbeabsichtigte Folgen haben. Ein Benutzer könnte beispielsweise seine Rolle von 'Benutzer' in 'Administrator' ändern. Dadurch könnten Administratorberechtigungen in die falschen Hände gelangen.

Wenn Sie verhindern möchten, dass Ihre Benutzer die Attribute ändern, die Sie ihnen geben, setzen Sie die Option **Angepasste Attribute in der App ändern** auf der Registerkarte **Profile** des {{site.data.keyword.appid_short_notm}}-Dashboards auf **Aus**. Standardmäßig ist die Option auf **Ein** gesetzt.
{: tip}

</br>

## Nächste Schritte
{: #next-custom-attributes}

Weitere Informationen zum Arbeiten mit einem SDK für eine bestimmte Sprache finden Sie in den folgenden GitHub-Repositorys:

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android-SDK <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">iOS Swift-SDK <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js-SDK <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">Server Swift-SDK <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>


Sie haben kein SDK für die Sprache gefunden, in der Ihre App geschrieben ist? Kein Problem! Sie können den Service mithilfe der APIs integrieren. {{site.data.keyword.appid_short_notm}} stellt eine <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">REST-API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> bereit, die die Anmeldung - anonym oder mit Authentifizierung - über einen unterstützten [Identitätsprovider](/docs/services/appid?topic=appid-managing-idp) ermöglicht. Wenn Sie Unterstützung bei der Implementierung der API in Sprachen wie z. B. Python und Go benötigen, dann lesen Sie die Informationen in <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">unseren Blogs <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
{: tip}
