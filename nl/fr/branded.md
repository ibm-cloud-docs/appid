---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Personnalisation de la connexion
{: #branding}

Vous pouvez afficher vos propres interfaces utilisateur personnalisées tout en tirant parti des fonctions d'authentification et d'autorisation d'{{site.data.keyword.appid_full}}. Avec un répertoire cloud comme fournisseur d'identité, vos utilisateurs peuvent interagir avec votre application avec un minimum d'aide de votre part. Ils peuvent se connecter, s'inscrire, modifier leur mot de passe et effectuer bien d'autres opérations sans demander votre aide.
{: shortdesc}

Avec un répertoire cloud comme fournisseur d'identité, le [flux des données d'identification du mot de passe du propriétaire de la ressource](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) est utilisé pour fournir des jetons d'accès et d'identité.

**Remarque** : Vous ne pouvez apporter des pages de connexion personnalisées que si un répertoire cloud est la seule option configurée. Avec tout autre fournisseur d'identité défini sur **on**, l'écran de connexion préconfiguré s'affiche.

## Affichage d'écrans personnalisés avec le SDK Android
{: #branded-ui-android}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le SDK Android. Vous pouvez choisir la combinaison d'écrans avec lesquels vos utilisateurs pourront interagir. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Découvrez notre blogue ! <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
{: shortdesc}

</br>
**Se connecter**

1. Définissez **Répertoire cloud** sur **On** comme fournisseur d'identité.
2. Placez la commande suivante dans votre code.
  ```java
  AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
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
  {: codeblock}

</br>
**S'inscrire**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Inscription.
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
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: codeblock}

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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
   		 });
    ```
    {: codeblock}

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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
  		 });
   ```
   {: codeblock}

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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
   		 });
   ```
   {: codeblock}

</br>
</br>

## Affichage d'écrans personnalisés avec le SDK Swift iOS
{: #branded-ui-ios-swift}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le SDK Swift iOS. Vous pouvez choisir la combinaison d'écrans avec lesquels vos utilisateurs pourront interagir.
{: shortdesc}

</br>
**Se connecter**

1. Dans l'onglet Fournisseur d'identité de l'interface graphique, définissez Répertoire cloud sur **On**.
2. Connectez-vous à l'aide du mot de passe du propriétaire de la ressource. Vous pouvez obtenir des jetons d'accès et d'identité en fournissant le nom d'utilisateur et le mot de passe de l'utilisateur final.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}

</br>
**S'inscrire**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Inscription.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

</br>
**Mot de passe oublié**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et **E-mail d'oubli de mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Mot de passe oublié.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

</br>
**Détails du compte**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Changer les détails.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>
**Changer le mot de passe**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud.
2. Appelez LoginWidget pour démarrer le flux Changer le mot de passe.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}

</br>

## Affichage d'écrans personnalisés avec le SDK Node.js
{: #branded-ui-nodejs}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le SDK Node.js. Vous pouvez choisir la combinaison d'écrans avec lesquels vos utilisateurs pourront interagir.
{: shortdesc}

**Se connecter**
1. Définissez Répertoire cloud sur **On** dans les paramètres de votre fournisseur d'identité et spécifiez un point d'extrémité de rappel.
2. Ajoutez à votre application une route 'post' qui sera appelée avec le nom d'utilisateur et le mot de passe en paramètres et connectez-vous à l'aide du mot de passe du propriétaire de la ressource.
    **Remarque** : `WebAppStrategy` autorise les utilisateurs à se connecter à vos applications Web avec un nom d'utilisateur et un mot de passe. Une fois la connexion établie, un jeton d'accès de l'utilisateur est stocké dans la session HTTP et reste disponible pendant toute la durée de la session. Une fois la session HTTP fermée ou arrivée à expiration, le jeton n'est plus valide.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
    ```
    {: codeblock}

</br>
**S'inscrire**

1. Définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On** dans les paramètres de répertoire cloud. Si cette option est définie sur no, le processus se termine sans réception des jetons d'accès et d'identité.
2. Transmettez la propriété WebAppStrategy `show` et définissez-la sur `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

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
  {: codeblock}

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
  {: codeblock}

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
  {: codeblock}
