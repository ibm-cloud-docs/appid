---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Applicazioni di backend
{: #adding-backend}

Puoi utilizzare gli SDK e le API {{site.data.keyword.appid_full}} per proteggere i tuoi endpoint e API dell'applicazione di backend.
{: shortdesc}


## Descrizione del flusso
{: #understanding}

**Quando questo flusso sarebbe utile?**

Parte dello sviluppo delle applicazioni di backend è di verificare che le tue API siano protette da accessi non autorizzati. Gli SDK {{site.data.keyword.appid_short_notm}} rendono semplice proteggere i tuoi endpoint API e garantiscono la sicurezza della tua applicazione.

**Quali sono le basi tecniche del flusso?**

{{site.data.keyword.appid_short_notm}} implementa la specifica [OAuth2](https://tools.ietf.org/html/rfc6749) e OIDC, che utilizza i token di connessione per l'autenticazione e l'autorizzazione. Questi token sono formattati come [JSON Web Tokens](https://tools.ietf.org/html/rfc7519), che vengono firmati digitalmente e contengono delle attestazioni che descrivono il soggetto che sta venendo autenticato e il provider di identità. Le API della tua applicazione vengono protette dai token di accesso e identità. I client che devono accedere alle tue API, possono autenticarsi con il provider di identità tramite {{site.data.keyword.appid_short_notm}} in cambio di questi token. Le attestazioni nei token devono essere convalidate per concedere l'accesso alle API protette.

Per ulteriori informazioni su come vengono utilizzati i token in {{site.data.keyword.appid_short_notm}}, consulta [Descrizione dei token](/docs/services/appid/authorization.html#tokens).
{: tip}

**A cosa assomiglia questo flusso?**

![{{site.data.keyword.appid_short_notm}} - Flusso di backend. I passi vengono elencati in ordine nella seguente immagine.](images/backend-flow.png)

1. Un client esegue una richiesta POST al server di autorizzazione {{site.data.keyword.appid_short_notm}} per ottenere un token di accesso. Una richiesta POST normalmente ha la seguente forma:

  ```
  POST/oauth/v3/{tenantId}/token HTTP/1.1
  Content_type: application/x-www-form-urlencoded
  Authorization header = "Basic" + base64encode({clientId}:{secret})
  FormData = {grant_type}
  ```
  {: screen}

2. Se il client soddisfa le qualifiche, il server di autorizzazione restituisce un token di accesso.

3. Il client invia una richiesta alla risorsa protetta.

4. La risorsa protetta o l'API convalida il token. Se il token è valido, viene concesso al client l'accesso alla risorsa. Se il token non può essere convalidato, l'accesso viene negato.


## Protezione di risorse con l'SDK Node.js
{: #secure-node}

L'SDK server {{site.data.keyword.appid_short_notm}} applica l'autenticazione e l'autorizzazione con il [framework Passport](http://www.passportjs.org/). Con l'`ApiStrategy`, puoi proteggere le tue risorse di backend richiedendo che i token di accesso e identità siano convalidati nell'intestazione dell'autorizzazione come parte della richiesta.
{: shortdesc}

**Prima di cominciare**

Devi avere i seguenti prerequisiti prima di poter iniziare:
 * Un'istanza di {{site.data.keyword.appid_short_notm}}
 * NPM versione 4 o superiore
 * Node versione 6 o superiore

**Installazione dell'SDK**

1. Aggiungi l'SDK {{site.data.keyword.appid_short_notm}} Node.js al file `package.json` della tua applicazione.

  ```
  "dependencies": {
      "ibmcloud-appid": "^4.0.0"
  }
  ```
  {: codeblock}

2. Immetti il seguente comando.

  ```
  npm install
  ```
  {: codeblock}

**Inizializzazione dell'SDK**

Puoi inizializzare l'SDK utilizzando un `oauth server url`.

1. Ottieni il tuo `oauth server url`.
  1. Passa alla scheda **Service Credentials** del dashboard {{site.data.keyword.appid_short_notm}}. 
  2. Se ancora non hai una serie di credenziali, fai clic su **New credential** e quindi su **Add** per creare una nuova serie. Se le hai, salta questo passo.
  3. Fai clic sul pulsante di attivazione **View credentials** per visualizzare le tue informazioni.
  4. Copia il tuo `oauth server url` per utilizzarlo nel prossimo passo.

2. Inizializza la strategia passport {{site.data.keyword.appid_short_notm}} come mostrato nel seguente esempio.

  ```javascript
  var express = require('express'); 
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy; 
  passport.use(new APIStrategy({ oauthServerUrl: "{oauth-server-url}" })); 
  var app = express();
  app.use(passport.initialize());
  ```
  {: codeblock}


Se la tua applicazione Node.js viene eseguita su {{site.data.keyword.Bluemix_notm}} ed è associata alla tua istanza di {{site.data.keyword.appid_short_notm}}, non c'è bisogno di fornire la configurazione della strategia API. La configurazione di {{site.data.keyword.appid_short_notm}} ottiene le informazioni utilizzando la variabile di ambiente VCAP_SERVICES.
{: tip}

**Protezione dell'API**

Il seguente frammento di codice illustra come utilizzare `ApiStrategy` in un'applicazione Express per proteggere l'API GET `/protected`.

  ```javascript
   app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', { session: false }), function(request, response){
      console.log("Security context", request.appIdAuthorizationContext);
      response.send(200, "Success!");
      }
   );
   ```
  {: codeblock}

Dopo la convalida dei token, viene chiamato il successivo middleware nella catena di richieste e viene aggiunta la proprietà `appIdAuthorizationContext` all'oggetto della richiesta. La proprietà contiene i token di accesso e identità originali, nonché le informazioni sul payload decodificate dei rispettivi token.


## Protezione di risorse con l'SDK Swift
{: #secure-swift}

Puoi utilizzare {{site.data.keyword.appid_short_notm}} per proteggere le tue risorse lato server utilizzando l'SDK Swift.
{: shortdesc}

L'SDK server Swift {{site.data.keyword.appid_short_notm}} [](https://github.com/ibm-cloud-security/appid-serversdk-swift) fornisce un plug-in middleware di protezione dell'API utilizzato per proteggere le tue applicazioni di back-end. Associando le tue API al middleware, puoi proteggere la tua applicazione da accessi non autorizzati. Dopo che l'API è protetta, il middleware garantisce che i token generati da {{site.data.keyword.appid_short_notm}} siano convalidati. Puoi quindi modificare il comportamento dell'API in base ai risultati della convalida.

Vedi il seguente frammento di codice per un esempio di come proteggere l'API `/protectedendpoint`.

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// setup routes
let router = Router()

// mandatory option to be passed in if app not deployed on IBM Cloud
let options = [
    "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/d8438de6-c325-4956-ad34-abd49194affd",
]
let apiCreds = Credentials()

// Minimum macOS version required
if #available(OSX 10.12, *) {

    // setup API protection
    let apiKituraCredentialsPlugin = APIKituraCredentialsPlugin(options: options)
    apiCreds.register(plugin: apiKituraCredentialsPlugin)

    // associate route with API protection
    router.all(middleware: apiCreds)

    // create protected API
    router.get("/protectedendpoint") { request, response, next in

        response.headers["Content-Type"] = "text/html; charset=utf-8"
        do {
            if let userProfile = request.userProfile  {
                try response.status(.OK).send(
                    "<!DOCTYPE html><html><body>" +
                        "Welcome " + userProfile.displayName  +
                        "! You are logged in with " + userProfile.provider + ".
" +
                    "</body></html>\n\n").end()
                next()
                return
            }
            try response.status(.unauthorized).send(
                "<!DOCTYPE html><html><body>” + “You are not authorized!" +
                "</body></html>\n\n").end()
        }
        catch {}
        next()
    }

    // Start server
    Kitura.addHTTPServer(onPort: 8090, with: router)

    Kitura.run()  
}
```
{: codeblock}

## Proteggere le risorse manualmente
{: secure-api}

La protezione delle tue applicazioni di backend e delle risorse protette implica la convalida dei token. Puoi convalidare i token di accesso e identità {{site.data.keyword.appid_short_notm}} in molti modi. Per informazioni sulla convalida dei token, consulta [Convalida dei token](/docs/services/appid/tokens.html).


## Fasi successive
{: #next}

Con {{site.data.keyword.appid_short_notm}} installato nella tua applicazione, sei quasi pronto ad iniziare ad autenticare gli utenti. Prova ad eseguire una delle seguenti attività:

* Configura i tuoi [provider di identità](/docs/services/appid/identity-providers.html)
* Personalizza e configura [il widget di accesso](/docs/services/appid/login-widget.html)
* Informazioni sull'<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK Node.js<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
* Informazioni sull'<a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK Swift<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
