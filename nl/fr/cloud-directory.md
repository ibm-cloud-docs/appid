---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Gestion de Cloud Directory
{: #cd}

{{site.data.keyword.appid_short_notm}} peut être configuré pour utiliser
Cloud Directory comme fournisseur d'identité.
Lorsque des utilisateurs s'inscrivent avec leur adresse e-mail et un mot de passe, ils sont ajoutés à votre annuaire et
vous pouvez dès lors les gérer à partir de l'interface graphique du service.
{: shortdesc}

<!--- What is a cloud directory? --->

## Gestion des paramètres d'annuaire

Vous pouvez configurer les notifications et le niveau de contrôle de votre
application par les utilisateurs.
Dans l'onglet **Paramètres d'annuaire** de l'interface graphique,
vous pouvez choisir le niveau d'autonomie dont bénéficieront vos utilisateurs.


1. Pour permettre aux utilisateurs d'utiliser une adresse e-mail pour s'inscrire,
vous devez **activer** l'option
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe**.
Lorsque cette option est **désactivée**, vous pouvez toujours ajouter des utilisateurs via la console,
mais seulement pour vos besoins de développement.

2. Configurez les détails de l'expéditeur.
Spécifiez l'adresse e-mail à partir de laquelle les messages seront envoyés, quel nom d'expéditeur apparaîtra
et à qui les utilisateurs pourront répondre.
**Remarque **: lors de la configuration de votre URL d'action,
accordez à l'utilisateur un délai suffisant
pour lui laisser le temps de cliquer sur le lien.
Pour bénéficier de certaines options, telles que la possibilité de demander une
réinitialisation de son mot de passe, l'utilisateur doit confirmer la validité
(l'existence) de son adresse e-mail.

3. Déterminez les types d'e-mails reçus par l'utilisateur et les informations sur l'expéditeur.



## Gestion des messages

Un modèle est un exemple d'e-mail que vous pouvez envoyer à vos utilisateurs.
Vous pouvez personnaliser le modèle en modifiant le contenu et la présentation du
message.
Chaque type de message peut être **activé** ou **désactivé** dans l'onglet Paramètres d'annuaire.


1. Sélectionnez un **Type de message**.
2. Personnalisez votre message en changeant sa conception et son contenu.
Vous pouvez utiliser des paramètres à cet effet.
N'oubliez pas de sauvegarder vos changements !


### Types de messages

<dl>
  <dt> Bienvenue </dt>
    <dd>Vous pouvez envoyer un e-mail de bienvenue à chaque utilisateur de votre application venant de s'inscrire.
Réservez le meilleur accueil à vos utilisateurs. Pour les fidéliser, choisissez un message aussi engageant que
possible.
<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Paramètres utilisables dans tous les types de messages </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Affiche l'image que vous avez configurée pour votre widget de connexion. </td>
        </tr>
	 <tr>
          <td> %{display.headerColor} </td>
          <td> Affiche la couleur d'en-tête que vous avez configurée pour votre widget de connexion. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> Affiche le pseudonyme (appelé nom d'écran dans l'interface) que l'utilisateur a choisi d'utiliser lorsqu'il interagit avec l'application.</td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> Affiche l'adresse e-mail avec laquelle l'utilisateur s'est inscrit.</td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> Affiche le prénom spécifié par l'utilisateur.</td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Affiche le nom complet de l'utilisateur. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Affiche le nom de famille spécifié par l'utilisateur.</td>
        </tr>
      </tbody>
    </table>

    **Remarque **: un blanc apparaîtra à la place d'un paramètre si l'utilisateur n'a pas fourni l'information correspondante. </dd>
  <dt> Mot de passe oublié</dt>
    <dd> Un utilisateur peut demander à faire réinitialiser son mot de passe s'il l'a
oublié ou s'il doit en changer pour une raison quelconque.
Vous pouvez personnaliser l'e-mail de réponse à cette demande.
Le mot de passe restera inchangé tant que l'utilisateur n'aura pas cliqué sur le lien figurant dans cet e-mail de réponse.
<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Paramètres de changement de mot de passe</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Affiche le nombre d'heures de validité du lien. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Affiche le nombre de minutes de validité du lien. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> Affiche un code d'accès à usage unique incorporé dans l'URL.
Chaque personne recevra donc un code différent. Exemple : <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Affiche le lien sur lequel l'utilisateur doit cliquer pour réinitialiser son mot de passe.
</td>
        </tr>
       </tbody>
    </table></dd>
  <dt> Vérification
</dt>
    <dd> Vous pouvez demander que l'utilisateur confirme l'existence de son compte mail en lui envoyant un e-mail à cet effet.
Vous limiterez ainsi le nombre de faux comptes (notamment les robots) qui peuvent s'inscrire à votre application.
Vous pouvez restreindre l'accès à votre application tant que l'utilisateur n'a pas prouvé la validité de son adresse e-mail.
Utilisable aussi comme moyen de gérer pour quels utilisateurs vous créez des profils.
<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Paramètres du message de vérification </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Affiche le nombre d'heures de validité du lien. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Affiche le nombre de minutes de validité du lien. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> Affiche une URL de vérification à usage unique.
</td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> Affiche l'URL d'action que vous avez spécifiée dans les paramètres.
</td>
        </tr>
      </tbody>
    </table></dd>
  <dt> Changement du mot de passe
</dt>
    <dd> Vous pouvez faire savoir à l'utilisateur que son mot de passe a changé.
C'est particulièrement utile s'il n'en a pas fait la demande.
Il peut alors prendre les mesures appropriées pour sécuriser à nouveau son compte.
<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Paramètres de changement de mot de passe</th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> Affiche l'heure à laquelle un nouveau mot de passe est entré en vigueur. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Affiche l'adresse IP d'où provient la demande de changement de mot de passe. </td>
        </tr>
      </tbody>
    </table></dd>
</dl>



## Gestion de Cloud Directory avec le SDK Android
{: #managing-android}

Veillez à **activer** le **fournisseur d'identité Cloud Directory** lorsque vous
utilisez les API suivantes.


### Connexion avec le mot de passe du propriétaire de la ressource
Vous pouvez obtenir des jetons d'accès et d'identité en fournissant le nom d'utilisateur et le mot de passe de l'utilisateur final.

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

### Inscription

Veillez à **activer** l'option
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de Cloud Directory.


 Utilisez la classe LoginWidget pour démarrer le flux Inscription.
 ```java
 LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
			 @Override
			 public void onAuthorizationFailure (AuthorizationException exception) {
				 //Exception occurred 		}

			 @Override
        public void onAuthorizationCanceled () {
				 //Sign up canceled by the user
			 }

			 @Override
			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
				 if (accessToken != null && identityToken != null) {
				     //User authenticated
				 } else {
				     //email verification is required
				 }

			 }
		 });
 ```
 {: codeblock}

### Mot de passe oublié
Veillez à **activer** les options
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et
**E-mail d'oubli de mot de passe** dans les paramètres de Cloud Directory.


Utilisez la classe LoginWidget pour démarrer le flux Mot de passe oublié
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
 			 public void onAuthorizationFailure (AuthorizationException exception) {
 				 //Exception occurred 		}

 			 @Override
        public void onAuthorizationCanceled () {
 				 //forogt password canceled by the user
 			 }

 			 @Override
 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
 				 //forgot password finished, in this case accessToken and identityToken will be null.

 			 }
 		 });
  ```
  {: codeblock}

### Changer les détails
Veillez à **activer** l'option
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de Cloud Directory.
Utilisez la classe LoginWidget pour démarrer le flux Changer les détails.
Cette API ne peut être utilisée que lorsque l'utilisateur se connecte en utilisant
Cloud Directory comme fournisseur d'identité.

   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  				 //Exception occurred 		}

  			 @Override
        public void onAuthorizationCanceled () {
  				 //changed details canceled by the user
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  				 //User authenticated, and fresh tokens received
  			 }
  		 });
   ```
   {: codeblock}

### Changer le mot de passe
Veillez à **activer** l'option **Autoriser les
utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les
paramètres de Cloud Directory.


Utilisez la classe LoginWidget pour démarrer le flux Changer le mot de passe.
Cette API ne peut être utilisée que lorsque l'utilisateur se connecte en utilisant Cloud
Directory comme fournisseur d'identité.


   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   				 //Exception occurred 		}

   			 @Override
        public void onAuthorizationCanceled () {
   				 //change password canceled by the user
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   				   //User authenticated, and fresh tokens received
   			 }
   		 });
   ```
   {: codeblock}

## Gestion de Cloud Directory avec le SDK Swift iOS


### Connexion avec le mot de passe du propriétaire de la ressource

Vous pouvez obtenir des jetons d'accès et d'identité en fournissant le nom d'utilisateur et le mot de passe de l'utilisateur final.
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

### Inscription

Veillez à **activer** l'option **Autoriser les
utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les
paramètres de Cloud Directory.


Utilisez la classe LoginWidget pour démarrer le flux Inscription.
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

### Mot de passe oublié
Veillez à **activer** les options
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et
**E-mail d'oubli de mot de passe** dans les paramètres de Cloud Directory.


Utilisez la classe LoginWidget pour démarrer le flux Mot de passe oublié
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

### Changer les détails

Veillez à **activer** l'option
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de Cloud Directory.


Utilisez la classe LoginWidget pour démarrer le flux Changer les détails.
Cette API ne peut être utilisée que lorsque l'utilisateur se connecte en utilisant
Cloud Directory comme fournisseur d'identité.

  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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

### Changer le mot de passe

Veillez à **activer** l'option
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de Cloud Directory.


Utilisez la classe LoginWidget pour démarrer le flux Changer le mot de passe.
Cette API ne peut être utilisée que lorsque l'utilisateur se connecte en utilisant
Cloud Directory comme fournisseur d'identité.

  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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


## Gestion de Cloud Directory avec le SDK Node.js
Assurez-vous que le fournisseur d'identité Cloud Directory est **activé** et inclut le point d'extrémité de rappel.


### Flux Connexion avec le mot de passe du propriétaire de la ressource
WebAppStrategy permet aux utilisateurs de se connecter à votre application web en
utilisant un nom d'utilisateur et un mot de passe.
Après une connexion réussie, le jeton d'accès de l'utilisateur est conservé dans la session HTTP et reste disponible aussi longtemps
que la session HTTP est active.
Une fois la session HTTP détruite ou arrivée à expiration, le jeton est également détruit.


Pour permettre aux utilisateurs de se connecter avec un nom d'utilisateur et
un mot de passe, ajoutez à votre application une route 'post' qui sera appelée avec
le nom d'utilisateur et le mot de passe en paramètres.


  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Explication des composants de cette commande</th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> Spécifiez comme valeur l'URL de la page vers laquelle vous souhaitez rediriger l'utilisateur en cas
d'authentification réussie.
La valeur par défaut est l'URL de la demande d'origine.
Exemple : <code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td> Spécifiez comme valeur l'URL de la page vers laquelle vous souhaitez rediriger l'utilisateur en cas
d'échec de l'authentification.
La valeur par défaut est l'URL de la demande d'origine.
</td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td> Mettez cet argument à <code>true</code> si vous voulez qu'un message d'erreur soit retourné
par Cloud Directory. La valeur par défaut est false. </td>
      </tr>
     </tbody>
  </table>


**Remarque **:
  * Si vous voulez soumettre la demande au moyen d'un formulaire HTML,
utilisez le middleware [body-parser](https://www.npmjs.com/package/body-parser).

  * Utilisez [connect-flash](https://www.npmjs.com/package/connect-flash) pour obtenir le
message d'erreur retourné.
Référez-vous au fichier `web-app-sample-server.js`.

### S'inscrire
Pour lancer le formulaire d'inscription {{site.data.keyword.appid_short_notm}}, passez
la propriété WebAppStrategy "show" en lui donnant pour valeur `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

    **Remarque **:
    * Si, dans vos paramètres Cloud Directory, l'option
