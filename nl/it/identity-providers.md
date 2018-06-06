---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Configurazione dei provider di identità sociali 
{: #setting-up-idp}

I provider di identità forniscono un ulteriore livello di autenticazione per le tue applicazioni web e mobili. Con {{site.data.keyword.appid_full}} puoi configurare uno o diversi provider di identità per impostare un'esperienza SSO (single sign-on) per la tua applicazione.
{: shortdesc}

## Configurazione predefinita
{: #default}

{{site.data.keyword.appid_short_notm}} fornisce una configurazione predefinita per aiutarti con la configurazione iniziale dei tuoi provider di identità.
{: shortdesc}

Le credenziali predefinite sono impostate per Facebook e Google. Sei limitato a 100 utilizzi delle credenziali per istanza, al giorno. Poiché sono credenziali IBM, dovrebbero essere utilizzate solo nelle tue applicazioni nella modalità di sviluppo. Prima di pubblicare la tua applicazione, [aggiorna la configurazione con le tue proprie credenziali](/docs/services/appid/identity-providers.html).


## Configurazione di Facebook
{: #facebook}

Puoi configurare il servizio {{site.data.keyword.appid_short}} per utilizzare Facebook come provider di identità.
{: shortdesc}

### Ottenere un ID applicazione e un segreto da Facebook

Per utilizzare Facebook come provider di identità, devi aggiungere e impostare la piattaforma del sito web sull'applicazione Facebook.

1. Accedi al tuo account sul <a href="https://developers.facebook.com/docs/apps/register" target="_blank">sito Facebook for developers <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
2. Prendi nota del segreto e dell'ID applicazione di Facebook. Hai bisogno di questi valori per configurare il tuo progetto web per l'autenticazione nel tuo dashboard del servizio.
3. Aggiungi la piattaforma web e immetti l'URL del sito.
4. Dall'elenco dei prodotti, seleziona **Facebook Login**.
5. Nel campo Valid OAuth redirect URLs, immetti l'URL dell'endpoint di callback del server di autenticazione. Dopo aver configurato la tua istanza del servizio, puoi aggiungere questo valore.
6. Fai clic su **Save Changes**.


### Configurazione di {{site.data.keyword.appid_short_notm}} per l'autenticazione Facebook

Quando disponi del tuo ID applicazione e del segreto Facebook e la tua applicazione Facebook for Developers è configurata per utilizzare i client web, puoi modificare l'autenticazione Facebook nel tuo dashboard del servizio.

1. Dalla scheda **Manage** del tuo dashboard del servizio, seleziona **Facebook** e fai clic su **Edit**.
2. Immetti l'ID applicazione e il segreto di Facebook che hai ottenuto dal sito web Facebook for Developers.
3. Copia l'URI nel campo **Redirect URI for Facebook for Developers**. Incolla l'URI nel campo **Valid OAuth redirect URIs** nella sezione **Facebook Login** del portale Facebook Developers.
4. Fai clic su **Save**.
5. Facoltativo: per le applicazioni web, immetti l'URL di reindirizzamento nel campo **Web Application Redirect URLs**. Questo valore viene determinato dallo sviluppatore e utilizzato per accedere all'URL di reindirizzamento dopo il completamento del processo di autorizzazione.


## Configurazione di Google
{: #google}

Puoi configurare il servizio {{site.data.keyword.appid_short}} per utilizzare Google come provider di identità.
{: shortdesc}

### Ottenere l'ID client e il segreto da Google

Crea un progetto in <a href="https://developers.google.com/" target="_blank">Google Developers Console <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>, configuralo per utilizzare i client web e richiama un segreto e un ID client.

1. Crea un progetto.
2. Aggiungi l'API Google+ al tuo progetto Google.
3. Aggiungi le credenziali all'API Google+.
    1. Seleziona l'API Google+ come il tipo di API.
    2. Seleziona **Web Browser** come posizione da cui stai richiamando l'API.
    3. Scegli **User data**.
    4. Riempi i campi obbligatori e crea un ID client. Viene contemporaneamente creato un segreto.
4. Prendi nota del segreto e dell'ID client Google. Nella scheda delle credenziali, seleziona l'ID che hai creato per ottenere i tuoi ID client e segreto.

### Configurazione di {{site.data.keyword.appid_short}} per l'autenticazione Google

Dopo aver configurato il tuo progetto Google e disporre di segreto e di un ID client, puoi modificare il tuo dashboard del servizio per l'autenticazione con Google.

1. Dalla scheda **Manage** del tuo dashboard del servizio, seleziona **Google** e fai clic su **Edit**.
2. Immetti il segreto e l'ID client ottenuti da Google Developers Console.
3. Autorizza l'URL {{site.data.keyword.appid_short}}.
    1. Copia **Redirect URL for Google Developer Console** dai dettagli del tuo provider di identità Google.
    2. Nella scheda delle credenziali del tuo progetto Google, seleziona l'ID client che hai creato per questa integrazione.
    3. Incolla l'URL da {{site.data.keyword.appid_short}} nel campo **Authorized redirect URIs** e fai clic su **Save**.
4. Fai clic su **Save** per aggiornare la tua configurazione di Google in {{site.data.keyword.appid_short}}.
5. Facoltativo: per le applicazioni web, immetti un URL di reindirizzamento nella scheda **Mangage**. Dopo il completamento del processo di autorizzazione, viene inviato un utente a questo URL.
