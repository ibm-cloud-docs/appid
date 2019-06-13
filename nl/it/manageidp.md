---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, development, identity provider, tokens, customization, lifetime

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


# Gestione delle autenticazioni
{: #managing-idp}

I provider di identità (IdP) aggiungono un livello di sicurezza per le tue applicazioni mobili e web, tramite l'autenticazione. Con {{site.data.keyword.appid_full}}, puoi configurare uno o più provider di identità per creare un'esperienza di accesso personalizzata per i tuoi utenti.
{: shortdesc}


{{site.data.keyword.appid_short_notm}} interagisce con i provider di identità utilizzando più protocolli come ad esempio OpenID Connect, SAML e altri. Ad esempio, OpenID Connect è il protocollo utilizzato con molti provider social come Facebook e Google. I provider aziendali quali <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> o <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>, generalmente usano SAML come loro protocollo di identità. Per [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), il servizio utilizza SCIM per verificare le informazioni sull'identità.

Quando utilizzi i provider di identità aziendali o social, {{site.data.keyword.appid_short_notm}} ha l'accesso in lettura alle informazioni sull'account degli utenti. Il servizio utilizza un token e le asserzioni restituite dal provider di identità per verificare se un utente è chi dice di essere. Poiché il servizio non ha mai l'accesso in scrittura alle informazioni, gli utenti devono utilizzare il provider di identità di loro scelta per effettuare delle azioni, come il ripristino della propria password. Ad esempio, se un utente accede alla tua applicazione con Facebook e poi volesse modificare la propria password, deve andare all'indirizzo `www.facebook.com` per farlo.

Quando utilizzi [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), {{site.data.keyword.appid_short_notm}} è il provider di identità. Il servizio utilizza il tuo registro per verificare l'identità dei tuoi utenti. Poiché {{site.data.keyword.appid_short_notm}} è il provider, gli utenti possono avvalersi della funzionalità avanzata, come il ripristino delle loro password, direttamente nella tua applicazione.

Come gestisco l'identità dell'applicazione? Consulta [Identità dell'applicazione](/docs/services/appid?topic=appid-app).
{: tip}

Il servizio può essere configurato per utilizzare diversi provider. Consulta la seguente tabella per informazioni sulle tue opzioni.

<table>
  <tr>
    <th>Provider</th>
    <th>Tipo</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)</td>
    <td>Registro gestito</td>
    <td>Puoi mantenere il tuo registro utenti nel cloud. Quando un utente si registra alla tua applicazione, viene aggiunto alla tua directory di utenti. Questa opzione fornisce ai tuoi utenti maggiore libertà nel gestire il proprio account all'interno della tua applicazione.</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid?topic=appid-enterprise#enterprise)</td>
    <td>Aziendale</td>
    <td>Puoi creare un'esperienza SSO (single sign-on) per i tuoi utenti finali.</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid?topic=appid-social#facebook)</td>
    <td>Social</td>
    <td>Gli utenti finali possono accedere alla tua applicazione utilizzando le loro credenziali Facebook.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid?topic=appid-social#google)</td>
    <td>Social</td>
    <td>Gli utenti finali possono accedere alla tua applicazione utilizzando le loro credenziali Google.</td>
  </tr>
  <tr>
    <td>[Personalizzato](/docs/services/appid?topic=appid-custom-identity#custom-identity)</td>
    <td> </td>
    <td>Se nessuna delle opzioni fornite soddisfa le tue necessità specifiche, puoi configurare il tuo flusso di identità per lavorare con {{site.data.keyword.appid_short_notm}}.</td>  
  </tr>
</table>

## Gestione dei provider
{: #managing-providers}

Un provider di identità crea e gestisce le informazioni su un'entità come ad esempio un utente, un ID funzionale o un'applicazione. Il provider verifica l'identità dell'entità utilizzando delle credenziali, come ad esempio una password. Successivamente, l'IdP invia le informazioni sull'identità a un altro provider di servizi. Poiché il provider di identità autentica l'entità, {{site.data.keyword.appid_short_notm}} è in grado di autorizzarla e di concedere l'accesso alle tue applicazioni.
{: shortdesc}

Per gestire i tuoi provider di identità:

1. Passa al tuo dashboard del servizio.
2. Nella sezione **Identity Providers** della navigazione, seleziona la pagina **Manage**.
3. Sulla scheda **Identity Providers**, imposta i provider che desideri utilizzare su **On**.
4. Facoltativo: decidi se disattivare gli utenti anonimi (**Anonymous users**) o lasciare il valore predefinito, ossia **On**. Quando impostato su **On**, gli attributi utente vengono associati all'utente dal momento in cui iniziano ad interagire con la tua applicazione. Per ulteriori informazioni sul percorso per diventare un utente identificato, consulta [Autenticazione progressiva](/docs/services/appid?topic=appid-anonymous#progressive)

{{site.data.keyword.appid_short_notm}} fornisce delle credenziali predefinite per aiutarti con la configurazione iniziale di Facebook e Google+. Sei limitato a 100 utilizzi delle credenziali per istanza, al giorno. Poiché sono credenziali IBM, sono pensate per essere utilizzate solo per lo sviluppo. Prima di pubblicare la tua applicazione, aggiorna la configurazione con le tue proprie credenziali.
{: tip}


## Aggiunta di URI di reindirizzamento
{: #add-redirect-uri}

Un URI di reindirizzamento è l'endpoint di callback della tua applicazione. Durante il flusso di accesso, {{site.data.keyword.appid_short_notm}} convalida gli URI prima di consentire ai client di partecipare al flusso di lavoro di autorizzazione, e questo aiuta a impedire attacchi di phishing e di concedere perdite di codice. Registrando il tuo URI, stai indicando a {{site.data.keyword.appid_short_notm}} che l'URI è attendibile ed è valido per il reindirizzamento dei tuoi utenti.

Assicurati di registrare solo gli URI delle applicazioni che ritieni attendibili.
{: note}


1. Fai clic su **Authentication Settings** per visualizzare le tue opzioni di configurazione di token e URI.

2. Nel campo **Add web redirect URI**, immetti l'URI. Ogni URI deve iniziare con `http://` o `https://` e deve includere il percorso completo, compresi gli eventuali parametri di query, perché il reindirizzamento venga eseguito correttamente. Hai bisogno di aiuto con la formattazione del tuo URI? Consulta la seguente tabella per qualche esempio.

  <table>
    <tr>
      <th>Tipo</th>
      <th>URI di esempio</th>
    </tr>
    <tr>
      <td>Dominio personalizzato</td>
      <td><code>http://mydomain.net/myapp2path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Dominio secondario Ingress</td>
      <td><code>https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Disconnessione</td>
      <td><code>http://mydomain.net/myapp2path/appid_logout</code></td>
    </tr>  
  </table>

3. Fai clic sul simbolo **+** nella casella **Add web redirect URIs**.

4. Ripetere i passi da uno a tre fino a che al tuo elenco non vengono aggiunti tutti gli URI possibili.



Non sei sicuro da dove proviene il tuo URI di reindirizzamento? Guarda il seguente breve video per vedere da dove proviene e come aggiungerlo al tuo elenco.

<iframe class="embed-responsive-item" id="redirecturi" title="{{site.data.keyword.appid_short_notm}}: Come correggere un URI di reindirizzamento non valido" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6hxqbvpc054?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>



## Configurazione della durata del token
{: #idp-token-lifetime}

La durata del token riinizia ad ogni accesso utente. Ad esempio, hai impostato la tua durata del token di aggiornamento su 10 giorni. Vengono creati un token di accesso e un token di aggiornamento quando l'utente accede per la prima volta. Se l'utente ritorna alla tua applicazione pochi giorni dopo, 3 giorni per essere precisi, non ha bisogno di riaccedere. Ma, se l'utente ha atteso 12 giorni dopo l'accesso iniziale e poi ritorna alla tua applicazione, dovrà riaccedere e sarà associata all'utente un serie di token. Per ulteriori informazioni sui token, consulta [Descrizione dei token](/docs/services/appid?topic=appid-tokens#tokens).

1. Per consentire l'accesso senza il bisogno di un'interazione da parte dell'utente, imposta **refresh tokens** su **On**.

2. Imposta la tua durata del token di aggiornamento. La scadenza viene impostata in giorni e può essere un qualsiasi valore compreso nell'intervallo tra 1 e 90. Più piccolo è il numero, maggiore è la frequenza in cui un utente deve accedere.

3. Imposta la tua durata del token di accesso. La scadenza viene impostata in minuti e può essere un valore compreso nell'intervallo tra 5 e 1440. Più piccolo è il valore e maggiore è la protezione che hai in caso di furto del token.

4. Imposta la tua durata del token anonimo. Viene assegnato un [token anonimo](/docs/services/appid?topic=appid-anonymous#progressive) agli utenti nel momento in cui iniziano ad interagire con la tua applicazione. Quando un utente accede, le informazioni nel token anonimo vengono poi trasferite al token associato all'utente. La scadenza viene impostata in giorni e può essere un qualsiasi compreso tra 1 e 90.


Quando imposti una scadenza del token, si applica a tutti i provider che hai configurato, compresi quelli social e aziendali.
{: tip}
