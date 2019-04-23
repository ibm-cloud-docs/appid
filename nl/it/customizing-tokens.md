---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, tokens, access, claim, attributes

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


# Personalizzazione dei token
{: #customizing-tokens}

Puoi configurare i tuoi token {{site.data.keyword.appid_short_notm}} per soddisfare i bisogni specifici della tua applicazione.
{: shortdesc}

## Descrizione della personalizzazione
{: #understanding-customization}

{{site.data.keyword.appid_short_notm}} utilizza diversi tipi di token per proteggere le tue applicazioni.

* Token di accesso: abilitano la comunicazione con le risorse di backend protette dai filtri di autorizzazione. Se un token di accesso non è associato a un utente specifico, il token avrà delle funzionalità limitate.
* Token di identità: contengono le informazioni personali e sono utilizzati per autenticare un utente. A seconda della configurazione della tua applicazione, i token di identità possono essere emessi prima che un utente venga autenticato. Questo ti consente di iniziare l'associazione degli attributi con i tuoi utenti prima che accedano alla tua applicazione.
* Token di aggiornamento: possono essere utilizzati per estendere il periodo di tempo in cui un utente non ha bisogno di riautenticarsi.

Vuoi avere ulteriori informazioni sui token? Ulteriori informazioni in [Descrizione dei token](/docs/services/appid?topic=appid-tokens#tokens).
{: tip}


Puoi personalizzare i tuoi token [nella GUI](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-ui) oppure utilizzando [l'API](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-api) impostando la validità della durata o aggiungendo delle attestazioni personalizzate ai tuoi token. Controlla la seguente tabella per vedere come viene configurata la durata o continua a leggere per trovare ulteriori informazioni sull'associazione degli attributi personalizzati.

<table>
  <tr>
    <th>Tipo di token</th>
    <th>Tipo di valore</th>
    <th>Valore predefinito</th>
    <th>Opzioni</th>
  </tr>
  <tr>
    <td>Accesso</td>
    <td>Minuti</td>
    <td>60</td>
    <td>Qualsiasi valore compreso tra 5 e 1440</td>
  </tr>
  <tr>
    <td>Identità</td>
    <td>Minuti</td>
    <td>60</td>
    <td>Qualsiasi valore compreso tra 5 e 1440</td>
  </tr>
  <tr>
    <td>Aggiornamento</td>
    <td>Giorni</td>
    <td>30</td>
    <td>Qualsiasi valore compreso tra 1 e 9</td>
  </tr>
  <tr>
    <td>Anonimo</td>
    <td>Giorni</td>
    <td>30</td>
    <td>Qualsiasi valore compreso tra 1 e 9</td>
  </tr>
</table>


Poiché i token vengono utilizzati per identificare gli utenti e proteggere le tue risorse, la durata di un token influenza diverse cose. Personalizzando la tua configurazione del token puoi assicurarti che vengano soddisfati i tuoi bisogni di sicurezza e di esperienza utente. Tuttavia, se un token dovesse mai diventare compromesso, un utente malintenzionato ha più tempo per colpire la tua applicazione. Puoi trovare ulteriori informazioni sulle considerazioni relative alla sicurezza in [Attributi personalizzati](/docs/services/appid?topic=appid-custom-attributes).
{: important}


## Descrizione delle attestazioni e degli attributi personalizzati
{: #custom-claims}

Puoi associare degli attributi del profilo utente alle tue attestazioni del token di accesso e identità. Questo significa che non devi passare all'[endpoint /userinfo](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo) o eseguire il pull degli attributi personalizzati successivamente, perché sono archiviati già nei token.
{: shortdesc}

### Cos'è un'attestazione?
{: #custom-claims-defined}

Un'attestazione è una dichiarazione che un'entità fa su se stessa o per conto di qualcun altro. Ad esempio, se hai effettuato l'accesso in un'applicazione utilizzando un provider di identità, il provider invierà all'applicazione un gruppo di attestazioni o dichiarazioni sul tuo conto per consentirle di unirle alle informazioni che ti riguardano a essa già note. In questo modo, quando esegui l'accesso, l'applicazione viene configurata con le tue informazioni, nel modo in cui l'hai configurata. Consulta il seguente esempio per vedere come formattare l'oggetto JSON.

```
{
  "accessTokenClaims": [
            {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
          "idTokenClaims": [
            {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
  "access": {
    "expires_in": 3600
  },
  "refresh": {
    "expires_in": 2592000,
    "enabled": true
  },
  "anonymousAccess": {
    "expires_in": 2592000,
    "enabled": true
  }
}
```
{: screen}

Se hai personalizzato le informazioni di scadenza per il tuo token, devi impostarle in ogni richiesta. In caso contrario, questa richiesta sovrascrive la tua configurazione corrente e, per tutto quanto non è definito, viene utilizzato il valore predefinito.
{: note}

### Perché dovrei aggiungere delle attestazioni ai miei token?
{: #why-custom-claims}

Senza dover effettuare ulteriori chiamate di rete, tutto ciò che è necessario che la tua applicazione conosca su un utente o su cosa può fare, è già nel token. A condizione che tu non abbia una quantità enorme di dati, questo ti rende più efficiente. Inoltre, puoi garantire l'integrità di questi attributi associati quando vengono inviati attraverso la rete perché sono archiviati in un token firmato.


### Quali tipi di attestazioni posso definire?
{: #custom-claim-types}

Le attestazioni fornite da {{site.data.keyword.appid_short_notm}} rientrano in diverse categorie che vengono differenziate dal loro livello di personalizzazione.

*Attestazioni registrate*: esistono alcune attestazioni nei token di accesso e identità che vengono definite da {{site.data.keyword.appid_short_notm}} e che non possono essere sovrascritte dalle associazioni personalizzate. Se la tua attestazione è limitata, viene ignorata dal servizio. Le attestazioni sono `iss`, `aud`, `sub`, `iat`, `exp`, `amr` e `tenant`.

*Attestazioni limitate*: a seconda del token a cui sono associate le attestazioni, alcune di esse hanno delle possibilità di personalizzazione limitate. Per un token di accesso, `scope` è l'unica attestazione limitata. Non può essere sovrascritta dalle associazioni personalizzate, ma può essere estesa con i tuoi ambiti. Quando l'attestazione scope viene associata a un token di accesso, il valore deve essere una stringa e non può essere preceduta da `appid_` o sarà ignorata. Nei token di identità, le attestazioni `identities` e `oauth_clients` non possono essere modificate o sovrascritte.

*Attestazioni normalizzate*: ogni token di identità contiene una serie di attestazioni riconosciute da {{site.data.keyword.appid_short_notm}} come attestazioni normalizzate. Quando sono disponibili, vengono direttamente associate dal tuo provider di identità al token. Queste attestazioni non possono essere omesse in modo esplicito ma possono essere sovrascritte dalle associazioni delle attestazioni personalizzate. Le attestazioni includono `name`, `email`, `picture`, `local` e `gender`.


### Come vengono associate le attestazioni ai token?
{: #custom-claims-mapping}

Ogni associazione viene definita da un oggetto dell'origine dati e da un chiave utilizzata per richiamare l'attestazione. Ogni attestazione personalizzata viene impostata per ogni token separatamente e vengono applicate in sequenza. Puoi registrare fino a 100 attestazioni per ogni token fino a un payload massimo di 100KB.

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Icona idea"/> Descrizione degli oggetti dell'associazione dell'attestazione</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>Valore obbligatorio</td>
        <td>Definisce l'origine dell'attestazione. Può fare riferimento alle informazioni utente del provider di identità o agli attributi personalizzati {{site.data.keyword.appid_short_notm}} dell'utente. </br> Le opzioni includono: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid` e `attributes`.</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>Valore obbligatorio</td>
        <td>Definisce l'attestazione dei dati di origine. </td>
      </tr>
    </tbody>
  </table>

Puoi fare riferimento alle attestazioni nidificate nelle tue associazioni utilizzando la sintassi dot. Esempio: `nested.attribute`
{:tip}

</br>

## Configurazione dei token {{site.data.keyword.appid_short_notm}}
{: #configuring-tokens}

Puoi configurare i tuoi token {{site.data.keyword.appid_short_notm}} utilizzando la GUI o le API di gestione.
{: shortdesc}


### Configurazione della durata del token con la GUI.
{: #configuring-tokens-ui}

1. Passa al tuo dashboard del servizio.
2. Nella sezione **Identity Providers** della navigazione, seleziona la pagina **Manage**.
3. Nella scheda **Settings** configura i tuoi token.
  1. Per consentire l'accesso senza il bisogno di un'interazione da parte dell'utente, imposta **refresh tokens** su **On**.
  2. Imposta la tua durata del token di aggiornamento. La scadenza viene impostata in giorni e può essere un qualsiasi valore compreso nell'intervallo tra 1 e 90. Più piccolo è il numero, maggiore è la frequenza in cui un utente deve accedere.
  3. Imposta la tua durata del token di accesso. La scadenza viene impostata in minuti e può essere un valore compreso nell'intervallo tra 5 e 1440. Più piccolo è il valore e maggiore è la protezione che hai in caso di furto del token.
  4. Imposta la tua durata del token anonimo. Viene assegnato un [token anonimo](/docs/services/appid?topic=appid-anonymous#anonymous) agli utenti nel momento in cui iniziano ad interagire con la tua applicazione. Quando un utente accede, le informazioni nel token anonimo vengono poi trasferite al token associato all'utente. La scadenza viene impostata in giorni e può essere un qualsiasi compreso tra 1 e 90.

</br>

### Configurazione dei token con le API di gestione
{: #configuring-tokens-api}

**Prima di cominciare**

Assicurati di aver i seguenti prerequisiti:

* L'ID tenant della tua istanza {{site.data.keyword.appid_short_notm}}. Può essere trovato nella sezione **Service Credentials** della GUI.
* Il tuo token IAM (Identity and Access Management). Per un aiuto nell'ottenimento del token IAM, consulta la [Documentazione IAM](/docs/iam?topic=iam-iamtoken_from_apikey).

**Associazione delle tue intestazioni**

1. Esegui una richiesta PUT all'endpoint `/config/tokens` con la tua configurazione del token.

  Intestazione:
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  Corpo:
  ```
   {
       "access": {
           "expires_in": 3600,
       },
       "refresh": {
           "expires_in": 2592000,
           "enabled": true
       },
       "anonymous": {
           "expires_in": 2592000,
           "enabled": true
       },
       "accessTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "name_id"
           }
       ],
       "idTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "attributes.uid"
           }
       ]
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Icona idea"/> Descrizione della configurazione del token</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>Facoltativo</td>
        <td>L'oggetto che contiene la data di scadenza, `expires_in`, in minuti dei tuoi token di accesso e identità. </br> </br> La scadenza predefinita è 60 minuti. </td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>Facoltativo</td>
          <td>L'oggetto che contiene la data di scadenza, `expires_in`, in giorni del tuo token di aggiornamento. </br> </br> La scadenza predefinita è 30 giorni. </td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>Facoltativo</td>
          <td>L'oggetto che contiene la data di scadenza, `expires_in`, in giorni dei tuoi token di accesso e identità anonimi. </br> </br> La scadenza predefinita è 30 giorni.
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>Facoltativo</td>
          <td>Un array che contiene gli oggetti creati quando vengono associate le attestazioni correlate ai token di accesso.</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>Facoltativo</td>
          <td>Un array che contiene gli oggetti creati quando vengono associate le attestazioni correlate ai token di identità.</td>
      </tr>
    </tbody>
  </table>

  Richiesta di esempio:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
            }
          ],
          "idTokenClaims": [
            {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
  }' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
