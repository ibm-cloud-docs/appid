---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Domande frequenti (FAQ)

Questa FAQ fornisce risposte a domande comuni sul servizio {{site.data.keyword.appid_full}}.
{: shortdesc}


## Come {{site.data.keyword.appid_short_notm}} calcola i prezzi?
{: #pricing}

Con {{site.data.keyword.appid_short_notm}}, paghi meno rispetto all'utilizzo di ulteriori risorse.
{: shortdesc}

Il piano di livello graduale è composto da due parti: il numero di eventi di autenticazione e il numero di utenti autorizzati. Ti viene effettuato un addebito ogni mese, in base al riepilogo delle due parti. Il prezzo totale è l'addebito cumulativo per ogni livello di utilizzo, che consiste dalla tua quantità moltiplicata per il prezzo unitario di quel livello.

### Eventi di autenticazione

Un evento di autenticazione si verifica quando viene emesso un nuovo token {{site.data.keyword.appid_short_notm}}. Per gli utenti identificati, ogni nuovo token è valido per un'ora. I token sono validi per un mese per gli utenti anonimi. Dopo che il token scade, devi creare un nuovo token per accedere alle risorse protette. Quando utilizzi l'ID applicazione per l'autenticazione mobile, i token degli utenti vengono archiviati in `key-store/key-chain` e aggiunti ad ogni richiesta futura. È possibile accedere ai token utilizzando l'SDK Android o iOS Swift {{site.data.keyword.appid_short_notm}}. Quando utilizzi il servizio per l'autenticazione web, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">archivia il token dell'utente <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> nei cookie della sessione.

### Utenti autorizzati

Un utente autorizzato è un utente univoco che accede al tuo servizio direttamente o indirettamente. Ti viene effettuato un addebito per un utente autorizzato ogni volta che un nuovo utente accede da ogni provider di identità, inclusi gli utenti anonimi. Ad esempio, se un utente accede con Facebook e successivamente utilizzando Google, vengono considerati due utenti autorizzati separati.

Per ulteriori informazioni sui prezzi del livello graduale, consulta la [Documentazione dei prezzi di {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>

## Quale tipo di attività viene monitorata dall'ID applicazione?
{: #activity-monitor}

Puoi tenere traccia dell'attività che è stata generata all'interno dell'applicazione che è associata all'istanza del servizio. Puoi anche monitorare l'attività amministrativa effettuata nell'ID applicazione utilizzando il servizio Programma di traccia dell'attività.

Per visualizzare l'attività generata dalla tua applicazione: 

1. Accedi al tuo account IBM Cloud.
2. Dal dashboard, seleziona l'istanza del tuo ID applicazione.
3. Fai clic sulla scheda **Panoramica**.
4. Visualizza l'attività elencata in **Log attività**.

</br>
Per monitorare l'attività amministrativa: 

1. Accedi al tuo account IBM Cloud. Passa all'organizzazione e allo spazio in cui è stato eseguito il provisioning della tua istanza dell'ID applicazione.
2. Dal catalogo, esegui il provisioning di un'istanza del servizio Programma di traccia dell'attività. Assicurati di essere nello stesso spazio della tua istanza dell'ID applicazione.
3. Nel dashboard del programma di traccia dell'attività, fai clic sulla scheda **Gestisci**.
4. Nell'elenco a discesa seleziona le seguenti configurazioni per ricercare tutti gli eventi che sono stati generati dall'ID applicazione.
<table>
  <tr>
    <th> Campo</th>
    <th> Configurazione </th>
  </tr>
  <tr>
    <td><i>Log vista</i></td>
    <td><b>Log spazio</b></td>
  </tr>
  <tr>
    <td><i>Search</i></td>
    <td><b>target.name</b></td>
  </tr>
  <tr>
    <td>Filtro </td>
    <td>appid</td>
  </tr>
</table>
5. Fai clic su **Filtro**.

Controlla la [Documentazione del programma di traccia dell'attività](/docs/services/cloud-activity-tracker/index.html) per ulteriori informazioni su come funziona il servizio.
