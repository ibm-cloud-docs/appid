---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Personnalisation de l'expérience de connexion
{: #branding}

Vous pouvez afficher vos propres écrans et tirer parti des fonctions d'authentification et d'autorisation d'{{site.data.keyword.appid_full}}. Avec un répertoire cloud comme fournisseur d'identité, vos utilisateurs peuvent interagir avec votre application avec un minimum d'aide de votre part. Ils peuvent se connecter sans demander de l'aide.
{: shortdesc}

Lorsque vous utilisez vos propres écrans, le [flux Resource Owner Password Credentials](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) est utilisé pour fournir des jetons d'accès et d'identité.


## Affichage d'écrans personnalisés avec le SDK Android
{: #branded-ui-android}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le SDK Android.  <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Consultez ce blog ! <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //User authenticated
        }
         });
  ```
  {: pre}

</br>
</br>

## Affichage d'écrans personnalisés avec le SDK Swift iOS
{: #branded-ui-ios-swift}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le SDK Swift iOS.
{: shortdesc}

</br>
**Se connecter**

1. Dans l'onglet Fournisseur d'identité de l'interface graphique, définissez Répertoire cloud sur **On**.
2. Connectez-vous à l'aide du mot de passe du propriétaire de la ressource. Des jetons d'accès et d'identité sont obtenus lorsqu'un utilisateur tente de se connecter à l'aide de ses nom d'utilisateur et mot de passe.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: pre}


</br>
</br>

## Affichage d'écrans personnalisés avec le SDK Node.js
{: #branded-ui-nodejs}

Lorsque le répertoire cloud est activé, vous pouvez appeler des écrans personnalisés avec le SDK Node.js. 
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

