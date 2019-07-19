---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-09"

keywords: authentication, authorization, identity, app security, secure, development, two factor, mfa 

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


# Autenticazione multifattore (MFA, multi-factor authentication)
{: #cd-mfa}


Richiedendo più fattori durante l'accesso, puoi aumentare la sicurezza dell'autenticazione utente alle tue applicazioni. Con Cloud Directory per {{site.data.keyword.appid_full}}, il primo fattore è la password dell'utente Cloud Foundry, di cui fa normalmente uso per eseguire l'accesso. Il secondo fattore di autenticazione è un codice monouso che {{site.data.keyword.appid_short_notm}} invia all'utente come un SMS o per email. {{site.data.keyword.appid_short_notm}} utilizza una combinazione di entrambi i fattori per verificare l'identità di un utente.
{: shortdesc}

La MFA {{site.data.keyword.appid_short_notm}} è supportata come parte del flusso del codice di autorizzazione OAuth 2.0 per gli utenti Cloud Directory mediante il Widget di accesso. Se stai utilizzando l'accesso aziendale con SAML 2.0 oppure l'accesso social, puoi abilitare la MFA mediante tale provider di identità.
{: note}

Quando la MFA è abilitata, il Widget di accesso {{site.data.keyword.appid_short_notm}} richiede una seconda forma di verifica (secondo fattore di autenticazione) ogni volta che un utente prova ad eseguire l'accesso. Dopo che un utente ha immesso correttamente le sue credenziali, gli viene inviato un codice monouso all'indirizzo email o al numero di telefono registrato nel suo account.

Consulta il seguente diagramma per vedere come funziona il flusso MFA.

![Flusso MFA](images/mfa.png)

1. A un utente viene presentato il Widget di accesso di {{site.data.keyword.appid_short_notm}} e immette le sue credenziali utente di Cloud Directory. Le credenziali possono essere il suo indirizzo email oppure il suo nome utente e la sua password. Le credenziali dell'utente di Cloud Directory rappresentano il primo fattore di autenticazione.

2. Le credenziali vengono convalidate e viene restituita la schermata MFA per la verifica del secondo fattore. In base alla configurazione del secondo fattore, l'utente riceve una email oppure un SMS con un codice monouso e lo immette nella schermata di verifica.

3. Se il codice MFA viene convalidato, l'utente viene reindirizzato nuovamente all'applicazione ed esegue l'accesso.


## Descrizione della MFA
{: #cd-mfa-understanding}


La MFA è un metodo per confermare l'identità di un utente richiedendogli di utilizzare più fattori per provare che è chi afferma di essere. Questi fattori possono essere qualcosa che hanno in aggiunta a qualcosa che conoscono o a qualcosa che sono.
{: shortdesc}

La prima volta che viene abilitata, la MFA è configurata per utilizzare l'email per impostazione predefinita. Puoi modificare l'impostazione per utilizzare un SMS ma non puoi configurare entrambi contemporaneamente. Sia per l'email che per gli SMS, ci sono alcune impostazioni che sono configurate per tuo conto e non possono essere modificate.


<table>
  <tr>
    <th>Impostazione</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td>Caratteri codice</td>
    <td>Sei caratteri numerici</td>
  </tr>
  <tr>
    <td>Scadenza del codice</td>
    <td>Quindici minuti <br> Se un utente non convalida il suo codice entro 15 minuti, può richiedere l'invio di un altro codice a condizione che la sessione di autenticazione non sia scaduta. Entro la sessione di autenticazione, il codice può essere inviato più volte. Quando la sessione di autenticazione scade, l'utente deve ripetere il processo di accesso dall'inizio.</td>
  </tr>
</table>

<p>Definito in SCIM come un <a href="https://tools.ietf.org/html/rfc7643#section-2.4" target="_blank">attributo a più valori <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>, l'email o il numero di telefono di un utente Cloud Directory può contenere quanto segue:
<ul>
  <li>value: il valore dell'attributo effettivo, come ad esempio un indirizzo email o un numero di telefono.</li>
  <li>primary: un valore booleano che indica il valore predefinito per l'attributo. Il valore di attributo primario <code>true</code> può ricorrere una sola volta. Se non viene specificato, si presume che il valore di <code>primary</code> sia <code>false</code>.</li>
</ul>Per ulteriori informazioni, consulta la [documentazione di Cloud Directory](/docs/services/appid?topic=appid-cloud-directory#cloud-directory).</p>



## Configurazione del canale email della MFA
{: #cd-mfa-configure-email}

Puoi configurare {{site.data.keyword.appid_short_notm}} per inviare il codice della MFA ai tuoi utenti tramite email.
{: shortdesc} 

Quando abiliti la MFA per la prima volta, possono verificarsi queste due cose:

- Per impostazione predefinita, viene selezionato il canale email. Puoi passare al [canale SMS](/docs/services/appid?topic=appid-cd-mfa#cd-mfa-configure-sms).
- {{site.data.keyword.appid_short_notm}} registra automaticamente l'email primaria collegata al tuo profilo utente di Cloud Directory.

Se l'email di un utente non è già confermata, tramite le [API di gestione](https://us-south.appid.cloud.ibm.com/swagger-ui/#/) o tramite la verifica dell'email quando esegue la registrazione, ne viene eseguita la conferma quando esegue correttamente la verifica di un codice MFA.

Prima di iniziare, assicurati che la tua istanza di {{site.data.keyword.appid_short_notm}} sia nel [piano di prezzi a livello graduale](/docs/services/appid?topic=appid-faq#faq-pricing).
{: note}

### Con la GUI
{: #cd-mfa-configure-email-gui}

Puoi configurare il canale email della MFA attraverso la GUI.

1. Passa alla scheda **Cloud Directory > Multi-factor authentication** del dashboard {{site.data.keyword.appid_short_notm}}.

2. Nella casella **Enable multi-factor authentication**, nella **scheda delle impostazioni**, passa MFA a **Enabled**. Riconosci che comprendi che la MFA comporta un addebito come un [evento di sicurezza avanzata](/docs/services/appid?topic=appid-faq#faq-pricing). Per impostazione predefinita, **Email** è selezionato come metodo di autenticazione (**Authentication method**).

3. Nella scheda **Email channel**, esamina **Email template**. Puoi scegliere di inviare il template con il testo fornito oppure di scrivere un tuo messaggio. Assicurati di utilizzare le tag HTML corrette. Nella GUI, puoi aggiungere i parametri e inserire le immagini. Per modificare la [lingua](/docs/services/appid?topic=appid-cd-messages#cd-languages) del messaggio, puoi utilizzare <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">le API <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per impostare la lingua. Sei tuttavia responsabile del contenuto e della traduzione del messaggio. Consulta la seguente tabella per vedere l'elenco di tabelle che puoi utilizzare in questo messaggio e tutti gli altri messaggi che puoi inviare. Se un utente non fornisce le informazioni estratte dal parametro, questi campi saranno vuoti.

  <table>
    <thead>
      <tr>
        <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Parametri dei messaggi della MFA</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>%{display.logo}</code></td>
        <td> Visualizza l'immagine che hai configurato per il tuo Widget di accesso. </td>
      </tr>
      <tr>
        <td><code>%{user.displayName}</code></td>
        <td> Visualizza il nome della schermata che un utente ha scelto di utilizzare durante l'interazione con l'applicazione. </td>
      </tr>
      <tr>
        <td><code>%{user.email}</code></td>
        <td> Visualizza l'indirizzo email registrato dell'utente. </td>
      </tr>
      <tr>
        <td><code>%{user.username}</code></td>
        <td> Visualizza il nome utente specificato dall'utente quando il metodo di autenticazione è impostato su nome utente e password. </td>
      </tr>
      <tr>
        <td><code>%{user.firstName}</code></td>
        <td> Visualizza il nome specificato dall'utente. </td>
      </tr>
      <tr>
        <td><code>%{user.formattedName}</code></td>
        <td> Visualizza il nome completo dell'utente. </td>
      </tr>
      <tr>
        <td><code>%{user.lastName}</code></td>
        <td> Visualizza il cognome specificato dall'utente. </td>
      </tr>
      <tr>
        <td><code>%{mfa.code}</code></td>
        <td> Visualizza il codice di verifica MFA monouso. </td>
      </tr>
    </tbody>
  </table>

  Se un utente non fornisce le informazioni estratte dal parametro, questi campi saranno vuoti.
  {: tip}


### Con le API
{: #cd-mfa-configure-email-apis}

**Prima di cominciare**

Assicurati di aver i seguenti prerequisiti:

* L'ID tenant della tua istanza {{site.data.keyword.appid_short_notm}}. Questo ID può essere trovato nella sezione **Service Credentials** del dashboard.
* Il tuo token IAM (Identity and Access Management). Per un aiuto nell'ottenimento del token IAM, consulta la [Documentazione IAM](/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey).


1. Abilita la MFA, effettuando una richiesta PUT all'endpoint `/config/mfa` con la tua configurazione MFA per impostare `isActive` su `true`.

  Intestazione:
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: codeblock}

  Corpo:
  ```
   {
       "isActive": true
   }
  ```
  {: codeblock}

  Richiesta di esempio:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. Abilita il tuo canale MFA effettuando una richiesta PUT all'endpoint `/mfa/channels/{channel}` con la tua configurazione MFA. Quando `isActive` è impostato su `true`, il tuo canale MFA è abilitato.

  Intestazione:
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channel}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: codeblock}

  Corpo:
  ```
   {
       "isActive": true
   }
  ```
  {: codeblock}

  Richiesta di esempio:

  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/mfa/channels/email'
  ```
  {: screen}

Se la tua istanza {{site.data.keyword.appid_short_notm}} Cloud Directory è configurata per operare con un dispatcher di email personalizzato, la MFA utilizza lo stesso dispatcher per inviare il codice monouso. Per ulteriori informazioni sulla configurazione di un dispatcher personalizzato, consulta la documentazione di [Cloud Directory](/docs/services/appid?topic=appid-cd-messages#cd-custom-email).
{: note}




## Configurazione della MFA per operare con SMS
{: #cd-mfa-configure-sms}

Puoi inviare un messaggio SMS ai tuoi utenti come una seconda forma di verifica. Quando abiliti SMS, {{site.data.keyword.appid_short_notm}} prova automaticamente a registrare il primo numero di telefono primario [valido](https://en.wikipedia.org/wiki/E.164) trovato nel profilo di un utente Cloud Directory. Se il numero non è valido o se non viene trovato alcun numero di telefono nel profilo dell'utente, viene visualizzato un widget di registrazione per consentire all'utente di aggiungere un numero. Il numero fa quindi parte del profilo dell'utente e, dopo la convalida, diventa il numero predefinito utilizzato per la MFA.
{: shortdesc}

**Prima di cominciare**

{{site.data.keyword.appid_short_notm}} utilizza [Nexmo](https://www.nexmo.com/products/sms) per inviare codici monouso SMS della MFA. Prima di iniziare, assicurati di disporre di un'istanza di {{site.data.keyword.appid_short_notm}} che sia nel [piano dei prezzi a livello graduale](/docs/services/appid?topic=appid-faq#faq-pricing) e delle seguenti informazioni Nexmo.

 - Ottieni il tuo segreto e la tua chiave API Nexmo. Puoi trovare il segreto e la chiave API Nexmo nella pagina delle impostazioni del tuo account nel dashboard Nexmo. Consulta la [documentazione di Nexmo](https://developer.nexmo.com/concepts/guides/authentication#api-key-and-secret) per ulteriori informazioni su come ottenere le tue credenziali.

 - Registra il tuo ID mittente o il numero `from` con Nexmo. Questo numero `from` è quello che appare sul telefono del tuo utente per mostrare da chi proviene l'SMS. In alcuni paesi, Nexmo supporta ID mittente alfanumerici. {{site.data.keyword.appid_short_notm}} utilizza il valore che hai immesso come ID mittente di Nexmo. Quindi, se sono supportati da Nexmo, puoi utilizzare gli ID con {{site.data.keyword.appid_short_notm}}. Per ulteriori informazioni, consulta la [documentazione di Nexmo](https://help.nexmo.com/hc/en-us/articles/217571017-What-is-a-Sender-ID).


### Con la GUI
{: #cd-mfa-configure-sms-gui}

Per configurare la MFA con la GUI, consulta [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory).
{: note}

1. Passa alla scheda **Cloud Directory > Multi-factor authentication** del dashboard {{site.data.keyword.appid_short_notm}}.

2. Nella casella **Enable multi-factor authentication**, nella **scheda delle impostazioni**, passa MFA a **Enabled**. Riconosci che comprendi che la MFA comporta un addebito come un [evento di sicurezza avanzata](/docs/services/appid?topic=appid-faq#faq-pricing).

3. Seleziona **SMS** come tuo metodo di autenticazione (**Authentication method**).

4. Nella scheda **SMS channel**, configura le informazioni sul tuo account Nexmo.

    1. Se non hai già un account con Nexmo, creane uno.

    2. Dal dashboard Nexmo, fai clic su **SMS**.

    3. Nella sezione **Code it yourself**, copia la tua chiave API e incollala nella casella **key** nel dashboard {{site.data.keyword.appid_short_notm}}.

    4. Copia il segreto API (**API Secret**) nel dashboard Nexmo e incollalo nella casella **Secret** nel dashboard {{site.data.keyword.appid_short_notm}}.

    5. Immetti [l'ID](https://help.nexmo.com/hc/en-us/articles/217571017-What-is-a-Sender-ID) da cui vuoi inviare i messaggi. Un formato di numero valido rispetta il [formato della numerazione internazionale E.164](https://en.wikipedia.org/wiki/E.164) Ad esempio, numero degli Stati Uniti ha il formato `+1 999 888 7777 `. Devi specificare sia il prefisso internazionale, che inizia con un simbolo `+`, che il numero dell'abbonato nazionale. In alcuni paesi, Nexmo supporta ID mittente alfanumerici. {{site.data.keyword.appid_short_notm}} utilizza il valore che hai immesso come ID mittente di Nexmo. Quindi, se sono supportati da Nexmo, puoi utilizzare gli ID con {{site.data.keyword.appid_short_notm}}.



### Con le API
{: #cd-mfa-configure-sms-api}

**Prima di cominciare**

Assicurati di aver i seguenti prerequisiti:

* L'ID tenant della tua istanza {{site.data.keyword.appid_short_notm}}. Questo ID può essere trovato nella sezione **Service Credentials** del dashboard.
* Il tuo token IAM (Identity and Access Management). Per un aiuto nell'ottenimento del token IAM, consulta la [Documentazione IAM](/docs/iam?topic=iam-iamtoken_from_apikey).


1. Abilita la MFA, effettuando una richiesta PUT all'endpoint `/config/mfa` con la tua configurazione MFA per impostare `isActive` su `true`.

Intestazione:

  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: codeblock}

Corpo:

  ```
  {
   "isActive": true
   }
  ```
  {: codeblock}


Richiesta di esempio:

  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
    "isActive": true
      }'
  '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. Abilita il tuo canale MFA effettuando una richiesta PUT all'endpoint `/mfa/channels/{channel}` con la tua configurazione MFA. Quando `isActive` è impostato su `true`, il tuo canale MFA è abilitato.
`config` prende il segreto e la chiave API Nexmo e il numero `from`.

Intestazione:

  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channel}
      Host: <management-server-url>
      Authorization: Bearer <IAM_TOKEN>
      Content-Type: application/json
  ```
  {: codeblock}

Corpo:

  ```
  {
      "isActive": true,
      "config": {
        "key": "nexmo key",
        "secret": "nexmo secret",
        "from": sender-phoneNumber
      }
  }
  ```
  {: codeblock}

Richiesta di esempio:

  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
         "isActive": true,
      "config": {
          "key": "key",
          "secret": "secret",
          "from": 12345678900
        }
     }'
   '{management-url}/management/v4/{tenantId}/mfa/channels/nexmo'
  ```
  {: screen}


3. Una volta configurato correttamente il canale, verifica che la tua configurazione e la tua connessione Nexmo siano impostati correttamente utilizzando il pulsante di test nell'IU oppure utilizzando l'API di gestione.

Intestazione:

  ```
  POST /management/v4/{tenantId}/config/cloud_directory/sms_dispatcher/test
     Host: <management-server-url>
     Authorization: Bearer <IAM_TOKEN>
     Content-Type: application/json
  ```
  {: codeblock}

Corpo:

  ```
  {
    "phone_number": "phoneNumber-receives-test-message"
  }
  ```
  {: codeblock}

Richiesta di esempio:

  ```
  $ curl -X POST
  --header 'Content-Type: application/json'
  --header 'Accept: application/json'
  --header 'Authorization: Bearer <IAM_TOKEN>'
  -d '{
        "phone_number": "+1 999 999 9999"
      }'
  '{management-url}/management/v4/{tenantId}/config/cloud_directory/sms_dispatcher/test'
  ```
  {: screen}

  </br>
