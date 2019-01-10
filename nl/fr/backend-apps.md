---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Applications d'arrière-plan
{: #adding-backend}

Vous pouvez utiliser les SDK et API {{site.data.keyword.appid_full}} pour protéger les noeuds finaux et les API de votre application d'arrière-plan.
{: shortdesc}


## Comprendre le flux
{: #understanding}

**Dans quelles circonstances ce flux est-il utile ?**

Le développement d'applications d'arrière plan consiste notamment à vérifier que vos API sont protégées contre les accès non autorisés. Les SDK {{site.data.keyword.appid_short_notm}} facilitent la protection de vos noeuds finaux d'API et garantissent la sécurité de votre application.

**Quelle est la base technique du flux ?**

{{site.data.keyword.appid_short_notm}} implémente [OAuth2](https://tools.ietf.org/html/rfc6749) et la spécification OIDC, qui utilise des jetons bearer pour l'authentification et l'autorisation. Ces jetons sont formatés comme des [jetons Web JSON](https://tools.ietf.org/html/rfc7519), signés numériquement et contenant des réclamations qui décrivent le sujet en cours d'authentification et le fournisseur d'identité. Les API de votre application sont protégées par des jetons d'accès et d'identité. Les clients qui doivent accéder à vos API peuvent s'authentifier auprès du fournisseur d'identité via {{site.data.keyword.appid_short_notm}} en échange de ces jetons. Les réclamations contenues dans les jetons doivent être validées pour qu'un accès aux API protégées soit accordé.

Pour plus d'informations sur l'utilisation des jetons dans {{site.data.keyword.appid_short_notm}}, voir [Understanding tokens](/docs/services/appid/authorization.html#tokens).
{: tip}

**A quoi ressemble ce flux ?**

Flux d'arrière-plan ![{{site.data.keyword.appid_short_notm}}. Les étapes sont répertoriées dans l'ordre dans l'image suivante.](images/backend-flow.png)

1. Un client effectue une requête POST sur le serveur d'autorisations {{site.data.keyword.appid_short_notm}} afin d'obtenir un jeton d'accès. Une requête POST est généralement au format suivant :

  ```
  POST/oauth/v3/{tenantId}/token HTTP/1.1
  Content_type: application/x-www-form-urlencoded
  Authorization header = "Basic" + base64encode({clientId}:{secret})
  FormData = {grant_type}
  ```
  {: screen}

2. Si le client remplit les conditions requises, le serveur d'autorisations renvoie un jeton d'accès.

3. Le client envoie une demande à la ressource protégée.

4. La ressource protégée ou l'API valide le jeton. Si le jeton est valide, l'accès à la ressource est accordé au client. Si le jeton ne peut pas être validé, l'accès est refusé.


## Protection des ressources à l'aide du logiciel SDK Node.js
{: #secure-node}

Le logiciel SDK du serveur {{site.data.keyword.appid_short_notm}} contrôle l'authentification et l'autorisation avec l'[infrastructure Passport](http://www.passportjs.org/). Avec `ApiStrategy`, vous pouvez sécuriser vos ressources d'arrière-plan en exigeant que des jetons d'accès et d'identité soient validés dans l'en-tête de l'autorisation dans le cadre de la demande.
{: shortdesc}

**Avant de commencer**

Les éléments suivants sont prérequis pour pouvoir commencer :
 * Une instance d'{{site.data.keyword.appid_short_notm}}
 * NPM version 4 ou ultérieure
 * Noeud version 6 ou ultérieure

**Installation du logiciel SDK**

1. Ajoutez le logiciel SDK Node.js {{site.data.keyword.appid_short_notm}} au fichier `package.json` de votre application.

  ```
  "dependencies": {
      "ibmcloud-appid": "^4.0.0"
  }
  ```
  {: codeblock}

2. Exécutez la commande suivante.

  ```
  npm install
  ```
  {: codeblock}

**Initialisation du logiciel SDK **

Vous pouvez initialiser le logiciel SDK en utilisant une URL de serveur `oauth server url`.

1. Obtenez votre `oauth server url`.
  1. Accédez à l'onglet **Données d'identification pour le service** du tableau de bord {{site.data.keyword.appid_short_notm}}.
  2. Si vous ne disposez pas encore d'un ensemble de données d'identification, cliquez sur **Nouvelles données d'identification** puis sur **Ajouter** pour créer un nouvel ensemble. Dans le cas contraire, ignorez cette étape.
  3. Cliquez sur le bouton **Afficher les données d'identification** pour afficher vos informations.
  4. Copiez votre URL `oauth server url` à utiliser à l'étape suivante.

2. Initialisez la stratégie Passport {{site.data.keyword.appid_short_notm}}, comme indiqué dans l'exemple suivant.

  ```javascript
  var express = require('express'); 
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy; 
  passport.use(new APIStrategy({ oauthServerUrl: "{oauth-server-url}" })); 
  var app = express();
  app.use(passport.initialize());
  ```
  {: codeblock}


Si votre application Node.js s'exécute sur {{site.data.keyword.Bluemix_notm}} et est liée à votre instance d'{{site.data.keyword.appid_short_notm}}, il n'est pas nécessaire de fournir la configuration de la stratégie d'API. La configuration d'{{site.data.keyword.appid_short_notm}} obtient les informations à l'aide de la variable d'environnement VCAP_SERVICES.
{: tip}

**Sécurisation de l'API**

Le fragment suivant montre comment utiliser `ApiStrategy` dans une application Express pour protéger l'API GET `/protected`.

  ```javascript
   app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', { session: false }), function(request, response){
      console.log("Security context", request.appIdAuthorizationContext);
      response.send(200, "Success!");
      }
   );
   ```
  {: codeblock}

Lorsque les jetons sont valides, le middleware suivant de la chaîne de demande est appelé et la propriété `appIdAuthorizationContext` est ajoutée à l'objet de la demande. La propriété contient les jetons d'accès et d'identité d'origine ainsi que les informations de contenu décodées des jetons respectifs.


## Protection des ressources à l'aide du logiciel SDK Swift
{: #secure-swift}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} pour protéger vos ressources côté serveur en utilisant le logiciel SDK Swift.
{: shortdesc}

Le [logiciel SDK serveur Swift](https://github.com/ibm-cloud-security/appid-serversdk-swift) {{site.data.keyword.appid_short_notm}} fournit un plug-in middleware de protection d'API qui est utilisé pour protéger vos applications d'arrière-plan. En associant vos API au middleware, vous pouvez protéger votre application contre les accès non autorisés. Une fois l'API protégée, le middleware s'assure que les jetons générés par {{site.data.keyword.appid_short_notm}} sont validés. Vous pouvez alors modifier le comportement de l'API en fonction des résultats de la validation.

Voir le fragment de code suivant pour un exemple de protection de l'API `/protectedendpoint`.

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// setup routes
let router = Router()

// mandatory option to be passed in if app not deployed on IBM Cloud
let options = [
    "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/d8438de6-c325-4956-ad34-abd49194affd",
]
let apiCreds = Credentials()

// Minimum macOS version required
if #available(OSX 10.12, *) {

    // setup API protection
    let apiKituraCredentialsPlugin = APIKituraCredentialsPlugin(options: options)
    apiCreds.register(plugin: apiKituraCredentialsPlugin)

    // associate route with API protection
    router.all(middleware: apiCreds)

    // create protected API
    router.get("/protectedendpoint") { request, response, next in

        response.headers["Content-Type"] = "text/html; charset=utf-8"
        do {
            if let userProfile = request.userProfile  {
                try response.status(.OK).send(
                    "<!DOCTYPE html><html><body>" +
                        "Welcome " + userProfile.displayName  +
                        "! You are logged in with " + userProfile.provider + ".
" +
                    "</body></html>\n\n").end()
                next()
                return
            }
            try response.status(.unauthorized).send(
                "<!DOCTYPE html><html><body>” + “You are not authorized!" +
                "</body></html>\n\n").end()
        }
        catch {}
        next()
    }

    // Start server
    Kitura.addHTTPServer(onPort: 8090, with: router)

    Kitura.run()  
}
```
{: codeblock}

## Protection manuelle des ressources
{: secure-api}

La sécurisation de vos applications d'arrière-plan et de vos ressources protégées implique la validation de jetons. Vous pouvez valider des jetons d'accès et d'identité {{site.data.keyword.appid_short_notm}} de plusieurs manières. Pour obtenir de l'aide sur la validation des jetons, consultez [Validating tokens](/docs/services/appid/tokens.html).


## Etapes suivantes
{: #next}

{{site.data.keyword.appid_short_notm}} est installé dans votre application ? Vous êtes pratiquement prêt à commencer l'authentification des utilisateurs ! Essayez d'effectuer l'une des activités suivantes :

* Configurer vos [fournisseurs d'identité](/docs/services/appid/identity-providers.html)
* Personnaliser et configurer [le widget de connexion](/docs/services/appid/login-widget.html)
* En savoir plus sur le <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">logiciel SDK Node.js<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
* En savoir plus sur le <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">logiciel SDK Swift<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
