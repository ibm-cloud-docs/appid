---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="blank"}
{:shortdesc: .shortdesc}


# Affichage des écrans par défaut
{: #default}

{{site.data.keyword.appid_full}} fournit un widget de connexion permettant de fournir aux utilisateurs des options de connexion sécurisée.
{: shortdesc}

Lorsque votre application est configurée pour utiliser un fournisseur d'identité, le widget de connexion dirige les visiteurs de votre application vers un écran de connexion. Par défaut, lorsqu'un seul fournisseur est activé, les visiteurs sont redirigés vers l'écran d'authentification de ce fournisseur d'identité. Le widget de connexion vous permet d'afficher un écran de connexion par défaut ou, avec le répertoire cloud, de réutiliser celui de votre interface utilisateur existante. Et, en plus, vous pouvez à tout moment mettre à jour votre flux de connexion, sans avoir besoin de changer votre code source.



Le service utilise des types d'autorisation d'accès OAuth 2 pour mapper le processus d'autorisation. Lorsque vous configurez des fournisseurs d'identité de réseaux sociaux tels que Facebook, le [flux d'octroi d'autorisation Oauth2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) est utilisé pour appeler le widget de connexion.

Vous voulez créer une expérience unique pour votre application ? Vous pouvez [apporter vos propres écrans](/docs/services/appid/branded.html) !
{: tip}


## Personnalisation de l'écran de connexion par défaut
{: #login-widget}

Vous pouvez personnaliser l'écran de connexion préconfiguré afin d'afficher le logo et les couleurs de votre choix.
{: shortdesc}

Pour personnaliser l'écran :

1. Ouvrez le tableau de bord du service {{site.data.keyword.appid_short_notm}}.
2. Sélectionnez la section **Personnalisation de la connexion**. Vous pouvez modifier l'apparence du widget de connexion pour l'adapter à la marque de votre entreprise.
3. Téléchargez le logo de votre entreprise en sélectionnant un fichier PNG ou JPG sur votre système local. La taille recommandée pour l'image est de 320 x 320 pixels. La taille maximale du fichier est 100 Ko.
4. Sélectionnez une couleur d'en-tête pour le widget dans la palette de couleurs ou entrez le code hexadécimal d'une autre couleur.
5. Examinez le panneau de prévisualisation, puis cliquez sur **Sauvegarder les modifications** lorsque vous êtes satisfait de vos personnalisations. Un message de confirmation s'affiche.
6. Dans votre navigateur, actualisez votre page de connexion afin de vérifier vos modifications.


## Planification des écrans à afficher
{: #plan}

{{site.data.keyword.appid_short_notm}} fournit un écran de connexion par défaut que vous pouvez appeler si vous ne disposez pas de vos propres écrans d'interface utilisateur.
{: shortdesc}

En fonction de votre configuration de fournisseur d'identité, les écrans que vous pouvez afficher varient. Le service ne fournit pas de fonctionnalité avancée pour les fournisseurs d'identité de réseaux sociaux car nous n'avons jamais accès aux informations de compte des utilisateurs. Les utilisateurs doivent accéder au fournisseur d'identité pour gérer leurs informations. Si, par exemple, un utilisateur souhaite changer son mot de passe Facebook, il doit accéder à www.facebook.com.

Consultez le tableau suivant pour voir les écrans que vous pouvez afficher pour chaque type de fournisseur d'identité.

<table>
  <thead>
    <tr>
      <th>Ecran de visualisation</th>
      <th>Fournisseur d'identité de réseau social</th>
      <th>Fournisseur d'identité d'entreprise</th>
      <th>Répertoire cloud</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Connexion</td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Inscription</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Mot de passe oublié</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Changement du mot de passe</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Détails du compte</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

Une fois que vous avez configuré vos paramètres pour des [fournisseurs d'identité de réseaux sociaux](/docs/services/appid/identity-providers.html) et le [répertoire cloud](/docs/services/appid/cloud-directory.html), cliquez sur le langage de votre choix dans l'image suivante pour commencer l'implémentation du code.


Cliquez sur l'image pour utiliser l'un des logiciels SDK fournis, ou les API. N'oubliez pas : vous pouvez aussi tirer profit d'App ID avec d'autres langages. En utilisant nos API, vous pouvez configurer un répertoire cloud dans n'importe quelle application. Pour de l'aide relative aux langages qui ne sont pas répertoriés dans l'image, consultez <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nos blogues<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
{: shortdesc}

</br>

## Affichage des écrans par défaut avec le logiciel SDK Android
{: #android}

Vous pouvez appeler les écrans préconfigurés avec le logiciel SDK Android.
{: shortdesc}

</br>

**Connexion**
1. Placez la commande suivante dans votre code.
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
            //User authenticated
        }
        });
    ```
  {: pre}

</br>
**Inscription**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux d'inscription.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
  		 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

  		 @Override
          public void onAuthorizationCanceled () {
          }

  		 @Override
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: pre}

</br>
**Mot de passe oublié**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et **E-mail d'oubli de mot de passe** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux d'oubli du mot de passe.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
   			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
          public void onAuthorizationCanceled () {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
    ```
    {: pre}

</br>
**Détails du compte**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux de changement des détails.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

  			 @Override
          public void onAuthorizationCanceled () {
          }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 }
  		 });
   ```
   {: pre}

</br>
**Changement du mot de passe**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux de changement du mot de passe.
   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

   			 @Override
          public void onAuthorizationCanceled () {
          }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
   ```
   {: pre}
