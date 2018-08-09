---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informazioni
{: #about}

Puoi utilizzare {{site.data.keyword.appid_full}} per aggiungere l'autenticazione alle tue applicazioni e per proteggere le tue risorse di back-end.
{:shortdesc}

## Motivi per usare il servizio
{: #reasons}

Perché dovrei utilizzare {{site.data.keyword.appid_short_notm}}? Verifica i seguenti scenari per vedere se uno di essi va bene per te.
{: shortdesc}

<table>
  <tr>
    <th> Scenario </th>
    <th> Motivo </th>
  </tr>
  <tr>
    <td> Devi aggiungere [autorizzazione e autenticazione](/docs/services/appid/authorization.html) alle tue applicazioni mobile e web ma non hai esperienza in fatto di sicurezza. </td>
    <td> {{site.data.keyword.appid_short_notm}} rende semplice aggiungere una fase di autenticazione alle tue applicazioni. Puoi utilizzare il servizio per comunicare con i [provider di identità](/docs/services/appid/identity-providers.html) per gestire l'accesso alle tue applicazioni. </td>
  </tr>
  <tr>
    <td> Desideri limitare l'accesso alle tue applicazioni e alle risorse di back-end. </td>
    <td> Il servizio ti fornisce la possibilità di [proteggere le tue risorse](/docs/services/appid/protecting-resources.html) da utenti anonimi e autenticati. </td>
  </tr>
  <tr>
    <td> Desideri creare esperienze dell'applicazione personalizzate per i tuoi utenti. </td>
    <td> Con {{site.data.keyword.appid_short_notm}}, puoi [archiviare i dati utente](/docs/services/appid/user-profile.html) come le preferenze dell'applicazione o le informazioni dai loro profili sociali pubblici e poi utilizzare quei dati per personalizzare ogni esperienza della tua applicazione. </td>
  </tr>
  <tr>
    <td> Vuoi dare agli utenti la possibilità di ottenere l'accesso alla tua applicazione con le loro email e una password. </td>
    <td> {{site.data.keyword.appid_short_notm}} ti consente di creare una [cloud directory](/docs/services/appid/cloud-directory.html), che ti permette di aggiungere la registrazione e l'accesso utente alle tue applicazioni. Cloud Directory ti viene fornito con il framework per conservare un registro utenti che può ridimensionarsi con la tua base di utenti. Con la funzionalità precostruita per il self-service, come ad esempio una verifica dell'email e le reimpostazioni della password, puoi assicurarti che la tua applicazione stia autenticando gli utenti in modo sicuro. </td>
  </tr>
</table>


## Integrazioni
{: #integrations}

Puoi utilizzare {{site.data.keyword.appid_short_notm}} con le altre offerte {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>Configurando Ingress in un cluster standard, puoi proteggere le tue applicazioni a livello di cluster. Per iniziare, consulta l'annotazione di Ingress per l'autenticazione {{site.data.keyword.appid_short_notm}}.</dd>
  <dt>{{site.data.keyword.openwhisk}} e API Connect</dt>
    <dd>Quando crei le tue API con [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) e [API Connect](/docs/apis/management/manage_apis.html), puoi proteggere le tue applicazioni a livello di gateway anziché a livello di codice della tua applicazione. Per vedere l'integrazione in azione, guarda <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Prova una delle nostre applicazioni Cloud Foundry di esempio per scoprire come integrare l'ID applicazione nelle tue applicazioni.</dd>
  <dt>Guida alla programmazione iOS</dt>
    <dd>Sviluppi applicazioni per Apple? Prova la <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">Guida alla programmazione iOS <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per conoscere, sperimentare e migliorare le tue applicazioni iOS esistenti con {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>


## Architettura
{: #architecture}

Con {{site.data.keyword.appid_short_notm}}, puoi aggiungere un livello di sicurezza alle tue applicazioni richiedendo agli utenti di effettuare l'accesso. Puoi anche utilizzare l'SDK server per proteggere le tue risorse di back-end.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} diagramma architettura](/images/appid_architecture.png)

<dl>
  <dt> Applicazione </dt>
    <dd><strong>SDK server</strong>: puoi proteggere le tue risorse di back-end ospitate in {{site.data.keyword.Bluemix_notm}} e le tue applicazioni web utilizzando l'SDK server. Estrae il token di accesso da una richiesta e lo convalida con {{site.data.keyword.appid_short_notm}}. </br>
    <strong>SDK client</strong>: puoi proteggere le tue applicazioni mobili con l'SDK client per Android o iOS. L'SDK client comunica con le tue risorse cloud per avviare automaticamente il processo di autenticazione quando individua una verifica dell'autorizzazione.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: dopo una corretta autenticazione, {{site.data.keyword.appid_short_notm}} restituisce i token di identità e accesso alla tua applicazione.</br>
    <strong>Cloud Directory</strong>: gli utenti possono registrarsi al servizio con la propria email e una password. Puoi quindi gestire i tuoi utenti in una vista elenco tramite la IU. Con Cloud Directory, {{site.data.keyword.appid_short_notm}} funziona come provider di identità.</dd>
  <dt>Esterna (terze parti)</dt>
    <dd><strong>Provider di identità sociali e aziendali</strong>:{{site.data.keyword.appid_short_notm}} supporta due provider di identità sociali, Facebook e Google+, e un provider di identità aziendale: SAML 2.0 Federation. Il servizio stabilisce un reindirizzamento al provider di identità e verifica i token di autenticazione restituiti. Se i token sono validi, il servizio concede l'accesso alla tua applicazione senza mai avere accesso alla reale passphrase.</dd>
</dl>


## Flusso della richiesta
{: #request}

Il seguente diagramma descrive in che modo una richiesta fluisce dall'SDK client ai tuoi provider di identità e alle tue risorse di back-end.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} flusso richiesta](/images/appidrequestflow.png)


* L'SDK client {{site.data.keyword.appid_short_notm}} effettua una richiesta alle tue risorse di back-end protette con l'SDK server {{site.data.keyword.appid_short_notm}}.
* L'SDK server {{site.data.keyword.appid_short_notm}} rileva una richiesta non autorizzata e restituisce il codice HTTP 401 e l'ambito di autorizzazione.
* L'SDK client rileva automaticamente l'HTTP 401 e avvia il processo di autenticazione.
* Quando l'SDK client contatta il servizio, l'SDK server restituisce il widget di accesso se è configurato più di un provider di identità. {{site.data.keyword.appid_short_notm}} richiama il provider di identità e presenta il modulo di accesso per tale provider o restituisce un codice concesso che permette l'autenticazione se non è stato configurato alcun provider di identità.
* {{site.data.keyword.appid_short_notm}} chiede all'applicazione client di autenticarsi fornendo una richiesta di verifica dell'autenticazione.
* Se è stato configurato un provider di identità quando l'utente accede, l'autenticazione viene gestita dal flusso OAuth corrispondente.
* Se l'autenticazione termina con lo stesso codice concesso, il codice viene inviato all'endpoint del token. L'endpoint restituisce due token: un token di accesso e un token di identità. Da questo punto in avanti, tutte le richieste effettuate con l'SDK client hanno un'intestazione di autorizzazione di nuova acquisizione.
* L'SDK client reinvia automaticamente la richiesta originale che ha attivato il flusso di autorizzazione.
* L'SDK server estrae l'intestazione di autorizzazione dalla richiesta, convalida l'intestazione con il servizio e concede l'accesso a una risorsa di back-end.

**Nota**: i protocolli implementati sono completamente conformi con OpenID Connect (OIDC).
