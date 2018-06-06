---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Autorizzazione e autenticazione
{: authorization}

Con {{site.data.keyword.appid_full}}, gli utenti possono utilizzare i token e i filtri di autorizzazione per assicurarsi che le proprie applicazioni siano protette. Prima che un utente possa concedere l'autorizzazione, la sua identità deve essere autenticata da un provider di identità.
{: shortdesc}


## Concetti chiave
{: key-concepts}

Per capire realmente il modo in cui il servizio suddivide il processo di autorizzazione e autenticazione, dovrai comprendere alcuni termini chiave.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> è un protocollo open standard utilizzato per fornire l'autorizzazione dell'applicazione.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> è un livello di autenticazione che funziona con OAuth 2.</dd>
  <dt>Token di accesso</dt>
    <dd><p>I token di accesso rappresentano l'autorizzazione e abilitano la comunicazione con le [risorse di back-end](/docs/services/appid/protecting-resources.html) protette dai filtri di autorizzazione impostati da {{site.data.keyword.appid_short}}. Il token è conforme alle specifiche JavaScript Object Signing and Encryption (JOSE). I token sono creati come <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.</br>
    Esempio:</p>
    <pre><code>Header: {
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
    </code></pre></dd>
  <dt>Token di identità</dt>
    <dd><p>I token di identità rappresentano l'autenticazione e contengono le informazioni sull'utente. Può fornirti le informazioni sui loro nome, email, sesso e ubicazione. Un token può anche restituire un URL a un'immagine dell'utente.</br>
    Esempio:</p>
    <pre><code>Header: {
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
    </pre></code></dd>
  <dt>Intestazioni di autorizzazione </dt>
    <dd><p>{{site.data.keyword.appid_short}} è conforme alla <a href="https://tools.ietf.org/html/rfc6750" target="blank">specifica di connessione del token <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e utilizza una combinazione di token di accesso e di identità che vengono inviati come un'intestazione di autorizzazione HTTP. L'intestazione di autorizzazione contiene tre parti diverse che sono separate da spazi vuoti. I token sono codificati base64. Il token di identità è facoltativo.</br>
    Esempio:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>Strategia API </dt>
    <dd><p>La strategia API si attende che le richieste contengano un'intestazione di autorizzazione con un token di accesso valido. La richiesta può includere anche un token di identità, ma non è obbligatorio. Se un token non è valido o è scaduto, la strategia dell'API restituisce un errore HTTP 401 che contiene la seguente intestazione HTTP: </p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>Se la richiesta restituisce un token valido, il controllo viene passato al prossimo middleware e la proprietà <code>appIdAuthorizationContext</code> viene trasmessa nell'oggetto della richiesta. Questa proprietà contiene i token di identità e di accesso originali e le informazioni sul payload decodificate come oggetti JSON semplici.</dd>
  <dt>Strategia applicazione web</dt>
    <dd>Quando la strategia dell'applicazione web individua dei tentativi non autenticati di accesso a una risorsa protetta, automaticamente esegue il reindirizzamento a un browser dell'utente alla pagina di autenticazione, che può essere fornita da {{site.data.keyword.appid_short}}. Dopo un'autenticazione corretta, l'utente viene riportato all'URL di callback dell'applicazione web. La strategia dell'applicazione web ottiene i token di accesso e di identità e li archivia in una sessione HTTP in <code>WebAppStrategy.AUTH_CONTEXT</code>. Spetta all'utente decidere se archiviare i token di accesso e di identità nel database dell'applicazione. </dd>
</dl>

</br>

## Come funziona il processo
{: #process}

Quando si codificano le applicazioni, una delle preoccupazioni più grandi è la sicurezza. Come puoi assicurarti che solo chi dispone dell'accesso corretto, stia utilizzando la tua applicazione? Utilizzi un processo di autorizzazione. In molte applicazioni, il processo di autorizzazione e di autenticazione sono legati tra loro; rendendo le modifiche alle tue politiche di sicurezza e ai provider di identità complicate. Con {{site.data.keyword.appid_short}}, l'autorizzazione e l'autenticazione sono processi separati.
{: shortdesc}

Quando configuri i provider di identità sociali come Facebook, viene utilizzato [Oauth2 Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) per richiamare il widget di accesso. Con Cloud Directory come tuo provider di identità, [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) viene utilizzato per fornire i token di accesso e di identità.

![Il percorso per diventare un utente identificato.](/images/authenticationtrail.png)

Quando un utente sceglie di accedere, diventa un utente identificato. Le informazioni sull'utente si ottengono dal provider di identità con cui hanno eseguito l'accesso. Il provider di identità restituisce i token di accesso e di identità a {{site.data.keyword.appid_short}} che contengono le informazioni sull'utente. Il servizio prende i token forniti e determina se un utente dispone delle credenziali corrette per accedere a un'applicazione. Se i token vengono convalidati, il servizio autorizza l'accesso agli utenti. Dopo che un utente è stato autorizzato, le relative informazioni di autenticazione vengono associate a un record utente. È possibile accedere al record utente e ai relativi attributi ancora da qualsiasi client che si autentica con la stessa identità. 

### Autenticazione progressiva

Con {{site.data.keyword.appid_short_notm}}, un utente anonimo può scegliere di diventare un utente identificato.

Ma come funziona?

Quando un utente sceglie di non accedere immediatamente, viene considerato un utente anonimo. Ad esempio, un utente può immediatamente iniziare ad aggiungere elementi a un carrello d'acquisto senza dover accedere. Per gli utenti anonimi, {{site.data.keyword.appid_short_notm}} crea un record utente ad hoc e richiama l'API di accesso OAuth che restituisce i token di identità e di accesso anonimi. Utilizzando quei token, l'applicazione può creare, leggere, aggiornare ed eliminare gli attributi che sono archiviati nel record utente.

![Il percorso per diventare un utente identificato quando iniziano come anonimi.](/images/anon-authenticationtrail.png)

Quando un utente anonimo accede, il token di accesso anonimo viene passato all'API di accesso. Il servizio autentica la chiamata con un provider di identità. Il servizio utilizza il token di accesso per trovare il record anonimo e allega l'identità ad esso. I nuovi token di identità e di accesso contengono le informazioni pubbliche condivise dal provider di identità. Dopo che un utente è stato identificato, i suoi token anonimi diventano non validi. Tuttavia, un utente è ancora in grado di accedere ai propri attributi perché sono accessibili con il nuovo token.

**Nota**: un'identità può essere assegnata solo a un record anonimo se non è ancora stata assegnata a un altro utente. Se l'identità è già associata a un altro utente {{site.data.keyword.appid_short_notm}}, i token contengono le informazioni di tale record utente e forniscono l'accesso a suoi attributi. I precedenti attributi degli utenti anonimi non sono accessibili tramite il nuovo token. Finché il token non scade, le informazioni possono ancora essere associate tramite il token di accesso anonimo. Durante lo sviluppo, puoi scegliere come unire gli attributi anonimi all'utente conosciuto.