</br>
</br>

## Affichage des écrans par défaut avec le logiciel SDK Swift iOS
{: #ios-swift}

Vous pouvez appeler les écrans préconfigurés avec le logiciel SDK Swift iOS.
{: shortdesc}

</br>
**Connexion**

1. Placez la commande suivante dans votre code.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
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
  {: pre}


</br>
**Inscription**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux d'inscription.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       if accessToken == nil && identityToken == nil {
        //email verification is required
        return
       }
     //User authenticated
      }
      public func onAuthorizationCanceled() {
        //Sign up canceled by the user
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: pre}

</br>
**Mot de passe oublié**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et **E-mail d'oubli de mot de passe** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux d'oubli du mot de passe. 
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
        //forgot password finished, in this case accessToken and identityToken will be null.
     }

     public func onAuthorizationCanceled() {
         //forgot password canceled by the user
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: pre}

</br>
**Détails du compte**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux de changement des détails.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>
**Changement du mot de passe**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux de changement du mot de passe.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}
</br>
</br>

## Affichage des écrans par défaut avec le logiciel SDK Node.js
{: #nodejs}

Vous pouvez appeler les écrans préconfigurés avec le logiciel SDK Node.js.
{: shortdesc}

</br>
**Connexion**
1. Activez le répertoire cloud dans les paramètres de votre fournisseur d'identité et spécifiez un noeud final de rappel.
2. Ajoutez à votre application une route 'post' qui sera appelée avec le nom d'utilisateur et le mot de passe en paramètres et connectez-vous à l'aide du mot de passe du propriétaire de la ressource.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
    ```
    {: pre}
    `WebAppStrategy` permet aux utilisateurs de se connecter à vos applications Web avec un nom d'utilisateur et un mot de passe. Une fois la connexion établie, le jeton d'accès d'un utilisateur est stocké dans la session HTTP et reste disponible pendant la session. Une fois la session HTTP fermée ou arrivée à expiration, le jeton n'est plus valide.
    {: tip}

</br>
**Inscription**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de répertoire cloud. Si cette option est définie sur no, le processus se termine sans extraction des jetons d'accès et d'identité.
2. Transmettez la propriété WebAppStrategy `show` et définissez-la sur `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**Mot de passe oublié**

1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et **E-mail d'oubli de mot de passe** dans les paramètres de répertoire cloud. Si cette option est définie sur no, le processus se termine sans extraction des jetons d'accès et d'identité.
2. Transmettez la propriété WebAppStrategy `show` et définissez-la sur `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>
**Détails du compte**
1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de répertoire cloud.
2. Transmettez la propriété WebAppStrategy `show` et définissez-la sur `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>
**Changement du mot de passe**
1. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de répertoire cloud.
2. Transmettez la propriété WebAppStrategy `show` et définissez-la sur `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: pre}

</br>
</br>

## Affichage des écrans par défaut avec le logiciel SDK Swift 
{: #swift}

Lorsque les fournisseurs d'identité de réseaux sociaux sont activés, vous pouvez appeler l'écran de connexion préconfiguré avec le logiciel SDK Swift.
{: shortdesc}

1. Le code suivant illustre l'utilisation de WebAppKituraCredentialsPlugin dans une application Kitura pour la protection du noeud final `/protected`.

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
</br>
</br>



