---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}




# Concetti chiave
{: #key-concepts}

Sei confuso circa le differenze tra autorizzazione e autenticazione? Non sei il solo. Consulta le informazioni su questa pagina per conoscere la terminologia specifica, i processi e il modo in cui il servizio utilizza i token.
{: shortdesc}


## Terminologia
{: #terms}


Questi termini chiave possono aiutarti a comprendere il modo in cui il servizio suddivide il processo di autorizzazione e autenticazione.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> è un protocollo open standard utilizzato per fornire l'autorizzazione dell'applicazione.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> è un livello di autenticazione che funziona con OAuth 2.</p>
    <p>Quando utilizzi contemporaneamente OIDC e {{site.data.keyword.appid_short_notm}}, le tue credenziali del servizio ti consentono di configurare i tuoi endpoint OAuth. Quando utilizzi l'SDK, gli URL dell'endpoint vengono creati automaticamente. Tuttavia, puoi anche creare gli URL utilizzando le tue credenziali di servizio. Puoi visualizzare il modo in cui assemblare l'URL nei seguenti esempio e tabella.</p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
      "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
      "profilesUrl": "https://appid-profiles.ng.bluemix.net/"
    }</code></pre>
    <table>
      <tr>
        <th>Endpoint</th>
        <th>Formato</th>
      </tr>
      <tr>
        <td>Autorizzazione</td>
        <td>{oauthServerUrl}/authorization</td>
      </tr>
      <tr>
        <td>Token</td>
        <td>{oauthServerUrl}/token</td>
      </tr>
      <tr>
        <td>Userinfo</td>
        <td>{oauthServerUrl}/userinfo</td>
      </tr>
      <tr>
        <td>JWKS</td>
        <td>{oauthServerUrl}/publickeys</td>
      </tr>
    </table>
    <p><strong>Nota</strong>: quando utilizzi l'SDK, gli URL dell'endpoint vengono creati automaticamente.</p></dd>
  <dt>Token</dt>
    <dd>Il servizio utilizza tre diversi tipi di token. I token di accesso rappresentano l'autorizzazione e abilitano la comunicazione con le [risorse di back-end](/docs/services/appid/backend-apps.html) che sono protette dai filtri di autorizzazione impostati da {{site.data.keyword.appid_short}}. I token di identità rappresentano l'autenticazione e contengono le informazioni sull'utente. È possibile utilizzare un token di aggiornamento per ottenere un nuovo token di accesso senza riautenticare l'utente. Utilizzando i token di aggiornamento, gli utenti possono consentire che le relative informazioni vengano ricordate dall'applicazione. In questo modo possono rimanere collegati. Per ulteriori informazioni sui token e su come vengono utilizzati in {{site.data.keyword.appid_short}}, consulta [Convalida dei token](tokens.html#remote-validation).
  </dd>
  <dt>Intestazioni di autorizzazione</dt>
    <dd><p>{{site.data.keyword.appid_short}} è conforme alla <a href="https://tools.ietf.org/html/rfc6750" target="blank">specifica di connessione del token <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e utilizza una combinazione di token di accesso e di identità che vengono inviati come un'intestazione di autorizzazione HTTP. L'intestazione di autorizzazione contiene tre parti diverse che sono separate da spazi vuoti. I token sono codificati base64. Il token di identità è facoltativo.</br>
    Esempio:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>Strategia API</dt>
    <dd><p>La strategia API si attende che le richieste contengano un'intestazione di autorizzazione con un token di accesso valido. La richiesta può includere anche un token di identità, ma non è obbligatorio. Se un token non è valido o è scaduto, la strategia dell'API restituisce un errore HTTP 401 che contiene la seguente intestazione HTTP:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>Se la richiesta restituisce un token valido, il controllo viene passato al prossimo middleware e la proprietà <code>appIdAuthorizationContext</code> viene trasmessa nell'oggetto della richiesta. Questa proprietà contiene i token di identità e di accesso originali e le informazioni sul payload decodificate come oggetti JSON semplici.</dd>
  <dt>Strategia applicazione web</dt>
    <dd>Quando la strategia dell'applicazione web individua dei tentativi non autenticati di accesso a una risorsa protetta, automaticamente esegue il reindirizzamento a un browser dell'utente alla pagina di autenticazione, che può essere fornita da {{site.data.keyword.appid_short}}. Dopo un'autenticazione corretta, l'utente viene riportato all'URL di callback dell'applicazione web. La strategia dell'applicazione web ottiene i token di accesso e di identità e li archivia in una sessione HTTP in <code>WebAppStrategy.AUTH_CONTEXT</code>. Spetta all'utente decidere se archiviare i token di accesso e di identità nel database dell'applicazione.</dd>
  <dt>Codifica e separazione dei dati</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} archivia e codifica gli attributi del profilo utente. Come un servizio a più tenant, ogni tenant ha una chiave di codifica e i dati utente in ogni tenant sono codificati con solo tale chiave.</p>
    <p>{{site.data.keyword.appid_short_notm}} assicura che le informazioni private siano codificate prima dell'archiviazione.</p></dd>
</dl>

</br>
</br>


