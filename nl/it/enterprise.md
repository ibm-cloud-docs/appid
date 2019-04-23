---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

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

# SAML
{: #enterprise}

SAML (Security Assertion Markup Language) è un open standard per lo scambio di dati di autenticazione e autorizzazione tra un provider di identità che asserisce l'identità dell'utente e un provider di servizi che utilizza le informazioni sull'identità dell'utente.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} funziona come un provider di servizi e avvia un accesso SSO (single sign-on) a un provider di terze parti come ad esempio Active Directory Federation Services. Il protocollo <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> supporta diversi profili e opzioni di associazione. {{site.data.keyword.appid_short_notm}} supporta il profilo SSO del browser web, con l'associazione HTTP Post.

Per i passi su come utilizzare un provider di identità SAML specifico, consulta questi post di blog sulla configurazione di {{site.data.keyword.appid_short_notm}} con [Ping One ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [an Azure Active Directory ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) o [an Active Directory Federation Service ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}



## Descrizione delle asserzioni
{: #saml-assertions}

Un'asserzione SAML è simile a un [attributo utente](/docs/services/appid?topic=appid-user-profile#user-profile). È una dichiarazione o un elemento di informazione su un utente che un provider di identità restituisce a {{site.data.keyword.appid_short_notm}} quando un utente accede con esito positivo alla tua applicazione. A seconda della configurazione della tua applicazione e del provider di identità da te utilizzato, le informazioni possono includere il nome e l'email di un utente oppure un altro campo di cui tu richiedi la specifica.
{: shortdesc}

Quando le asserzioni vengono restituite a {{site.data.keyword.appid_short_notm}}, il servizio attua la federazione dell'identità dell'utente. Se corrisponde a una delle seguenti attestazioni OIDC, l'asserzione SAML viene automaticamente aggiunta al token di identità. Se uno o più di questi valori viene modificato sul lato del provider, i nuovi valori sono disponibili solo dopo che l'utente ha effettuato di nuovo l'accesso.

 * `name`
 * `email`
 * `locale`
 * `picture`

Le asserzioni che non corrispondono ad alcuno dei nomi standard vengono ignorate per impostazione predefinita ma, se il tuo provider SAML restituisce altre asserzioni, è possibile ottenere le informazioni quando un utente esegue l'accesso. Creando un array delle asserzioni che vuoi utilizzare, puoi [inserire le informazioni nei tuoi token](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Assicurati però di non aggiungere più informazioni del necessario ai tuoi token. I token sono di norma inviati in intestazioni http, che sono di dimensioni limitate.
{: tip}

### Quale aspetto deve avere un'asserzione SAML per {{site.data.keyword.appid_short_notm}}?
{: #saml-example}

Il servizio prevede che un'asserzione SAML sia simile al seguente esempio.

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}


### Quali tipi di algoritmi sono supportati da {{site.data.keyword.appid_short_notm}}?
{: #saml-signatures}

{{site.data.keyword.appid_short_notm}} utilizza l'algoritmo <a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per elaborare le firme digitali XML.




## Fornitura di metadati al tuo provider di identità
{: #saml-provide-idp}

Per configurare la tua applicazione, devi fornire informazioni a un provider di identità compatibile con SAML. Le informazioni vengono scambiate tramite un file XML di metadati che contiene inoltre dati di configurazione utilizzati per stabilire l'attendibilità.
{: shortdesc}

Non puoi abilitare SAML senza averlo prima configurato come un provider di identità.
{: tip}

1. Nella scheda **Manage** del dashboard {{site.data.keyword.appid_short_notm}}, fai clic su **Edit** nella riga **SAML** per configurare le tue impostazioni.
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

3. Fornisci i dati al tuo provider di identità. Se il tuo provider di identità supporta il caricamento del file di metadati, puoi farlo. In caso contrario, configura le proprietà manualmente. Non tutti i provider di identità utilizzano le stesse proprietà, quindi potresti non utilizzarle tutte.

  I nomi delle proprietà potrebbero differire tra i provider di identità.
  {: tip}

4. Passa **SAML 2.0 Federation** a **Enabled**.

## Fornitura di metadati a {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

Puoi ottenere i dati dal tuo provider di identità e fornirli a {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Fornitura dei metadati con la GUI
{: #saml-provide-gui}

1. Passa alla scheda **SAML 2.0** del dashboard {{site.data.keyword.appid_short_notm}}. Immetti i seguenti metadati che hai ottenuto dal provider di identità nella sezione **Provide Metadata from SAML IdP**.
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


### Fornitura dei metadati con l'API
{: #saml-provide-api}

1. Ottieni i tuoi metadati SAML eseguendo una richiesta GET all'[endpoint API /getSamlMetadata](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

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

2. Configura la tua richiesta POST con l'[endpoint API /set_saml_idp](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

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
{: #saml-testing}

Puoi verificare la configurazione tra il tuo provider di identità SAML e {{site.data.keyword.appid_short_notm}}.

1. Assicurati di aver salvato la tua configurazione.
2. Passa alla scheda **SAML 2.0** del dashboard {{site.data.keyword.appid_short_notm}} e fai clic su **Test**. Si apre una nuova scheda.
3. Accedi con un utente che il tuo provider di identità ha già autenticato.
4. Dopo aver completato il modulo, verrai reindirizzato a un'altra pagina.
  * Autenticazione riuscita: la connessione tra {{site.data.keyword.appid_short_notm}} e il provider di identità funziona correttamente. La pagina visualizza [token di accesso e identità](/docs/services/appid?topic=appid-tokens#tokens) validi.
  * Autenticazione non riuscita: la connessione viene interrotta. La pagina visualizza gli errori e il file XML di risposta SAML.


Stai avendo dei problemi? Consulta [Risoluzione dei problemi con le configurazioni del provider di identità](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}
