---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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



# Descrizione dei token
{: #tokens}

Quando un utente viene correttamente autenticato, l'applicazione riceve i token da {{site.data.keyword.appid_short_notm}}. Il servizio utilizza tre tipi principali di token per completare il processo di autenticazione.
{: shortdesc}


## Token di accesso
{: #access}

I token di accesso rappresentano l'autorizzazione e abilitano la comunicazione con le [risorse di backend](/docs/services/appid?topic=appid-backend) che sono protette dai filtri di autorizzazione impostati da {{site.data.keyword.appid_short}}. Il token è conforme alle specifiche JavaScript Object Signing and Encryption (JOSE). Il token viene creato come <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> firmati con un chiave web JSON che utilizza l'algoritmo RS256.

Token di esempio:
  ```
  Intestazione: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
  }
  ```
  {: screen}

## Cosa sono i token di identità?
{: #identity}

I token di identità rappresentano l'autenticazione e contengono le informazioni sull'utente. Può fornirti le informazioni sui loro nome, email, sesso e ubicazione. Un token può anche restituire un URL a un'immagine dell'utente. Il token viene creato come <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> firmati con un chiave web JSON che utilizza l'algoritmo RS256.

Token di esempio:
  ```
  Intestazione: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "exp": 1551903163,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "iat": 1551899553,
    "email": "appid155@mailinator.com",
    "name": "appid155@mailinator.com",
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "identities": [
      {
        "provider": "cloud_directory",
        "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
    ],
    "amr": [
      "cloud_directory"
    ]
  }
  ```
  {: screen}


I token di identità contengono solo delle informazioni utente parziali. Per visualizzare tutte le informazioni fornite dal provider di identità, puoi utilizzare l'[endpoint delle informazioni sull'utente](/docs/services/appid?topic=appid-predefined-attributes#predefined-access-api).

## Cosa sono i token di aggiornamento?
{: #refresh}

{{site.data.keyword.appid_short}} supporta la capacità di acquisire nuovi token di accesso e identità senza la riautenticazione, come definito in <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Un token di aggiornamento può essere utilizzato per rinnovare il token di accesso in modo che un utente non debba eseguire alcuna azione per accedere, come ad esempio fornire le credenziali. Simili ai token di accesso, i token di aggiornamento contengono i dati che consentono a {{site.data.keyword.appid_short_notm}} di determinare se sei autorizzato. Tuttavia, questi token sono opachi.

I token di aggiornamento sono configurati per avere una durata maggiore rispetto a un token di accesso regolare, per cui quando un token di accesso scade, il token di aggiornamento sarà ancora valido e può essere utilizzato per rinnovare il token di accesso. I token di aggiornamento di {{site.data.keyword.appid_short_notm}} possono essere configurati per durare da 1 a 90 giorni. Per sfruttare appieno i token di aggiornamento, conserva i token per tutta la loro durata o finché non vengono rinnovati. Un utente non può accedere direttamente alle risorse con un solo token di aggiornamento, il che li rende molto più sicuri da conservare rispetto a un token di accesso. Come procedura ottimale, i token di aggiornamento devono essere memorizzati in modo sicuro dal client che li ha ricevuti e devono essere inviati solo al server di autorizzazione che li ha emessi.

Per ulteriore comodità, {{site.data.keyword.appid_short_notm}} rinnova anche il proprio token di aggiornamento — e la sua data di scadenza — quando viene rinnovato il token di accesso, consentendo all'utente di rimanere collegato finché sono attivi prima della scadenza del token di aggiornamento corrente. D'altra parte, se desideri utilizzare i token di aggiornamento per forzare l'utente ad accedere periodicamente, la tua applicazione potrebbe utilizzare solo i token di aggiornamento restituiti quando l'utente ha eseguito l'accesso immettendo le proprie credenziali. Tuttavia, ti consigliamo di utilizzare sempre il token di aggiornamento più recente ricevuto da {{site.data.keyword.appid_short_notm}}, come descritto dalle <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">Specifiche OAuth 2.0 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.


Sebbene questi token possano semplificare il processo di accesso, la tua applicazione non deve dipendere da essi, perché possono venire revocati in qualsiasi momento, come ad esempio quando credi che i tuoi token di aggiornamento siano stati compromessi. Se devi revocare un token di aggiornamento, esistono due modi per farlo. Se hai il token di aggiornamento, puoi revocarlo in base a <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. In alternativa, se hai l'ID utente, puoi revocare il token di aggiornamento utilizzando <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">l'API di gestione <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Per ulteriori informazioni sull'accesso all'API di gestione, consulta [gestione dell'accesso al servizio](/docs/services/appid?topic=appid-service-access-management#service-access-management).

Per esempi di utilizzo dei token di aggiornamento e di come usarli per implementare una funzionalità ricordami, consulta gli [esempi introduttivi](/docs/services/appid?topic=appid-getting-started#getting-started).


## Da dove provengono i token?
{: #where}

I token sono emessi tramite il server {{site.data.keyword.appid_short_notm}} OAuth e formattati come [JSON Web Tokens (JWT)](https://jwt.io/introduction/). I token sono stati firmati con la [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) con l'algoritmo RS256.

## Cosa succede alle informazioni contenute nel token?
{: #contains}

Il token di accesso contiene una serie di attestazioni JWT standard e una serie di attestazioni specifiche {{site.data.keyword.appid_short_notm}} come ad esempio un ID tenant. Il token di identità contiene le informazioni specifiche sull'utente. Le informazioni nei token vengono memorizzate come attestazioni che fanno parte di un [profilo dell'utente](/docs/services/appid?topic=appid-user-profile#user-profile).

## Come vengono ricevuti i token?
{: #received}

I token vengono ricevuti dalla tua applicazione dopo una corretta autenticazione. La tua applicazione può utilizzare i token per richiamare le informazioni sull'autorizzazione e l'autenticazione dell'utente. Il token di accesso può essere utilizzato per ottenere l'accesso alle risorse protette inviando una richiesta alla risorsa. Nella richiesta, il token di accesso viene descritto nello [schema di autenticazione della connessione](https://tools.ietf.org/html/rfc6750#page-5). Per estrarre i token, la tua applicazione deve analizzare l'intestazione.

Richiesta di esempio:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## Come vengono impostati i token?
{: #set}

Le configurazioni del token possono essere abilitate e disabilitate mediante il dashboard {{site.data.keyword.appid_short_notm}}. Per ulteriori informazioni sulle tue opzioni di configurazione, consulta [Gestione dei token](/docs/services/appid?topic=appid-managing-idp#managing-idp).
