---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Configurazione di provider di identità aziendali
{: #enterprise}

Se hai già un repository utenti esistente e un modo certificato per autenticare gli utenti nei tuoi sistemi interni, puoi configurare il servizio {{site.data.keyword.appid_full}} per utilizzare un provider di identità aziendale.
{: shortdesc}

## Descrizione di SAML
{: #saml}

SAML è un open standard per lo scambio di dati di autenticazione e autorizzazione tra un provider di identità che asserisce l'identità dell'utente e un provider di servizi che consuma le informazioni sull'identità dell'utente.
{: shortdesc}

Come funziona?

{{site.data.keyword.appid_short_notm}} funziona come un provider di servizi e avvia un accesso SSO (single sign on) a un provider di terze parti come Active Directory Federation Services. Il protocollo <a href="http://saml.xml.org/saml-specifications" target="_blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> supporta diversi profili e opzioni di associazione. {{site.data.keyword.appid_short_notm}} supporta il profilo SSO del browser web, con l'associazione HTTP Post.

### Asserzioni SAML e attestazioni token di identità

Un'asserzione SAML è un pacchetto di informazioni che contiene una o più istruzioni. L'asserzione contiene la decisione dell'autorizzazione e potrebbe contenere informazioni sull'identità dell'utente.

Quando un utente accede con un provider di identità, quel provider invia un'asserzione a {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} propaga le informazioni sull'identità dell'utente restituite nell'asserzione SAML alla tua applicazione come attestazioni token OIDC. L'attributo SAML deve corrispondere a una delle seguenti attestazioni OIDC per essere aggiunto al token di identità.

È possibile aggiungere le seguenti attestazioni:
* `name`
* `email`
* `locale`
* `picture`

Gli elementi di attributo SAML rimanenti che non corrispondono a nessuno dei nomi standard vengono ignorati.

## Configurazione della tua applicazione per lavorare con un provider di identità SAML esterno
{: #configuring-saml}

Puoi configurare il servizio {{site.data.keyword.appid_short_notm}} per utilizzare un provider di identità SAML (Security Assertion Markup Language).
{: shortdesc}

### Fornitura di metadati al tuo provider di identità

Per configurare la tua applicazione, devi fornire informazioni a un provider di identità compatibile con SAML. Le informazioni vengono scambiate tramite un file XML di metadati che contiene inoltre dati di configurazione utilizzati per stabilire l'attendibilità.

1. Nella scheda **Manage** del dashboard {{site.data.keyword.appid_short_notm}}, imposta **SAML 2.0** su **On**. Quindi, fai clic su **Edit** per configurare le tue impostazioni SAML.
2. Fai clic su **Download SAML Metadata file**. Il tuo provider di identità si aspetta le seguenti informazioni dal file.
  <table>
    <tr>
      <th> Variabile </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>L'identificativo che consente al provider di identità di sapere che {{site.data.keyword.appid_short_notm}} ha emesso la richiesta SAML.</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>La posizione in cui il provider di identità invia le asserzioni SAML dopo aver autenticato correttamente un utente.</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>Le istruzioni su come il provider di identità deve inviare la risposta SAML.</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>Il modo in cui il provider di identità conosce il formato dell'identificativo che deve inviare nell'oggetto di un'asserzione. Il modo in cui {{site.data.keyword.appid_short_notm}} identifica gli utenti.</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>Il modo in cui un provider di identità controlla se è necessario firmare l'asserzione. Il servizio si aspetta che l'asserzione sia firmata, ma non supporta asserzioni crittografate.</td>
    </tr>
  </table>

3. Fornisci i dati al tuo provider di identità. Se il tuo provider di identità supporta il caricamento del file di metadati, puoi farlo. In caso contrario, configura le proprietà manualmente. Non tutti i provider di identità utilizzeranno le stesse proprietà, quindi se non le usi tutte, va bene.

I nomi delle proprietà possono differire tra i provider di identità.
{: tip}

### Fornitura di metadati a {{site.data.keyword.appid_short_notm}}

Dovrai ottenere i dati dal provider di identità e fornirli a {{site.data.keyword.appid_short_notm}}.

1. Passa alla scheda **SAML 2.0** del dashboard {{site.data.keyword.appid_short_notm}}. Inserisci i seguenti metadati che hai ottenuto dal provider di identità nella sezione **Provide Metadata from SAML IdP**.
  <table>
    <tr>
      <th> Variabile </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>L'URL a cui l'utente viene reindirizzato per l'autenticazione. È ospitato dal tuo provider di identità SAML.</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>Il nome globalmente univoco per un provider di identità SAML.</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>Il certificato emesso dal tuo provider di identità SAML. È utilizzato per firmare e convalidare le asserzioni SAML. Tutti i provider sono diversi, ma potresti essere in grado di scaricare il certificato di firma dal tuo provider di identità. Il certificato deve essere in formato <code>.pem</code>.</td>
    </tr>
  </table>

2. Facoltativo: fornisci un **certificato secondario** che viene utilizzato se la convalida della firma non riesce sul certificato primario. Se la chiave di firma rimane la stessa, {{site.data.keyword.appid_short_notm}} non blocca l'autenticazione per i certificati scaduti.

3. Aggiorna il **nome provider** e fai clic su **Save**. Il nome predefinito è SAML.


### Verifica della configurazione

Puoi verificare la configurazione tra il tuo provider di identità SAML e {{site.data.keyword.appid_short_notm}}.

1. Assicurati di aver salvato la tua configurazione.
2. Passa alla scheda **SAML 2.0** del dashboard {{site.data.keyword.appid_short_notm}} e fai clic su **Test**. Si apre una nuova scheda.
3. Accedi con un utente che il tuo provider di identità ha già autenticato.
4. Dopo aver completato il modulo, verrai reindirizzato a un'altra pagina.
  * Autenticazione riuscita: la connessione tra {{site.data.keyword.appid_short_notm}} e il provider di identità funziona correttamente. La pagina visualizza [token di accesso e identità](/docs/services/appid/authorization.html#key-concepts) validi.
  * Autenticazione non riuscita: la connessione viene interrotta. La pagina visualizza gli errori e il file XML di risposta SAML.
