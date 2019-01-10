---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# SAML
{: #enterprise}


SAML (Security Assertion Markup Language) è un open standard per lo scambio di dati di autenticazione e autorizzazione tra un provider di identità che asserisce l'identità dell'utente e un provider di servizi che utilizza le informazioni sull'identità dell'utente.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} funziona come un provider di servizi e avvia un accesso SSO (single sign on) a un provider di terze parti come Active Directory Federation Services. Il protocollo <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> supporta diversi profili e opzioni di associazione. {{site.data.keyword.appid_short_notm}} supporta il profilo SSO del browser web, con l'associazione HTTP Post.

Per i passi su come utilizzare un provider di identità SAML specifico, consulta questi post di blog sulla configurazione di {{site.data.keyword.appid_short_notm}} con [Ping One ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [an Azure Active Directory ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) o [an Active Directory Federation Service ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}


## Asserzioni SAML e attestazioni token di identità

Un'asserzione SAML è un pacchetto di informazioni che contiene una o più istruzioni. L'asserzione contiene la decisione dell'autorizzazione e potrebbe contenere informazioni sull'identità dell'utente.

Quando un utente accede con un provider di identità, quel provider invia un'asserzione a {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} propaga le informazioni sull'identità dell'utente restituite nell'asserzione SAML alla tua applicazione come attestazioni token OIDC. L'attributo SAML deve corrispondere a una delle seguenti attestazioni OIDC per essere aggiunto al token di identità.

È possibile aggiungere le seguenti attestazioni:
* `name`
* `email`
* `locale`
* `picture`

Gli elementi di attributo SAML rimanenti che non corrispondono a nessuno dei nomi standard vengono ignorati. Nota che se uno o più di questi valori viene modificato sul lato del provider, i nuovi valori sono disponibili solo dopo che l'utente ha effettuato di nuovo l'accesso.


Cerchi un esempio? Consulta <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Setting up {{site.data.keyword.appid_long}} with your Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> o <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/" target="_blank">Setting up {{site.data.keyword.appid_long}} with Ping One <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.

## Fornitura di metadati al tuo provider di identità
{: #provide-idp}

Per configurare la tua applicazione, devi fornire informazioni a un provider di identità compatibile con SAML. Le informazioni vengono scambiate tramite un file XML di metadati che contiene inoltre dati di configurazione utilizzati per stabilire l'attendibilità.
{: shortdesc}

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

I nomi delle proprietà potrebbero differire tra i provider di identità.
{: tip}

## Fornitura di metadati a {{site.data.keyword.appid_short_notm}}
{: #provide-appid}

Ottieni i dati dal tuo provider di identità e forniscili a {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

**Fornitura dei metadati con la GUI**

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

Vuoi impostare un contesto di autenticazione? Puoi farlo tramite l'API.
{: tip}

</br>
</br>

**Fornitura dei metadati con l'API**

1. Ottieni i tuoi metadati SAML eseguendo una richiesta GET all'[endpoint API /getSamlMetadata](https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/getSamlMetadata).

  Codice di esempio:
  ```
  <?xml version="1.0"?>
  <getSamlMetadata>
    <?xml version="1.0"?> <EntityDescriptor> <SPSSODescriptor> <NameIDFormat> </NameIDFormat> <AssertionConsumerService /> </SPSSODescriptor>
   </EntityDescriptor>
    </getSamlMetadata>
  ```
  {: codeblock}

  Output di esempio:
  ```
    {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    },
    "validation_data": {
      "certificates": [
        {
          "certificate_index": 0,
          "expiration_timestamp": 1674473996,
          "warning": "Your certificate will expire in 18 days."
        }
      ]
    }
  }
  ```
  {: screen}

2. Configura la tua richiesta POST con l'[endpoint API /set_saml_idp](https://appid-management.ng.bluemix.net/swagger-ui/#!/Identity_Providers/set_saml_idp).

  1. Nel seguente esempio di metadati, sostituisci le variabili con le tue informazioni.

    ```
    Put {Management URI}/config/idps/saml
    Content-Type: application/json
    {
      "isActive": true,
      "config": {
        "entityID": "https://example.com/saml2/metadata/706634",
        "signInUrl": "https://example.com/saml2/sso-redirect/706634",
        "certificates": [
          "primary-certificate-example-pem-format"
        ],
        "displayName": "my saml example"
      }
    }
    ```
    {: codeblock}

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

  2. Facoltativo: aggiungi un certificato secondario all'array di certificati che segue il certificato primario. Il certificato secondario viene utilizzato se la convalida della firma non riesce con il certificato primario. Se la chiave di firma rimane la stessa, {{site.data.keyword.appid_short_notm}} non blocca l'autenticazione per i certificati scaduti.

    Esempio:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "certificates": [
          "primary-certificate-example-pem-format",
          "secondary-certificate-example-pem-format"
        ],
        ...
      }
    }
    ```
    {: screen}
  {: #configuring-saml-new}
  3. Facoltativo: aggiungi un contesto di autenticazione aggiungendo un array di classi e una stringa di confronto al tuo codice. Assicurati di aggiornare entrambi i parametri `class` e `comparison` con i tuoi valori. Un contesto di autenticazione viene utilizzato per verificare la qualità dell'autenticazione e delle asserzioni SAML.

    Esempio:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "authnContext": {
          "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
          "comparison": "sampleComparisonValue"
        }
      }
    }
    ```
    {: screen}

3. Esegui la richiesta. Se scegli di aggiungere dei valori facoltativi, la tua richiesta dovrebbe essere simile al seguente esempio.

  ```
  Put {Management URI}/config/idps/saml
  Content-Type: application/json
  {
    "isActive": true,
    "config": {
      ...
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
        "comparison": "sampleComparisonValue"
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
      "displayName": "my saml example"
    }
  }
  ```
  {: codeblock}


## Verifica della configurazione
{: #testing}

Puoi verificare la configurazione tra il tuo provider di identità SAML e {{site.data.keyword.appid_short_notm}}.

1. Assicurati di aver salvato la tua configurazione.
2. Passa alla scheda **SAML 2.0** del dashboard {{site.data.keyword.appid_short_notm}} e fai clic su **Test**. Si apre una nuova scheda.
3. Accedi con un utente che il tuo provider di identità ha già autenticato.
4. Dopo aver completato il modulo, verrai reindirizzato a un'altra pagina.
  * Autenticazione riuscita: la connessione tra {{site.data.keyword.appid_short_notm}} e il provider di identità funziona correttamente. La pagina visualizza [token di accesso e identità](/docs/services/appid/authorization.html#tokens) validi.
  * Autenticazione non riuscita: la connessione viene interrotta. La pagina visualizza gli errori e il file XML di risposta SAML.


Stai avendo dei problemi? Consulta [Risoluzione dei problemi con le configurazioni del provider di identità](/docs/services/appid/ts_saml.html).
{: tip}
