---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, backend, back-end, oauth, 

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

# Applicazioni di backend
{: #backend}

Puoi utilizzare gli SDK e le API {{site.data.keyword.appid_full}} per proteggere i tuoi endpoint e API dell'applicazione di backend.
{: shortdesc}


## Descrizione del flusso
{: #backend-understanding}

Parte dello sviluppo delle applicazioni di backend consiste nel verificare che le tue API siano protette da accessi non autorizzati. Gli SDK {{site.data.keyword.appid_short_notm}} rendono semplice proteggere i tuoi endpoint API e garantiscono la sicurezza della tua applicazione.


### Qual è la base tecnica del flusso?
{: #backend-technical-flow}

{{site.data.keyword.appid_short_notm}} implementa la specifica [OAuth 2.0](https://tools.ietf.org/html/rfc6749) e OIDC, che utilizza i token di connessione per l'autenticazione e l'autorizzazione. Questi token sono formattati come [JSON Web Tokens](https://tools.ietf.org/html/rfc7519), che vengono firmati digitalmente e contengono delle attestazioni che descrivono il soggetto che sta venendo autenticato e il provider di identità. Le API della tua applicazione vengono protette dai token di accesso e identità. I client che devono accedere alle tue API, possono autenticarsi con il provider di identità tramite {{site.data.keyword.appid_short_notm}} in cambio di questi token. Le attestazioni nei token devono essere convalidate per concedere l'accesso alle API protette.

Per ulteriori informazioni su come vengono utilizzati i token in {{site.data.keyword.appid_short_notm}}, consulta [Descrizione dei token](/docs/services/appid?topic=appid-tokens#tokens).
{: tip}


### Come si presenta questo flusso?
{: #backend-flow}

Flusso di backend ![{{site.data.keyword.appid_short_notm}}. I passi sono elencati in ordine, seguendo l'immagine.](images/backend-flow.png)

1. Un client esegue una richiesta POST al server di autorizzazione {{site.data.keyword.appid_short_notm}} per ottenere un token di accesso. Una richiesta POST normalmente ha la seguente forma:

  ```
  POST/oauth/v4/{tenantId}/token HTTP/1.1
  Content_type: application/x-www-form-urlencoded
  Authorization header = "Basic" + base64encode({clientId}:{secret})
  FormData = {grant_type}
  ```
  {: screen}

2. Se il client soddisfa le qualifiche, il server di autorizzazione restituisce un token di accesso.

3. Il client invia una richiesta alla risorsa protetta. Le richieste possono essere inviate in più modi, a seconda di quale libreria client HTTPS stai utilizzando, ma una richiesta generalmente ha il seguente formato:

  ```
  curl -H 'Authorization: Bearer {access_token}' {https://my-protected-resource.com}
  ```
  {: screen}

4. La risorsa protetta o l'API convalida il token. Se il token è valido, viene concesso al client l'accesso alla risorsa. Se il token non può essere convalidato, l'accesso viene negato.



## Protezione di risorse utilizzando un SDK
{: #backend-secure}

Puoi utilizzare gli SDK {{site.data.keyword.appid_short_notm}} per implementare autenticazione e autorizzazione per le tue applicazioni lato server. La `ApiStrategy` interviene nella protezione delle tue risorse di backup richiedendo la convalida di token di accesso e identità come parte della richiesta.
{: shortdesc}

L'SDK Node.js {{site.data.keyword.appid_short_notm}} opera in combinazione con il [framework Passport](http://www.passportjs.org/).
{: ph data-hd-programlang='javascript'}

L'SDK Swift lato server {{site.data.keyword.appid_short_notm}} fornisce un plugin middleware di protezione API utilizzato per proteggere le tue applicazioni di backend. Associando le tue API con il middleware, puoi proteggere la tua applicazione da accessi non autorizzati. Dopo che l'API è protetta, il middleware garantisce che i token generati da {{site.data.keyword.appid_short_notm}} siano convalidati. Puoi quindi modificare il comportamento dell'API in base ai risultati della convalida.
{: ph data-hd-programlang='swift'}

Vedi il seguente frammento di codice per un esempio di come proteggere l'API `/protectedendpoint`.
{: ph data-hd-programlang='swift'}

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// setup routes
let router = Router()

// mandatory option to be passed in if app not deployed on IBM Cloud
let options = [
    "oauthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/d8438de6-c325-4956-ad34-abd49194affd",
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
                        "! You are logged in with " + userProfile.provider + "." +
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
{: pre}
{: ph data-hd-programlang='swift'}


### Prima di cominciare
{: #backend-secure-before}
{: ph data-hd-programlang='javascript'}

Prima di iniziare, devi avere i seguenti prerequisiti.
{: ph data-hd-programlang='javascript'}
  * Un'istanza di {{site.data.keyword.appid_short_notm}}
  * NPM versione 4 o superiore
  * Node versione 6 o superiore
  {: ph data-hd-programlang='javascript'}

### Installazione dell'SDK
{: #backend-secure-install}
{: ph data-hd-programlang='javascript'}

1. Aggiungi l'SDK {{site.data.keyword.appid_short_notm}} Node.js al file `package.json` della tua applicazione.
{: ph data-hd-programlang='javascript'}
  ```
  "dependencies": {
      "ibmcloud-appid": "^6.0.0"
  }
  ```
  {: pre}
  {: ph data-hd-programlang='javascript'}

2. Immetti il seguente comando.
{: ph data-hd-programlang='javascript'}

  ```
  npm install
  ```
  {: pre}
  {: ph data-hd-programlang='javascript'}

### Inizializzazione dell'SDK
{: #backend-secure-initialize}
{: ph data-hd-programlang='javascript'}

1. Ottieni il tuo `oauth server url`.
  1. Passa alla scheda **Service Credentials** del dashboard {{site.data.keyword.appid_short_notm}}.
  2. Se ancora non hai una serie di credenziali, fai clic su **New credential** e quindi su **Add** per creare una nuova serie. Se le hai, salta questo passo.
  3. Fai clic sul pulsante di attivazione **View credentials** per visualizzare le tue informazioni.
  4. Copia il tuo `oauth server url` per utilizzarlo nel prossimo passo.
  {: ph data-hd-programlang='javascript'}

2. Inizializza la strategia passport {{site.data.keyword.appid_short_notm}} come mostrato nel seguente esempio.
{: ph data-hd-programlang='javascript'}
  ```javascript
  var express = require('express'); 
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy; 
  passport.use(new APIStrategy({ oauthServerUrl: "{oauth-server-url}" })); 
  var app = express();
  app.use(passport.initialize());
  ```
  {: pre}
  {: ph data-hd-programlang='javascript'}


Se la tua applicazione Node.js viene eseguita su {{site.data.keyword.cloud_notm}} ed è associata alla tua istanza di {{site.data.keyword.appid_short_notm}}, non c'è bisogno di fornire la configurazione della strategia API. La configurazione di {{site.data.keyword.appid_short_notm}} ottiene le informazioni utilizzando la variabile di ambiente VCAP_SERVICES.
{: tip}
{: ph data-hd-programlang='javascript'}


### Protezione dell'API
{: #backend-secure-api-strategy}
{: ph data-hd-programlang='javascript'}

Il seguente frammento di codice illustra come utilizzare `ApiStrategy` in un'applicazione Express per proteggere l'API GET `/protected`.
{: ph data-hd-programlang='javascript'}

  ```javascript
   app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', { session: false }), function(request, response){
      console.log("Security context", request.appIdAuthorizationContext);
      response.send(200, "Success!");
      }
   );
   ```
  {: pre}
  {: ph data-hd-programlang='javascript'}

Dopo la convalida dei token, viene chiamato il successivo middleware nella catena di richieste e viene aggiunta la proprietà `appIdAuthorizationContext` all'oggetto della richiesta. La proprietà contiene i token di accesso e identità originali e le informazioni sul payload decodificate dei token.
{: ph data-hd-programlang='javascript'}


## Proteggere le risorse manualmente
{: #backend-secure-api}

Per garantire la sicurezza delle tue applicazioni di backend e delle tue risorse protette, devi convalidare un token. Quando un client invia una richiesta alla tua risorsa, puoi verificare che il token soddisfi le specifiche definite. Il token può includere delle informazioni di identificazione o qualsiasi altra configurazione da te implementata. Puoi convalidare i token di accesso e identità {{site.data.keyword.appid_short_notm}} in molti modi. Per un aiuto, consulta [Convalida dei token](/docs/services/appid?topic=appid-token-validation#token-validation).


## Passi successivi
{: #backend-next}

Con {{site.data.keyword.appid_short_notm}} installato nella tua applicazione, sei quasi pronto ad iniziare ad autenticare gli utenti. Prova ad eseguire una delle seguenti attività:

* Configura i tuoi [provider di identità](/docs/services/appid?topic=appid-social)
* Personalizza e configura [il widget di accesso](/docs/services/appid?topic=appid-login-widget)
* Informazioni sull'<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK Node.js<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
* Informazioni sull'<a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK Swift<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
