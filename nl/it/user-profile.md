---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}


# Accesso agli attributi dell'utente
{: #user-profile}

Un attributo utente è un segmento di informazioni in un'entità archiviata e conservata da {{site.data.keyword.appid_full}}. Il profilo contiene gli attributi e l'identità di un utente che è gestito da un provider di identità o può essere anonimo. Puoi utilizzare i profili per creare esperienze personalizzate della tua applicazione per ogni utente.
{:shortdesc}


{{site.data.keyword.appid_short_notm}} fornisce un'API per l'accesso, sia in modo anonimo che tramite autenticazione con un IdP OpenId Connect (OIDC) ai [provider di identità](/docs/services/appid/identity-providers.html). L'endpoint API dell'attributo del profilo utente è una risorsa protetta dal token di accesso generato da {{site.data.keyword.appid_short_notm}} durante il processo di autorizzazione e accesso.


## Memorizzazione, lettura ed eliminazione degli attributi utente
{: #storing-data}

{{site.data.keyword.appid_short_notm}} fornisce un'API REST <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank"> <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per eseguire le operazioni di creazione, richiamo, aggiornamento ed eliminazione sugli attributi degli utenti. Il servizio fornisce anche un SDK per i client mobili <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.

## Accesso agli attributi dell'utente con l'SDK Android
{: #accessing}

Quando ottieni un token di accesso, è possibile ottenere l'accesso all'endpoint degli attributi protetti dell'utente. Puoi ottenere l'accesso utilizzando i seguenti metodi API.

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

Quando il token di accesso non viene esplicitamente trasmesso, {{site.data.keyword.appid_short_notm}} utilizza l'ultimo token ricevuto.

Ad esempio, puoi richiamare questo codice per impostare un nuovo attributo o sovrascriverne uno esistente.

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//attributi ricevuti nel formato JSON per una risposta positiva
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Si è verificata un'eccezione
		}
	});
  ```
  {: pre}

### Accesso anonimo
{: #anonymous notoc}

Con {{site.data.keyword.appid_short_notm}}, puoi accedere a [in modo anonimo](/docs/services/appid/user-profile.html#anonymous).

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Si è verificata un'eccezione
		}

		@Override
		public void onAuthorizationCanceled() {
			//Autenticazione annullata dall'utente
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
			//Utente autenticato
		}
	});
  ```
  {: pre}

### Autenticazione progressiva
{: #progressive notoc}

Quando l'utente contiene un token di accesso anonimo, può essere identificato trasmettendolo al metodo `loginWidget.launch`.

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {: pre}

Dopo un accesso anonimo, si verifica l'autenticazione progressiva anche se il widget di accesso viene richiamato trasmettendo un token di accesso, perché il servizio ha utilizzato l'ultimo token ricevuto. Se desideri cancellare i tuoi token memorizzati, esegui il seguente comando.

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {: pre}


## Accesso agli attributi dell'utente con l'SDK iOS
{: #accessing}

Accesso agli attributi degli utenti passando un token di accesso tramite i seguenti metodi API.
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

Quando il token di accesso non viene esplicitamente trasmesso, {{site.data.keyword.appid_short_notm}} utilizza l'ultimo token ricevuto.

Ad esempio, puoi richiamare questo codice per impostare un nuovo attributo o sovrascriverne uno esistente.

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributi ricevuti come un dizionario
      } else {
          // Si è verificato un errore
      }
  })
  ```
  {: pre}


### Accesso anonimo

Con {{site.data.keyword.appid_short_notm}}, puoi accedere a [in modo anonimo](/docs/services/appid/user-profile.html#anonymous).

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?, response:Response?) {
          //Utente autenticato
      }

      public func onAuthorizationCanceled() {
          //Autenticazione annullata dall'utente
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Si è verificato un errore
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {: pre}

### Autenticazione progressiva

Quando ospiti un token di accesso anonimo, l'utente può essere identificato trasmettendolo al metodo `loginWidget.launch`.

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {: pre}

Dopo un accesso anonimo, si verifica l'autenticazione progressiva anche se il widget di accesso viene richiamato trasmettendo un token di accesso, perché il servizio ha utilizzato l'ultimo token ricevuto. Se desideri cancellare i tuoi token memorizzati, esegui il seguente comando.

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {: pre}

## Codifica e separazione dei dati
{: #data}

{{site.data.keyword.appid_short_notm}} archivia e codifica gli attributi del profilo utente. Come un servizio a più tenant, ogni tenant ha una chiave di codifica e i dati utente in ogni tenant sono codificati con solo tale chiave.

{{site.data.keyword.appid_short_notm}} assicura che le informazioni private siano codificate prima dell'archiviazione.
