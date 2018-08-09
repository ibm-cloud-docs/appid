---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Gestion de l'expérience de connexion

{{site.data.keyword.appid_full}} fournit un widget de connexion permettant de fournir aux utilisateurs des options de connexion sécurisée.
{: shortdesc}

Lorsque votre application est configurée pour utiliser un fournisseur d'identité, le widget de connexion dirige les visiteurs de votre application vers un écran de connexion. Par défaut, lorsqu'un seul fournisseur est défini comme actif, les visiteurs sont redirigés vers l'écran d'authentification de ce fournisseur d'identité. Le widget de connexion vous permet d'afficher un écran de connexion par défaut ou, avec le répertoire cloud, de réutiliser celui de votre interface utilisateur existante.

Vous pouvez à tout moment mettre à jour votre flux de connexion, sans avoir besoin de changer votre code source.
{: tip}

Le service utilise des types d'autorisation d'accès OAuth 2 pour mapper le processus d'autorisation. Lorsque vous configurez des fournisseurs d'identité de réseaux sociaux tels que Facebook, le [flux d'octroi d'autorisation Oauth2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) est utilisé pour appeler le widget de connexion. Lorsque vous affichez vos propres écrans d'interface utilisateur, le [flux Resource Owner Password Credentials](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) est utilisé pour la connexion et l'obtention de jetons d'accès et d'identité.


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


