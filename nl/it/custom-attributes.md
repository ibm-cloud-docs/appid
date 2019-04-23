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

# Attributi dell'utente personalizzati
{: #custom-attributes}

Con {{site.data.keyword.appid_full}}, puoi salvare, accedere e aggiornare gli attributi personalizzati.
{: shortdesc}


## Impostazione degli attributi
{: #setting-custom-attributes}

Puoi impostare i ruoli e gli ambiti che sono noti come attributi per un profilo utente. Puoi anche sovrascrivere gli attributi esistenti che potrebbero essere stati estratti da un provider di identità esterno.
{: shortdesc}


Gli attributi sono parti di informazioni relative ai tuoi utenti. Salvandoli, puoi creare dei profili sui tuoi utenti che ti consentono di personalizzare la loro esperienza. Più attributi vengono aggiunti ai loro profili e più può essere personalizzata la loro esperienza dell'applicazione. Consulta questo blog per vedere come la creazione dei profili utente può fare la differenza: <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="blank">Introducing {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.


Puoi archiviare 100 KB di informazioni per ogni utente.
{: note}


**Per impostare un attributo:**

Tutte le richieste in entrata alla tua applicazione hanno un'intestazione Authorization, con `access_token`. Puoi utilizzare `access_token` per eseguire richieste agli endpoint di attributi personalizzati con uno degli SDK forniti oppure utilizzando [le API degli attributi](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes).


iOS Swift:
{: ph data-hd-programlang='swift'}

  ```
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // si è verificato un errore
		}
		// attributi ricevuti come un dizionario
	})
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  ```
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
  {: codeblock}
  {: ph data-hd-programlang='java'}

  ```
	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributi restituiti come un dizionario
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
      return // si è verificato un errore
		}
    // attributi ricevuti come un dizionario
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

</br>

## Accesso agli attributi personalizzati
{: #accessing-custom-attributes}

A seconda della tua configurazione, gli attributi sono codificati e salvati come parte di un profilo utente quando un utente interagisce con la tua applicazione. L'interazione potrebbe essere un accesso utente o l'impostazione di una preferenza nella tua applicazione. Per accedere agli attributi, puoi passare un token di accesso tramite un metodo API. Se non viene esplicitamente passato un token di accesso {{site.data.keyword.appid_short_notm}} utilizza l'ultimo token ricevuto.
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

Swift lato server:
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

## Considerazioni sulla sicurezza
{: #security-custom-attributes}

Prima di iniziare a lavorare con gli attributi personalizzati, assicurati di comprendere le considerazioni sulla sicurezza.

Per impostazione predefinita, gli attributi personalizzati sono modificabili e possono essere aggiornati utilizzando un token di accesso {{site.data.keyword.appid_short_notm}} da un'applicazione client. Questo significa che senza prendere delle precauzioni appropriate, l'utente o l'applicazione può aggiornare gli attributi personalizzati immediatamente dopo il primo accesso utente, a condizione che abbiano accesso a un token di accesso. Questo può potenzialmente portare a delle conseguenze non volute. Ad esempio, un utente potrebbe modificare il suo ruolo da utente ad amministratore e questo potrebbe esporre i privilegi di amministrazione a utenti malintenzionati.

Per evitare che i tuoi utenti modifichino gli attributi che gli hai fornito, imposta **Change custom attributes from the app** su **Off** nella scheda **Profiles** del dashboard {{site.data.keyword.appid_short_notm}}. Per impostazione predefinita, è impostato su **On**.
{: tip}

</br>

## Passi successivi
{: #next-custom-attributes}

Per ulteriori informazioni sull'utilizzo di uno specifico linguaggio SDK, consulta i seguenti repository GitHub:

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK Android <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK iOS Swift <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK Node.js <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK Server Swift <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>


È impossibile trovare un SDK per il linguaggio in cui è scritta la tua applicazione? Nessun problema! Puoi integrare il servizio utilizzando le API. {{site.data.keyword.appid_short_notm}} fornisce un'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">API REST <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> che consente di accedere, in modo anonimo o tramite l'autenticazione, con un [provider di identità](/docs/services/appid?topic=appid-managing-idp) supportato. Per un aiuto nell'implementazione dell'API in linguaggi quali Python e Go, <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">consulta i nostri blog <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
{: tip}
