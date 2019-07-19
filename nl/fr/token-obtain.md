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



# Obtention de jetons
{: #obtain-tokens}

Lorsque les utilisateurs ou les services de back end interagissent avec votre application, ils peuvent avoir besoin d'être autorisés à effectuer des actions spécifiques. {{site.data.keyword.appid_short_notm}} vérifie que l'entité qui fait la demande est autorisée et renvoie les clés d'accès et d'identité à votre application. Si l'entité qui fait la demande est un utilisateur final, les jetons peuvent contenir des informations sur l'utilisateur telles que l'étendue de ses droits et son nom. S'il s'agit d'un service de back end, seul un code d'accès est retourné.
{: shortdesc}


## Obtention de votre ID de client et de votre secret
{: #obtain-clientid-secret}

Pour obtenir des jetons, vous devez avoir votre ID de client et votre secret. Les données d'identification sont spécifiques à chaque application et sont utilisées pour identifier et valider les utilisateurs auxquels un jeton peut être attribué. 
{: shortdesc}


### Via l'interface graphique
{: #credentials-gui}

1. Accédez à l'onglet **Applications** du tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Si vous avez déjà un ensemble de données d'identification, vous pouvez passer à l'étape 3. Dans le cas contraire, vous devez le créer.
    1. Sur l'onglet **Applications**, cliquez sur **Ajouter une application**.
    2. Donnez un nom à votre application et cliquez sur **Sauvegarder** pour retourner à une liste de vos applications enregistrées. Le nom de votre application ne doit pas dépasser 50 caractères.

3. Dans la liste des applications enregistrées, sélectionnez l'application avec laquelle vous voulez travailler. La ligne se développe pour afficher vos données d'identification.

4. Copiez votre ID client et votre secret.


### Avec l'API
{: #credentials-api}

1.  Envoyez une requête POST au noeud final [`/management/v4/{tenantId}/applications`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication).

  Demande :

  ```
  curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  Exemple de réponse :

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

2. Copiez l'ID client et le secret.



## Obtention des jetons d'accès et d'identité
{: #obtain-access-id-tokens}

Avec un ID client et un code secret, vous pouvez obtenir des jetons d'accès et d'identité en suivant les étapes suivantes.
{: shortdesc}


### Obtention de jetons à l'aide d'un SDK
{: obtain-token-sdk}

1. Obtenez votre ID de titulaire, votre ID client, votre secret et l'adresse URL du serveur OAuth à partir de vos données d'identification.

2. En utilisant les informations de l'étape 1, mettez à jour le fragment de code suivant et ajoutez-le dans votre application. Le code par défaut est Node.js. Si vous travaillez avec un autre langage, vous pouvez choisir celui qui s'applique à votre cas au début de cette rubrique.

  Node :
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

  Java :
  {: ph data-hd-programlang='java'}
  ```
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
    @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
        //Exception occurred
      }

    @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
        //User authenticated
        }
  });
  ```
  {: codeblock}
  {: ph data-hd-programlang='java'}

iOS Swift :
{: ph data-hd-programlang='swift'}

  ```
  class delegate : TokenResponseDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
    //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
    //Exception occurred
      }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

Server Swift :
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

### Obtention de jetons à l'aide de l'API
{: #obtain-tokens-api}

1. Obtenez votre ID de titulaire, votre ID client, votre secret et l'adresse URL du serveur OAuth à partir de vos données d'identification.

2. Codez votre ID client et votre secret.

    1. Copiez votre ID client et votre secret en suivant les étapes décrites dans la section précédente.
    2. Utilisez un encodeur en Base64 pour encoder vos informations d'autorisation.
    3. Copiez la sortie.

3. Faites une demande à l'API pour obtenir un jeton. La section des données de votre demande varie selon le type d'octroi que vous utilisez. 

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

Le type d'octroi que vous utilisez pour obtenir votre jeton peut varier selon le type d'autorisation que vous utilisez. Pour une liste détaillée des options, consultez la [documentation Swagger](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token).