## Affichage des écrans par défaut
{: #default}

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


Cliquez sur le langage de votre choix dans l'image suivante pour commencer l'implémentation du code.

<img usemap="#default-options-map" border="0" class="image" id="options" src="images/default-options.png" width="750" alt="Cliquez sur une icône de langage SDK pour commencer avec le répertoire cloud dans vos applications." style="width:750px;" />
<map name="default-options-map" id="default-options-map">
<area href="login-widget.html#android" alt="Gestion de l'expérience de connexion avec le SDK Android" shape="rect" coords="113, 8, 224, 123" />
<area href="login-widget.html#ios-swift" alt="Gestion de l'expérience de connexion avec le SDK Swift iOS." shape="rect" coords="251, 12, 362, 127" />
<area href="login-widget.html#nodejs" alt="Gestion de l'expérience de connexion avec le SDK Node.js." shape="rect" coords="387, 10, 498, 125" />
<area href="login-widget.html#swift" alt="Gestion de l'expérience de connexion avec le SDK Swift." shape="rect" coords="525, 10, 636, 125" />
</map>
</br>

### Affichage des écrans par défaut avec le SDK Android
{: #android}

Vous pouvez appeler les écrans préconfigurés avec le SDK Android.
{: shortdesc}

</br>

**Se connecter**
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
**S'inscrire**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
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

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et **E-mail d'oubli de mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Mot de passe oublié.
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

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Changer les détails.
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
**Changer le mot de passe**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Changer le mot de passe.
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

### Affichage des écrans par défaut avec le SDK Swift iOS
{: #ios-swift}

Vous pouvez appeler les écrans préconfigurés avec le SDK Swift iOS.
{: shortdesc}

</br>
**Se connecter**

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
**S'inscrire**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
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

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et **E-mail d'oubli de mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Mot de passe oublié.
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

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Changer les détails.
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
**Changer le mot de passe**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Changer le mot de passe.
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

### Affichage des écrans par défaut avec le SDK Node.js
{: #nodejs}

Vous pouvez appeler les écrans préconfigurés avec le SDK Node.js.
{: shortdesc}

</br>
**Se connecter**
1. Définissez Répertoire cloud sur **On** dans les paramètres de votre fournisseur d'identité et spécifiez un point d'extrémité de rappel.
2. Ajoutez à votre application une route 'post' qui sera appelée avec le nom d'utilisateur et le mot de passe en paramètres et connectez-vous à l'aide du mot de passe du propriétaire de la ressource.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
    ```
    {: pre}
    `WebAppStrategy` permet aux utilisateurs de se connecter à vos applications Web avec un nom d'utilisateur et un mot de passe. Une fois la connexion établie, le jeton d'accès d'un utilisateur est stocké dans la session HTTP et reste disponible pendant la session. Une fois la session HTTP fermée ou arrivée à expiration, le jeton n'est plus valide.{: tip}

</br>
**S'inscrire**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud. Si cette option est définie sur no, le processus se termine sans extraction des jetons d'accès et d'identité.
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

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et **E-mail d'oubli de mot de passe** sur **On** dans les paramètres de répertoire cloud. Si cette option est définie sur no, le processus se termine sans extraction des jetons d'accès et d'identité.
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
1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Transmettez la propriété WebAppStrategy `show` et définissez-la sur `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>
**Changer le mot de passe**
1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
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
### Affichage de l'interface utilisateur par défaut avec le SDK Swift
{: #swift}

Lorsque les fournisseurs d'identité de réseaux sociaux sont activés, vous pouvez appeler l'écran de connexion préconfiguré avec le SDK Swift.
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


### Affichage d'écrans personnalisés avec le SDK Android
{: #branded-ui-android}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le SDK Android. Vous pouvez choisir la combinaison d'écrans avec lesquels vos utilisateurs pourront interagir. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Consultez ce blogue <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour un exemple détaillé.
{: shortdesc}

</br>
**Se connecter**

1. Définissez **Répertoire cloud** sur **On** comme fournisseur d'identité.
2. Placez la commande suivante dans votre code.
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
             //Exception occurred
      }

          @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //User authenticated
        }
         });
  ```
  {: pre}

</br>
</br>

### Affichage d'écrans personnalisés avec le SDK Swift iOS
{: #branded-ui-ios-swift}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le SDK Swift iOS.
{: shortdesc}

</br>
**Se connecter**

1. Dans l'onglet Fournisseur d'identité de l'interface graphique, définissez Répertoire cloud sur **On**.
2. Connectez-vous à l'aide du mot de passe du propriétaire de la ressource. Des jetons d'accès et d'identité sont obtenus lorsqu'un utilisateur tente de se connecter à l'aide de ses nom d'utilisateur et mot de passe.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: pre}
</br>
</br>

### Affichage d'écrans personnalisés avec le SDK Node.js
{: #branded-ui-nodejs}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le SDK Node.js. Vous pouvez choisir la combinaison d'écrans avec lesquels vos utilisateurs pourront interagir. Si vous choisissez une système de back end de type Node.js, vous pouvez utiliser notre module en libre-service qui se trouve dans le SDK {{site.data.keyword.appid_short_notm}} Node.js (lien).
{: shortdesc}

**Se connecter**
1. Définissez Répertoire cloud sur **On** dans les paramètres de votre fournisseur d'identité et spécifiez un point d'extrémité de rappel.
2. Ajoutez à votre application une route 'post' qui sera appelée avec le nom d'utilisateur et le mot de passe en paramètres et connectez-vous à l'aide du mot de passe du propriétaire de la ressource.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
    ```
    {: pre}
    `WebAppStrategy` permet aux utilisateurs de se connecter à vos applications Web avec un nom d'utilisateur et un mot de passe. Une fois la connexion établie, le jeton d'accès d'un utilisateur est stocké dans la session HTTP et reste disponible pendant la session. Une fois la session HTTP fermée ou arrivée à expiration, le jeton n'est plus valide.{: tip}

</br>
</br>

## Affichage d'écrans personnalisés avec l'API
{: #branding}

Vous pouvez afficher vos propres écrans et tirer parti des fonctions d'authentification et d'autorisation d'{{site.data.keyword.appid_short_notm}}. Avec un répertoire cloud comme fournisseur d'identité, vos utilisateurs peuvent interagir avec votre application avec un minimum d'aide de votre part. Ils peuvent se connecter, s'inscrire, réinitialiser leur mot de passe et effectuer bien d'autres opérations sans demander votre aide.
{: shortdesc}

Pour rendre cela possible, {{site.data.keyword.appid_short_notm}} a exposé des API REST. Vous pouvez utiliser l'API REST API pour générer un serveur de back end destiné à vos applications Web, ou pour interagir avec une application mobile avec vos propres écrans personnalisés.

L'API de gestion est sécurisée via des jetons générés par IBM Cloud Identity et Access Management. Cela signifie que les propriétaires de compte peuvent spécifier quels membres de leur équipe dispose de tel ou tel niveau d'accès pour chaque instance de service. Pour plus d'informations sur la façon dont IAM et {{site.data.keyword.appid_short_notm}} fonctionnent ensemble, voir [Gestion des accès de service](/docs/services/appid/iam.html).

Lorsqu'un utilisateur clique pour se connecter depuis votre écran personnalisé, le [flux Resource Owner Password Credentials](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) est utiliser pour obtenir des jetons d'accès et d'identité directement depuis vos applications Web ou mobiles.

Une fois que vous avez configuré vos [paramètres](/docs/services/appid/cloud-directory.html),


**Inscrivez-vous**
Vous pouvez utiliser le noeud final `/sign_up` pour autoriser les utilisateurs à s'inscrire eux-mêmes à votre application.
Indiquez les données suivantes dans le corps de demande :
  * Votre tenantID (ID titulaire).
  * Les données utilisateur du répertoire cloud. Voir [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) pour plus de détails. 
    * Un attribut `password`.
    * Dans le tableau d'e-mails avec un attribut `primary` défini sur `true`, vous devez avoir au moins 1 adresse e-mail.

En fonction de vos [configurations d'e-mail](/docs/services/appid/cloud-directory.html), il est possible qu'un utilisateur reçoive une demande de vérification, ou un e-mail de bienvenue lorsqu'il s'inscrit à votre application. Ces deux types d'e-mail sont déclenchés quand un utilisateur s'inscrit à votre application. L'e-mail de vérification comporte un bouton **Vérifier**. Une fois que l'utilisateur clique sur le bouton et confirme son identité, {{site.data.keyword.appid_short_notm}} affiche un écran de remerciement pour la vérification.  

Vous pouvez présenter votre propre page post-vérification :

1. Accédez à l'onglet des **pages d'arrivée personnalisées** du tableau de bord {{site.data.keyword.appid_short_notm}}.
2. Entrez l'URL de votre page d'arrivée dans la zone **URL pour la page de vérification de votre adresse e-mail personnalisée**

Quand cette valeur est fournie, {{site.data.keyword.appid_short_notm}} appel l'URL au moyen d'une requête `context`. Lorsque vous appelez le noeud final `/sign_up/confirmation_result` et transmettez le paramètre `context` reçu, le résultat vous indique si l'utilisateur a vérifié son compte. Si tel est le cas, vous pouvez afficher votre page personnalisée.

</br>
**Mot de passe oublié**

Vous pouvez utiliser le noeud final `/forgot_password` pour autoriser les utilisateurs à récupérer leurs mots de passe en cas d'oubli.

Indiquez les données suivantes dans le corps de demande :
  * Votre tenantID (ID titulaire).
  * L'e-mail de l'utilisateur de répertoire cloud.

Lorsque le noeud final est appelé, un e-mail de réinitialisation de mot de passe est envoyé à l'utilisateur. Cet e-mail contient un bouton **Réinitialiser**. Une fois que l'utilisateur a cliqué sur le bouton, {{site.data.keyword.appid_short_notm}} affiche un écran permettant à l'utilisateur de réinitialiser son mot de passe.

Vous pouvez présenter votre propre page post-réinitialisation de mot de passe :

1. Accédez à l'onglet des **pages d'arrivée personnalisées** du tableau de bord {{site.data.keyword.appid_short_notm}}.
2. Entrez l'URL de votre page d'arrivée dans la zone d'**URL pour la page de réinitialisation de mot de passe personnalisée**  

Quand cette valeur est fournie, {{site.data.keyword.appid_short_notm}} appel l'URL au moyen d'une requête `context`. Le paramètre `context` est utilisé pour recevoir le résultat quand le noeud final `/forgot_password/confirmation_result` est appelé. En cas de réussite, vous pouvez afficher votre page personnalisée.

Ajoutez une chaîne aléatoire à votre page de réinitialisation de mot de passe personnalisée et transmettez-la à votre système de back end quand la demande est soumise. Faites en sorte que votre gestionnaire valide la chaîne et appelle le noeud final `/change_password` uniquement si elle est valide. En procédant ainsi, vous pouvez réduire la vulnérabilité de votre noeud final de réinitialisation de mot de passe de back end.
{: tip}

</br>
**Changer le mot de passe**

Vous pouvez utiliser le noeud final `/change_password` de deux façons. Quand un utilisateur soumet une demande de réinitialisation ou quand un utilisateur est connecté à votre application et souhaite mettre à jour son mot de passe.

Pour mettre à jour un mot de passe après une demande de réinitialisation :

Indiquez les données suivantes dans le corps de demande :
  * Votre tenantID (ID titulaire).
  * Le nouveau mot de passe de l'utilisateur.
  * L'UUID utilisateur de répertoire cloud.
  * Facultatif : L'adresse IP à partir de laquelle a été effectuée la réinitialisation du mot de passe. Si vous choisissez de transmettre l'adresse IP, l'espace réservé `%{passwordChangeInfo.ipAddress}` est disponible pour le modèle d'e-mail de changement de mot de passe.

En fonction de votre configuration, quand un mot de passe est changé il est possible que {{site.data.keyword.appid_short_notm}} envoie un e-mail à l'utilisateur pour lui faire savoir qu'il y a eu un changement.

</br>
Pour autoriser des utilisateurs à changer leurs mots de passe lorsqu'ils sont connectés à votre application : 

Indiquez les données suivantes dans le corps de demande :
  * Votre tenantID (ID titulaire).
  * Le nouveau mot de passe de l'utilisateur.
  * L'UUID utilisateur de répertoire cloud.

Votre page de changement de mot de passe doit inviter l'utilisateur à entrer son mot de passe en cours et son nouveau mot de passe.
{: tip}

Votre système de back end valide le mot de passe en cours de l'utilisateur avec l'API ROP, et si celui-ci est valide, appelle le noeud final avec le nouveau mot de passe. En fonction de votre configuration, quand un mot de passe est changé il est possible que {{site.data.keyword.appid_short_notm}} envoie un e-mail à l'utilisateur pour lui faire savoir qu'il y a eu un changement.

</br>
**Renvoyer**

Vous pouvez utiliser le noeud final `/resend/{templateName}` pour renvoyer un e-mail quand un utilisateur ne l'a pas reçu.

Indiquez les données suivantes dans le corps de demande :
  * Le tenantID (ID titulaire).
  * Le nom de modèle.
  * L'UUID utilisateur de répertoire cloud.


**Changer les détails**

Quand un utilisateur est connecté à votre application, il peut mettre à jour certaines de ses informations. Vous pouvez utiliser le noeud final `/Users/{userId}` pour récupérer et mettre à jour ses informations.

Quand les détails de l'utilisateur sont mises à jour, le noeud final obtient les données utilisateur mises à jour dans le corps de demande au [format SCIM](https://tools.ietf.org/html/rfc7643#section-8.2). Veillez à modifier uniquement les détails pertinents.

L'adresse e-mail des utilisateurs ne peut pas être changée.
{: tip}
