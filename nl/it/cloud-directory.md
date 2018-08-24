---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configurazione di Cloud Directory
{: #cd}

Gli utenti possono registrarsi e accedere alle tue applicazioni mobili e web utilizzando un'email o il nome utente e una password. Una directory cloud è un registro utenti che viene conservato nel cloud. Quando un utente si registra alla tua applicazione, viene aggiunto alla tua directory di utenti. Con questa funzione, gli utenti hanno la libertà di gestire il proprio account all'interno della tua applicazione.
{: shortdesc}

</br>

## Gestione delle impostazioni della directory
{: #cd-settings}

Puoi configurare le notifiche e il livello di controllo utente per la tua applicazione. La configurazione della tua directory cloud può essere eseguita velocemente, come mostrato nella seguente immagine. Queste impostazioni possono essere aggiornate in qualsiasi momento dal dashboard del servizio.
{: shortdesc}


![Configurazione di Cloud Directory](/images/cloud-directory.png)
Figura. Il percorso di configurazione per Cloud Directory


1. Assicurati che Cloud Directory sia stato attivato come un provider di identità e imposta **Allow users to sign up and reset their password** su **On**. Se impostato su **Off**, puoi aggiungere utenti tramite la console per scopi di sviluppo.
2. Scegliere se gli utenti effettueranno l'autenticazione con un nome utente o una email specificati. Questo campo viene utilizzato per i flussi di registrazione, accesso e della password dimenticata. Se consenti agli utenti di accedere con un nome utente e una password, il nome utente deve avere una lunghezza di almeno 8 caratteri e non può contenere spazi, virgole o barre. **Nota:** puoi spostarti tra le opzioni solo quando non sono presenti utenti nel tuo Cloud Directory.
3. Configura i tuoi dettagli del mittente. Specifica l'indirizzo email da cui devono essere visualizzati i tuoi messaggi, il mittente e a chi i tuoi utenti possono rispondere.
  Quando configuri l'URL di azione, assicurati di dare tempo sufficiente a un utente per fare clic sul link. Un utente deve verificare la propria email per avere alcune opzioni, come la possibilità di richiedere un ripristino della propria password.
  {: tip}
4. Determina i tipi di email che un utente riceve e le informazioni sul mittente.
5. Con i template forniti, personalizza i tuoi messaggi con il tuo marchio o messaggi personalizzati. Per ulteriori informazioni, vedi [Gestione dei messaggi](/docs/services/appid/cloud-directory.html#cd-messages).
6. Visualizza chi si è registrato alla tua applicazione nella scheda **Users** della GUI.

Un singolo utente può accedere fino a 5 volte al minuto. Se viene effettuato un sesto tentativo, viene visualizzato un errore.
{: tip}

</br>

## Gestione dei messaggi
{: #cd-messages}

Un template è un esempio di messaggio email che potresti inviare ai tuoi utenti. Puoi personalizzare il template aggiornando il contenuto e il layout del messaggio.
{: shortdesc}

1. Nella scheda **Identity Providers > Cloud Directory > Settings** del dashboard, configura i messaggi che vuoi inviare a **On** .

2. Facoltativo: utilizza <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">le API di gestione della lingua <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per impostare un altra lingua che desideri utilizzare nei tuoi modelli del messaggio. Per un elenco dei codici lingua supportati, consulta [Lingue supportate](#languages).

3. Seleziona un **Message type**.

4. Personalizza il tuo messaggio modificando il contenuto e il design del messaggio. Puoi utilizzare i parametri per personalizzare i tuoi messaggi. Non dimenticare di salvare le tue modifiche!

### Tipi di messaggi

Puoi inviare diversi tipi di messaggi ai tuoi utenti. Puoi scegliere di inviare il messaggio di esempio che viene programmato nella IU o puoi personalizzare il contenuto per un'esperienza dell'applicazione più personale.

<dl>
  <dt>Benvenuto</dt>
    <dd><p>Una volta registrato, puoi dare il benvenuto a un utente nella tua applicazione tramite email. Per dare il benvenuto e trattenere i tuoi utenti, rendi il tuo messaggio il più interessante possibile.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Tutti i parametri del messaggio </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> Visualizza l'immagine che hai configurato per il tuo widget di accesso. </td>
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
      </tbody>
    </table>
    <p>**Nota**: se un utente non fornisce le informazioni estratte dal parametro, questi campi saranno vuoti.</p></dd>
  <dt>Password dimenticata</dt>
    <dd><p>Un utente può chiedere di reimpostare la propria password se la dimentica o deve aggiornarla per un qualsiasi motivo. Puoi personalizzare la risposta dell'email alla loro richiesta. Quando un utente richiede una modifica, la sua password rimane non modificata finché non fa clic sul link in questa email.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Parametri di modifica della password </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> Visualizza il numero di ore in cui il link è valido. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> Visualizza il numero di minuti in cui il link è valido. </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.code}</code></td>
          <td> Visualizza il passcode monouso come parte dell'URL. Ciò significa che ogni persona ha un codice diverso. Esempio: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.link}</code></td>
          <td> Visualizza il link su cui può fare clic un utente per reimpostare la propria password. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Verifica</dt>
    <dd><p>Puoi richiedere che un utente verifichi il proprio account tramite email. Richiedendo una verifica, limiti il numero di account falsi che possono registrarsi alla tua applicazione. Puoi limitare l'accesso alla tua applicazione finché un utente verifica la propria email o utilizzarla come un modo per gestire per quali utenti crei i profili.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Parametri del messaggio di verifica </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> Visualizza il numero di ore in cui il link è valido. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> Visualizza il numero di minuti in cui il link è valido. </td>
        </tr>
        <tr>
          <td><code>%{verify.code}</code></td>
          <td> Verifica l'URL di verifica monouso. </td>
        </tr>
        <tr>
          <td><code>%{verify.link}</code></td>
          <td> Verifica l'URL di azione che hai specificato nelle impostazioni. </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>Modifica della password</dt>
    <dd><p>Puoi far sapere a un utente quando la propria password è stata aggiornata. Ciò è utile se non ha richiesto che la sua password venga modificata. Gli utenti possono prendere le misure appropriate per riproteggere i propri account.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Parametri di modifica della password </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
          <td> Visualizza l'ora in cui una nuova password entra in vigore. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Visualizza l'indirizzo IP da cui è stata richiesta la modifica della password. </td>
        </tr>
      </tbody>
    </table>
    </dd>
</dl>
</br>
**NOTA**: {{site.data.keyword.appid_short_notm}} utilizza <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> come un un servizio di recapito email. Tutte le email vengono inviate con un unico account SendGrid.


</br>

## Gestione della complessità della password
{: #strength}

Puoi configurare i requisiti delle password che possono essere utilizzati con Cloud Directory.
{: shortdesc}

Una password complessa rende difficile o persino improbabile, che qualcuno la indovini in modo manuale o automatizzato. La complessità della password viene impostata come una stringa regex.

Alcuni esempi di complessità password comuni:

- Deve avere una lunghezza di almeno 8 caratteri. Regex di esempio: `^.{8,}$`
- Deve contenere 1 numero, 1 lettera minuscola e 1 maiuscola. Regex di esempio: `^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Deve contenere solo lettere e numeri inglesi. Regex di esempio: `^[A-Za-z0-9]*$`
- Deve avere almeno 1 carattere univoco. Regex di esempio: `^(\w)\w*?(?!\1)\w+$`

Devi utilizzare <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">le API di gestione <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per configurare i requisiti.

</br>



</br>

## Lingue supportate
{: #languages}

Puoi utilizzare <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">le API di gestione della lingua <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per configurare la lingua in cui può essere scritta la comunicazione del tuo utente. Tuttavia per impostazione predefinita è disponibile solo l'inglese. Sei responsabile della traduzione dei messaggi. Dopo aver impostato la configurazione con l'API, la GUI viene aggiornata in modo che puoi modificare il testo del modello.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Codice</th>
    <th>Lingua</th>
    <th>regione</th>
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
    <td>Macao</td>
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
    <td>Kenia</td>
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
    <td>Macao</td>
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
    <td>Kenia</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>Swahili</td>
    <td>Tanzania</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>Svedese </td>
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
    <td>Tailandese </td>
    <td>Thailandia</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>Turco </td>
    <td>Turchia</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>Ucraino </td>
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
    <td>Uzbeco (Alfabeto cirillico) </td>
    <td>Uzbekistan</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>Uzbeco (alfabeto latino) </td>
    <td>Uzbekistan</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>Vietnamita </td>
    <td>Vietnam</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>Gallese </td>
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
