---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, development,

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

# Esercitazione introduttiva
{: #getting-started}

La sicurezza delle applicazioni può essere incredibilmente complicata. Per la maggior parte degli sviluppatori, è una delle parti più difficili nella creazione di un'applicazione. Come puoi essere sicuro di proteggere le informazioni dei tuoi utenti? Integrando {{site.data.keyword.appid_full}} nelle tue applicazioni, puoi proteggere le risorse e aggiungere l'autenticazione; anche quando non hai molta esperienza in materia di sicurezza.
{: shortdesc}

Richiedendo agli utenti di accedere alla tua applicazione, puoi memorizzare i dati utente come le preferenze dell'applicazione o le informazioni dai profili sociali pubblici e quindi utilizzare tali dati per personalizzare ogni esperienza della tua applicazione. {{site.data.keyword.appid_short_notm}} ti fornisce un framework, ma puoi anche portare le tue schermate di accesso personalizzate quando lavori con Cloud Directory.

Ci piacerebbe ricevere dei tuoi feedback e domande.
* Se hai domande tecniche su {{site.data.keyword.appid_short_notm}}, inserisci la tua domanda in <a href="https://stackoverflow.com" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e contrassegnala con la tag `ibm-appid`.
* Per domande sul servizio e sulle istruzioni per l'utilizzo iniziale, utilizza il forum <a href="https://developer.ibm.com" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Includi la tag `appid`.

## Creazione di un'istanza del servizio
{: #create}

Per iniziare, crea e associa un'istanza di {{site.data.keyword.appid_short_notm}} alla tua applicazione.
{: shortdesc}

1. Nel catalogo {{site.data.keyword.cloud_notm}}, seleziona {{site.data.keyword.appid_short_notm}}. Si apre la schermata di configurazione del servizio.
2. Dai un nome alla tua istanza del servizio o utilizza il nome predefinito.
3. Seleziona il tuo piano dei costi e fai clic su **Crea**.
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

Pronte all'uso, le applicazioni di esempio sono configurate con due provider di identità e la capacità di controllare l'autenticazione. Sono offerte delle applicazioni di esempio in `iOS Swift`, `Android`, `Node.js` e `Java`. Se non vedi un linguaggio con cui ti senti a tuo agio a lavorare, non ti preoccupare. Puoi integrare {{site.data.keyword.appid_short_notm}} nella tua applicazione di esempio utilizzando le API fornite.

Per creare un'applicazione di esempio:

1. Fai clic su **Download Sample**.
2. Fai clic sul linguaggio che preferisci per scaricare l'esempio.
  Non vedi la lingua che stai cercando? Non preoccuparti. Puoi trarre vantaggio da {{site.data.keyword.appid_short_notm}} tramite le API. Puoi inoltre consultare i <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nostri blog <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per ulteriore assistenza con altre lingue.
  {: tip}
3. Assicurati di aver installato o completato i prerequisiti.
4. Segui i passi **Build & Run** per configurare il tuo esempio con {{site.data.keyword.appid_short_notm}}.
5. Fai clic su **Review Activity** per visualizzare tutti gli eventi di autenticazione che si sono verificati. Ogni tipo di accesso crea un evento visibile su questa pagina.
6. Personalizza il widget di accesso.
  1. Aggiungi un'immagine come un logo del produttore facendo clic su **Select** e selezionando dal tuo sistema locale un'immagine da caricare.
  2. Scegli uno schema di colori selezionando una delle opzioni di colore o specificando un valore esadecimale.
  3. Passa dal web al dispositivo mobile per vedere come lo schema di colori appaia su ogni tipo di dispositivo.
  4. Quando sei soddisfatto delle tue scelte, fai clic su **Save Changes**.
7. In un browser, aggiorna la tua pagina di accesso. Le modifiche effettuate nel passo precedente sono già visibili.


## Passi successivi
{: #next}

Sei pronto ad utilizzare le tue applicazioni? Inizia [aggiungendo il servizio alla tua applicazione](/docs/services/appid?topic=appid-web-apps#web-apps). Il servizio fornisce gli SDK per la maggior parte dei linguaggi utilizzati, ma se non vedi un SDK per il linguaggio in cui è scritta la tua applicazione, puoi ancora avvalerti di {{site.data.keyword.appid_short_notm}} utilizzando le API.
