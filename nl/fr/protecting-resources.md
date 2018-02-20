---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Sécurisation des ressources de back-end

Vous pouvez utiliser les SDK de serveur {{site.data.keyword.appid_short_notm}} pour protéger les points d'extrémité et y accéder dans vos applications. Vous pouvez également utiliser les SDK de client pour accéder aux ressources protégées.

**Remarque** : L'appel d'une ressource protégée démarre le widget de connexion, si nécessaire. Si un jeton d'accès valide a déjà été obtenu, le widget de connexion n'est pas
démarré et
l'accès direct à la ressource est autorisé.

## Protection des ressources dans Liberty for Java
{: #protecting-liberty}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} pour protéger des noeuds finaux dans vos applications IBM Liberty for Java. Liberty for Java intègre des capacités de gestion des demandes OIDC (Open ID Connect).

Avant de commencer :
* Vous devez disposer d'une [application IBM Liberty for Java](https://console.bluemix.net/catalog/starters/liberty-for-java) existante, non liée. Pour vous familiariser avec le développement d'applications Liberty for Java, voir la documentation [](/docs/runtimes/liberty/index.html).
* Assurez-vous que [Apache Maven](https://maven.apache.org/download.cgi) est installé.
* Découvrez comment OIDC fonctionne avec Liberty for Java.

Pour protéger vos ressources :

1. Téléchargez le modèle Liberty for Java depuis l'interface utilisateur. Il contient un fichier zip qui inclut les fichiers Liberty standard.
2. Ouvrez le terminal et accédez au répertoire dans lequel vous avez extrait le modèle.
3. Connectez-vous à {{site.data.keyword.Bluemix_notm}} à l'aide de la ligne de commande Cloud Foundry. A l'invite, entrez vos données d'identification.

  ```
  cf login
  ```
  {: codeblock}

4. Déployez l'application. L'exécution de la commande suivante crée une instance Liberty for Java nommée d'après l'ID titulaire.

  ```
  cf push
  ```
  {: codeblock}

5. Liez votre instance de service à la nouvelle instance Liberty for Java et redéployez l'application.
6. Ouvrez votre application dans un navigateur et connectez-vous à l'aide de vos données d'identification pour passer en revue les activités d'authentification.

## Protection des ressources dans Node.js
{: #protecting-resources-nodesdk}

Le SDK serveur d'{{site.data.keyword.appid_short_notm}} fournit une stratégie de passeport ApiStrategy qui est utilisée dans les applications de back end déployées sur {{site.data.keyword.Bluemix_notm}}. Pour protéger votre application contre des accès non autorisés, vous devez instrumenter votre serveur Node.js avec la stratégie ApiStrategy. Le module `appid-serversdk-nodejs npm module` fournit la stratégie de passeport ApiStrategy et la méthode de vérification servant à valider le jeton d'accès et le jeton d'identité émis par {{site.data.keyword.appid_short_notm}}.

Le SDK serveur d'{{site.data.keyword.appid_short_notm}} utilise <a href="http://passportjs.org/" target="_blank">l'infrastructure Passport<img src="../../icons/launch-glyph.svg" alt="icône de lien externe"></a> pour contrôler l'autorisation.

Le fragment de code suivant illustre comment utiliser la stratégie `APIStrategy` dans une application Express simple pour protéger les méthodes GET de noeud final `/protected`.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

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


## Accès aux ressources protégées avec le SDK Swift iOS
{: #requesting-swift}

1. Importez BMSCore.

  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Appel d'une demande de ressource protégée.

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


## Accès aux ressources protégées avec le SDK Android
{: #requesting-android}

1. Appel d'une demande de ressource protégée.

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
