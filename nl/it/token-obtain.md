---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-29"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}



# Ottenimento dei token
{: #obtain-tokens}

Quando gli utenti e i servizi di backend interagiscono con la tua applicazione, potrebbero dover essere autorizzati per eseguire azioni specifiche. {{site.data.keyword.appid_short_notm}} verifica che l'entità che effettua la richiesta sia autorizzata e restituisce i token di accesso e identità alla tua applicazione. Se l'entità che effettua la richiesta è un utente finale, i token potrebbero contenere delle informazioni sull'utente, ad esempio l'ambito delle loro autorizzazioni e il loro nome. Se si tratta di un servizio di backend, viene restituito solo un token di accesso.
{: shortdesc}


## Ottenimento del tuo segreto e del tuo ID client
{: #obtain-clientid-secret}

Per poter ottenere i token, devi avere i tuoi segreto e ID client. Le credenziali sono specifiche per ogni applicazione e vengono utilizzate per identificare e convalidare gli utenti a cui potrebbe essere assegnato un token. 
{: shortdesc}


### Utilizzando la GUI
{: #credentials-gui}

1. Passa alla scheda **Applications** del dashboard {{site.data.keyword.appid_short_notm}}.

2. Se hai già una serie di credenziali elencate, puoi andare al passo 3. Se non è così, creane una.
    1. Sulla scheda **Applications**, fai clic su **Add application**.
    2. Fornisci alla tua applicazione un nome e fai clic su **Save** per ritornare a un elenco di tue applicazioni registrate. Il nome della tua applicazione non può superare i 50 caratteri.

3. Dall'elenco delle applicazioni registrate, seleziona l'applicazione con cui vuoi lavorare. La riga si espande per mostrare le tue credenziali.

4. Copia il tuo ID e il tuo segreto client.


### Utilizzando l'API
{: #credentials-api}

1.  Esegui una richiesta POST all'endpoint [`/management/v4/{tenantId}/applications`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication).

  Richiesta:

  ```
  curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  Risposta di esempio:

  ```
  {
    "clientId": "c90830bf-11b0-4b65-bffe-9773f8703bad",
    "tenantId": "b42f7429-fc24-48ds-b4f9-616bcc31cfd5",
    "secret": "YWQyNjdkZjMtMGRhZC00ZWRkLThiOTQtN2E3ODEyZjhkOWQz",
    "name": "testing",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48ds-b4f9-616bcb31cfd5",
    "profilesUrl": "https://us-south.appid.cloud.ibm.com",
    "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48ds-b4f9-616bcb31cfd5/.well-known/openid-configuration"
  }
  ```
  {: screen}

2. Copia l'ID e il segreto client.



## Ottenimento dei token di accesso e identità
{: #obtain-access-id-tokens}

Con un ID e un segreto client, puoi ottenere i token di accesso e identità utilizzando la seguente procedura.
{: shortdesc}


### Ottenimento dei token utilizzando un SDK
{: obtain-token-sdk}

1. Ottieni l'ID tenant, l'ID client, il segreto e l'URL del server OAuth dalle tue credenziali.

2. Utilizzando le informazioni dal passo 1, aggiorna il seguente frammento di codice e aggiungilo alla tua applicazione. Il codice predefinito è per Node.js. Se stai utilizzando un altro linguaggio, puoi scegliere quello che ti è stato applicato all'inizio di questo argomento.

  Node:
  {: ph data-hd-programlang='javascript'}

  ```
  const config = {
    tenantId: "{tenant-id}",
    clientId: "{client-id}",
    secret: "{secret}",
    oauthServerUrl: "{oauth-server-url}"
  };

  const TokenManager = require('ibmcloud-appid').TokenManager;

  const tokenManager = new TokenManager(config);

  async function getAppIdentityToken() {
    try {
        const tokenResponse = await tokenManager.getApplicationIdentityToken();
        console.log('Token response : ' + JSON.stringify(tokenResponse));

        //the token response contains the access_token, expires_in, token_type
    } catch (err) {
        console.log('err obtained : ' + err);
    }
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

  Java:
  {: ph data-hd-programlang='java'}
  ```
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
    @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
        //Si è verificata un'eccezione
      }

    @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
        //Utente autenticato
        }
  });
  ```
  {: codeblock}
  {: ph data-hd-programlang='java'}

iOS Swift:
{: ph data-hd-programlang='swift'}

  ```
  class delegate : TokenResponseDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
    //Utente autenticato
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
    //Si è verificata un'eccezione
      }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

Server Swift:
{: ph data-hd-programlang='swift'}

  ```
  let options = [
    "clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}


</br>

### Ottenimento dei token utilizzando l'API
{: #obtain-tokens-api}

1. Ottieni l'ID tenant, l'ID client, il segreto e l'URL del server OAuth dalle tue credenziali.

2. Codifica il tuo ID client e il tuo segreto.

    1. Copia il tuo ID e il tuo segreto client utilizzando la procedura dalla precedente sezione.
    2. Utilizza un codificatore base64 per codificare le tue informazioni di autorizzazione.
    3. Copia l'output.

3. Effettua una richiesta all'API per ottenere un token. La sezione dei dati della tua richiesta varia a seconda del tipo di concessione che stai utilizzando. 

  ```
  curl -X POST \
  https://{region}.appid.cloud.ibm.com/oauth/v4/{tenant_id}/token \
  -H 'Authorization: Basic base64Encoded{{client-ID}:{client-secret}}' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H `Accept: application/json` \
  -F grant_type=password \
  -F username=testuser@test.com \
  -F password=testuser
  ```
  {: codeblock}

Il tipo di concessione che utilizzi per ottenere il tuo token può variare a seconda del tipo di autorizzazione che stai utilizzando. Per un elenco dettagliato di opzioni, consulta la [documentazione swagger](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token).
