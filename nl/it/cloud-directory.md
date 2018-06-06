---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configurazione di Cloud Directory
{: #cd}

Puoi configurare {{site.data.keyword.appid_short_notm}} in modo che utilizzi Cloud Directory come un provider di identità. Gli utenti possono registrarsi e accedere alle tue applicazioni web e mobile utilizzando un'email e una password. Una directory cloud è un registro utenti che viene conservato nel cloud. Quando un utente si registra alla tua applicazione con la propria email e una password, viene aggiunto alla tua directory di utenti. Con questa funzione, gli utenti finali hanno la libertà di gestire i propri account all'interno della tua applicazione.
{: shortdesc}

</br>

## Gestione delle impostazioni della directory
{: #cd-settings}

Puoi configurare le notifiche e il livello di controllo utente per la tua applicazione. La configurazione della tua directory cloud può essere eseguita velocemente, come mostrato nella seguente immagine. Queste impostazioni possono essere aggiornate in qualsiasi momento dal dashboard del servizio.
{: shortdesc}

![Configurazione di Cloud Directory](/images/cloud-directory.png)

1. Assicurati che Cloud Directory sia stato attivato come un provider di identità e imposta **Allow users to sign up and reset their password** su **On**. Puoi ancora aggiungere gli utenti tramite la console quando è impostato su **Off**, ma solo per scopi di sviluppo.
2. Configura i tuoi dettagli del mittente. Specifica l'indirizzo email da cui devono essere visualizzati i tuoi messaggi, il mittente e a chi i tuoi utenti possono rispondere.
  **Nota**: assicurati, quando configuri il tuo URL di azione, di fornire abbastanza tempo agli utenti per fare clic sul link. Un utente deve verificare la propria email per avere alcune opzioni, come la possibilità di richiedere un ripristino della propria password.
3. Determina i tipi di email che un utente riceve e le informazioni sul mittente.
4. Utilizzando i template forniti, personalizza i tuoi messaggi con il tuo marchio o con messaggi personalizzati. Per ulteriori informazioni, vedi [Gestione dei messaggi](/docs/services/appid/cloud-directory.html#cd-messages).
5. Visualizza chi si è registrato alla tua applicazione nella scheda **Users** della GUI.

</br>

## Gestione dei messaggi
{: #cd-messages}

Un template è un esempio di un messaggio email che puoi inviare ai tuoi utenti. Puoi personalizzare il template aggiornando il contenuto e il layout del messaggio. Puoi impostare questi messaggi su **On** o **Off** nella scheda delle impostazioni della directory.
{: shortdesc}

1. Seleziona un **Message type**.
2. Personalizza il tuo messaggio modificando il contenuto e il design del messaggio. Puoi utilizzare i parametri per personalizzare i tuoi messaggi. Non dimenticare di salvare le tue modifiche!

### Tipi di messaggi

Esistono vari tipi di messaggi che puoi inviare ai tuoi utenti. Puoi scegliere di inviare il messaggio di esempio che viene programmato nella IU o puoi personalizzare il contenuto per un'esperienza dell'applicazione più personale.

<dl>
  <dt>Benvenuto </dt>
    <dd><p>Puoi dare il benvenuto a un utente nella tua applicazione tramite email, dopo che si è registrato. Per dare il benvenuto e trattenere i tuoi utenti, rendi il tuo messaggio il più interessante possibile.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parametri che possono essere utilizzati in qualsiasi tipo di messaggio </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Visualizza l'immagine che hai configurato per il tuo widget di accesso. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> Visualizza il nome della schermata scelta da un utente da utilizzare quando si interagisce con l'applicazione. </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> Visualizza l'indirizzo email registrato dell'utente. </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> Visualizza il nome specificato dall'utente. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Visualizza il nome completo dell'utente. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Visualizza il cognome specificato dall'utente. </td>
        </tr>
      </tbody>
    </table>
    <p>**Nota**: se un utente non fornisce le informazioni estratte dal parametro, questi campi saranno vuoti.</p></dd>
  <dt>Password dimenticata</dt>
    <dd><p>Un utente può richiedere il ripristino della propria password se la dimentica o ha bisogno di aggiornarla per qualsiasi motivo. Puoi personalizzare la risposta dell'email alla loro richiesta. Quando un utente richiede una modifica, la sua password rimane non modificata finché non fa clic sul link in questa email.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parametri di modifica della password </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Visualizza il numero di ore in cui il link è valido. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Visualizza il numero di minuti in cui il link è valido. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> Visualizza il passcode monouso come parte dell'URL. Questo significa che ogni persona ha un codice differente. Esempio: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Visualizza il link su cui può fare clic un utente per reimpostare la propria password. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Verifica</dt>
    <dd><p>Puoi richiedere che un utente verifichi il proprio account tramite email. Richiedendo una verifica, limiti il numero di account falsi che possono registrarsi alla tua applicazione. Puoi limitare l'accesso alla tua applicazione finché un utente verifica la propria email o utilizzarla come un modo per gestire per quali utenti crei i profili.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parametri del messaggio di verifica </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Visualizza il numero di ore in cui il link è valido. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Visualizza il numero di minuti in cui il link è valido. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> Verifica l'URL di verifica monouso. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> Verifica l'URL di azione che hai specificato nelle impostazioni. </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>Modifica della password</dt>
    <dd><p>Puoi consentire che un utente sappia quando la propria password è stata aggiornata. Questo è utile se non richiede che la propria password venga modificata. Gli utenti possono prendere le misure appropriate per riproteggere i propri account.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parametri di modifica della password </th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
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
**NOTA**: {{site.data.keyword.appid_short_notm}} utilizza <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> come un un servizio di recapito email. Tutte le email vengono inviate utilizzando un solo account SendGrid.

</br>
## Fasi successive
Ora che hai configurato Cloud Directory, sei pronto per aggiungere il codice del widget di accesso al tuo codice dell'applicazione. Fai clic su un'icona di linguaggio SDK nella seguente immagine per visualizzare cosa devi fare.
{: shortdesc}

<img usemap="#options-map" border="0" class="image" id="options" src="images/options.png" width="750" alt="Fai clic su un'icona di linguaggio SDK per iniziare ad utilizzare Cloud Directory nelle tue applicazioni." style="width:750px;" />
<map name="options-map" id="options-map">
<area href="branded.html#branded-ui-android" alt="Gestione dell'esperienza di accesso con l'SDK Android" shape="rect" coords="187, 6, 305, 120" />
<area href="branded.html#branded-ui-ios-swift" alt="Gestione dell'esperienza di accesso con l'SDK iOS Swift." shape="rect" coords="333, 6, 448, 125" />
<area href="branded.html#branded-ui-nodejs" alt="Gestione dell'esperienza di accesso con l'SDK Node.js." shape="rect" coords="472, 7, 590, 121" />
</map>
