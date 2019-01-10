---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Accesso agli attributi dell'utente personalizzati
{: #custom}

Con {{site.data.keyword.appid_full}}, puoi salvare ed accedere agli attributi personalizzati.
{: shortdesc}

**Perché dovrei voler salvare ulteriori attributi su un utente?**

Gli attributi sono parti di informazioni relative ai tuoi utenti. Salvandoli, puoi creare dei profili sui tuoi utenti che ti consentono di personalizzare la loro esperienza. Più attributi vengono aggiunti ai loro profili e più possono essere personalizzate le loro applicazioni. Consulta questo blog per vedere come la creazione dei profili utente può fare la differenza: <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">Introducing {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.

</br>

**Come vengono salvati gli attributi?**

A seconda della tua configurazione, gli attributi sono codificati e salvati come parte di un profilo utente quando un utente interagisce con la tua applicazione. L'interazione potrebbe essere un accesso utente o l'impostazione di una preferenza nella tua applicazione.

</br>

**Esiste un limite alla quantità di informazioni che possono essere archiviate per ogni utente?**

Puoi archiviare 100KB di informazioni per ogni utente.

</br>

**Esistono delle considerazioni sulla sicurezza ti cui dovrei tenere conto?**

Per impostazione predefinita, gli attributi personalizzati sono modificabili e possono essere aggiornati utilizzando un token di accesso {{site.data.keyword.appid_short_notm}} da un'applicazione client. Questo significa che senza prendere delle precauzioni appropriate, l'utente o l'applicazione può aggiornare gli attributi personalizzati immediatamente dopo il primo accesso utente, a condizione che abbiano accesso a un token di accesso. Questo può potenzialmente portare a delle conseguenze non volute. Ad esempio, un utente potrebbe modificare il proprio ruolo da utente ad amministratore e potrebbe esporre i privilegi di gestione a utenti malintenzionati.

Per evitare che i tuoi utenti modifichino gli attributi che gli hai fornito, imposta **Change custom attributes from the app** su **Off** nella scheda **Profiles** del dashboard {{site.data.keyword.appid_short_notm}}. Per impostazione predefinita, è impostato su **On**.
{: tip}

</br>


## Accesso con l'SDK iOS
{: #ios}

 Puoi accedere agli attributi degli utenti personalizzati passando un token di accesso tramite i seguenti metodi API.

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
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // si è verificato un errore
		}
		// attributi ricevuti come un dizionario
	})
  ```
  {: pre}

Per ulteriori informazioni sull'utilizzo di iOS Swift, consulta <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
{: tip}

</br>


## Accesso con l'SDK Android
{: #android}

Puoi accedere agli attributi degli utenti personalizzati passando un token di accesso tramite i seguenti metodi API.

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
appId.getUserProfileManager().setAttribute(name, value, useThisToken, new UserProfileResponseListener() {
	@Override
		public void onSuccess(JSONObject attributes) {
		//attributi ricevuti nel formato JSON per una risposta positiva
		}

	@Override
		public void onFailure(UserAttributesException e) {
		// si è verificata un'eccezione
	}
});
```
{: pre}

Per ulteriori informazioni sull'utilizzo di Android, consulta <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
{: tip}

</br>

## Accesso con l'SDK Node.js Server
{: #node}

Puoi accedere agli attributi degli utenti personalizzati passando un token di accesso tramite i seguenti metodi API.

  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  Utilizzo di esempio:

  ```javascript

	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributi restituiti come un dizionario
	});
  ```
  {: pre}

Per ulteriori informazioni sull'utilizzo dell'SDK Node.js Server, consulta <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
{: tip}

</br>

## Accesso con l'SDK Swift Server
{: #swift}

Puoi accedere agli attributi degli utenti personalizzati passando un token di accesso tramite i seguenti metodi API.

  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  Utilizzo di esempio:

  ```swift

	let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

	userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
			return // si è verificato un errore
		}
		// attributi ricevuti come un dizionario
	}
  ```

  {: pre}

Per ulteriori informazioni sull'utilizzo dell'SDK Swift Server, consulta <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
{: tip}


## Accesso a con l'API
{: #api}

È impossibile trovare un SDK per il linguaggio in cui è scritta la tua applicazione? Nessun problema! Puoi integrare il servizio utilizzando le API.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} fornisce un'<a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API REST <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> che consente di accedere, in modo anonimo o tramite l'autenticazione, con un [provider di identità](/docs/services/appid/manageidp.html) supportato.
