---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: authentication, authorization, identity, app security, secure

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
{:faq: data-hd-content-type='faq'}


# Domande frequenti (FAQ)
{: #faq}

Questa FAQ fornisce risposte a domande comuni sul servizio {{site.data.keyword.appid_full}}.
{: shortdesc}


## Come calcola i prezzi {{site.data.keyword.appid_short_notm}}?
{: #faq-pricing}
{: faq}

Con {{site.data.keyword.appid_short_notm}}, paghi meno rispetto all'utilizzo di ulteriori risorse.
{: shortdesc}

Il piano di livello graduale è composto da tre parti: il numero di eventi di autenticazione, la sicurezza avanzata e regolare e il numero di utenti autorizzati. Ti viene effettuato un addebito ogni mese, in base al riepilogo delle due parti. Il prezzo totale è l'addebito cumulativo per ogni livello di utilizzo, che consiste dalla tua quantità moltiplicata per il prezzo unitario di quel livello.

I tuoi primi 1000 eventi di autenticazione e i tuoi primi 1000 utenti autorizzati sono gratuiti ogni mese, tranne per gli eventuali eventi di sicurezza avanzata. Gli eventi di sicurezza avanzata comportano degli ulteriori costi.

### Eventi di autenticazione
{: #faq-authentication}

Un evento di autenticazione si verifica quando viene emesso un nuovo token regolare o anonimo. I token possono essere emessi come una risposta a una richiesta di accesso iniziata da un utente o al posto dell'utente da un'applicazione. Per impostazione predefinita, i token di accesso sono validi per un'ora e i token anonimi per 30 giorni. Dopo che il token scade, devi creare un nuovo token per accedere alle risorse protette. Puoi aggiornare il tempo di scadenza dei tuoi token {{site.data.keyword.appid_short_notm}} nella pagina **Identity Providers > Manage > Authentication Settings** del dashboard del servizio.

#### Funzioni di sicurezza avanzate

Le funzioni di sicurezza avanzate ti forniscono la possibilità di rafforzare la sicurezza della tua applicazione.
{: shortdesc}

<table>
  <tr>
    <th>Funzione</th>
    <th>Vantaggio</th>
  </tr>
  <tr>
    <td>Autenticazione multifattore (MFA, multi-factor authentication)</td>
    <td>[MFA for Cloud Directory](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) conferma l'identità di un utente richiedendo a un utente di immettere un passcode monouso inviato alla sua email in aggiunta all'immissione di email e password.</td>
  </tr>
  <tr>
    <td>Gestione della politica della password</td>
    <td>Come proprietario dell'account, puoi applicare password più sicure per Cloud Directory configurando una serie di regole a cui devono conformarsi le password degli utenti. Gli esempi includono, il numero di accessi tentati prima del blocco, le date di scadenza, l'intervallo di tempo minimo tra gli aggiornamenti della password o il numero di volte in cui può essere ripetuta una password. Per un elenco completo delle opzioni e delle informazioni di configurazione, consulta [Gestione della password avanzata](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password).</td>
  </tr>
</table>

Per impostazione predefinita, le funzioni di sicurezza avanzate sono disabilitate. Se attivi la MFA o la gestione della politica della password, ti verrà addebitato un ulteriore costo. Se disabiliti tutte le funzioni avanzate, il tuo account torna alla politica di costo più basso. Ad esempio, se hai ottenuto 10.000 token di accesso. Hai quindi attivato la politica di gestione della password e ne hai ottenuti altri 10.000. Pagherai 20.000 eventi di autenticazione e 10.000 eventi di sicurezza avanzata.

Queste funzioni sono disponibili solo per le istanze presenti sul piano dei prezzi a livello graduale e che sono state create dopo il 15 marzo 2018.
{: note}

### Utenti autorizzati
{: #faq-authorized}

Un utente autorizzato è un utente univoco che accede al tuo servizio direttamente o indirettamente, inclusi gli utenti anonimi. Ti viene effettuato un addebito per un utente autorizzato ogni volta che un nuovo utente accede alla tua applicazione, inclusi gli utenti anonimi. Ad esempio, se un utente accede con Facebook e successivamente utilizzando Google, viene considerato come due utenti autorizzati separati.

Per le informazioni sui prezzi più aggiornate, puoi creare una stima dei costi facendo clic su **Aggiungi alla stima** nella sezione {{site.data.keyword.appid_short_notm}} del [catalogo {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/catalog/services/app-id).
{: tip}



## Perché devo inserire nella whitelist il mio URI di reindirizzamento?
{: #faq-redirect}
{: faq}

Un URI di reindirizzamento è l'endpoint di callback della tua applicazione. Per impedire gli attacchi di phishing, {{site.data.keyword.appid_short_notm}} convalida l'URI rispetto alla whitelist degli URI di reindirizzamento. Quando si verifica il phishing, esiste la possibilità che un aggressore possa accedere ai token del tuo utente. Per ulteriori informazioni sugli URI di reindirizzamento, vedi [Aggiunta di URI di reindirizzamento](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).

Non includere parametri di query nel tuo URL. Vengono ignorati nel processo di convalida. URL di esempio: `http://host:[port]/path`
{: tip}



## Come funziona la crittografia in {{site.data.keyword.appid_short_notm}}?
{: #faq-encryption}
{: faq}

Consulta la seguente tabella per le risposte alle domande più frequenti sulla crittografia.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Perché utilizzate la crittografia?</td>
      <td>Un modo con cui proteggiamo le informazioni dei nostri utenti è di codificare i dati del cliente quando inattivi. Il servizio codifica i dati del cliente quando inattivi con le chiavi per tenant.</td>
    </tr>
    <tr>
      <td>Avete creato i vostri algoritmi? Quali utilizzate nel vostro codice?</td>
      <td>Non abbiamo creato i nostri, il servizio utilizza <code>AES</code> e <code>SHA-256</code> con salting.</td>
    </tr>
    <tr>
      <td>Utilizzate provider o moduli di crittografia open source o pubblici? Avete mai esposto le funzioni di crittografia? </td>
      <td>Il servizio utilizza le librerie Java <code>javax.crypto</code>, ma non espone mai una funzione di crittografia.</td>
    </tr>
    <tr>
      <td>Come memorizzate le chiavi?</td>
      <td>Le chiavi sono generate, codificate con una chiave master specifica per ogni regione e poi archiviate localmente. Le chiavi master sono memorizzate in {{site.data.keyword.keymanagementserviceshort}}. Ai livelli di archiviazione e middleware, è presente la crittografia al livello del servizio, ossia è presente una chiave per tutti i clienti. Al livello dell'applicazione, ogni cliente ha la propria chiave di crittografia.</td>
    </tr>
    <tr>
      <td>Quale è la complessità della chiave che utilizzate?</td>
      <td>Il servizio utilizza 16 byte.</td>
    </tr>
    <tr>
      <td>Richiamate delle API remote che espongono le funzionalità di crittografia?</td>
      <td>No, non lo facciamo.</td>
    </tr>
  </tbody>
</table>

