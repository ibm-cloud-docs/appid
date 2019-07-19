---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-10"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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

# Personalizzazione delle email
{: #cd-types}

Quando un utente interagisce con la tua applicazione, potresti voler inviare una risposta o chiedere una verifica. {{site.data.keyword.appid_short_notm}} fornisce dei template predefiniti che puoi utilizzare per le interazioni. Puoi anche utilizzare i template come una guida e personalizzare la tua messaggistica per rispondere alle esigenze del tuo marchio.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} utilizza <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> come servizio di recapito email. Tutte le email vengono inviate con un unico account SendGrid.
{: note}

## Template di email
{: #cd-messages}

Quando invii messaggi ai tuoi utenti, puoi utilizzare qualsiasi combinazione dei seguenti template. In alternativa, puoi modificare i template per personalizzare il tuo messaggio.
{: shortdesc}

Oltre ai seguenti tipi di messaggio, puoi anche avvalerti dei template [SSO](/docs/services/appid?topic=appid-cd-sso#cd-sso) e [MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa).
{: tip}

Per un'ulteriore personalizzazione, puoi usare i parametri nei tuoi messaggi. Consulta la seguente tabella per vedere i parametri che puoi utilizzare in tutti i tipi di messaggio.

<table>
  <tr>
    <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Tutti i parametri del messaggio </th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> Visualizza l'immagine che hai configurato per il tuo Widget di accesso.</td>
  </tr>
  <tr>
    <td><code>%{user.displayName}</code></td>
    <td> Visualizza il nome della schermata che un utente ha scelto di utilizzare durante l'interazione con l'applicazione.</td>
  </tr>
  <tr>
    <td><code>%{user.email}</code></td>
    <td> Visualizza l'indirizzo email registrato dell'utente.</td>
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
</table>


### Email: benvenuto
{: #cd-messages-welcome}

Quando un utente si registra per la tua applicazione, potresti volergli inviare un messaggio di benvenuto alla tua applicazione. 
{: shortdesc}

1. Vai alla scheda **Workflow templates > Welcome email** del dashboard del servizio.

2. Imposta **Welcome email** su **Enabled**.

3. Personalizza il contenuto del tuo messaggio. Puoi aggiungere parametri e inserire messaggi utilizzando l'IU. Per modificare la [lingua](/docs/services/appid?topic=appid-cd-messages#cd-languages) del messaggio, puoi utilizzare <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">le API <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per impostare la lingua. Sei tuttavia responsabile del contenuto e della traduzione del messaggio. Consulta la seguente tabella per vedere l'elenco di tabelle che puoi utilizzare in questo messaggio e tutti gli altri messaggi che puoi inviare. Se un utente non fornisce le informazioni estratte dal parametro, questi campi saranno vuoti.

4. Fai clic su **Save**.


### Email: verifica
{: #cd-messages-verification}

Quando un utente si registra per la tua applicazione utilizzando la sua email, puoi inviargli una email che gli chiede di confermare la sua identità. Richiedendo una verifica, limiti il numero di account falsi che possono registrarsi alla tua applicazione. Puoi limitare l'accesso alla tua applicazione finché un utente verifica la propria email o utilizzarla come un modo per gestire per quali utenti crei i profili.
{: shortdesc}

Gli utenti che vengono aggiunti manualmente tramite il dashboard {{site.data.keyword.appid_short_notm}} o l'API utente di creazione non ricevono automaticamente questa email.
{: note}


1. Vai alla scheda **Workflow templates > Email verification** del dashboard del servizio.

2. Imposta **Email verification** su **Enabled**.

3. Imposta **Allow users to sign in to your app without first verifying their email address** su **Yes**. Quando per questa impostazione viene specificato Yes, gli utenti possono interagire con la tua applicazione dopo aver eseguito la registrazione ma prima di verificare il loro indirizzo email. L'impostazione predefinita è no.

4. Personalizza il contenuto del tuo messaggio. Puoi aggiungere parametri e inserire messaggi utilizzando l'IU. Per modificare la [lingua](/docs/services/appid?topic=appid-cd-messages#cd-languages) del messaggio, puoi utilizzare <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">le API <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per impostare la lingua. Sei tuttavia responsabile del contenuto e della traduzione del messaggio. Consulta la seguente tabella per vedere i diversi parametri che puoi utilizzare nel tuo messaggio. Se un utente non fornisce le informazioni estratte dal parametro, questi campi saranno vuoti.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Parametri del messaggio di verifica</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> Visualizza il numero di ore per cui il link è valido. </td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td> Visualizza il numero di minuti per cui il link è valido. </td>
    </tr>
    <tr>
      <td><code>%{verify.code}</code></td>
      <td> Visualizza un URL di verifica monouso. </td>
    </tr>
    <tr>
      <td><code>%{verify.link}</code></td>
      <td> Verifica l'URL di azione che hai specificato nelle impostazioni. </td>
    </tr>
  </table>

  Puoi anche utilizzare i parametri di messaggio elencati nella sezione [Messaggio di benvenuto](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

5. Definisci un tempo di scadenza per l'URL dell'azione. La scadenza dell'URL è la quantità di tempo, in minuti, entro cui l'utente deve completare l'azione prima che il link di verifica scada. Questa impostazione influenza anche la quantità di tempo per cui il tuo link di reimpostazione della password è valido.
 
6. Immetti un URL per la pagina che vuoi visualizzare dopo che un utente ha eseguito la verifica della sua email nella casella **Thank you page URL**. Se scegli di lasciare vuoto questo campo, viene visualizzata una pagina predefinita {{site.data.keyword.appid_short_notm}}.

7. Fai clic su **Save**. 


### Email: reimposta password
{: #cd-messages-reset}

Quando un utente interagisce con la tua applicazione, potrebbe dimenticare la sua password o dovere aggiornarla. Puoi personalizzare la risposta dell'email alla loro richiesta. Quando un utente richiede una modifica della sua password, la password rimane invariata finché non fa clic sul link in questa email.
{: shortdesc}


1. Vai alla scheda **Workflow templates > Reset password** del dashboard del servizio.

2. Imposta **Forgot password email** su **Enabled**.

3. Personalizza il contenuto del tuo messaggio. Puoi aggiungere parametri e inserire messaggi utilizzando l'IU. Per modificare la [lingua](/docs/services/appid?topic=appid-cd-messages#cd-languages) del messaggio, puoi utilizzare <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">le API <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per impostare la lingua. Sei tuttavia responsabile del contenuto e della traduzione del messaggio. Consulta la seguente tabella per vedere i diversi parametri che puoi utilizzare nel tuo messaggio. Se un utente non fornisce le informazioni estratte dal parametro, questi campi saranno vuoti.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Parametri della password dimenticata</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> Visualizza il numero di ore per cui il link è valido.</td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td>Visualizza il numero di minuti per cui il link è valido.</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.code}</code></td>
      <td> Visualizza il passcode monouso come parte dell'URL. Ciò significa che ogni persona ha un codice diverso. Esempio: `https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478`</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> Visualizza il link su cui può fare clic un utente per reimpostare la propria password.</td>
    </tr>
  </table>

  Puoi anche utilizzare i parametri di messaggio elencati nella sezione [Messaggio di benvenuto](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

4. Definisci un tempo di scadenza per l'URL dell'azione. La scadenza dell'URL è la quantità di tempo, in minuti, entro cui l'utente deve completare l'azione prima che il link di verifica scada. Questa impostazione influenza anche la quantità di tempo per cui il tuo link di reimpostazione della password è valido.
 
5. Immetti un URL per la pagina che vuoi visualizzare dopo che un utente ha eseguito la verifica della sua email nella casella **Reset password page URL**. Se scegli di lasciare vuoto questo campo, viene visualizzata una pagina predefinita {{site.data.keyword.appid_short_notm}}.

6. Fai clic su **Save**.


### Email: modifica della password
{: #cd-messages-password-change}

Puoi inviare una notifica a un utente quando la sua password viene aggiornata. La notifica può essere utile nel caso in cui l'utente non abbia richiesto una modifica della sua password. Gli utenti possono prendere le misure appropriate per riproteggere i propri account.
{: shortdesc}

1. Vai alla scheda **Workflow templates > Password change** del dashboard del servizio.

2. Imposta **Password changed email** su **Enabled**.

3. Personalizza il contenuto del tuo messaggio. Puoi aggiungere parametri e inserire messaggi utilizzando l'IU. Per modificare la [lingua](/docs/services/appid?topic=appid-cd-messages#cd-languages) del messaggio, puoi utilizzare <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">le API <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per impostare la lingua. Sei tuttavia responsabile del contenuto e della traduzione del messaggio. Consulta la seguente tabella per vedere i diversi parametri che puoi utilizzare nel tuo messaggio. Se un utente non fornisce le informazioni estratte dal parametro, questi campi saranno vuoti.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Parametri di modifica della password</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> Visualizza l'ora in cui una nuova password entra in vigore. </td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> Visualizza l'indirizzo IP da cui è stata richiesta la modifica della password. </td>
    </tr>
  </table>

  Puoi anche utilizzare i parametri di messaggio elencati nella sezione [Messaggio di benvenuto](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

4. Fai clic su **Save**.




## Utilizzo di un mittente email personalizzato
{: #cd-custom-email}

Con {{site.data.keyword.appid_short_notm}}, puoi definire un punto di estensione personalizzato per inviare i tuoi messaggi email Cloud Directory. Definendo un punto di estensione, hai il controllo completo su come vengono inviate le email e puoi utilizzare il tuo nome di dominio. Per impostazione predefinita, {{site.data.keyword.appid_short_notm}} utilizza <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> come un servizio di recapito email.
 {: shortdesc}

Potresti voler utilizzare un mittente email personalizzato per i seguenti motivi:

- **Dominio personalizzato**
Configurando un dispatcher email personalizzato, hai il controllo completo su come vengono inviati i messaggi email. In particolare, puoi personalizzare il dominio email, il che può ridurre le possibilità di una email filtrata come posta indesiderata. Puoi anche migliorare ulteriormente l'esperienza personalizzata per i tuoi utenti dell'applicazione.

- **Informazioni approfondite e risoluzione dei problemi**
Ottieni delle informazioni approfondite dal tuo provider email, come ad esempio: il numero di persone che ha aperto le email o a cui i messaggi non sono stati recapitati. Poiché puoi tenere traccia di messaggi individuali e visualizzare le statistiche generali, questo può essere utile a risolvere dei problemi.

Dopo aver configurato il punto di estensione, viene richiamato da {{site.data.keyword.appid_short_notm}} ogni volta che un messaggio email deve essere inviato. Il punto di estensione contiene tutte le informazioni sul messaggio, incluso il contenuto finale del corpo dell'email.



### Configurazione del mittente personalizzato
{: #cd-messages-configure-custom-sender}

Per configurare il tuo mittente email personalizzato, devi utilizzare la <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher" target="_blank">Management API</a> di Cloud Directory.


1. Fornisci l'URL. Inoltre puoi fornire le informazioni sull'autorizzazione. I tipi di autorizzazione supportati sono: `Basic authorization` o `constant authorization header value`.

  Esempi di configurazione validi:
  ```
  {
    "custom": {
      "url": "https://example.com/send_mail"
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "basic",
        "username": "username",
        "password": "password"
      }
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "value",
        "value": "myApiKey"
      }
    }
  }
  ```
  {: screen}

2. Configura un punto di estensione che possa ascoltare la richiesta post. Questo endpoint dovrebbe essere in grado di leggere il payload proveniente da {{site.data.keyword.appid_short_notm}} e di inviare l'email con il tuo mittente email personalizzato.

3. Il corpo inviato da {{site.data.keyword.appid_short_notm}} è nel seguente formato: `{"jws": "jws-format-string"}`. Dopo aver decodificato e verificato il payload, il contenuto è una stringa JSON.

  ```
  {
    "tenant": "tenant-id",
      "iss" : "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "iat": 1539173126,
      "jti": "uniq-id",
      "message": {
        "to": "your@mail.com",
          "from": {
            "name": "My Awesome Service",
              "address": "no-reply@company.com"
        },
          "replyTo": {
            "name": "My Awesome Service",
              "address": "yes-reply@company.com"
        },
          "subject": "Welcome to My Awesome Service",
          "body": "<p>Hello<p><br/><p>Thanks for signing up John Doe</p>"
    }
  }
  ```
  {: screen}

  <table>
    <tr>
      <th>Variabile</th>
      <th>Descrizione</th>
    </tr>
    <tr>
      <td><code>tenant</code></td>
      <td>L'ID tenant della tua istanza {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code> iat </code></td>
      <td>La data/ora di quando è stato inviato il messaggio.</td>
    </tr>
    <tr>
      <td><code>iss</code></td>
      <td>L'applicazione o l'istanza {{site.data.keyword.appid_short_notm}} che ha emesso il token JWS.</td>
    </tr>
    <tr>
      <td><code>jti</code></td>
      <td>L'ID transazione univoco.</td>
    </tr>
    <tr>
      <td><code>message: to</code></td>
      <td>L'indirizzo email del destinatario del messaggio.</td>
    </tr>
    <tr>
      <td><code>message: from</code> </br><code>name</code> </br><code>address</code></td>
      <td></br>Il nome del mittente del messaggio.</br>L'indirizzo email del mittente.</td>
    </tr>
    <tr>
      <td><code>Optional: message: reply to</code></br><code>name</code></br><code>address</code></td>
      <td></br>Il nome che è collegato all'indirizzo email di risposta.</br>L'indirizzo email a cui un utente può rispondere.</td>
    </tr>
  </table>

  Puoi verificare che la tua richiesta ha avuto esito positivo controllando il codice di stato della risposta. Qualsiasi valore compreso nell'intervallo 200 - 299 viene considerato un esito positivo. Se ricevi una qualsiasi altra risposta, riprova ad eseguire la tua richiesta
  {: tip}

4. Ogni payload HTTP inviato da {{site.data.keyword.appid_short_notm}} viene automaticamente firmato in base allo standard JWS utilizzando una coppia di chiavi asimmetriche.
Per ogni istanza {{site.data.keyword.appid_short_notm}}, viene generata una chiave pubblica e una privata che non vengono condivise con le altre istanze. La chiave privata viene utilizzata per firmare il payload HTTP e puoi utilizzare la chiave pubblica per verificare che payload sia generato da {{site.data.keyword.appid_short_notm}} e non sia stato modificato da terze parti, <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys" target="_blank">Endpoint chiavi pubbliche</a>.

5. Codice di esempio per il punto di estensione (JavaScript)
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// Your {{site.data.keyword.appid_short_notm}} instance tenant ID
  	const tenantId = '<TENANT-ID>';

  	// Send request to {{site.data.keyword.appid_short_notm}}'s public keys endpoint
  	const keysOptions = {
  		method: 'GET',
  		url: `https://<REGION>.appid.cloud.ibm.com/oauth/v4/${tenantId}/publickeys`
  	};
  	const keysResponse = await request(keysOptions);
  	return JSON.parse(keysResponse.body).keys;
  }

  async function verifySignature(keysArray, kid, jws) {
  	const keyJson = keysArray.find(key => key.kid === kid);
  	if (keyJson) {
  		const pem = jwkToPem(keyJson);
  		await jwtVerify(jws, pem);
  		return;
  	}
  	throw new Error ("Unable to verify signature");
  }

  async function verifyAndSendMail(jws) {
  	// The API key for Sendgrid
  	const sgApiKey = '<SENDGRID-API-KEY>';

  	// Init Sendgrind
  	sgMail.setApiKey(sgApiKey);

  	// Decode message to get information
  	const data = jwtDecode(jws, {complete: true});

  	// Extract kid from header
  	const kid = data.header.kid;

  	const keysArray = await obtainPublicKeys();

  	// Verify the signature of the payload with the public keys
  	await verifySignature(keysArray, kid ,jws);

  	// Send the email with Your Sendgrid account
  	const message = data.payload.message;
  	const msg = {
  		to: message.to,
  		from: message.from.address,
  		subject: message.subject,
  		html: message.body,
  	};
  	console.log(`Sending email to ${message.to}`);
  	let sendgridResponse = await sgMail.send(msg);

  	return {result : 'email_sent',sendgridResponse};
  }
  ```
  {: screen}

6. Verifica che la tua configurazione sia impostata correttamente verificando il tuo dispatcher email. Utilizza l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">API di test</a> per attivare una richiesta al tuo mittente email personalizzato configurato.

Per un esempio funzionante completo, consulta <a href="https://www.ibm.com/cloud/blog/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users" target="_blank">Use your own provider for mail that is sent with {{site.data.keyword.appid_full}}</a>.



## Lingue supportate
{: #cd-languages}

Puoi utilizzare <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">le API di gestione della lingua <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per configurare la lingua in cui può essere scritta la comunicazione del tuo utente. Tuttavia per impostazione predefinita è disponibile solo l'inglese. Sei responsabile della traduzione dei messaggi. Dopo aver impostato la configurazione con l'API, la GUI viene aggiornata in modo che puoi modificare il testo del modello.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Codice</th>
    <th>Lingua</th>
    <th>Regione</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>Afrikaans</td>
    <td>Sudafrica</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>Albanese</td>
    <td>Albania</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>Amarico</td>
    <td>Etiopia</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>Arabo</td>
    <td>Algeria</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>Arabo</td>
    <td>Bahrain</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>Arabo</td>
    <td>Egitto</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>Arabo</td>
    <td>Iraq</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>Arabo</td>
    <td>Giordania</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>Arabo</td>
    <td>Kuwait</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>Arabo</td>
    <td>Libano</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>Arabo</td>
    <td>Libia</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>Arabo</td>
    <td>Mauritania</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>Arabo</td>
    <td>Marocco</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>Arabo</td>
    <td>Oman</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>Arabo</td>
    <td>Qatar</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>Arabo</td>
    <td>Arabia Saudita</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>Arabo</td>
    <td>Siria</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Arabo</td>
    <td>Tunisia</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>Arabo</td>
    <td>Emirati Arabi Uniti</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Arabo</td>
    <td>Yemen</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>Armeno</td>
    <td>Armenia</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>Assamese</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>Azero</td>
    <td>Azerbaijan</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>Basco</td>
    <td>Spagna</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Bielorusso</td>
    <td>Bielorussia</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengalese</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Bielorusso</td>
    <td>Bielorussia</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengalese</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>Bengalese</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>Bosniaco</td>
    <td>Bosnia</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>Bulgaro</td>
    <td>Bulgaria</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>Birmano</td>
    <td>Myanmar</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>Catalano</td>
    <td>Spagna</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>Cinese semplificato</td>
    <td>Cina</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>Cinese semplificato</td>
    <td>Singapore</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>Cinese tradizionale</td>
    <td>Hong Kong R.A.S. della Cina</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>Cinese tradizionale</td>
    <td>Macao (S.A.R.) della Repubblica Popolare Cinese</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>Cinese tradizionale</td>
    <td>Taiwan</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>Croato</td>
    <td>Croazia</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>Ceco</td>
    <td>Repubblica ceca</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>Danese</td>
    <td>Danimarca</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>Olandese</td>
    <td>Belgio</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>Olandese</td>
    <td>Paesi Bassi</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>Inglese</td>
    <td>Australia</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>Inglese</td>
    <td>Belgio</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>Inglese</td>
    <td>Camerun</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>Inglese</td>
    <td>Canada</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>Inglese</td>
    <td>Ghana</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>Inglese</td>
    <td>Hong Kong R.A.S. della Cina</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>Inglese</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>Inglese</td>
    <td>Irlanda</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>Inglese</td>
    <td>Kenya</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>Inglese</td>
    <td>Mauritius</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>Inglese</td>
    <td>Nuova Zelanda</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>Inglese</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>Inglese</td>
    <td>Filippine</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>Inglese</td>
    <td>Singapore</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>Inglese</td>
    <td>Sudafrica</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>Inglese</td>
    <td>Tanzania</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>Inglese</td>
    <td>Regno Unito</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>Inglese</td>
    <td>Stati uniti</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>Inglese</td>
    <td>Zambia</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>Inglese</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>Estone</td>
    <td>Estonia</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>Filippino</td>
    <td>Filippine</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>Finlandese</td>
    <td>Finlandia</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>Francese</td>
    <td>Algeria</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>Francese</td>
    <td>Camerun</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>Francese</td>
    <td>Repubblica democratica del Congo</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>Francese</td>
    <td>Belgio</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>Francese</td>
    <td>Canada</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>Francese</td>
    <td>Francia</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>Francese</td>
    <td>Costa d'Avorio (Côte d'Ivoire)</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>Francese</td>
    <td>Lussemburgo</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>Francese</td>
    <td>Mauritania</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>Francese</td>
    <td>Mauritius</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>Francese</td>
    <td>Marocco</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>Francese</td>
    <td>Senegal</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>Francese</td>
    <td>Svizzera</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>Francese</td>
    <td>Tunisia</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>Gallego</td>
    <td>Spagna</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>Ganda</td>
    <td>Uganda</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>Georgiano</td>
    <td>Georgia</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>Tedesco</td>
    <td>Austria</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>Tedesco</td>
    <td>Germania</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>Tedesco</td>
    <td>Lussemburgo</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>Tedesco</td>
    <td>Svizzera</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>Greco</td>
    <td>Grecia</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>Gujarati</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>Hausa</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>Ebraico</td>
    <td>Israele</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>Hindi</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>Ungherese</td>
    <td>Ungheria</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>Islandese</td>
    <td>Islanda</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>Igbo</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>Indonesiano</td>
    <td>Indonesia</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>Italiano</td>
    <td>Italia</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>Italiano</td>
    <td>Svizzera</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>Giapponese</td>
    <td>Giappone</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>Kannada</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>Kazaco</td>
    <td>Kazakistan</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>Khmer</td>
    <td>Cambogia</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>Kinyarwanda</td>
    <td>Rwanda</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>Konkani</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>Coreano</td>
    <td>Corea del Sud</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>Lituano</td>
    <td>Lituania</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>Lettone</td>
    <td>Lettonia</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>Khmer</td>
    <td>Cambogia</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>Macedone</td>
    <td>Macedonia</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>Malese (alfabeto latino)</td>
    <td>Malesia</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>Malayalam</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>Maltese</td>
    <td>Malta</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>Marathi</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>Mongolo (alfabeto cirillico)</td>
    <td>Mongolia</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>Nepalese</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>Nepalese</td>
    <td>Nepal</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>Norvegese (Bokmål)</td>
    <td>Norvegia</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>Norvegese (Nynorsk)</td>
    <td>Norvegia</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>Oriya (Odia)</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>Oromo</td>
    <td>Etiopia</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>Polacco</td>
    <td>Polonia</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>Portoghese</td>
    <td>Angola</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>Portoghese</td>
    <td>Brasile</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>Portoghese</td>
    <td>Macao S.A.R. della Repubblica Popolare Cinese</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>Portoghese</td>
    <td>Mozambico</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>Portoghese</td>
    <td>Portogallo</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>Punjabi</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>Romeno</td>
    <td>Romania</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>Russo</td>
    <td>Russia</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>Serbo (alfabeto cirillico)</td>
    <td>Serbia</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>Serbo (alfabeto latino)</td>
    <td>Montenegro</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>Serbo (alfabeto latino)</td>
    <td>Serbia</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>Singalese</td>
    <td>Sri Lanka</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>Slovacco</td>
    <td>Slovacchia</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>Sloveno</td>
    <td>Slovenia</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>Spagnolo</td>
    <td>Argentina</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>Spagnolo</td>
    <td>Bolivia</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>Spagnolo</td>
    <td>Cile</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>Spagnolo</td>
    <td>Colombia</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>Spagnolo</td>
    <td>Costa Rica</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>Spagnolo</td>
    <td>Repubblica Dominicana</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>Spagnolo</td>
    <td>Ecuador</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>Spagnolo</td>
    <td>El Salvador</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>Spagnolo</td>
    <td>Guatemala</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>Spagnolo</td>
    <td>Honduras</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>Spagnolo</td>
    <td>Messico</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>Spagnolo</td>
    <td>Nicaragua</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>Spagnolo</td>
    <td>Panama</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>Spagnolo</td>
    <td>Paraguay</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>Spagnolo</td>
    <td>Perù</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>Spagnolo</td>
    <td>Portorico</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>Spagnolo</td>
    <td>Spagna</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>Spagnolo</td>
    <td>Stati uniti</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>Spagnolo</td>
    <td>Uruguay</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>Spagnolo</td>
    <td>Venezuela</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>Swahili</td>
    <td>Kenya</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>Swahili</td>
    <td>Tanzania</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>Svedese</td>
    <td>Svezia</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>Tamil</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>Telugu</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>Tailandese</td>
    <td>Thailandia</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>Turco</td>
    <td>Turchia</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>Ucraino</td>
    <td>Ucraina</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>Urdu</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>Urdu</td>
    <td>Pakistan</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>Uzbeco (Alfabeto cirillico)</td>
    <td>Uzbekistan</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>Uzbeco (alfabeto latino)</td>
    <td>Uzbekistan</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>Vietnamita</td>
    <td>Vietnam</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>Gallese</td>
    <td>Regno Unito</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>Yoruba</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>Zulu</td>
    <td>Sudafrica</td>
  </tr>
</table>
