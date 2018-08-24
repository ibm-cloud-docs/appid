---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Sécurisation des ressources de back end
{: #secure-back-end}

Vous pouvez utiliser les SDK serveur {{site.data.keyword.appid_short_notm}} pour protéger les points d'extrémité et y accéder dans vos applications. Vous pouvez également utiliser les SDK client pour accéder aux ressources protégées.
{: shortdesc}

L'appel d'une ressource protégée démarre le widget de connexion, si nécessaire. Si un jeton d'accès valide a déjà été obtenu, le widget de connexion n'est pas démarré et l'accès direct à la ressource est autorisé.
{: tip}

## Protection des ressources dans Liberty for Java
{: #protecting-liberty}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} pour protéger des noeuds finaux dans vos applications IBM Liberty for Java. Liberty for Java dispose de la fonctionnalité intégrée de gestion des demandes OIDC (Open ID Connect).
{: shortdesc}



Avant de commencer :
* Vous devez disposer d'une <a href="https://console.bluemix.net/catalog/starters/liberty-for-java" target="_blank">application {{site.data.keyword.Bluemix_notm}} Liberty for Java <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> existante et non liée. Pour vous familiariser avec le développement d'applications Liberty for Java, voir la documentation [](/docs/runtimes/liberty/index.html).
* Assurez-vous que <a href="https://maven.apache.org/download.cgi" target="_blank">Apache Maven <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> est installé.
* Découvrez comment OIDC fonctionne avec Liberty for Java.



Pour protéger vos ressources :

1. Téléchargez le modèle Liberty for Java depuis l'interface utilisateur. Il contient un fichier compressé qui inclut les fichiers Liberty standard.
2. Suivez les instructions présentées dans l'interface utilisateur pour déployer votre application dans IBM Cloud. 
3. Ouvrez votre application dans un navigateur et connectez-vous à l'aide de vos données d'identification pour passer en revue les activités d'authentification.

## Protection des ressources dans Node.js
{: #protecting-resources-nodesdk}

Le logiciel SDK serveur d'{{site.data.keyword.appid_short_notm}} fournit une stratégie de passeport ApiStrategy qui est utilisée dans les applications de back end déployées sur {{site.data.keyword.Bluemix_notm}}. Pour protéger votre application contre des accès non autorisés, vous devez instrumenter votre serveur Node.js avec la stratégie ApiStrategy. Le module `appid-serversdk-nodejs npm module` fournit la stratégie de passeport ApiStrategy et la méthode de vérification servant à valider le jeton d'accès et le jeton d'identité émis par {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

Le logiciel SDK serveur d'{{site.data.keyword.appid_short_notm}} utilise <a href="http://passportjs.org/" target="_blank">l'infrastructure Passport<img src="../../icons/launch-glyph.svg" alt="icône de lien externe"></a> pour contrôler l'autorisation.

Le fragment de code suivant illustre comment utiliser la stratégie `APIStrategy` dans une application Express simple pour protéger les méthodes GET de noeud final `/protected`.
  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {: codeblock}


## Protection des ressources à l'aide du logiciel SDK Swift
{: #protecting-swift}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} pour protéger vos ressources côté serveur en utilisant le logiciel SDK Swift.
{: shortdesc}

Le logiciel SDK serveur Swift {{site.data.keyword.appid_short_notm}}
fournit un
plug-in middleware de protection d'API qui est utilisé pour protéger vos applications de back end. En associant vos API au middleware, vous pouvez protéger votre application contre les accès non autorisés. Une fois l'API protégée, le middleware s'assure que les jetons générés par {{site.data.keyword.appid_short_notm}} sont validés. Vous pouvez alors modifier le comportement de l'API en fonction des résultats de la validation.

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


## Accès aux ressources protégées avec le logiciel SDK Swift iOS
{: #requesting-swift}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} pour protéger les noeuds finaux de vos applications Swift iOS.
{: shortdesc}

1. Importez BMSCore.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Appelez une demande de ressource protégée.
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager =
AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## Accès aux ressources protégées avec le logiciel SDK Android
{: #requesting-android}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} pour protéger les noeuds finaux de vos applications Swift Android.
{: shortdesc}

1. Appelez une demande de ressource protégée.
  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //code handling the response here
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //code handling the failure here
  });
  ```
  {: codeblock}
