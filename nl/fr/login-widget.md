---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

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


# Affichage du widget de connexion
{: #login-widget}

{{site.data.keyword.appid_full}} fournit un widget de connexion qui vous permet d'offrir à vos utilisateurs des options de connexion sécurisée.
{: shortdesc}

Lorsque votre application est configurée pour utiliser un fournisseur d'identité, le widget de connexion dirige les visiteurs de votre application vers un écran de connexion. Le widget de connexion vous permet d'afficher des écrans préconfigurés pour vos flux de connexion. De plus, il vous permet à tout moment de mettre à jour votre flux de connexion, sans avoir à changer votre code source.

Vous voulez créer une expérience unique pour votre application ? Vous pouvez [apporter vos propres écrans](/docs/services/appid?topic=appid-branded) !
{: tip}

## Comprendre le widget de connexion
{: #widget-understanding}

Vous pouvez tirer parti d'{{site.data.keyword.appid_short_notm}}, y compris sans vos propres écrans d'interface utilisateur, en affichant le widget de connexion.
{: shortdesc}

### Quelle est la valeur par défaut ?
{: #widget-default}

Lorsque plusieurs fournisseurs d'identité sont configurés, l'utilisateur est redirigé vers le widget de connexion lorsqu'il tente de se connecter à votre application. L'utilisation du widget de connexion permet aux utilisateurs de choisir le fournisseur avec lequel ils souhaitent vérifier leur identité. Toutefois, lorsqu'un seul fournisseur est défini sur **Activé**, les visiteurs sont redirigés vers cet écran d'authentification des fournisseurs d'identité.

### Quelle quantité d'informations {{site.data.keyword.appid_short_notm}} obtient-il d'un fournisseur d'identité ?
{: #widget-obtain-info}

Lorsque vous utilisez des fournisseurs d'identité sociaux ou d'entreprise, {{site.data.keyword.appid_short_notm}} dispose d'un accès en lecture aux informations de compte des utilisateurs. Le service utilise un jeton et les assertions qui sont renvoyées par le fournisseur d'identité pour vérifier qu'un utilisateur est bien qui il prétend être. Le service ne disposant jamais d'un accès en écriture aux informations, les utilisateurs doivent passer par le fournisseur d'identité qu'ils ont choisi pour effectuer des actions telles que la réinitialisation de leur mot de passe. Par exemple, si un utilisateur se connecte à votre application avec Facebook et souhaite changer de mot de passe, il doit se rendre sur www.facebook.com pour le faire.

Lorsque vous utilisez [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), le fournisseur d'identité est {{site.data.keyword.appid_short_notm}}. Le service utilise votre registre pour vérifier l'identité de vos utilisateurs. {{site.data.keyword.appid_short_notm}} étant le fournisseur, les utilisateurs peuvent tirer parti des fonctionnalités avancées, telles que la réinitialisation de leur mot de passe, directement dans votre application.


### Quels écrans peuvent être affichés pour chaque fournisseur ?
{: #widget-options}

Consultez le tableau suivant pour voir les écrans que vous pouvez afficher pour chaque type de fournisseur d'identité.

<table>
  <thead>
    <tr>
      <th>Ecran du widget de connexion</th>
      <th>Fournisseur d'identité de réseau social</th>
      <th>Fournisseur d'identité d'entreprise</th>
      <th>Cloud Directory</th>
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

</br>
</br>

## Personnalisation du widget de connexion
{: #widget-customize}

{{site.data.keyword.appid_short_notm}} fournit un écran de connexion par défaut que vous pouvez appeler si vous ne disposez pas de vos propres écrans d'interface utilisateur. Vous pouvez personnaliser l'écran pour afficher le logo et les couleurs de votre choix.
{: shortdesc}

Pour personnaliser l'écran :

1. Ouvrez le tableau de bord du service {{site.data.keyword.appid_short_notm}}.
2. Sélectionnez la section **Personnalisation de la connexion**. Vous pouvez modifier l'apparence du widget de connexion pour l'adapter à la marque de votre entreprise.
3. Téléchargez le logo de votre entreprise en sélectionnant un fichier PNG ou JPG sur votre système local. La taille recommandée pour l'image est de 320 x 320 pixels. La taille maximale du fichier est 100 Ko.
4. Sélectionnez une couleur d'en-tête pour le widget dans la palette de couleurs ou entrez le code hexadécimal d'une autre couleur.
5. Examinez le panneau de prévisualisation, puis cliquez sur **Sauvegarder les modifications** lorsque vous êtes satisfait de vos personnalisations. Un message de confirmation s'affiche.
6. Dans votre navigateur, actualisez votre page de connexion afin de vérifier vos modifications.

N'oubliez pas ! Vous pouvez aussi tirer profit d'{{site.data.keyword.appid_short_notm}} avec d'autres langues. Si vous ne trouvez pas de logiciel SDK pour la langue dans laquelle vous travaillez, vous pouvez toujours utiliser les API. Consultez <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">nos blogues<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
{: tip}


## Affichage du widget de connexion avec le logiciel Android
{: #widget-display-android}

Vous pouvez appeler des écrans préconfigurés avec le [logiciel SDK client Android](https://github.com/ibm-cloud-security/appid-clientsdk-android).
{: shortdesc}

Placez la commande suivante dans votre code.

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
{: codeblock}

</br>

### Inscription
{: #widget-android-signup}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de s'inscrire à votre application** et **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doivent être définis sur **Activé**.
2. Ajoutez le code suivant à votre application. Lorsqu'un utilisateur s'inscrit à votre application à partir de votre écran personnalisé, le flux d'inscription est démarré. L'appel suivant enregistre non seulement l'utilisateur, mais peut également envoyer un courrier électronique de vérification pour terminer l'enregistrement, en fonction de vos configurations de Cloud Directory.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
          public void onAuthorizationCanceled () {
          //Sign up canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              //User authenticated
          } else {
              //email verification is required
          }
      }
  });
  ```
  {: pre}

</br>

### Mot de passe oublié
{: #widget-android-forgot-password}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doit être défini sur **Activé**.
2. Dans l'onglet **Réinitialiser le mot de passe** du tableau de bord du service, vérifiez que **E-mail d'oubli de mot de passe** est défini sur **Activé**.
3. Ajoutez le code suivant à votre application. Lorsqu'un utilisateur clique sur "Mot de passe oublié" dans votre application, le logiciel SDK appelle l'API forgot_password pour lui envoyer un courrier électronique lui permettant de réinitialiser son mot de passe.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
          public void onAuthorizationCanceled () {
          // Forgot password canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Forgot password finished, in this case accessToken and identityToken will be null.
      }
  });
  ```
  {: codeblock}

</br>

### Changement des détails
{: #widget-android-change-details}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de s'inscrire à votre application** et **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doivent être définis sur **Activé**.
2. Dans l'onglet **Mot de passe modifié** du tableau de bord du service, définissez **Courrier électronique de changement de mot de passe** sur
3. Appelez le widget de connexion pour démarrer le flux de changement des détails.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
          public void onAuthorizationCanceled () {
          // Changed details canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // User authenticated, and fresh tokens received
      }
  });
  ```
  {: codeblock}

</br>

### Changement du mot de passe
{: #widget-android-change-password}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de s'inscrire à votre application** et **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doivent être définis sur **Activé**.
2. Placez le code suivant dans votre application pour démarrer le flux de changement de mot de passe.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
          public void onAuthorizationCanceled () {
          // Change password canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // User authenticated, and fresh tokens received
      }
  });
  ```
  {: codeblock}



## Affichage du widget de connexion avec le logiciel SDK Swift iOS
{: #widget-display-ios-swift}

Vous pouvez appeler des écrans préconfigurés avec le [logiciel SDK client Swift iOS](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

Placez la commande suivante dans votre code.

  ```swift
  import IBMCloudAppID
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
  {: codeblock}

</br>

### Inscription
{: #widget-ios-signup}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de s'inscrire à votre application** et **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doivent être définis sur **Activé**.
2. Ajoutez le code suivant dans votre application. Lorsqu'un utilisateur tente de s'inscrire à votre application, le widget de connexion est appelé et affiche votre page d'inscription personnalisée.

  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

### Mot de passe oublié
{: #widget-ios-forgot-password}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doit être défini sur **Activé**.
2. Dans l'onglet **Réinitialiser le mot de passe** du tableau de bord du service, vérifiez que **E-mail d'oubli de mot de passe** est défini sur **Activé**.
3. Ajoutez le code suivant dans votre application. Lorsqu'un utilisateur de votre application demande que son mot de passe soit mis à jour, le widget de connexion est appelé et le processus démarre.

  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

### Changement des détails
{: #widget-ios-change-details}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de s'inscrire à votre application** et **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doivent être définis sur **Activé**.
2. Dans l'onglet **Mot de passe modifié** du tableau de bord du service, définissez **Courrier électronique de changement de mot de passe** sur
3. Appelez le widget de connexion pour démarrer le flux de changement des détails.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //changed details canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>

### Changement du mot de passe
{: #widget-ios-change-password}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de s'inscrire à votre application** et **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doivent être définis sur **Activé**.
2. Placez le code suivant dans votre application pour démarrer le flux de changement de mot de passe.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //change password canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
           //Exception occurred
      }
   }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}


## Affichage du widget de connexion avec le logiciel SDK Node.js
{: #widget-display-nodejs}

Vous pouvez appeler des écrans préconfigurés avec le [logiciel SDK serveur Node.js](https://github.com/ibm-cloud-security/appid-serversdk-nodejs).
{: shortdesc}

Ajoutez à votre application une route 'post' qui sera appelée avec le nom d'utilisateur et le mot de passe en paramètres et connectez-vous à l'aide du mot de passe du propriétaire de la ressource.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

`WebAppStrategy` permet aux utilisateurs de se connecter à vos applications Web avec un nom d'utilisateur et un mot de passe. Une fois la connexion établie, le jeton d'accès d'un utilisateur est stocké dans la session HTTP et reste disponible pendant la session. Lorsque la session HTTP a été détruite ou est arrivée à expiration, le jeton n'est plus valide.
{: tip}

</br>

### Inscription
{: #widget-nodejs-signup}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de s'inscrire à votre application** et **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doivent être définis sur **Activé**.
2. Ajoutez le code suivant dans votre application. Lorsqu'un utilisateur tente de s'inscrire à votre application, le widget de connexion est appelé et affiche votre page d'inscription personnalisée.

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

### Mot de passe oublié
{: #widget-nodejs-forgot-password}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doit être défini sur **Activé**.
2. Dans l'onglet **Réinitialiser le mot de passe** du tableau de bord du service, vérifiez que **E-mail d'oubli de mot de passe** est défini sur **Activé**.
3. Placez le code suivant dans votre application pour transmettre la propriété *show* à `WebAppStrategy.FORGOT_PASSWORD`. Lorsqu'un utilisateur demande que son mot de passe pour votre application soit mis à jour, le widget de connexion est appelé et le processus démarre.

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

### Changement des détails
{: #widget-nodejs-change-details}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de s'inscrire à votre application** et **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doivent être définis sur **Activé**.
2. Dans l'onglet **Mot de passe modifié** du tableau de bord du service, définissez **Courrier électronique de changement de mot de passe** sur
3. Placez le code suivant dans votre application pour transmettre la propriété *show* à `WebAppStrategy.FORGOT_PASSWORD` afin de lancer le formulaire de changement de détails.

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

### Changement du mot de passe
{: #widget-nodejs-change-password}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de s'inscrire à votre application** et **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doivent être définis sur **Activé**.
2. Dans l'onglet **Mot de passe modifié** du tableau de bord du service, définissez **Courrier électronique de changement de mot de passe** sur
3. Placez le code suivant dans votre application pour transmettre la propriété *show* à `WebAppStrategy.FORGOT_PASSWORD` afin de lancer le formulaire de changement de détails.

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
