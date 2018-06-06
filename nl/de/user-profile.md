---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Auf Benutzerattribute zugreifen
{: #user-profile}

Sie können Endbenutzerdaten verwalten, die Sie zur Erstellung personalisierter Apps verwenden können.
{:shortdesc}

Ein Benutzerattribut ist ein Informationssegment in einer Entität, die von {{site.data.keyword.appid_full}} verwaltet wird. Das Profil enthält die Attribute und Identität eines Benutzers. Es kann anonym oder mit einer Identität verknüpft sein, die von einem Identitätsprovider verwaltet wird.

{{site.data.keyword.appid_short_notm}} stellt eine API bereit, die eine anonyme Anmeldung oder eine Anmeldung mit einer Authentifizierung über einen OIDC-[Identitätsprovider](/docs/services/appid/identity-providers.html) (OIDC = OpenId Connect) ermöglicht. Der API-Endpunkt des Benutzerprofilattributs ist eine Ressource, die durch ein Zugriffstoken geschützt ist, das beim Anmelde- und Berechtigungsprozess von {{site.data.keyword.appid_short_notm}} generiert wird.


## Benutzerattribute speichern, lesen und löschen
{: #storing-data}

{{site.data.keyword.appid_short_notm}} stellt eine <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST-API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> zum Ausführen von Operationen zum Erstellen, Abrufen, Aktualisieren und Löschen für Benutzerattribute bereit. Der Service stellt auch ein SDK für mobile Clients für <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> und <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> bereit.

## Über das Android-SDK auf Benutzerattribute zugreifen
{: #accessing}

Wenn Sie ein Zugriffstoken anfordern, können Sie Zugriff auf den Endpunkt der geschützten Benutzerattribute zugreifen. Sie können Zugriff durch die folgenden API-Methoden erhalten.

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

Wenn ein Zugriffstoken nicht explizit übergeben wird, verwendet {{site.data.keyword.appid_short_notm}} das zuletzt empfangene Token.

Sie können beispielsweise diesen Code aufrufen, um ein neues Attribut festzulegen oder ein vorhandenes Attribut zu überschreiben.

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//Attribute im JSON-Format nach erfolgreicher Antwort empfangen
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Ausnahmebedingung aufgetreten.
  			 }
	});
  ```
  {: codeblock}

### Anonyme Anmeldung
{: #anonymous notoc}

Mit {{site.data.keyword.appid_short_notm}} können Sie sich [anonym](/docs/services/appid/user-profile.html#anonymous) anmelden.

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
			 public void onAuthorizationFailure (AuthorizationException exception) {
			//Ausnahmebedingung aufgetreten.
  			 }

		@Override
		public void onAuthorizationCanceled() {
			//Authentifizierung von Benutzer abgebrochen
		}

		@Override
 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
			//Benutzer authentifiziert
		}
	});
  ```
  {: codeblock}

### Progressive Authentifizierung
{: #progressive notoc}

Benutzer mit einem anonymen Zugriffstoken können identifiziert werden, indem es der Methode `loginWidget.launch` übergeben wird.

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {: codeblock}

Nach einer anonymen Anmeldung tritt eine progressive Authentifizierung auf, sogar wenn das Anmelde-Widget aufgerufen wird, ohne dass dabei ein Zugriffstoken übergeben wird. Grund hierfür ist, dass der Service das zuletzt empfangene Token verwendet. Führen Sie den folgenden Befehl aus, um gespeicherte Token zu löschen.

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {: codeblock}


## Über das iOS-SDK auf Benutzerattribute zugreifen
{: #accessing}

Wenn Sie ein Zugriffstoken anfordern, können Sie Zugriff auf den Endpunkt der geschützten Benutzerattribute zugreifen. Sie können Zugriff durch die folgenden API-Methoden erhalten.

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

Wenn ein Zugriffstoken nicht explizit übergeben wird, verwendet {{site.data.keyword.appid_short_notm}} das zuletzt empfangene Token.

Sie können beispielsweise diesen Code aufrufen, um ein neues Attribut festzulegen oder ein vorhandenes Attribut zu überschreiben.

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attribute als Wörterbuch erhalten
      } else {
          // Ein Fehler ist aufgetreten
      }
  })
  ```
  {: codeblock}


### Anonyme Anmeldung
{: #anonymous notoc}

Mit {{site.data.keyword.appid_short_notm}} können Sie sich [anonym](/docs/services/appid/user-profile.html#anonymous) anmelden.

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Benutzer authentifiziert
      }

      public func onAuthorizationCanceled() {
          //Authentifizierung von Benutzer abgebrochen
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Fehler aufgetreten
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {: codeblock}

### Progressive Authentifizierung
{: #progressive notoc}

Benutzer mit einem anonymen Zugriffstoken können identifiziert werden, indem es der Methode `loginWidget.launch` übergeben wird.

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {: codeblock}

Nach einer anonymen Anmeldung tritt eine progressive Authentifizierung auf, sogar wenn das Anmelde-Widget aufgerufen wird, ohne dass dabei ein Zugriffstoken übergeben wird. Grund hierfür ist, dass der Service das zuletzt empfangene Token verwendet. Führen Sie den folgenden Befehl aus, um gespeicherte Token zu löschen.

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {: codeblock}

## Datentrennung und -verschlüsselung
{: #data}

{{site.data.keyword.appid_short_notm}} speichert und verschlüsselt die Attribute von Benutzerprofilen. Als Multi-Tenant-Service besitzt jeder Tenant einen designierten Verschlüsselungsschlüssel. Die Benutzerdaten in jedem Tenant werden nur mit dem Schlüssel des Tenants verschlüsselt.

{{site.data.keyword.appid_short_notm}} stellt sicher, dass die privaten Daten vor dem Speichern verschlüsselt werden.
