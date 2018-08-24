---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Esercitazione introduttiva
{: #gettingstarted}

La sicurezza delle applicazioni può essere incredibilmente complicata. Per la maggior parte degli sviluppatori, è una delle parti più difficili nella creazione di un'applicazione. Come puoi essere sicuro di proteggere le informazioni dei tuoi utenti? Integrando {{site.data.keyword.appid_full}} nelle tue applicazioni, puoi proteggere le risorse e aggiungere l'autenticazione; anche quando non hai molta esperienza in materia di sicurezza.
{: shortdesc}

Richiedendo agli utenti di accedere alla tua applicazione, puoi memorizzare i dati utente come le preferenze dell'applicazione o le informazioni dai profili sociali pubblici e quindi utilizzare tali dati per personalizzare ogni esperienza della tua applicazione. App ID fornisce per te un framework di accesso, ma puoi anche portare le tue schermate di accesso personalizzate quando lavori con Cloud Directory.

Come proprietario dell'account, puoi ora impostare politiche che definiscono il modo in cui i membri del tuo team possono interagire con le istanze di {{site.data.keyword.appid_short_notm}}. Puoi decidere chi può creare, aggiornare ed eliminare le istanze del servizio. Per ulteriori informazioni, vedi [Gestione dell'accesso al servizio](/docs/services/appid/iam.html).
{:tip}

## Creazione di un'istanza del servizio
{: #create}

Per iniziare, crea e associa un'istanza di {{site.data.keyword.appid_short_notm}} alla tua applicazione.
{: shortdesc}

1. Nel catalogo {{site.data.keyword.Bluemix}}, seleziona {{site.data.keyword.appid_short_notm}}. Si apre la schermata di configurazione del servizio.
2. Dai un nome alla tua istanza del servizio o utilizza il nome predefinito.
3. Seleziona il tuo piano dei costi e fai clic su **Create**.
4. Associa la tua istanza di {{site.data.keyword.appid_short_notm}}.
    1. Per visualizzare un elenco di applicazioni che puoi associare alla tua istanza del servizio, fai clic su **Connessioni**.
    2. Fai clic su **Crea connessione**. Viene visualizzata una pagina con tutte le applicazioni che puoi associare.
    3. Fai clic su **Connetti** sull'applicazione che vuoi associare.
    4. Fai clic su **Riprepara** per applicare la modifica.

Questo è tutto! Sei pronto per iniziare a configurare le impostazioni della tua applicazione.


## Configurazione di un'applicazione di esempio
{: #sample-app}

Puoi utilizzare una delle applicazioni di esempio preconfigurate per acquisire familiarità con l'utilizzo del servizio.
{: shortdesc}

Pronte all'uso, le applicazioni di esempio sono configurate con due provider di identità e la capacità di controllare l'autenticazione. Puoi anche utilizzare la funzione del widget di accesso per personalizzare una pagina di accesso e vedere quanto velocemente gli aggiornamenti che esegui vengono visualizzati nella tua applicazione.

Per configurare un'applicazione di esempio dalla GUI:

1. Dopo aver creato un'istanza del servizio, puoi scegliere un'applicazione di esempio con il linguaggio con cui ti senti più a tuo agio. Puoi scegliere tra iOS Swift, Android, Node.js e Java. Vuoi utilizzare una SDK? Puoi integrare {{site.data.keyword.appid_short_notm}} utilizzando le API.
2. Segui la procedura nella GUI per **Creare ed eseguire** la tua applicazione di esempio. Ogni linguaggio viene configurato in modo leggermente diverso, per cui assicurati di selezionare il linguaggio dell'applicazione che hai scaricato dal menu a discesa. Una volta che la tua applicazione è stata configurata, puoi aprirla in un browser e accedere utilizzando le tue credenziali. Assicurati che i prerequisiti per il linguaggio dell'applicazione siano installati.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> API Android 27 o superiore </li><li> Java 8.x </li><li> Strumenti SDK Android 25.2.5+ </li><li> Strumenti piattaforma SDK Android 26.1.1+ </li><li> Strumenti di build Android versione 27.0.0+ </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (versione 1.1.0 o superiore) </li><li> iOS 10.0 o superiore </li><li> MacOS 10.11.5 </li><li> Xcode (versione 9.0.1 o superiore) </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> La CLI {{site.data.keyword.Bluemix_notm}} </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> La CLI {{site.data.keyword.Bluemix_notm}} </li><li> Maven </li></ul></dd>
  </dl>

  Non vedi la lingua che stai cercando? Non preoccuparti. Puoi trarre vantaggio da {{site.data.keyword.appid_short_notm}} tramite le API. Puoi inoltre consultare i <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nostri blog <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per ulteriore assistenza con altre lingue.
  {: tip}

3. Fai clic su **Review Activity** per visualizzare gli eventi di autenticazione che si sono verificati. Dopo aver eseguito l'accesso, puoi visualizzare un evento.
4. Personalizza la tua esperienza di accesso. Puoi selezionare un'immagine, come ad esempio il tuo logo e un colore dell'intestazione. Puoi selezionare una delle opzioni di colore o inserire un valore esadecimale. Quando sei soddisfatto dell'anteprima, fai clic su **Save Changes**.
5. Nel tuo browser, aggiorna la tua pagina di accesso. Le modifiche effettuate nel passo precedente sono già visibili.

## Fasi successive
{: #next}

Sei pronto ad utilizzare le tue applicazioni? Inizia [aggiungendo il servizio alla tua applicazione](/docs/services/appid/install.md). Il servizio fornisce gli SDK per la maggior parte delle lingue utilizzate, ma se non vedi un SDK per la lingua in cui è scritta la tua applicazione, puoi ancora utilizzare l'API.

</br>
</br>
