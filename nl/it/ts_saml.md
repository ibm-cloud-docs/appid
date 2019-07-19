---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, development, troubleshooting, redirected, validation

subcollection: appid

---

{:external: target="_blank" .external}
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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Risoluzione dei problemi: SAML
{: #troubleshooting-idp}

Se hai dei problemi durante la configurazione di SAML da utilizzare con {{site.data.keyword.appid_full}}, considera queste tecniche per la risoluzione dei problemi e per ottenere assistenza.
{: shortdesc}


## Problemi comuni relativi alla configurazione
{: #ts-common-saml}

Il framework SAML supporta più profili, flussi e configurazioni, il che significa che è essenziale che la tua configurazione del provider di identità sia eseguita corretta. Consulta i seguenti argomenti per risolvere alcuni dei problemi comuni che potresti riscontrare quando utilizzi SAML.
{: shortdesc}


Per messaggi e codici di errore specifici dal tuo provider di identità che non vedi in questa pagina, può essere utile cercare la [specifica SAML](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html) per spiegazioni dettagliate. Se non trovi cosa stai cercando, puoi contattare l'amministratore dei tuoi provider di identità per ulteriori informazioni.
{: note}



### Manca il parametro `RelayState`
{: #ts-saml-relaystate}

**Cosa sta succedendo**

Il parametro `RelayState` manca dalla tua risposta di autenticazione.


**Perché sta succedendo**

{{site.data.keyword.appid_short_notm}} invia un parametro opaco noto come `RelayState` come parte della richiesta di autenticazione. Se non vedi il parametro nella tua risposta, il tuo provider di identità potrebbe non essere configurato per restituirlo correttamente. `RelayState` ha il seguente formato.

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

**Come porvi rimedio**

Verifica che il tuo provider SAML sia configurato per restituire il parametro `RelayState` a {{site.data.keyword.appid_short_notm}} senza modificarlo in alcun modo.


### L'ID nome manca o non è corretto
{: #ts-saml-nameid}

**Cosa sta succedendo**

Quando invii una richiesta di autenticazione, ricevi un errore relativo a `NameID`.

**Perché sta succedendo**

{{site.data.keyword.appid_short_notm}}, come provider di servizi, definisce il modo in cui vengono identificati gli utenti dal servizio e dal provider di identità. Con {{site.data.keyword.appid_short_notm}}, gli utenti vengono identificati nella richiesta di autenticazione `NameID` nel campo `NameID` come mostrato nel seguente esempio.

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**Come porvi rimedio**

Per risolvere il problema, assicurati che il tuo provider di identità `NameID` sia formattato come un indirizzo email. Verifica che tutti gli utenti nel tuo registro del provider di identità abbiano un formato di indirizzo email valido. Quindi, verifica che il campo `NameID` sia definito in modo appropriato in modo che venga restituita sempre un'email valida - anche se gli utenti nel tuo registro hanno più email.



### Errore di firma della risposta
{: #ts-saml-response-sign-fail}

**Cosa sta succedendo**

Quando invii una richiesta di autenticazione, ricevi il seguente messaggio di errore: 

```
Could not verify SAML assertion signature. Ensure {{site.data.keyword.appid_short_notm}} is configurated with your SAML provider's signing certificate.
```
{: screen}

**Perché sta succedendo**

{{site.data.keyword.appid_short_notm}} si attende che tutte le asserzioni SAML nella tua risposta siano firmate. Se il servizio non può trovare o verificare la firma nella risposta, viene restituito l'errore.

**Come porvi rimedio**

Per risolvere il problema, assicurati che:

* Hai estratto il certificato di firma dal tuo file XML di metadati dei provider di identità. Assicurati di utilizzare la chiave con `<KeyDescriptor use="signing">`.
* Hai impostato l'algoritmo di firma della risposta su XXX. 





### Errore di decrittografia della risposta
{: #ts-saml-decrypt-fail}

**Cosa sta succedendo**

Ricevi uno dei seguenti messaggi di errore in risposta alla tua richiesta di autenticazione.

Messaggio di errore 1:

```
Unexpectedly received an encrypted assertion. Please enable response encryption in your {{site.data.keyword.appid_short_notm}} SAML configuration.
```
{: screen}

Messaggio di errore 2: 

```
Could not decrypt SAML assertion. Ensure your SAML provider is configured with the {{site.data.keyword.appid_short_notm}} encryption.
```
{: screen}


**Perché sta succedendo**

Se il tuo provider di identità è configurato per la crittografia, {{site.data.keyword.appid_short_notm}} deve essere configurato per firmare le richieste di autenticazione SAML (AuthnRequest). Quindi, il tuo provider di identità deve essere configurato per attendersi la configurazione corrispondente. Potresti ricevere questi errori per uno dei seguenti motivi:

- {{site.data.keyword.appid_short_notm}} non è configurato per aspettarsi che la risposta SAML del provider di identità sia crittografata.
- {{site.data.keyword.appid_short_notm}} non può decrittografare correttamente le tue asserzioni.


**Come porvi rimedio**

Se ricevi il messaggio di errore 1, verifica che la tua configurazione SAML sia configurata per aspettarsi una risposta crittografata. Per impostazione predefinita, {{site.data.keyword.appid_short_notm}} non si aspetta che la risposta sia crittografata. Per configurare la crittografia, imposta il parametro `encryptResponse` su **true** utilizzando [l'API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

Se ricevi il messaggio di errore 2, assicurati che il tuo certificato sia corretto. Puoi ottenere il certificato di firma dal file XML di metadati {{site.data.keyword.appid_short_notm}}. Assicurati di utilizzare la chiave con `<KeyDescriptor use="signing">`. Verifica che il tuo provider di identità sia configurato all'utilizzo di `` come algoritmo di firma. 


### Codice di errore del risponditore
{: #ts-saml-responder}

**Cosa sta succedendo**

Quando invii una richiesta di autenticazione, ricevi il seguente messaggio di errore generico:

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**Perché sta succedendo**

Anche se {{site.data.keyword.appid_short_notm}} invia la richiesta di autenticazione iniziale, il provider di identità deve eseguire l'autenticazione utente e restituire la risposta. Esistono diversi motivi che possono causare l'emissione di questo messaggio di errore da parte del tuo provider di identità.

Potresti visualizzare il messaggio se il tuo provider di identità: 

* Non riesce a trovare o verificare il nome utente.
* Non supporta il formato `NameID` definito nella richiesta di autenticazione (`AuthnRequest`).
* Non supporta il contesto di autenticazione.
* Richiede che la richiesta di autenticazione sia firmata o utilizzi un algoritmo specifico nella firma.

**Come porvi rimedio**

Per risolvere il problema, verifica la tua configurazione e il tuo nome utente. Verifica di aver definito le variabili e il contesto di autenticazione corretti. Controlla se la tua richiesta deve essere firmata in un modo specifico.




### Richiesta di autenticazione non supportata
{: #ts-saml-unsupported-request}

**Cosa sta succedendo**

Ricevi un messaggio relativo a una richiesta di autenticazione non supportata.

**Perché sta succedendo**

Quando {{site.data.keyword.appid_short_notm}} genera una richiesta di autenticazione, può utilizzare il contesto di autenticazione per richiedere la qualità dell'autenticazione e delle asserzioni SAML.

**Come porvi rimedio**

Per risolvere il problema, puoi aggiornare il tuo contesto di autenticazione. Per impostazione predefinita, {{site.data.keyword.appid_short_notm}} utilizza la classe di autenticazione `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` e il confronto `exact`. Puoi aggiornare il parametro di contesto per adattarsi al tuo caso di utilizzo utilizzando le API.




### Errore di firma della richiesta SAML
{: #ts-saml-request-sign-fail}

**Cosa sta succedendo**

Ricevi un errore che indica che una richiesta di autenticazione non può essere verificata.

**Perché sta succedendo**

{{site.data.keyword.appid_short_notm}} può essere configurato per firmare la richiesta di autenticazione SAML (`AuthNRequest`), ma il tuo provider di identità deve essere configurato per attendersi la configurazione corrispondente.

**Come porvi rimedio**

Per risolvere il problema:

* Verifica che {{site.data.keyword.cloud_notm}} sia configurato per firmare la richiesta di autenticazione impostando il parametro `signRequest` su `true` utilizzando l'[API set SAML IdP](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp). Puoi controllare se la tua richiesta di autenticazione sia firmata controllando l'URL della richiesta. La firma è inclusa come un parametro di query. Ad esempio: `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* Verifica che il tuo provider di identità sia configurato con il certificato corretto. Per ottenere il certificato di firma controlla il file XML di metadati {{site.data.keyword.cloud_notm}} che hai scaricato dal dashboard {{site.data.keyword.cloud_notm}}. Assicurati di utilizzare la chiave con `<KeyDescriptor use="signing">`.

* Verifica che il tuo provider di identità sia configurato all'utilizzo di `` come algoritmo di firma.



## Debug della tua connessione
{: #ts-saml-debug-connection}

La tua configurazione è corretta ma hai ancora un bug? Consulta alcuni dei seguenti suggerimenti utili per il debug della tua connessione SAML.
{: shortdesc}


### Come acquisisco la mia risposta e la mia richiesta di autenticazione SAML?
{: #ts-saml-capture}

Esistono diverse opzioni per i plugin dei browser come [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) e [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) che possono essere utilizzate per acquisire le tue risposte e richieste SAML. Non vuoi utilizzare un plugin? Nessun problema. Atlassian fornisce le istruzioni per un [approccio di estrazione più manuale](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html).


### Non comprendo i messaggi. Come posso decodificarli?
{: #ts-saml-decode-messages}

Se ancora hai dei problemi dopo l'utilizzo del tuo strumento di debug SAML, prova ad utilizzare gli [strumenti per sviluppatori SAML](https://www.samltool.com/online_tools.php) per un ulteriore aiuto nella decodifica dei tuoi messaggi. Importante! A seconda di dove intercetti i tuoi messaggi SAML, la tua richiesta potrebbe essere [codificata URL](https://www.samltool.com/online_tools.php), [compressa e decodificata base 64](https://www.samltool.com/decode.php) o [crittografata](https://www.samltool.com/decrypt.php).

Non utilizzare gli strumenti online per la decrittografia dei messaggi SAML come la tua risposta SAML. Gli strumenti hanno bisogno di accedere alla chiave privata di crittografia per poter decrittografare le informazioni. La chiave dovrebbe essere mantenuta privata e l'accesso controllato. Lo strumento di decrittografia menzionato in questa sezione dovrebbe essere utilizzato solo per scopi di debug.
{: important}

