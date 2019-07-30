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



# Tokens abrufen
{: #obtain-tokens}

Wenn Benutzer oder Back-End-Services mit der App interagieren, müssen sie möglicherweise berechtigt sein, bestimmte Aktionen auszuführen. Von {{site.data.keyword.appid_short_notm}} wird überprüft, ob die Entität, von der die Anforderung erstellt wird, dazu berechtigt ist, und Zugriffs- sowie Identitätstoken an die App zurückgegeben. Wenn es sich bei der Entität, von der die Anforderung erstellt wird, um einen Endbenutzer handelt, enthalten die Tokens möglicherweise Informationen zu dem Benutzer, zum Beispiel den Umfang einer Berechtigungen und seinen Namen. Wenn es sich um einen Back-End-Service handelt, wird nur ein Zugriffstoken zurückgegeben.
{: shortdesc}


## Client-ID und geheimen Schlüssel abrufen
{: #obtain-clientid-secret}

Damit Sie Tokens abrufen können, müssen Sie über eine Client-ID und einen geheimen Schlüssel verfügen. Die Berechtigungsnachweise sind für jede einzelne Anwendung spezifisch und werden dazu verwendet, die Benutzer zu identifizieren und zu überprüfen, denen möglicherweise ein Token zugeordnet wird. 
{: shortdesc}


### Mit der grafischen Benutzerschnittstelle
{: #credentials-gui}

1. Navigieren Sie zur Registerkarte **Anwendungen** des {{site.data.keyword.appid_short_notm}}-Dashboards.

2. Wenn bereits ein Satz an Berechtigungsnachweisen aufgelistet wird, können Sie mit Schritt 3 fortfahren; ist dies nicht der Fall, erstellen Sie diese.
    1. Klicken Sie in der Registerkarte **Anwendungen** auf **Anwendung hinzufügen**.
    2. Legen Sie für die Anwendung einen Namen fest und klicken Sie auf **Speichern**, um zur Liste der registrierten Apps zurückzukehren. Der Name Ihrer Anwendung darf nicht mehr als 50 Zeichen lang sein.

3. Wählen Sie in der Liste der registrierten Apps die Anwendung aus, mit der Sie arbeiten möchten. Die erweiterte Zeile zeigt Ihre Berechtigungsnachweise an.

4. Kopieren Sie Ihre Client-ID und Ihren geheimen Schlüssel.


### Mit der API
{: #credentials-api}

1.  Erstellen Sie eine POST-Anforderung an den [Endpunkt `/management/v4/{tenantId}/applications`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication).

  Anforderung:

  ```
  curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  Beispielantwort:

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

2. Kopieren Sie die Client-ID und den geheimen Schlüssel.



## Zugriffs- und Identitätstoken abrufen
{: #obtain-access-id-tokens}

Mit einer Client-ID und einem geheimen Schlüssel können Sie durch Ausführen der folgenden Schritte die Zugriffs- und Identitätstoken abrufen.
{: shortdesc}


### Tokens mit SDK abrufen
{: obtain-token-sdk}

1. Rufen Sie Ihre Tenant-ID, Ihre Client-ID, den geheimen Schlüssel und die OAuth-Server-URL von Ihren Berechtigungsnachweisen ab.

2. Aktualisieren Sie mithilfe der Informationen aus Schritt 1 das folgende Code-Snippet und fügen Sie es in Ihre Anwendung ein. Der Standardcode ist der für Node.js. Wenn Sie mit einer anderen Sprache arbeiten, können Sie diese am Anfang dieses Abschnitts auswählen.

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
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password, new TokenResponseListener() {
    @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
        // Ausnahmebedingung aufgetreten.
  			 }

    @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
        // Benutzer authentifiziert.
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
    // Benutzer authentifiziert.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
    // Ausnahmebedingung aufgetreten.
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

### Tokens mit API abrufen
{: #obtain-tokens-api}

1. Rufen Sie Ihre Tenant-ID und Ihre Client-ID, den geheimen Schlüssel und die OAuth-Server-URL von Ihren Berechtigungsnachweisen ab.

2. Verschlüsseln Sie die Client-ID und den geheimen Schlüssel.

    1. Kopieren Sie die Client-ID und den geheimen Schlüssel mithilfe der Schritte aus dem vorherigen Abschnitt.
    2. Verwenden Sie einen Base64-Encoder, um Ihre Autorisierungsinformationen zu verschlüsseln.
    3. Kopieren Sie die Ausgabe.

3. Erstellen Sie eine Anforderung für die API zum Abrufen eines Tokens. Der Datenabschnitt der Anforderung variiert abhängig von der Art des Bewilligungstyps, den Sie verwenden. 

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

Die Art des Bewilligungstyps, den Sie zum Abrufen des Tokens verwenden, kann abhängig vom Typ der jeweils verwendeten Autorisierung abweichen. Eine detaillierte Liste der Optionen finden Sie in der [Swagger-Dokumentation](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token).