## Descrizione dei token
{: #tokens}

Quando un utente viene correttamente autenticato, l'applicazione riceve i token da {{site.data.keyword.appid_short_notm}}. Il servizio utilizza tre tipi principali di token per completare il processo di autenticazione.
{: shortdesc}


**Cos'è un token di accesso?**

I token di accesso rappresentano l'autorizzazione e abilitano la comunicazione con le [risorse di back-end](/docs/services/appid/backend-apps.html) che sono protette dai filtri di autorizzazione impostati da {{site.data.keyword.appid_short}}. Il token è conforme alle specifiche JavaScript Object Signing and Encryption (JOSE). Il token viene creato come <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> firmati con un chiave web JSON che utilizza l'algoritmo RS256.

Token di esempio:
  ```
  Intestazione: {
      "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "exp": "1495562664",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "amr": ["facebook"],
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "iat": "1495559064",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
  ```
  {: screen}

**Cos'è un token di identità?**

I token di identità rappresentano l'autenticazione e contengono le informazioni sull'utente. Può fornirti le informazioni sui loro nome, email, sesso e ubicazione. Un token può anche restituire un URL a un'immagine dell'utente. Il token viene creato come <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> firmati con un chiave web JSON che utilizza l'algoritmo RS256.

Token di esempio:
  ```
  Intestazione: {
      "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "exp: "1495562664",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "iat": "1495559064",
      "name": "John Smith",
      "email": "js@mail.com",
      "gender", "male",
      "locale": "en",
      "picture": "<URL-to-photo>",
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "identities": [
          "provider": "facebook"
          "id": "377440159275659"
      ],
      "amr": ["facebook"],
      "oauth_client":{
        "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
  }
  ```
  {: screen}

I token di identità contengono solo delle informazioni utente parziali. Per visualizzare tutte le informazioni fornite dal provider di identità, puoi utilizzare l'[endpoint sulle informazioni utente](/docs/services/appid/predefined.html#api).

**Cos'è un token di aggiornamento?**

{{site.data.keyword.appid_short}} supporta la capacità di acquisire nuovi token di accesso e identità senza la riautenticazione, come definito in <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Un token di aggiornamento può essere utilizzato per rinnovare il token di accesso in modo che un utente non debba eseguire alcuna azione per accedere, come ad esempio fornire le credenziali. Simili ai token di accesso, i token di aggiornamento contengono i dati che consentono a {{site.data.keyword.appid_short_notm}} di determinare se sei autorizzato. Tuttavia, questi token sono opachi.

I token di aggiornamento sono configurati per avere una durata maggiore rispetto a un token di accesso regolare, per cui quando un token di accesso scade, il token di aggiornamento sarà ancora valido e può essere utilizzato per rinnovare il token di accesso. I token di aggiornamento di {{site.data.keyword.appid_short_notm}} possono essere configurati per durare da 1 a 90 giorni. Per sfruttare appieno i token di aggiornamento, conserva i token per tutta la loro durata o finché non vengono rinnovati. Un utente non può accedere direttamente alle risorse con un solo token di aggiornamento, il che li rende molto più sicuri da conservare rispetto a un token di accesso. Come procedura ottimale, i token di aggiornamento devono essere memorizzati in modo sicuro dal client che li ha ricevuti e devono essere inviati solo al server di autorizzazione che li ha emessi.

Per ulteriore comodità, {{site.data.keyword.appid_short_notm}} rinnova anche il proprio token di aggiornamento — e la sua data di scadenza — quando viene rinnovato il token di accesso, consentendo all'utente di rimanere collegato finché sono attivi prima della scadenza del token di aggiornamento corrente. D'altra parte, se desideri utilizzare i token di aggiornamento per forzare l'utente ad accedere periodicamente, la tua applicazione potrebbe utilizzare solo i token di aggiornamento restituiti quando l'utente ha eseguito l'accesso immettendo le proprie credenziali. Tuttavia, ti consigliamo di utilizzare sempre l'ultimo token di aggiornamento ricevuto da App ID, come descritto dalle <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">Specifiche Oauth <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.


Sebbene questi token possano semplificare il processo di accesso, la tua applicazione non deve dipendere da essi, perché possono venire revocati in qualsiasi momento, come ad esempio quando credi che i tuoi token di aggiornamento siano stati compromessi. Se devi revocare un token di aggiornamento, esistono due modi per farlo. Se hai il token di aggiornamento, puoi revocarlo in base a <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. In alternativa, se hai l'ID utente, puoi revocare il token di aggiornamento utilizzando <a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="_blank">l'API di gestione <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Per ulteriori informazioni sull'accesso all'API di gestione, consulta [gestione dell'accesso al servizio](iam.html#service-access-management).

Per esempi di utilizzo dei token di aggiornamento e di come usarli per implementare una funzionalità ricordami, consulta gli [esempi introduttivi](index.html).


**Da dove provengono i token?**

I token sono emessi tramite il server {{site.data.keyword.appid_short_notm}} OAuth e formattati come [JSON Web Tokens (JWT)](https://jwt.io/introduction/). I token sono stati firmati con la [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) con l'algoritmo RS256.

**Cosa succede alle informazioni contenute nel token?**

Il token di accesso contiene una serie di attestazioni JWT standard e una serie di attestazioni specifiche {{site.data.keyword.appid_short_notm}} come ad esempio un ID tenant. Il token di identità contiene le informazioni specifiche sull'utente. Le informazioni nei token vengono memorizzate come attestazioni che fanno parte di un [profilo dell'utente](/docs/services/appid/user-profile.html).

**Come vengono ricevuti i token?**

I token vengono ricevuti dalla tua applicazione dopo una corretta autenticazione. La tua applicazione può utilizzare i token per richiamare le informazioni sull'autorizzazione e l'autenticazione dell'utente. Il token di accesso può essere utilizzato per ottenere l'accesso alle risorse protette inviando una richiesta alla risorsa. Nella richiesta, il token di accesso viene descritto nello [schema di autenticazione della connessione](https://tools.ietf.org/html/rfc6750#page-5). Per estrarre i token, la tua applicazione deve analizzare l'intestazione.

Richiesta di esempio:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

</br>
</br>
