---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Accesso alle informazioni utente predefinite
{: #predefined}

Puoi visualizzare le informazioni specifiche del provider di identità dei tuoi utenti.
{: shortdesc}


## Accesso con l'SDK iOS
{: #ios}

Se i nuovi token non vengono inoltrati esplicitamente al SDK, {{site.data.keyword.appid_short_notm}} utilizza gli ultimi token ricevuti per richiamare e convalidare la risposta. Ad esempio, puoi eseguire il seguente codice dopo un'autenticazione riuscita e l'SDK richiama ulteriori informazioni sull'utente.

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // si è verificato un errore
	}
	// informazioni utente richiamate correttamente
}

```
{: pre}

In alternativa, puoi inoltrare esplicitamente i token di accesso e di identità. Il token di identità è facoltativo, ma quando viene passato, viene utilizzato per convalidare la risposta delle informazioni utente.

```
AppID.sharedInstance.userProfileManager.getUserInfo(accessToken: String, identityToken: String?) { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // si è verificato un errore
	}
	// informazioni utente richiamate correttamente
}
```
{: pre}

</br>

## Accesso con l'SDK Android
{: #android}

Se i nuovi token non vengono inoltrati esplicitamente al SDK, {{site.data.keyword.appid_short_notm}} utilizza gli ultimi token ricevuti per richiamare e convalidare la risposta. Ad esempio, puoi eseguire il seguente codice dopo un'autenticazione riuscita e l'SDK richiama ulteriori informazioni sull'utente.

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		// informazioni utente richiamate correttamente
	}

	@Override
	public void onFailure(UserInfoException e) {
		// si è verificata un'eccezione
	}
});
```
{: pre}

In alternativa, puoi inoltrare esplicitamente i token di accesso e di identità. Il token di identità è facoltativo, ma quando viene passato, viene utilizzato per convalidare la risposta delle informazioni utente.

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(accessToken, identityToken, new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		// attributo "name" richiamato correttamente
	}

	@Override
	public void onFailure(UserInfoException e) {
		// si è verificata un'eccezione
	}
});
```
{: pre}

</br>

## Accesso con l'SDK Node.js Server
{: #node}


Utilizzando un SDK lato server, puoi richiamare ulteriori informazioni sui tuoi utenti. Puoi richiamare il seguente metodo utilizzando i token di identità e di accesso memorizzati oppure puoi inoltrare esplicitamente i token. Il token di identità è facoltativo, ma quando viene passato, viene utilizzato per convalidare la risposta delle informazioni utente.


```javascript
let userProfileManager = UserProfileManager(options: options)

let accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;
let identityToken = req.session[WebAppStrategy.AUTH_CONTEXT].identityToken;


// Richiama la informazioni utente e le convalida con il token di identità fornito
userProfileManager.getUserInfo(accessToken, identityToken).then(function (profile) {
	// informazioni utente richiamate correttamente
});

// Richiama la informazioni utente senza convalida
userProfileManager.getUserInfo(accessToken).then(function (profile) {
	// informazioni utente richiamate correttamente
});
```
{: pre}

</br>

## Accesso con l'SDK Swift Server
{: #swift}

Utilizzando un SDK lato server, puoi richiamare ulteriori informazioni sui tuoi utenti. Puoi richiamare il seguente metodo utilizzando i token di identità e di accesso memorizzati oppure puoi inoltrare esplicitamente i token. Il token di identità è facoltativo, ma quando viene passato, viene utilizzato per convalidare la risposta delle informazioni utente.


```swift
let userProfileManager = UserProfileManager(options: options)

let accessToken = "<access token>"
let identityToken = "<identity token>"

// Se viene fornito il token di identità (metodo consigliato), la risposta viene convalidata con il token
userProfileManager.getUserInfo(accessToken: accessToken, identityToken: identityToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // si è verificato un errore
	}
	// informazioni utente richiamate correttamente
}

// Richiama le informazioni utente senza convalida
userProfileManager.getUserInfo(accessToken: accessToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // si è verificato un errore
	}
	// informazioni utente richiamate correttamente
}

```
{: pre}

</br>

## Accesso a con l'API
{: #api}

Puoi visualizzare ulteriori informazioni tramite l'endpoint `/userinfo`.

1. Assicurarti di disporre di un token di accesso valido con un ambito `openid`. Puoi verificare che il token è valido utilizzando l'endpoint `/introspect`.

2. Esegui una richiesta all'endpoint `/userinfo`.
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  Output di esempio:
  ```
  "sub": "cad9f1d4-e23b-3683-b81b-d1c4c4fd7d4c",
  "name": "John Doe",
  "email": "john.doe@gmail.com",
  "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
  "gender": "male",
  "locale": "en",
  "identities": [
      {
          "provider": "google",
          "id": "104560903311317789798",
          "profile": {
              "id": "104560903311317789798",
              "email": "john.doe@gmail.com",
              "verified_email": true,
              "name": "John Doe",
              "given_name": "John",
              "family_name": "Doe",
              "link": "https://plus.google.com/104560903311317789798",
              "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
              "gender": "male",
              "locale": "en",
              "idpType": "google"
          }
      }
  ]
  ```
  {: screen}

3. Verificare che l'attestazione `sub` corrisponda esattamente all'attestazione `sub` nel token di identità. Se non corrispondono, non utilizzare le informazioni restituite. Per ulteriori informazioni sulla sostituzione dei token, consulta la <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">specifica OIDC <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.

Se le modifiche vengono apportate da un provider di identità esterno, puoi ottenere le informazioni aggiornate quando gli utenti accedono nuovamente. I tuoi nuovi token richiamano i dati più aggiornati.
{: tip}
