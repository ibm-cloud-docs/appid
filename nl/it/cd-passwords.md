---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

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

# Definizione delle politiche della password
{: #cd-strength}

Puoi configurare i requisiti delle password che possono essere utilizzati con Cloud Directory. Definendo gli specifici requisiti che i tuoi utenti devono rispettare, puoi garantire delle applicazioni più sicure.
{: shortdesc}

## Politica: Complessità della password
{: #cd-password-strength}

Una password complessa rende difficile o persino improbabile, che qualcuno la indovini in modo manuale o automatizzato. Per impostare i requisiti per la complessità di una password dell'utente, puoi utilizzare la seguente procedura.
{: shortdesc}

1. Vai alla scheda **Password policies** del dashboard {{site.data.keyword.appid_short_notm}}.

2. Nella casella **Define password strength**, fai clic su **Edit**. Viene aperta una schermata.

3. Immetti una stringa regex valida nella casella **Password strength**.

  Esempi:
    - Deve avere una lunghezza di almeno 8 caratteri. (`^.{8,}$`)
    - Deve avere un numero, una lettera minuscola e una lettera maiuscola. (`^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`)
    - Deve avere solo lettere e numeri inglesi. (`^[A-Za-z0-9]*$`)
    - Deve avere almeno un carattere univoco. (`^(\w)\w*?(?!\1)\w+$`)

4. Fai clic su **Save**.

La complessità della password può essere impostata nella pagina delle impostazioni di Cloud Directory nella console {{site.data.keyword.appid_short_notm}} o utilizzando <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">le API di gestione <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
{: note}


## Politiche della password avanzate
{: #cd-advanced-password}


Puoi migliorare la sicurezza della tua applicazione mediante l'applicazione di vincoli della password.
{: shortdesc}


Puoi creare una politica della password avanzata che consiste in qualsiasi combinazione delle seguenti cinque funzioni:

 - Blocco dopo la ripetizione di credenziali non corrette
 - Evitare il riutilizzo della password
 - Scadenza della password
 - Periodo minimo tra le modifiche alla password
 - Assicurati che la password non includa il nome utente


 Quando abiliti questa funzione, viene attivata un'ulteriore fatturazione per le funzionalità di sicurezza avanzate. Per ulteriori informazioni, vedi [Come calcola i prezzi {{site.data.keyword.appid_short_notm}}](/docs/services/appid?topic=appid-faq#faq-pricing).
 {: important}


### Politica: Evitare il riutilizzo della password
{: #cd-avoid-reuse}

Quando i tuoi utenti stanno modificando le proprie password, potresti volergli impedire di scegliere una password utilizzata recentemente.
{: shortdesc}

Utilizzando la GUI o l'API, puoi scegliere il numero di password che un utente deve utilizzare prima di poter ripetere una password utilizzata precedentemente. Le opzioni di impostazione includono qualsiasi valore intero compreso nell'intervallo 1 .- 10.

Se questa opzione è attivata, un utente non può utilizzare una password che ha usato di recente. Se prova a impostare la sua password su una password utilizzata di recente, viene visualizzato un errore nella GUI del Widget di accesso predefinita e gli viene richiesto di immettere un'altra opzione.

Le password precedenti sono memorizzate in modo sicuro nello stesso modo in cui viene memorizzata la password corrente di un utente.
{: note}


### Politica: Blocco dopo la ripetizione di credenziali non corrette
{: #cd-lockout}

Potresti voler proteggere gli account dei tuoi utenti bloccando temporaneamente la capacità di accedere quando viene rilevato un comportamento sospetto, come ad esempio più tentativi di accesso consecutivi con una password non corretta. Questa misura può aiutare ad evitare che dei malintenzionati ottengano l'accesso all'account di un utente indovinandone la password.
{: shortdesc}

Utilizzando la GUI o l'API, puoi impostare il numero massimo di tentativi di accesso non riusciti che un utente effettua prima che il proprio account venga bloccato temporaneamente. Puoi anche definire la quantità di tempo per cui l'account viene bloccato. Hai le seguenti opzioni:

* Numero di tentativi: qualsiasi valore intero compreso tra 1 e 10.
* Periodo di blocco: qualsiasi valore intero specificato in minuti nell'intervallo compreso tra 1 minuto e 1440 minuti (24 ore).

Se un account viene bloccato, gli utenti non possono accedere o completare altre operazioni self service, come ad esempio la modifica della propria password, finché non trascorre il periodo di blocco specificato. Quando termina il periodo di blocco, l'utente viene sbloccato automaticamente.

Puoi sbloccare un utente prima del termine del periodo di blocco. Per vedere se gli utenti sono bloccati, controlla se il campo `active` è impostato su `false`. Puoi anche controllare se il loro stato sulla scheda **Users** del dashboard del servizio è impostato su `disabled`. Per sbloccare un utente, devi utilizzare [l'API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) per impostare il campo `active` su `true`.


### Politica: Periodo minimo tra le modifiche alla password
{: #cd-minimum-time}

Potresti voler impedire ai tuoi utenti di modificare velocemente le password impostando un periodo minimo di tempo in cui un utente deve attendere tra le modifiche alla password.
{: shortdesc}

Questa funzione è particolarmente utile quando utilizzata con la politica "Evitare il riutilizzo della password". Senza questa limitazione, un utente potrebbe semplicemente modificare la propria password più volte in rapida successione in modo da eludere la limitazione di riutilizzo delle password recenti. Puoi selezionare un qualsiasi valore nell'intervallo compreso tra 1 e 720 ore (30 giorni). Il campo viene specificato in ore.


### Politica: Scadenza della password
{: #cd-expiration}

Per motivi di sicurezza, potresti voler applicare una politica di rotazione della password, come ad esempio che i tuoi utenti debbano modificare le proprie password dopo un periodo di tempo specificato.
{: shortdesc}

Utilizzando la GUI o l'API, puoi impostare un periodo di tempo in cui le password del tuo utente rimangono valide. Dopo la scadenza della password di un utente, l'utente è costretto a reimpostare la propria password al successivo accesso. Puoi selezionare un qualsiasi numero di giorni completi nell'intervallo compreso tra 1 e 90.

Puoi iniziare a lavorare rapidamente con il Widget di accesso utilizzando la GUI predefinita fornita. All'utente viene richiesto di fornire una nuova password prima del completamento dell'accesso.

Se stai utilizzando un'esperienza di accesso personalizzata, viene attivato un errore quando un utente tenta di accedere con una password scaduta. È tua responsabilità configurare la tua applicazione in modo da fornire l'esperienza utente necessaria. Puoi richiamare l'API di modifica della password per impostare la nuova password.

La risposta endpoint del token è simile alla seguente:

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

Quando questa opzione viene attivata per la prima volta, tutte le password utente esistenti non hanno una data di scadenza. Il periodo di scadenza inizia per tali utenti quando viene modificata la loro password. Potresti voler incoraggiare gli utenti ad aggiornare la propria password dopo che hai attivato questa funzione.
{: note}


### Politica: Assicurati che la password non includa il nome utente
{: #cd-no-username}

Per delle password più sicure, potresti voler impedire agli utenti di includere il loro nome utente o la prima parte del loro indirizzo email.
{: shortdesc}

Questo vincolo non è sensibile a maiuscole/minuscole. Gli utenti non possono modificare le maiuscole/minuscole di alcuni o di tutti i caratteri in modo da utilizzare delle informazioni personali. Per configurare questa opzione, imposta lo switch su **on**.
{: note}

