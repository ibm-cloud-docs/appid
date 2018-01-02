---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Gestion de l'expérience de connexion
Avec le widget de connexion, quelques minutes suffisent pour mettre en place
un mécanisme de connexion.
A tout moment, vous pouvez mettre à jour le widget ou son thème sans ajouter ni supprimer ou changer
le code source du mécanisme sous-jacent.
{: shortdesc}



## Personnalisation du widget de connexion
{: #login-widget}

Vous pouvez configurer votre widget de connexion pour afficher le logo et les couleurs de votre choix.
{: shortdesc}

Lorsque le service {{site.data.keyword.appid_short}} est configuré avec deux fournisseurs d'identité (ou plus), l'utilisateur peut en sélectionner un dans le widget de connexion. Vous pouvez personnaliser votre widget de connexion en procédant comme suit :

1. Ouvrez le tableau de bord du service {{site.data.keyword.appid_short_notm}}.
2. Sélectionnez la section **Personnalisation de la connexion**, dans laquelle vous pouvez modifier l'apparence du widget de connexion pour l'adapter à l'image de marque de votre entreprise.
3. Téléchargez le logo de votre entreprise en sélectionnant un fichier PNG ou JPG sur votre système local. La taille recommandée pour l'image est de 320 x 320 pixels. La taille maximale du fichier est 100 Ko.
4. Sélectionnez une couleur d'en-tête pour le widget dans la palette de couleurs ou entrez le code hexadécimal d'une autre couleur.
5. Examinez le panneau de prévisualisation, puis cliquez
sur **Sauvegarder les modifications** lorsque vous êtes satisfait de
vos personnalisations. Un message de confirmation s'affiche.

**Remarque** : Il n'est pas nécessaire de régénérer votre application. L'image est stockée dans la base de données d'{{site.data.keyword.appid_short}} et s'affiche lors de la prochaine connexion.

## Exécution du widget de connexion avec le SDK Android

{: #authenticate-android}

Si vous configurez plusieurs fournisseurs d'identité, en visitant votre application,
les utilisateurs se verront présenter un widget de connexion.
Par défaut, si vous ne configurez qu'un seul fournisseur d'identité, l'utilisateur sera redirigé vers l'écran d'authentification dudit
fournisseur.



Une fois que le SDK client d'{{site.data.keyword.appid_short_notm}} est initialisé, vous pouvez authentifier vos utilisateurs en exécutant le widget de connexion.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        @Override
        public void onAuthorizationCanceled () {
          //Authentication canceled by the user
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //User authenticated
        }
      });
  ```
  {: codeblock}

## Exécution du widget de connexion avec le SDK iOS

{: #authenticate-ios}

Si vous configurez plusieurs fournisseurs d'identité, en visitant votre application,
les utilisateurs se verront présenter un widget de connexion.
Par défaut, si vous ne configurez qu'un seul fournisseur d'identité, l'utilisateur sera redirigé vers l'écran d'authentification dudit
fournisseur.



1. Ajoutez l'importation ci-dessous au fichier dans lequel utiliser
le SDK.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Exécutez la commande ci-dessous pour lancer le widget.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }
      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }
      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

## Exécution du widget de connexion avec le SDK Node.js

{: #authenticate-nodejs}

Vous pouvez utiliser `WebAppStrategy` pour protéger des ressources
d'application Web.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {: codeblock}


## Exécution du widget de connexion avec le SDK Swift

{: #authenticate-swift}

Le plug-in WebAppKituraCredentialsPlugin est basé sur le flux d'octroi d'autorisation OAuth2 authorization_code et doit être utilisé pour les applications Web utilisant des navigateurs. Le plug-in fournit des outils pour implémenter les flux d'authentification et d'autorisation. Il fournit également des mécanismes pour détecter des tentatives non authentifiées d'accès à des ressources protégées et redirige alors automatiquement le navigateur de l'utilisateur vers la page d'authentification. Si l'authentification aboutit, l'utilisateur est dirigé vers l'URL de rappel de l'application Web, laquelle utilise le plug-in pour obtenir des jetons d'accès et d'identité auprès d'{{site.data.keyword.appid_short_notm}}. Après avoir obtenu ces jetons, le plug-in les stocke dans une session HTTP sous WebAppKituraCredentialsPlugin.AuthContext.

Le code ci-dessous explique comment utiliser le plug-in
WebAppKituraCredentialsPlugin dans une application Kitura pour protéger le noeud final
`/protected`.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // The following URLs will be used for AppID OAuth flows
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Setup Kitura to use session middleware
  // Must be configured with proper session storage for production
  // environments. See https://github.com/IBM-Swift/Kitura-Session for
  // additional documentation
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)

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

  // Explicit login endpoint
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType:
webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback to finish the authorization process. Will retrieve access and identity
tokens from AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType:
webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Logout endpoint. Clears authentication information from session
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Protected area
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType:
webappKituraCredentialsPlugin.name), { (request, response, next) in
      let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]

      guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
          response.status(.unauthorized)
          return next()
      }

      response.send(json: identityTokenPayload!)
      next()
  })
  var port = 3000
  if let portString = ProcessInfo.processInfo.environment["PORT"]{
      port = Int(portString)!
  }
  print("Starting on \(port)")

  // Add an HTTP server and connect it to the router
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start the Kitura runloop (this call never returns)
  Kitura.run()
  ```
  {: codeblock}
