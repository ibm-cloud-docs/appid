---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

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

Quando hai un provider di identità basato su SAML, puoi configurare {{site.data.keyword.appid_short_notm}} ad agire come un provider di servizi che avvia un accesso SSO (single sign-on) a un provider di terze parti. Durante il flusso di accesso, i tuoi utenti possono essere facilmente autenticati e possono ottenere dei token di sicurezza {{site.data.keyword.appid_short_notm}} che gli permettono di accedere alle tue applicazioni e API protette.
{: shortdesc}

 
Utilizzi un provider di identità SAML specifico? Consulta uno di questi post di blog sulla configurazione di {{site.data.keyword.appid_short_notm}} con [Ping One ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-ping-one), [an Azure Active Directory ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory) o [an Active Directory Federation Service ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service).
{: tip}


## Descrizione di SAML
{: #saml-understanding}

SAML (Security Assertion Markup Language) è un open standard per lo scambio di dati di autenticazione e autorizzazione tra un provider di identità che asserisce l'identità dell'utente e un provider di servizi che utilizza le informazioni sull'identità dell'utente.
{: shortdesc}

Il protocollo <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> supporta diversi profili e opzioni di associazione. {{site.data.keyword.appid_short_notm}} supporta il profilo SSO del browser web, con l'associazione HTTP Post.

### Quali sono le basi tecniche dei flussi?
{: #saml-tech-basis}

SAML 2.0 è uno dei framework più consolidati per gli standard di autenticazione e autorizzazione. È un protocollo basato su XML tra un provider di servizi ({{site.data.keyword.appid_short_notm}}) e un provider di identità. Quando un provider di identità autentica un utente, crea dei token SAML, che contengono asserzioni o istruzioni sull'utente. Le istruzioni potrebbero contenere:

- informazioni sull'autenticazione come ad esempio il modo in cui l'utente ha eseguito l'autenticazione - una password, MFA, ecc ...
- attributi associati all'utente - a quale gruppo appartiene.
- decisioni di autorizzazione che indicano se all'utente è consentito eseguire una particolare azione su una particolare risorsa.

Quando le asserzioni vengono restituite a {{site.data.keyword.appid_short_notm}}, il servizio attua la federazione dell'identità dell'utente e vengono generati i token appropriati. Se corrisponde a una delle seguenti attestazioni OIDC, l'asserzione SAML viene automaticamente aggiunta al token di identità.  Se uno o più di questi valori viene modificato sul lato del provider, i nuovi valori sono disponibili solo dopo che l'utente ha effettuato di nuovo l'accesso.

 * `name`
 * `email`
 * `locale`
 * `picture`

Le asserzioni che non corrispondono ad alcuno dei nomi standard vengono ignorate per impostazione predefinita ma, se il tuo provider SAML restituisce altre asserzioni, è possibile ottenere le informazioni quando un utente esegue l'accesso. Creando un array delle asserzioni che vuoi utilizzare, puoi [inserire le informazioni nei tuoi token](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Assicurati però di non aggiungere più informazioni del necessario ai tuoi token. I token sono di norma inviati in intestazioni http, che sono di dimensioni limitate.
{: tip}

### Come si presenta il flusso?
{: #saml-flow}

Sebbene {{site.data.keyword.appid_short_notm}} e il tuo provider di identità utilizzano il framework SAML per autenticare l'utente, {{site.data.keyword.appid_short_notm}} utilizza ancora il più moderno framework OAuth 2.0/ OIDC per scambiare i token di sicurezza con l'applicazione. Consulta la seguente immagine per vedere un flusso dettagliato di informazioni.

![Flusso di autenticazione aziendale SAML](/images/ibmid-flow.png)

1. Un utente accede alla pagina di login o alla risorsa con restrizioni sulla propria applicazione, che avvia una richiesta all'endpoint {{site.data.keyword.appid_short_notm}} `/authorization` tramite un'API o un SDK {{site.data.keyword.appid_short_notm}}. Se l'utente non è autorizzato, il flusso di autenticazione inizia con un reindirizzamento a {{site.data.keyword.appid_short_notm}}.
2. {{site.data.keyword.appid_short_notm}} genera una richiesta di autenticazione SAML (AuthNRequest) e il browser reindirizza automaticamente l'utente al provider di identità SAML.
3. Il provider di identità analizza la richiesta SAML, autentica l'utente e genera una risposta SAML con le relative asserzioni.
4. Il provider di identità reindirizza l'utente e la risposta a {{site.data.keyword.appid_short_notm}} con la risposta SAML.
5. Se l'autenticazione ha esito positivo, {{site.data.keyword.appid_short_notm}} crea dei token di identità e accesso che rappresentano l'autenticazione e l'autorizzazione di un utente e li restituisce all'applicazione. Se l'autenticazione ha esito negativo, {{site.data.keyword.appid_short_notm}} restituisce il codice di errore del provider di identità all'applicazione.
6. All'utente viene concesso l'accesso all'applicazione o alle risorse protette.



### SSO modifica il flusso?
{: #saml-sso-flow}

Il profilo SSO del browser web che {{site.data.keyword.appid_short_notm}} implementa, viene avviato dal provider di servizi, il che significa che {{site.data.keyword.appid_short_notm}} deve inviare una richiesta SAML al provider di identità per avviare la sessione di autenticazione. 

{{site.data.keyword.appid_short_notm}} non supporta al momento i flussi avviati dal provider di identità che non possono essere utilizzati con il servizio in questo momento.
{: note}

Se il tuo provider di identità supporta SSO, è possibile che l'autenticazione SAML utilizzi la sessione SSO già stabilita per autenticare l'utente. Se non è così, l'utente viene reindirizzato alla pagina di accesso. Potrebbe essere reindirizzato se il tuo provider di identità non può soddisfare i requisiti di autenticazione definiti nella richiesta di autenticazione di {{site.data.keyword.cloud_notm}} che è stata utilizzata per stabilire l'SSO. Ad esempio, se il tuo provider di identità stabilisce una sessione SSO utente utilizzando i dati biometrici, il contesto di autenticazione predefinito di {{site.data.keyword.appid_short_notm}} deve essere modificato. Per impostazione predefinita, {{site.data.keyword.appid_short_notm}} assume che gli utenti vengano autenticati tramite una password su HTTPS: `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.



## Configurazione di SAML in modo che utilizzi {{site.data.keyword.appid_short_notm}}
{: #saml-configure}

Puoi configurare SAML per utilizzare {{site.data.keyword.appid_short_notm}} fornendo i metadati da {{site.data.keyword.appid_short_notm}} al tuo provider di identità e i metadati dal tuo provider di identità a {{site.data.keyword.appid_short_notm}}.



### Fornitura di metadati al tuo provider di identità
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
      <td>Il modo in cui il provider di identità conosce il formato dell'identificativo che deve inviare nell'oggetto di un'asserzione e come {{site.data.keyword.appid_short_notm}} identifica gli utenti. L'ID deve avere il seguente formato: <code><saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"/></code></td>
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



### Fornitura di metadati a {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

Puoi ottenere i dati dal tuo provider di identità e fornirli a {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

**Fornitura dei metadati con la GUI** 

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

</br>

**Fornitura dei metadati con l'API**

1. Visualizza la tua configurazione SAML corrente, inclusi i tuoi certificati e contesto di autenticazione, effettuando una richiesta GET all'endpoint API [`/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

  Codice di esempio:
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
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
    }
  }
  ```
  {: screen}

2. Crea la tua configurazione SAML sostituendo i valori nel seguente esempio con le informazioni dal tuo provider. I valori mostrati nell'esempio sono obbligatori, ma puoi scegliere di includere ulteriori informazioni come mostrato nella tabella.

  ```
  "config": {
    "authnContext": {
      "class": [
        "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
      ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
    ],
    "displayName": "my saml example",
  }
  ```
  {: codeblock}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> Variabile </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>L'URL a cui l'utente viene reindirizzato per l'autenticazione. È ospitato dal tuo provider di identità SAML.</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>Il nome globalmente univoco per un provider di identità SAML.</td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>Il nome che assegni alla tua configurazione SAML.</td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>Il certificato emesso dal tuo provider di identità SAML. È utilizzato per firmare e convalidare le asserzioni SAML. Tutti i provider sono diversi, ma potresti essere in grado di scaricare il certificato di firma dal tuo provider di identità. Il certificato deve essere in formato <code>.pem</code>.</td>
    </tr>
    <tr>
      <td>Facoltativo: <code>secondary-certificate-example-pem-format</code></td>
      <td>Il certificato di backup emesso dal tuo provider di identità SAML. Viene utilizzato se la convalida della firma non riesce con il certificato primario. <strong>Nota</strong>: se la chiave di firma rimane la stessa, {{site.data.keyword.appid_short_notm}} non blocca l'autenticazione per i certificati scaduti.</td>
    </tr>
    <tr>
      <td>Facoltativo: <code>authnContext</code></td>
      <td>Il contesto di autenticazione viene utilizzato per verificare la qualità dell'autenticazione e delle asserzioni SAML. Puoi aggiungere un contesto di autenticazione aggiungendo un array di classi e una stringa di confronto al tuo codice. Assicurati di aggiornare entrambi i parametri <code>class</code> e <code>comparison</code> con i tuoi valori. Ad esempio, un parametro <code>class</code> può essere simile a <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code>.</td>
    </tr>
  </table>

3. Effettua una richiesta PUT all'endpoint API [`/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) per fornire la configurazione creata nel passo 2 a {{site.data.keyword.appid_short_notm}}. Consulta il seguente esempio per vedere a cosa può somigliare la tua richiesta.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
      ],
      "displayName": "my saml example",
    }
  }
  ```
  {: screen}



## Verifica della configurazione
{: #saml-testing}

Puoi verificare la configurazione tra il tuo provider di identità SAML e {{site.data.keyword.appid_short_notm}}.

1. Assicurati di aver salvato la tua configurazione.
2. Passa alla scheda **SAML 2.0** del dashboard {{site.data.keyword.appid_short_notm}} e fai clic su **Test**. Si apre una nuova scheda.
3. Accedi con un utente che il tuo provider di identità ha già autenticato.
4. Dopo aver completato il modulo, verrai reindirizzato a un'altra pagina.
  * Autenticazione riuscita: la connessione tra {{site.data.keyword.appid_short_notm}} e il provider di identità funziona correttamente. La pagina visualizza [token di accesso e identità](/docs/services/appid?topic=appid-tokens#tokens) validi.
  * Autenticazione non riuscita: la connessione viene interrotta. La pagina visualizza gli errori e il file XML di risposta SAML.


Stai avendo dei problemi? Consulta [Risoluzione dei problemi: SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}




## FAQ di SAML
{: #saml-assertions}

Le asserzioni SAML possono essere restituite in diversi modi. Consulta i seguenti esempi per vedere il modo in cui {{site.data.keyword.appid_short_notm}} si attende venga formattata la risposta.
{: shortdesc}


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

