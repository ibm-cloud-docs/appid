---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Esercitazione introduttiva
{: #gettingstarted}

{{site.data.keyword.appid_full}} ti aiuta ad aggiungere l'autenticazione alle tue applicazioni web e mobile e a proteggere le tue risorse di backend.
{: shortdesc}

## Creazione di un'istanza del servizio
{: #create}

Crea un'istanza di {{site.data.keyword.appid_short_notm}} per iniziare.
{: shortdesc}

1. Nel catalogo {{site.data.keyword.Bluemix}}, seleziona {{site.data.keyword.appid_short_notm}}. Si apre la schermata di configurazione del servizio.
2. Dai un nome alla tua istanza del servizio o utilizza il nome predefinito.
3. Per associare la tua istanza, seleziona un'applicazione dal menu **Connect to**. Se hai selezionato **Leave unbound**, puoi associare l'istanza del servizio successivamente.
4. Seleziona il tuo piano dei costi e fai clic su **Create**.

## Configurazione di un'applicazione di esempio 
{: #sample-app}

Puoi utilizzare una delle applicazioni di esempio preconfigurate per acquisire familiarità con l'utilizzo del servizio.
{: shortdesc}

Pronte all'uso, le applicazioni di esempio sono configurate con due provider di identità e la capacità di controllare l'autenticazione. Puoi anche utilizzare la funzione del widget di accesso per personalizzare una pagina di accesso e vedere quanto velocemente gli aggiornamenti che esegui vengono visualizzati nella tua applicazione.

Per configurare un'applicazione di esempio dalla GUI: 

1. Dopo aver creato l'istanza del servizio, puoi scegliere un'applicazione di esempio in un linguaggio con cui ti senti a tuo agio a lavorare. Puoi scegliere da iOS Swift, Android, Node.js e Java. Vuoi utilizzare una SDK? Controlla il nostro blog in <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">utilizzando {{site.data.keyword.appid_short_notm}} con altri linguaggi come Python <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
2. Segui la procedura nella GUI per **Creare ed eseguire** la tua applicazione di esempio. Ogni linguaggio viene configurato in modo leggermente diverso, per cui assicurati di selezionare il linguaggio dell'applicazione che hai scaricato dal menu a discesa. Una volta che la tua applicazione è stata configurata, puoi aprirla in un browser e accedere utilizzando le tue credenziali.
  **Nota**: assicurati che i prerequisiti siano installati per il linguaggio con cui vuoi lavorare.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> API Android 25 o superiore </li><li> Java 8.x </li><li> Strumenti SDK Android 25.2.5+ </li><li> Strumenti piattaforma SDK Android 25.0.3+ </li><li> Strumenti di build Android versione 25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (versione 1.1.0 o superiore)</li><li> iOS 9 o superiore</li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> La CLI Cloud Foundry </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> La CLI Cloud Foundry </li><li> Maven </li></ul></dd>
  </dl>
3. Fai clic su **Review Activity** per visualizzare gli eventi di autenticazione che si sono verificati. Dovresti visualizzare almeno un evento se hai eseguito l'accesso.
4. Personalizza la tua esperienza di accesso. Puoi selezionare un'immagine, come ad esempio il tuo logo e un colore dell'intestazione. Puoi selezionare una delle opzioni di colore o inserire un valore esadecimale. Quando sei soddisfatto dell'anteprima, fai clic su **Save Changes**. Puoi visualizzare un esempio dell'esperienza di accesso di esempio nella seguente immagine.
5. Nel tuo browser, aggiorna la tua pagina di accesso. Le modifiche effettuate nel passo precedente sono già visibili.