**Autoriser les utilisateurs à se connecter sans vérifier leur adresse électronique** est
**désactivée**, le processus se termine sans que soient
récupérés les jetons d'accès et d'identité {{site.data.keyword.appid_short_notm}}.

    * Veillez à **activer** l'option
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de Cloud Directory.



### Mot de passe oublié
Pour lancer le formulaire "Mot de passe oublié" {{site.data.keyword.appid_short_notm}}, passez
la propriété WebAppStrategy `show` en lui donnant pour valeur `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

**Remarque **:
* Si, dans vos paramètres Cloud Directory, l'option
**Autoriser les utilisateurs à se connecter sans vérifier leur adresse électronique** est
**désactivée**, le processus se termine sans que soient
récupérés les jetons d'accès et d'identité {{site.data.keyword.appid_short_notm}}.

* Veillez à **activer** les options
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** et
**E-mail d'oubli de mot de passe** dans les paramètres de Cloud Directory.


### Changer les détails
Pour lancer le formulaire "Changer les détails" {{site.data.keyword.appid_short_notm}}, passez
la propriété WebAppStrategy `show` en lui donnant pour valeur `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

**Remarque **:
* L'utilisateur doit être authentifié en utilisant Cloud Directory comme fournisseur d'identité.
* Veillez à **activer** l'option
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de Cloud Directory.



### Changer le mot de passe
Pour lancer le formulaire "Changer le mot de passe" {{site.data.keyword.appid_short_notm}}, passez
la propriété WebAppStrategy `show` en lui donnant pour valeur `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

**Remarque **:
* L'utilisateur doit être authentifié en utilisant Cloud Directory comme fournisseur d'identité.
* Veillez à **activer** l'option
**Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** dans les paramètres de Cloud Directory.

