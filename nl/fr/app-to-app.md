---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-14"

keywords: authentication, authorization, identity, app security, secure, application identity, app to app, access token

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

# Identité de l'application et autorisation
{: #app}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez sécuriser des applications en utilisant l'identité d'application et le flux d'autorisation grâce aux fonctionnalités d'OAuth2.0.
{: shortdesc}

## Comprendre le flux de communication
{: #app-understanding}

Vous pouvez souhaiter qu'une application communique avec un autre service ou une autre application sans aucune intervention de l'utilisateur, pour plusieurs raisons. Par exemple, une application non interactive qui doit accéder à une autre application pour effectuer son travail. Cela peut inclure des processus, des interfaces de ligne de commande, des démons ou un terminal IoT qui surveille et transmet des variables d'environnement à un serveur en amont. Le cas d'utilisation spécifique est propre à chaque application, mais le plus important à retenir est que les demandes sont échangées au nom de l'application, et non d'un utilisateur final, et que c'est l'application qui est authentifiée et autorisée.


### Comment fonctionne le flux ?
{: #app-flow-how}

{{site.data.keyword.appid_short_notm}} exploite le flux des données d'identification du client OAuth 2.0 pour protéger la communication. Lorsqu'une application s'enregistre auprès d'{{site.data.keyword.appid_short_notm}}, elle obtient un ID client et un secret. Avec ces informations, l'application peut demander un jeton d'accès à {{site.data.keyword.appid_short_notm}} et être autorisée à accéder à une ressource protégée ou une API. Dans l'identité d'application et le flux d'autorisation, l'application se voit uniquement attribuer un jeton d'accès. Elle n'obtient pas de jeton d'identité ou de jeton d'actualisation. Pour plus d'informations sur les jetons, voir [Connaissance des jetons](/docs/services/appid?topic=appid-tokens#tokens).

Ce flux de travaux est destiné à être utilisé uniquement avec des applications sécurisées dans lesquelles le secret ne risque pas d'être mal utilisé ou divulgué. L'application conserve toujours la valeur secrète du client. Elle ne fonctionne pas pour les applications mobiles.
{: tip}

### A quoi ressemble le flux ?
{: #app-flow-what}

Dans l'image suivante, vous pouvez voir le sens de la communication entre le service et votre application.

Identité d'application et flux d'autorisation ![{{site.data.keyword.appid_short_notm}}](images/app-to-app-flow.png)
Figure. Identité d'application et flux d'autorisation

1. Vous enregistrez l'application qui doit s'authentifier pour accéder à une ressource protégée avec {{site.data.keyword.appid_short_notm}}. 
2. L'application A s'enregistre auprès d'{{site.data.keyword.appid_short_notm}} pour obtenir un ID client et un secret.
3. L'application A fait une demande au noeud final `/token` du serveur d'autorisation {{site.data.keyword.appid_short_notm}} en envoyant les données d'identification extraites à l'étape précédente.
4. {{site.data.keyword.appid_short_notm}} valide la demande, authentifie l'application et renvoie à l'application A une réponse contenant un jeton d'accès.
5. L'application A est maintenant capable d'utiliser le jeton d'accès valide pour envoyer des requêtes à des ressources protégées telles que l'application B.

Le secret client utilisé pour authentifier le client est très sensible et doit rester confidentiel. Comme l'application utilise le secret client dans l'application, ce flux de travail doit être utilisé uniquement avec des applications fiables. L'utilisation d'une application de confiance garantit que le secret client n'est pas divulgué ou mal utilisé.
{: important}

## Enregistrement de votre application
{: #app-register}

### Avec l'interface graphique
{: #app-register-gui}

1. Dans l'onglet **Application** du tableau de bord {{site.data.keyword.appid_short_notm}}, cliquez sur **Ajouter une application**.
2. Ajoutez le nom de votre application et cliquez sur **Sauvegarder** pour revenir à la liste de vos applications enregistrées. Le nom de votre application ne doit pas dépasser 50 caractères.
3. Dans la liste des applications enregistrées, sélectionnez l'application ajoutée à l'étape précédente. La ligne se développe pour afficher vos données d'identification.

### Avec l'API
{: #app-register-api}

1. Envoyez une requête POST au noeud final [`/management/v4/{tenantId}/applications`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication).

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
    "clientId": "c90830bf-11b0-4b44-bffe-9773f8703bad",
    "tenantId": "b42f7429-fc24-48fa-b4f9-616bcc31cfd5",
    "secret": "YWQyNjdkZjMtMGRhZC00ZWRkLThiOTQtN2E3ODEyZjhkOWQz",
    "name": "testing",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48fa-b4f9-616bcb31cfd5",
    "profilesUrl": "https://us-south.appid.cloud.ibm.com",
    "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48fa-b4f9-616bcb31cfd5/.well-known/openid-configuration"
  }
  ```
  {: screen}

## Obtention d'un jeton d'accès
{: #obtain-token}

Lorsque votre application est enregistrée auprès d'{{site.data.keyword.appid_short_notm}} et que vous avez obtenu vos données d'identification, vous pouvez envoyer une demande au serveur d'autorisations {{site.data.keyword.appid_short_notm}} pour obtenir un jeton d'accès.

1. Envoyez une requête POST HTTP au noeud final [`/token`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token). L'autorisation pour la demande est `Basic auth`, avec l'ID client et le secret utilisés comme nom d'utilisateur et mot de passe codés en base64.

  Demande :
  ```
  curl -X POST \
    http://localhost:6002/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/token \
    -H 'Authorization: Basic base64Encoded{clientId:secret}' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    -d grant_type=client_credentials
  ```
  {: codeblock}

  Exemple de réponse :
  ```
  {
  "access_token": "eyJhbGciOiJS...F9A",
  "expires_in": "3600",
  "token_type": "Bearer"
  }
  ```
  {: codeblock}


## Tutoriel : flux de bout en bout avec le logiciel SDK Node.js
{: tutorial-node}

1. Obtenez un [jeton d'accès](/docs/services/appid?topic=appid-tokens#tokens) de l'une des manières suivantes :

  * A partir du [logiciel SDK serveur Node.js](https://github.com/ibm-cloud-security/appid-serversdk-nodejs) {{site.data.keyword.appid_short_notm}} à l'aide du gestionnaire de jetons. Initialisez le gestionnaire de jetons avec les données d'identification de votre application et appelez la méthode `getApplicationIdentityToken()` pour obtenir le jeton.

    ```
    const TokenManager = require('ibmcloud-appid').TokenManager;
    const config = {
     clientId: "<client-ID>",
     tenantId: "<tenant-ID>",
     secret: "<secret>",
     oauthServerUrl: "https://<region>.appid.cloud.ibm.com/oauth/v4/<tenant-ID>"
    };

    const tokenManager = new TokenManager(config);

    tokenManager.getApplicationIdentityToken().then((appIdAuthContext) => {
     console.log(' Access tokens from SDK : ' + JSON.stringify(appIdAuthContext));
    }).catch((err) => {
     //console.error('Error retrieving tokens : ' + err);
    });
    ```
    {: codeblock}

  * A partir du serveur d'autorisations {{site.data.keyword.appid_short_notm}}.
  
    L'URL `oauthServerUrl` contenue dans la demande est obtenue lors de l'enregistrement de votre application. Si vous avez enregistré votre application avec les API de gestion, l'URL du serveur se trouve dans le corps de la réponse. Si vous avez enregistré votre application en la liant à la console IBM Cloud, l'URL se trouve dans votre objet VCAP_SERVICES JSON ou dans vos valeurs confidentielles Kubernetes.
    {: note}

    ```
    var request = require('request');

    function getAccessToken() {
      let options = {
          method: 'POST',
          url: oauthServerUrl + '/token',
          headers: { 'content-type': 'application/x-www-form-urlencoded',
              'Authorization': 'Basic ' +Buffer.from('clientId: secret').toString('base64')
          },
          form: {
              grant_type: 'client_credentials'
          }
      };

      return new Promise((resolve, reject) => {
          request(options, function (error, response, body) {
              if (error) {
                  return reject(error);
              }

              let data = JSON.parse(body);
              if(data.access_token) {
                  resolve(data.access_token);
              } else {
                  reject(data);
              }
          })
      });
    }
    ```
    {: codeblock}

2. Envoyez une demande à votre ressource protégée en utilisant le jeton d'accès obtenu à l'étape précédente.

  ```
  let options = {
      method: 'GET',
      url: 'http://localhost:8081/protected_resource',
      headers: { authorization : 'Bearer ' + accessToken}
  }

  request(options, function (error, response, body) {
      if (error) {
       console.log(error)
      } else {
          res.status(response.statusCode).send({
      console.log(JSON.stringify(body));
          });
      }
  });
  ```
  {: codeblock}

3. Sécurisez vos ressources protégées à l'aide de la stratégie d'API du logiciel SDK Node.js {{site.data.keyword.appid_short_notm}}.

  ```
  const express = require('express'),
    passport = require('passport');

  var app = express();
  app.use(passport.initialize());

  passport.use(new APIStrategy({
      oauthServerUrl: "https://<region>.appid.cloud.ibm.com/oauth/v4/<tenant-ID>",
      tenantId:"<tenant-ID>"
  }));

  app.get('/protected_resource',
      passport.authenticate(APIStrategy.STRATEGY_NAME, {session: false}),
      (req, res) => {
          res.send("Hello from protected resource");
  });
  ```
  {: codeblock}
