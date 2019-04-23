---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# Configurazione di Cloud Directory
{: #cloud-directory}

Con {{site.data.keyword.appid_full}}, gli utenti possono registrarsi e accedere alle tue applicazioni mobili e web utilizzando un'email o il nome utente e una password. Una directory cloud è un registro utenti che viene conservato nel cloud. Quando un utente si registra alla tua applicazione, viene aggiunto alla tua directory di utenti. Con questa funzione, gli utenti hanno la libertà di gestire il proprio account all'interno della tua applicazione.
{: shortdesc}


## Gestione delle impostazioni della directory
{: #cd-settings}

Puoi configurare le notifiche e il livello di controllo utente per la tua applicazione. L'impostazione di Cloud Directory può essere eseguita rapidamente, come mostrato nella seguente immagine. Queste impostazioni possono essere aggiornate in qualsiasi modo dal dashboard del servizio e sono riflesse nella tua applicazione senza che sia richiesta alcuna modifica del codice.
{: shortdesc}


![Configurazione di Cloud Directory](images/cloud-directory.png)
Figura. Il percorso di configurazione per Cloud Directory


1. Passa alla scheda **Manage authentications** del dashboard {{site.data.keyword.appid_short_notm}} e assicurati che Cloud Directory sia impostato su **On**.

2. Nella scheda **Cloud Directory > Settings**, imposta **Allow users to sign up and sign in** su **Email and password** o **User name and password**. L'utente può eseguire l'accesso con una email che già possiede oppure creare un nome utente da utilizzare quando interagisce con la tua applicazione.

  Puoi alternare tra le opzioni prima che gli utenti vengano aggiunti alla tua directory. Dopo che il primo utente è stato aggiunto, gli utenti successivi devono utilizzare anche la stessa configurazione.
  {: note}

2. Decidi se vuoi che i tuoi utenti creino un nome utente o utilizzino la propria email quando accedono. Entrambe le opzioni richiedono una password. Dopo che gli utenti sono stati aggiunti alla tua directory, non puoi più alternare tra le opzioni.

3. Fai clic su **Edit** nella riga dei criteri della password per specificare tutti i requisiti che vuoi mettere in atto. I criteri della password sono forniti come regex. Per aiuto nel determinare la complessità della password o per vedere degli esempi comuni, consulta [Gestione della complessità della password](/docs/services/appid?topic=appid-cd-strength#cd-strength). Fai clic su **Save** per mettere in atto i tuoi requisiti.

4. Imposta **Allow users to sign up to your app** su **Yes**. Puoi ancora aggiungere utenti mediante la console, se l'opzione è impostata su **No**. Tuttavia, è più comune aggiungere utenti mediante la console solo per scopi di sviluppo.

5. Imposta **Allow users to manage their account from your app** su **Yes** se vuoi che i tuoi utenti possano reimpostare e modificare le proprie password oppure ripristinare i propri dettagli. Se vuoi limitare la capacità self-service dei tuoi utenti, imposta il valore su **No**.

6. Configura le tue impostazioni dell'email. Fai clic su **Edit** nella riga **Sender details** per aggiornare le tue impostazioni dell'email. Le impostazioni dell'email si applicano a tutta la comunicazione inviata tramite {{site.data.keyword.appid_short_notm}}.

    1. Specifica l'indirizzo email che deve inviare l'email. Se scegli di modificare il valore predefinito, l'email potrebbe essere inviata alla cartella della posta indesiderata di un utente.

    2. Aggiungi un nome per il mittente.

    3. Immetti un'email che può essere utilizzata per inviare una risposta.

    4. Fai clic su **Save**.
