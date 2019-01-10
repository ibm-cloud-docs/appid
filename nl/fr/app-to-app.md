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

# Identité de l'application et autorisation
{: #app}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez sécuriser des applications en utilisant l'identité d'application et le flux d'autorisation grâce aux fonctionnalités d'OAuth2.0.
{: shortdesc}

## Comprendre le flux de communication
{: #understanding}

**Dans quelles circonstances ce flux est-il utile ?**

Vous pouvez souhaiter qu'une application communique avec un autre service ou une autre application sans aucune intervention de l'utilisateur, pour plusieurs raisons. Par exemple, une application non interactive qui doit accéder à une autre application pour effectuer son travail. Cela peut inclure des processus, des interfaces de ligne de commande, des démons ou un terminal IoT qui surveille et transmet des variables d'environnement à un serveur en amont. Le cas d'utilisation spécifique est propre à chaque application, mais le plus important à retenir est que les demandes sont échangées au nom de l'application, et non d'un utilisateur final, et que c'est l'application qui est authentifiée et autorisée.

Consultez cet exemple dans la rubrique <a href="https://www.ibm.com/blogs/bluemix/2018/02/using-app-id-secure-docker-kubernetes-applications/" target="_blank">Using {{site.data.keyword.appid_short_notm}} to secure Docker and Kubernetes applications <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

**Comment fonctionnent l'identité d'application et le flux d'autorisation ?**

{{site.data.keyword.appid_short_notm}} exploite le flux de données d'identification du client OAuth2.0 pour protéger la communication. Lorsqu'une application s'enregistre auprès d'{{site.data.keyword.appid_short_notm}}, elle obtient un ID client et une valeur confidentielle. Avec ces informations, l'application peut demander un jeton d'accès à {{site.data.keyword.appid_short_notm}} et être autorisée à accéder à une ressource protégée ou une API. Dans l'identité d'application et le flux d'autorisation, l'application se voit uniquement attribuer un jeton d'accès. Elle n'obtient pas de jeton d'identité ou de jeton d'actualisation. Pour plus d'informations sur les jetons, voir [Understanding tokens](/docs/services/appid/authorization.html#tokens).

Ce flux de travaux est destiné à être utilisé uniquement avec des applications sécurisées dans lesquelles la valeur confidentielle ne risque pas d’être mal utilisée ou d’être divulguée. L'application conserve toujours la valeur secrète du client. Elle ne fonctionne pas pour les applications mobiles.
{: tip}

**A quoi ressemble le flux ?**

Dans l'image suivante, vous pouvez voir le sens de la communication entre le service et votre application.

Identité d'application et flux d'autorisation ![{{site.data.keyword.appid_short_notm}}](images/app-to-app-flow.png)
Figure. Identité d'application et flux d'autorisation

1. L'application A s'enregistre auprès d'{{site.data.keyword.appid_short_notm}} pour obtenir un ID client et une valeur confidentielle.
2. L'application A envoie une demande à {{site.data.keyword.appid_short_notm}} avec les données d'identification extraites à l'étape précédente.
3. {{site.data.keyword.appid_short_notm}} valide la demande, authentifie l'application et renvoie à l'application A une réponse contenant un jeton d'accès.
4. L'application A est maintenant en mesure d'utiliser le jeton d'accès pour envoyer des demandes à l'application B, par exemple une ressource protégée.

## Enregistrement de votre application
{: #registering}

**Enregistrement de votre application à l'aide de l'interface graphique**

1. Dans l'onglet **Application** du tableau de bord {{site.data.keyword.appid_short_notm}}, cliquez sur **Ajouter une application**.
2. Ajoutez le nom de votre application et cliquez sur **Sauvegarder** pour revenir à la liste de vos applications enregistrées. Le nom de votre application ne doit pas dépasser 50 caractères.
3. Dans la liste des applications enregistrées, sélectionnez l'application ajoutée à l'étape précédente. La ligne se développe pour afficher vos données d'identification.

**Enregistrement de votre application à l'aide de l'API**

1. Envoyez une requête POST au noeud final [`/management/v4/{tenantId}/applications`](https://appid-management.ng.bluemix.net/swagger-ui/#!/Applications/registerApplication).

  Demande :
  ```
  curl -X POST \  https://appid-management.ng.bluemix.net/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  Exemple de réponse :
  ```
  {
  "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
   "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
  "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
  "name": "ApplicationName",
   "oAuthServerUrl": "https://appid-oauth.eu-gb.bluemix.net/oauth/v3/39a37f57-a227-4bfe-a044-93b6e6060b61"
   }
  ```
  {: codeblock}


## Obtention d'un jeton d'accès
{: #obtain-token}

Lorsque votre application est enregistrée auprès d'{{site.data.keyword.appid_short_notm}} et que vous avez obtenu vos données d'identification, vous pouvez envoyer une demande au serveur d'autorisations {{site.data.keyword.appid_short_notm}} pour obtenir un jeton d'accès.

1. Envoyez une requête POST HTTP au noeud final [`/oauth/v3/{tenantId}/token`](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/token). L'autorisation pour la demande est `Basic auth`, avec l'ID client et la valeur confidentielle utilisés comme nom d'utilisateur et mot de passe codés au format base64.

  Demande :
  ```
  curl -X POST \
    http://localhost:6002/oauth/v3/39a37f57-a227-4bfe-a044-93b6e6060b61/token \
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

1. Obtenez un [jeton d'accès](/docs/services/appid/authorization.html#tokens) de l'une des manières suivantes :

  * A partir du [logiciel SDK serveur Node.js](https://github.com/ibm-cloud-security/appid-serversdk-nodejs) {{site.data.keyword.appid_short_notm}} à l'aide du gestionnaire de jetons. Initialisez le gestionnaire de jetons avec les données d'identification de votre application et appelez la méthode `getApplicationIdentityToken()` pour obtenir le jeton.

    ```
    const TokenManager = require('ibmcloud-appid').TokenManager;
    const config = {
     clientId: "29a19759-aafb-41c7-9ef7-ee7b0ca88818",
     tenantId: "39a37f57-a227-4bfe-a044-93b6e6060b61",
     secret: "ZTEzZTA2MDAtMjljZS00MWNlLTk5NTktZDliMjY3YzUxZTYx",
     oauthServerUrl: "https://appid-oauth.eu-gb.bluemix.net/oauth/v3/39a37f57-a227-4bfe-a044-93b6e6060b61"
    };

    const tokenManager = new TokenManager(config);

    tokenManager.getApplicationIdentityToken().then((appIdAuthContext) => {
     console.log(' Access tokens from SDK : ' + JSON.stringify(appIdAuthContext));
    }).catch((err) => {
     //console.error('Error retrieving tokens : ' + err);
    });
    ```
    {: codeblock}

  * A partir du serveur d'autorisations {{site.data.keyword.appid_short_notm}}. **Remarque **: l'URL `oauthServerUrl` contenue dans la demande est obtenue lors de l'enregistrement de votre application. Si vous avez enregistré votre application avec les API de gestion, l'URL du serveur se trouve dans le corps de la réponse. Si vous avez enregistré votre application en la liant à la console IBM Cloud, l'URL se trouve dans votre objet VCAP_SERVICES JSON ou dans vos valeurs confidentielles Kubernetes.

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
      oauthServerUrl: "https://appid-oauth.eu-gb.bluemix.net/oauth/v3/398ec248-5e93-48b8-a122-ccabc714fe85",
      tenantId:"398ec248-5e93-48b8-a122-ccabc714fe85"
  }));

  app.get('/protected_resource',
      passport.authenticate(APIStrategy.STRATEGY_NAME, {session: false}),
      (req, res) => {
          res.send("Hello from protected resource");
  });
  ```
  {: codeblock}
