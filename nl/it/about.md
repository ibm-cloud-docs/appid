---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}

# Informazioni su {{site.data.keyword.appid_short_notm}}
{: #about}

La sicurezza delle applicazioni può essere incredibilmente complicata. Per la maggior parte degli sviluppatori, è una delle parti più difficili nella creazione di un'applicazione. Come puoi essere sicuro di proteggere le informazioni dell'utente? Integrando {{site.data.keyword.appid_full}} nelle tue applicazioni, puoi proteggere le risorse e aggiungere l'autenticazione, anche quando non hai molta esperienza in materia di sicurezza.
{:shortdesc}


## Motivi per usare il servizio
{: #reasons}

{{site.data.keyword.appid_short_notm}} consente agli sviluppatori di aggiungere facilmente l'autenticazione alle loro applicazioni mobile e web con poche righe di codice e di proteggere i loro servizi e applicazioni native cloud su {{site.data.keyword.Bluemix_notm}}. Richiedendo agli utenti di accedere alla tua applicazione, puoi memorizzare i dati utente come le preferenze dell'applicazione o le informazioni dai profili sociali pubblici e quindi utilizzare tali dati per personalizzare ogni esperienza utente nella tua applicazione. {{site.data.keyword.appid_short_notm}} ti fornisce un framework di accesso, ma puoi anche portare le tue schermate di accesso personalizzate quando utilizzi Cloud Directory.
{: shortdesc}

Perché dovrei utilizzare {{site.data.keyword.appid_short_notm}}? Verifica i seguenti scenari per vedere se uno di essi va bene per te.

<table>
  <tr>
    <th>Scenario</th>
    <th>Soluzione</th>
  </tr>
  <tr>
    <td>Devi aggiungere [autorizzazione e autenticazione](/docs/services/appid/authorization.html) alle tue applicazioni mobile e web ma non hai esperienza in fatto di sicurezza.</td>
    <td>{{site.data.keyword.appid_short_notm}} rende semplice aggiungere una fase di autenticazione alle tue applicazioni. Puoi aggiungere l'accesso email o nome utente, social o aziendale alle tue applicazioni con API, SDK, IU pregenerate o personalizzate.</td>
  </tr>
  <tr>
    <td>Desideri limitare l'accesso alle tue applicazioni e alle risorse di back-end.</td>
    <td>Puoi proteggere facilmente le tue applicazioni, risorse di backend e API utilizzando l'autenticazione basata sugli standard fornita da {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td>Desideri creare esperienze dell'applicazione personalizzate per i tuoi utenti.</td>
    <td>Con {{site.data.keyword.appid_short_notm}}, puoi [archiviare i dati utente](/docs/services/appid/user-profile.html) come le preferenze dell'applicazione o le informazioni dai loro profili sociali pubblici e poi utilizzare quei dati per personalizzare ogni esperienza della tua applicazione.</td>
  </tr>
  <tr>
    <td>Vuoi gestire gli utenti in un modo scalabile.</td>
    <td> {{site.data.keyword.appid_short_notm}} ti consente di creare una [Cloud Directory](/docs/services/appid/cloud-directory.html), che ti permette di aggiungere la registrazione e l'accesso utente alle tue applicazioni. Cloud Directory ti viene fornito con il framework per conservare un registro utenti che può ridimensionarsi con la tua base di utenti. Con la funzionalità precostruita per il self-service, come ad esempio una verifica dell'email e le reimpostazioni della password, puoi assicurarti che la tua applicazione stia autenticando gli utenti in modo sicuro.</td>
  </tr>
</table>


## Integrazioni
{: #integrations}

Puoi utilizzare {{site.data.keyword.appid_short_notm}} con le altre offerte {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>Configurando Ingress in un cluster standard, puoi proteggere le tue applicazioni a livello di cluster. Per iniziare, consulta <a href="/docs/containers/cs_annotations.html#appid-auth">l'annotazione di Ingress per l'autenticazione {{site.data.keyword.appid_short_notm}}</a> o il post di blog <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Announcing {{site.data.keyword.appid_short_notm}} integration to {{site.data.keyword.containerlong_notm}} <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.</dd>
  <dt>{{site.data.keyword.openwhisk}} e API Connect</dt>
    <dd>Quando crei le tue API con [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) e [API Connect](/docs/services/apiconnect/getting-started.html), puoi proteggere le tue applicazioni a livello di gateway anziché a livello di codice della tua applicazione. Per vedere l'integrazione in azione, guarda <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Prova una delle applicazioni Cloud Foundry di esempio per scoprire come integrare {{site.data.keyword.appid_short_notm}} nelle tue applicazioni.</dd>
  <dt>Guida alla programmazione iOS</dt>
    <dd>Sviluppi applicazioni per Apple? Prova la <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">Guida alla programmazione iOS <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per conoscere, sperimentare e migliorare le tue applicazioni iOS esistenti con {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>Puoi anche monitorare l'attività amministrativa effettuata in {{site.data.keyword.appid_short_notm}} come lo modifiche alla configurazione del dashboard, utilizzando il servizio [{{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html).</dd>
  <dt>Guida alla programmazione Node.js</dt>
    <dd>Sviluppi applicazioni in Node.js? Prova la <a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Guida alla programmazione Node.js <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per conoscere, sperimentare e migliorare le tue applicazioni Node.js esistenti con {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>


## Architettura
{: #architecture}

Con {{site.data.keyword.appid_short_notm}}, puoi aggiungere un livello di sicurezza alle tue applicazioni richiedendo agli utenti di effettuare l'accesso. Puoi anche utilizzare le API o l'SDK server per proteggere le tue risorse di back-end.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} diagramma architettura](images/appid_architecture1.png)

<dl>
  <dt>Applicazione</dt>
    <dd><strong>SDK server</strong>: puoi proteggere le tue risorse di back-end ospitate in {{site.data.keyword.Bluemix_notm}} e le tue applicazioni web utilizzando l'SDK server. Estrae il token di accesso da una richiesta e lo convalida con {{site.data.keyword.appid_short_notm}}. </br>
    <strong>SDK client</strong>: puoi proteggere le tue applicazioni mobili con l'SDK client per Android o iOS. L'SDK client comunica con le tue risorse cloud per avviare automaticamente il processo di autenticazione quando individua una verifica dell'autorizzazione.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: dopo una corretta autenticazione, {{site.data.keyword.appid_short_notm}} restituisce i token di identità e accesso alla tua applicazione.</br>
    <strong>Cloud Directory</strong>: gli utenti possono registrarsi al servizio con la propria email e una password. Puoi quindi gestire i tuoi utenti in una vista elenco tramite la IU. Con Cloud Directory, {{site.data.keyword.appid_short_notm}} funziona come provider di identità.</dd>
  <dt>Esterna (terze parti)</dt>
    <dd><strong>Provider di identità sociali e aziendali</strong>:{{site.data.keyword.appid_short_notm}} supporta Facebook, Google+ e  SAML 2.0 Federation come opzioni del provider di identità. Il servizio stabilisce un reindirizzamento al provider di identità e verifica i token di autenticazione restituiti. Se i token sono validi, il servizio concede l'accesso alla tua applicazione senza mai avere accesso alla reale passphrase.</dd>
</dl>

</br>


