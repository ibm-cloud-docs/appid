---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Association d'une marque à votre application 
{: #branding}

Vous pouvez afficher vos propres écrans et tirer parti des fonctions d'authentification et d'autorisation d'{{site.data.keyword.appid_full}}. Si vous utilisez le répertoire cloud comme fournisseur d'identité, vos utilisateurs peuvent interagir avec votre application avec peu d'aide de votre part. Ils peuvent se connecter, s'inscrire, changer leur mot de passe, etc., sans avoir à demander de l'aide.
{: shortdesc}

Lorsque vous utilisez vos propres écrans, le [flux Resource Owner Password Credentials](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) est utilisé pour fournir des jetons d'accès et d'identité.


## Association d'une marque à votre application avec le logiciel SDK iOS Swift 
{: #branded-ui-ios-swift}

Lorsque le répertoire cloud est activé, vous pouvez appeler vos propres écrans de marque avec le logiciel SDK iOS Swift.
{: shortdesc}

</br>
**Connexion**

1. Dans l'onglet du fournisseur d'identité de l'interface graphique, activez le répertoire cloud. 
2. Appelez le widget de connexion pour démarrer le flux de connexion. Les jetons d'accès et d'identité sont obtenus lorsqu'un utilisateur tente de se connecte avec son nom d'utilisateur ou son adresse électronique et un mot de passe. 
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

**Inscription**

1. Dans l'onglet du fournisseur d'identité de l'interface graphique, activez le répertoire cloud.
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
3. Appelez le widget de connexion pour démarrer le flux d'inscription. 
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
  {: pre}

</br>

**Mot de passe oublié**

1. Dans l'onglet du fournisseur d'identité de l'interface graphique, activez le répertoire cloud.
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
3. Appelez le widget de connexion pour démarrer le flux d'oubli du mot de passe. 
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
  {: pre}

</br>

**Changement des détails**

1. Dans l'onglet du fournisseur d'identité de l'interface graphique, activez le répertoire cloud.
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
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
  {: pre}

</br>

**Changement du mot de passe**

1. Dans l'onglet du fournisseur d'identité de l'interface graphique, activez le répertoire cloud.
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
3. Appelez le widget de connexion pour démarrer le flux de changement du mot de passe. 
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
  {: pre}

</br>


## Association d'une marque à votre application avec le logiciel SDK Android 
{: #branded-ui-android}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le logiciel SDK Android. Vous pouvez choisir la combinaison d'écrans avec lesquels vos utilisateurs pourront interagir. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Consultez ce blogue <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour un exemple détaillé.
{: shortdesc}

</br>

**Connexion**

1. Activez le fournisseur d'identité **Répertoire cloud**. 
2. Obtenez des jetons d'accès, d'identité et d'actualisation en fournissant le nom d'utilisateur et le mot de passe de l'utilisateur final. 
3. Appelez le widget de connexion pour démarrer le flux de connexion. 
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //User authenticated
        }
  });
  ```
  {: pre}

</br>

**Inscription**

1. Activez le fournisseur d'identité **Répertoire cloud**. 
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
3. Appelez le widget de connexion pour démarrer le flux d'inscription. 
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


**Mot de passe oublié**

1. Activez le fournisseur d'identité **Répertoire cloud**. 
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
3. Appelez le widget de connexion pour démarrer le flux d'oubli du mot de passe. 
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
  {: pre}

</br>

**Changement des détails**

1. Activez le fournisseur d'identité **Répertoire cloud**. 
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
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
  {: pre}


</br>

**Changement du mot de passe**

1. Activez le fournisseur d'identité **Répertoire cloud**. 
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
3. Appelez le widget de connexion pour démarrer le flux de changement de mot de passe. 
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
  {: pre}

</br>
</br>


## Association d'une marque à votre application avec le logiciel SDK Node.js 
{: #branded-ui-nodejs}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le logiciel SDK Node.js.
{: shortdesc}

**Connexion**

Avec WebAppStrategy, les utilisateurs peuvent se connecter à vos applications Web avec leur nom d'utilisateur et un mot de passe. Une fois qu'un utilisateur est connecté à votre application, son jeton d'accès est conservé dans une session HTTP tant qu'il est actif. Lorsque la session HTTP est fermée ou expire, le jeton d'accès est détruit. 

1. Activez le répertoire cloud dans vos paramètres de fournisseur d'identité et spécifiez un noeud final de rappel. 
2. Ajoutez à votre application une route 'post' qui peut être appelée avec les paramètres de nom d'utilisateur et de mot de passe et connectez-vous avec le flux de mot de passe du propriétaire de la ressource.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: pre}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres de commande </th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>URL vers laquelle rediriger l'utilisateur lorsque l'authentification réussit. </td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>URL vers laquelle rediriger l'utilisateur si l'authentification échoue. </td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td>Lorsque la valeur est <code>true</code>, un message d'erreur est renvoyé depuis le service de répertoire cloud. Par défaut, la valeur est <code>false</code>.</td>
      </tr>
    </tbody>
  </table>

  1. Si vous soumettez la demande dans un formulaire HTML, vous pouvez utiliser le middleware [body parser](https://www.npmjs.com/package/body-parser). 
  2. Pour obtenir le message d'erreur renvoyé, vous pouvez utiliser [connect-flash](https://www.npmjs.com/package/connect-flash). Pour plus d'informations, voir l'[exemple d'application Web](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js). {: tip}

</br>
**Inscription**

1. Activez le répertoire cloud dans vos paramètres de fournisseur d'identité et spécifiez un noeud final de rappel. 
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
3. Pour **Autoriser les utilisateurs à se connecter sans vérifier leur adresse électronique**, sélectionnez **Non**. Sinon, les jetons d'accès et d'identité d'{{site.data.keyword.appid_short_notm}} ne pourront pas être extraits. 
4. Ajoutez à votre application une route 'post' qui peut être appelée avec les paramètres de nom d'utilisateur et de mot de passe et connectez-vous avec le flux de mot de passe du propriétaire de la ressource. 
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**Mot de passe oublié**

1. Activez le répertoire cloud dans vos paramètres de fournisseur d'identité et spécifiez un noeud final de rappel. 
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
3. Activez **E-mail d'oubli de mot de passe**. 
4. Transmettez la propriété *show* à `WebAppStrategy.FORGOT_PASSWORD` pour ouvrir le formulaire d'oubli de mot de passe. 
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**Changement des détails**

1. Activez le répertoire cloud dans vos paramètres de fournisseur d'identité et spécifiez un noeud final de rappel. 
2. Activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres du répertoire cloud. 
3. Vérifiez que l'utilisateur s'est authentifié précédemment auprès d'{{site.data.keyword.appid_short_notm}}.
4. Transmettez la propriété *show* à `WebAppStrategy.CHANGE_DETAILS` pour ouvrir le formulaire d'oubli de mot de passe. 
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## Association d'une marque à votre application avec l'API 
{: #branded-ui-api}

Vous pouvez afficher vos propres écrans et tirer parti des fonctions d'authentification et d'autorisation d'{{site.data.keyword.appid_short_notm}}. Si vous utilisez un répertoire cloud comme fournisseur d'identité, vos utilisateurs peuvent interagir avec votre application avec peu d'aide de votre part. Ils peuvent se connecter, s'inscrire, réinitialiser leur mot de passe, etc., sans demander d'aide.
{: shortdesc}

Pour que ces opérations soient possibles, {{site.data.keyword.appid_short_notm}} expose des API REST. Vous pouvez utiliser l'API REST pour générer un serveur de back end dédié à vos applications Web, ou pour interagir avec une application mobile avec vos propres écrans personnalisés.

L'API de gestion est sécurisée via des jetons générés par IBM Cloud Identity and Access Management. Cela signifie que les propriétaires de compte peuvent spécifier le niveau d'accès de chaque membre de leur équipe pour chaque instance de service. Pour plus d'informations sur la façon dont IAM et {{site.data.keyword.appid_short_notm}} fonctionnent ensemble, voir [Gestion des accès de service](/docs/services/appid/iam.html).

Une fois que vous avez configuré vos [paramètres](/docs/services/appid/cloud-directory.html), vous pouvez appeler les noeuds finaux ci-dessous pour afficher chaque écran. 


**Inscription**
Vous pouvez utiliser le noeud final `/sign_up` pour autoriser les utilisateurs à s'inscrire eux-mêmes à votre application.
Indiquez les données suivantes dans le corps de demande :
  * Votre ID titulaire.
  * Les données utilisateur du répertoire cloud. Voir [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) pour plus de détails.
    * Un attribut `password`.
    * Le tableau d'adresses électroniques dont l'attribut `primary` a la valeur `true` doit comporter au moins une adresse électronique. 

Selon vos [configurations de
courrier électronique](/docs/services/appid/cloud-directory.html), il est possible qu'un utilisateur reçoive une demande
de vérification
ou un courrier électronique de bienvenue lorsqu'il s'inscrit à votre application. Ces deux types de courrier électronique sont déclenchés lorsqu'un utilisateur s'inscrit à votre application. Le courrier électronique de vérification comporte un bouton **Vérifier**. Lorsque l'utilisateur clique sur le bouton et confirme son identité, {{site.data.keyword.appid_short_notm}} affiche un écran de remerciement pour la vérification.  

Vous pouvez présenter votre propre page post-vérification :

1. Accédez à l'onglet des **pages d'arrivée personnalisées** du tableau de bord {{site.data.keyword.appid_short_notm}}.
2. Entrez l'URL de votre page d'arrivée dans la zone d'**URL pour la page de vérification de votre adresse électronique personnalisée**. 

Si cette valeur est fournie, {{site.data.keyword.appid_short_notm}} appel l'URL au moyen d'une requête `context`. Lorsque vous appelez le noeud final `/sign_up/confirmation_result` et transmettez le paramètre `context` reçu, le résultat vous indique si l'utilisateur a vérifié son compte. Si tel est le cas, vous pouvez afficher votre page personnalisée.

</br>
**Mot de passe oublié**

Vous pouvez utiliser le noeud final `/forgot_password` pour autoriser les utilisateurs à récupérer leur mot de passe en cas d'oubli.

Indiquez les données suivantes dans le corps de demande :
  * Votre ID titulaire.
  * L'adresse électronique de l'utilisateur de répertoire cloud.

Lorsque le noeud final est appelé, un courrier électronique de réinitialisation de mot de passe est envoyé à l'utilisateur. Il contient un bouton **Réinitialiser**. Une fois que l'utilisateur a cliqué sur le bouton, {{site.data.keyword.appid_short_notm}} affiche un écran permettant à l'utilisateur de réinitialiser son mot de passe.

Vous pouvez présenter votre propre page post-réinitialisation de mot de passe :

1. Accédez à l'onglet des **pages d'arrivée personnalisées** du tableau de bord {{site.data.keyword.appid_short_notm}}.
2. Entrez l'URL de votre page d'arrivée dans la zone d'**URL pour la page de réinitialisation de mot de passe personnalisée**.   

Si cette valeur est fournie, {{site.data.keyword.appid_short_notm}} appel l'URL au moyen d'une requête `context`. Le paramètre `context` est utilisé pour recevoir le résultat lorsque le noeud final `/forgot_password/confirmation_result` est appelé. En cas de réussite, vous pouvez afficher votre page personnalisée.

Ajoutez une chaîne aléatoire à votre page de réinitialisation de mot de passe personnalisée et transmettez-la à votre système de back end lorsque la demande est soumise. Demandez à votre gestionnaire de valider la chaîne et appelez le noeud final `/change_password` uniquement si elle est valide. Ainsi, vous pouvez réduire la vulnérabilité de votre noeud final de réinitialisation de mot de passe sur le système de back end.
{: tip}

</br>
**Changement du mot de passe**

Vous pouvez utiliser le noeud final `/change_password` dans deux cas : lorsqu'un utilisateur soumet une demande de réinitialisation ou lorsqu'un utilisateur est connecté à votre application et souhaite mettre à jour son mot de passe.

Indiquez les informations suivantes dans le corps de demande pour mettre à jour le mot de passe après une demande de réinitialisation : 
  * Votre ID titulaire.
  * Le nouveau mot de passe de l'utilisateur.
  * L'identificateur unique universel de l'utilisateur de répertoire cloud.
  * Facultatif : l'adresse IP à partir de laquelle a été effectuée la réinitialisation du mot de passe. Si vous choisissez de transmettre l'adresse IP, l'espace réservé `%{passwordChangeInfo.ipAddress}` est disponible pour le modèle de courrier électronique de changement de mot de passe.

En fonction de votre configuration, lorsqu'un mot de passe est changé, il est possible qu'{{site.data.keyword.appid_short_notm}} envoie un courrier électronique à l'utilisateur pour lui faire savoir qu'il y a eu un changement.

</br>
Pour autoriser des utilisateurs à changer leur mot de passe lorsqu'ils sont connectés à votre application :

Indiquez les données suivantes dans le corps de demande :
  * Votre ID titulaire.
  * Le nouveau mot de passe de l'utilisateur.
  * L'identificateur unique universel de l'utilisateur de répertoire cloud.

Votre page de changement de mot de passe doit inviter l'utilisateur à entrer son mot de passe en cours et son nouveau mot de passe.
{: tip}

Votre système de back end valide le mot de passe en cours de l'utilisateur avec l'API ROP, et si celui-ci est valide, appelle le noeud final avec le nouveau mot de passe. En fonction de votre configuration, lorsqu'un mot de passe est changé, il est possible qu'{{site.data.keyword.appid_short_notm}} envoie un courrier électronique à l'utilisateur pour lui faire savoir qu'il y a eu un changement.

</br>
**Renvoi**

Vous pouvez utiliser `/resend/{templateName}` pour renvoyer un courrier électronique si un utilisateur ne l'a pas reçu pour une raison quelconque. 

Indiquez les données suivantes dans le corps de demande :
  * L'ID titulaire. 
  * Le nom de modèle.
  * L'identificateur unique universel de l'utilisateur de répertoire cloud.


**Changement des détails**

Lorsqu'un utilisateur est connecté à votre application, il peut mettre à jour certaines de ses informations. Vous pouvez utiliser le noeud final `/Users/{userId}` pour récupérer et mettre à jour ses informations.

Lorsque les détails de l'utilisateur sont mis à jour, le noeud final obtient les données utilisateur mises à jour dans le corps de demande au [format SCIM](https://tools.ietf.org/html/rfc7643#section-8.2). Veillez à modifier uniquement les détails pertinents.

L'adresse électronique des utilisateurs ne peut pas être changée.
{: tip}
