---

copyright:
  years: 2017
lastupdated: "2017-06-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Configurazione dei provider di identità
{: #setting-up-idp}

Puoi configurare Facebook, Google, ID IBM o una loro combinazione per configurare un'esperienza SSO (single sign-on) per i tuoi utenti. Utilizzando un provider di identità, gli utenti sono in grado di accedere con le credenziali con cui hanno già familiarità.
{:shortdesc}


## Configurazione dell'autenticazione Facebook
{: #facebook}

Configura il servizio {{site.data.keyword.appid_short}} per utilizzare Facebook come provider di identità.


### Ottenere un ID applicazione e un segreto da Facebook
{: #getting-facebook-appid}

Per utilizzare Facebook come provider di identità per le tue applicazioni web o mobili, devi aggiungere e impostare la piattaforma del sito web sull'applicazione Facebook.

1. Accedi al tuo account sul <a href="https://developers.facebook.com/docs/apps/register" target="_blank">sito Facebook for Developers <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
2. Prendi nota del segreto e dell'ID applicazione di Facebook. Hai bisogno di questi valori per configurare il tuo progetto web per l'autenticazione nel tuo dashboard del servizio.
3. Aggiungi la piattaforma web e immetti l'URL del sito.
4. Dall'elenco dei prodotti, seleziona **Facebook Login**.
5. Nel campo Valid OAuth redirect URLs, immetti l'URL dell'endpoint di callback del server di autenticazione. Dopo aver configurato la tua istanza del servizio, puoi aggiungere questo valore.
6. Fai clic su **Save Changes**.

### Configurazione di {{site.data.keyword.appid_short_notm}} per l'autenticazione Facebook
{: #configuring-facebook-appid}

Quando disponi del tuo ID applicazione e del segreto Facebook e la tua applicazione Facebook for Developers è configurata per utilizzare i client web, puoi modificare l'autenticazione Facebook nel tuo dashboard del servizio.

1. Dalla scheda **Manage** del tuo dashboard del servizio, seleziona **Facebook** e fai clic su **Edit**.
2. Immetti l'ID applicazione e il segreto di Facebook che hai ottenuto dal sito web Facebook for Developers.
3. Copia l'URI nel campo **Redirect URI for Facebook for Developers**. Incolla l'URI nel campo **Valid OAuth redirect URIs** nella sezione **Facebook Login** del portale Facebook Developers. 
4. Fai clic su **Save**.
5. Facoltativo: per le applicazioni web, immetti l'URL di reindirizzamento nel campo **Web Application Redirect URLs**. Questo valore viene determinato dallo sviluppatore e utilizzato per accedere all'URL di reindirizzamento dopo il completamento del processo di autorizzazione.


## Configurazione dell'autenticazione Google
{: #google}

Configura il servizio {{site.data.keyword.appid_short_notm}} per utilizzare Google come provider di identità.


### Ottenere l'ID client e il segreto da Google
{: #google-client-id}

Per utilizzare Google come un provider di identità, ottieni un ID client e un segreto di Google e crea un progetto nella Google Developers Console.

1. Apri la tua applicazione Google nella <a href="https://console.developers.google.com/apis/library" target="_blank">Google Developer Console <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
2. Aggiungi l'API Google+.
3. Crea le credenziali utilizzando OAuth. Nel campo **Application Type**, seleziona **Web application**. Nel campo **Authorized redirect URIs**, immetti l'URI di reindirizzamento {{site.data.keyword.appid_short_notm}}. Puoi ottenere l'URI di autorizzazione di reindirizzamento {{site.data.keyword.appid_short_notm}} dalla schermata di configurazione di Google del dashboard del servizio.
4. Prendi nota del segreto e dell'ID client di Google e salva le tue modifiche. 



### Configurazione di {{site.data.keyword.appid_short_notm}} per l'autenticazione Google
{: #google-client-appid}

Quando disponi del segreto e del client di Google e la tua console Google Developers è configurata per utilizzare i client web, puoi modificare l'autenticazione Google nel tuo dashboard del servizio.

1. Dalla scheda **Manage** del tuo dashboard del servizio, seleziona **Google** e fai clic su **Edit**.
3. Immetti l'ID client e il segreto di Google che hai ottenuto dalla console Google Developers.
4. Copia l'URI nel campo **Redirect URI for Google for Developers**. Incolla l'URI nel campo **Authorized redirect URIs** in **Restrictions** nella sezione **Client ID for web application** del portale Google Developers. 
5. Fai clic su **Save**.
6. Facoltativo: per le applicazioni web, immetti l'URI di reindirizzamento nel campo **Web Application Redirect URIs**. Questo valore viene determinato dallo sviluppatore e utilizzato per accedere all'URI di reindirizzamento dopo il completamento del processo di autorizzazione.


## Configurazione dell'autenticazione ID IBM

Per utilizzare l'ID IBM come un provider di identità, utilizza la <a href="https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide" target="_blank">IBMid-Federation-Guide <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Se già disponi di un'applicazione BlueID, ottieni un segreto e un ID client BlueID.


### Ottenere l'ID client e il segreto dall'ID IBM 

Per ottenere un ID client e un segreto, utilizzare la seguente procedura. 

1. In <a href="https://w3.innovate.ibm.com/tools/sso/home.html" target="_blank">SSO Self-Service Provisioner <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>, accedi al tuo account BlueID.
2. Registra un'applicazione BlueID. Assicurati di selezionare **preproduction** o **production** per il provider di identità.
3. In **Client Details** immetti l'URL di reindirizzamento dell'ID applicazione. Puoi ottenere l'URI di autorizzazione di reindirizzamento dalla schermata di configurazione dell'ID IBM del tuo dashboard del servizio.
4. Assicurati che **Authorization Code** sia selezionato.
5. Prendi nota dei tuoi ID client, segreto e del tipo di provider di identità dell'account BlueID. Fai clic su **Continue & Finish**.

### Configurazione dell'ID applicazione per l'autenticazione ID IBM

Quando disponi dei tuoi segreto e client BlueID e la tua applicazione BlueID è configurata con l'URI di reindirizzamento corretto, puoi modificare la sessione di autenticazione BlueID del tuo dashboard del servizio.

1. Dalla scheda **Manage** del tuo dashboard del servizio, seleziona **IBMid** e fai clic su **Edit**.
2. Immetti i tuoi segreto e ID client BlueID.
3. Copia l'URI nel campo **Redirect URI for IBMid for Developers** e incollalo in **Redirect URIs**.
4. Seleziona **preproduction** o **production** per il provider di identità e fai clic su **Save**.
5. Facoltativo: per le applicazioni web, immetti l'URI di reindirizzamento nel campo **Web Application Redirect URIs**. Questo valore viene determinato dallo sviluppatore e utilizzato per accedere all'URI di reindirizzamento dopo l'autorizzazione. 
