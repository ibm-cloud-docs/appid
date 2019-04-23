---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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
    <p>Quando utilizzi insieme OIDC e {{site.data.keyword.appid_short_notm}}, le tue credenziali dell'applicazione ti aiutano a configurare i tuoi endpoint OAuth. Quando utilizzi l'SDK, gli URL dell'endpoint vengono creati automaticamente. Tuttavia, puoi anche creare gli URL utilizzando le tue credenziali di servizio.</p> <p>L'URL assume il seguente formato: {{site.data.keyword.appid_short_notm}} service endpoint + "/oauth/v4" + /tenantID.</p>
    <p><pre class="codeblock">
    <code>{
      "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
      "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
      "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
      "name":testing",
      "oAuthServerUrl": "https://us-south.appid-oauth.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
      "profilesUrl": "https://us-south.appid.cloud.ibm.com",
      "discoveryEndpoint": "https://us-south.appid-oauth.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
    }</code></pre></p>
    <p>Utilizzando questo esempio, l'URL sarà <code>https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0</code>. Accoderai quindi l'endpoint a cui volevi eseguire una richiesta. Consulta la seguente tabella per vedere qualche endpoint di esempio.</p>
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
        <td>Informazioni utente</td>
        <td>{oauthServerUrl}/userinfo</td>
      </tr>
      <tr>
        <td>JWKS</td>
        <td>{oauthServerUrl}/publickeys</td>
      </tr>
    </table>
    <p><strong>Nota</strong>: quando utilizzi l'SDK, gli URL dell'endpoint vengono creati automaticamente.</p></dd>
  <dt>Token</dt>
    <dd>Il servizio utilizza tre diversi tipi di token. I token di accesso rappresentano l'autorizzazione e abilitano la comunicazione con le [risorse di backend](/docs/services/appid?topic=appid-backend) che sono protette dai filtri di autorizzazione impostati da {{site.data.keyword.appid_short}}. I token di identità rappresentano l'autenticazione e contengono le informazioni sull'utente. È possibile utilizzare un token di aggiornamento per ottenere un nuovo token di accesso senza riautenticare l'utente. Utilizzando i token di aggiornamento, gli utenti possono consentire che le relative informazioni vengano ricordate dall'applicazione. In questo modo possono rimanere collegati. I token sono impostati in <b>Identity Providers > Manage</b> del dashboard {{site.data.keyword.appid_short}}. Per ulteriori informazioni sui token e su come vengono utilizzati in {{site.data.keyword.appid_short}}, consulta [Gestione dei token](/docs/services/appid?topic=appid-tokens#tokens).
  </dd>
  <dt>Intestazioni di autorizzazione</dt>
    <dd><p>{{site.data.keyword.appid_short}} è conforme alla <a href="https://tools.ietf.org/html/rfc6750" target="blank">specifica di connessione del token <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e utilizza una combinazione di token di accesso e di identità che vengono inviati come un'intestazione di autorizzazione HTTP. L'intestazione di autorizzazione contiene tre parti diverse che sono separate da spazi vuoti. I token sono codificati base64. Il token di identità è facoltativo.</br>
    Esempio:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</code></pre></dd>
  <dt>Strategia API</dt>
    <dd><p>La strategia API si attende che le richieste contengano un'intestazione di autorizzazione con un token di accesso valido. La richiesta può includere anche un token di identità, ma non è obbligatorio. Se un token non è valido o è scaduto, la strategia dell'API restituisce un errore HTTP 401 che contiene la seguente intestazione HTTP:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>Se la richiesta restituisce un token valido, il controllo viene passato al prossimo middleware e la proprietà <code>appIdAuthorizationContext</code> viene trasmessa nell'oggetto della richiesta. Questa proprietà contiene i token di identità e di accesso originali e le informazioni sul payload decodificate come oggetti JSON semplici.</dd>
  <dt>Strategia applicazione web</dt>
    <dd>Quando la strategia dell'applicazione web individua dei tentativi non autenticati di accesso a una risorsa protetta, automaticamente esegue il reindirizzamento a un browser dell'utente alla pagina di autenticazione, che può essere fornita da {{site.data.keyword.appid_short}}. Dopo un'autenticazione corretta, l'utente viene riportato all'URL di callback dell'applicazione web. La strategia dell'applicazione web ottiene i token di accesso e di identità e li archivia in una sessione HTTP in <code>WebAppStrategy.AUTH_CONTEXT</code>. Spetta all'utente decidere se archiviare i token di accesso e di identità nel database dell'applicazione.</dd>
  <dt>Codifica e separazione dei dati</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} archivia e codifica gli attributi del profilo utente. Come un servizio a più tenant, ogni tenant ha una chiave di codifica e i dati utente in ogni tenant sono codificati con solo tale chiave.</p>
    <p>{{site.data.keyword.appid_short_notm}} assicura che le informazioni private siano codificate prima dell'archiviazione.</p></dd>
  <dt>URI di reindirizzamento</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} utilizza un elenco di URI completi e approvati per reindirizzare i tuoi utenti dopo un'interazione con la tua applicazione. Ad esempio, se l'utente esegue l'accesso correttamente, {{site.data.keyword.appid_short_notm}} lo reindirizza alla home page della tua applicazione oppure a un'altra pagina da te specificata. Il formato del tuo URI potrebbe variare a seconda della tua applicazione. Per ulteriori informazioni, consulta [Aggiunta di URI di reindirizzamento](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).</p></dd>
  <dt>JWKS (JSON Web Key Set)</dt>
    <dd>Un JWKS rappresenta un insieme di chiavi crittografiche. {{site.data.keyword.appid_short_notm}} utilizza un JWKS per verificare l'autenticità dei token generati dal servizio. Utilizzando l'ID chiave per verificare la firma, possiamo garantire che il token sia stato emesso da una fonte ritenuta attendibile, {{site.data.keyword.appid_short_notm}}, e che le informazioni all'interno del token non siano mai state modificate.</dd>
</dl>

