---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, customizing apps, directory, registry, 

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

# Association d'une marque à votre application
{: #branded}

Vous pouvez afficher vos propres écrans personnalisés, utiliser vos propres flux et tirer parti des fonctions d'authentification et d'autorisation d'{{site.data.keyword.appid_full}}. L'utilisation de Cloud Directory comme fournisseur d'identité permet à vos utilisateurs d'interagir avec votre application avec peu d'aide de votre part. Ils peuvent se connecter, s'inscrire, changer leur mot de passe, etc., sans avoir à demander de l'aide.
{: shortdesc}


## Comprendre la réutilisation des écrans
{: #branded-understand}

Lorsque vous réutilisez vos interfaces utilisateur existantes, vous pouvez créer un flux de connexion cohérent pour votre application. En utilisant les mêmes images, couleurs et images de marque, vos utilisateurs sont plus susceptibles de reconnaître votre marque, même s'ils n'interagissent pas directement avec votre application.

### Quelles sont les exigences liées à l'utilisation de mes propres écrans ?
{: #branded-requirements}


Pour afficher vos propres interfaces utilisateur, vous devez utiliser [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) comme fournisseur d'identité. Cloud Directory peut être [configuré](/docs/services/appid?topic=appid-cloud-directory) de différentes manières. Vous pouvez choisir les types de messages que vous souhaitez envoyer et personnaliser le contenu et la conception. Vous ne savez pas quoi choisir ? Pas de problème. L'interface graphique contient des exemples de messages que vous pouvez utiliser.


Vous souhaitez utiliser une autre [langue](/docs/services/appid?topic=appid-cd-messages#cd-languages) que l'anglais ? Vous pouvez choisir une autre langue en utilisant les <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization" target="_blank">API de gestion des langues <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour afficher votre propre contenu traduit.
{: tip}


### Puis-je utiliser mes propres écrans et ceux fournis par défaut ?
{: #branded-hybrid}

Oui ! Vous pouvez créer un flux hybride qui utilise certains de vos écrans et certains des écrans par défaut. Toutefois, vous ne pouvez utiliser qu'une seule option par flux. Par exemple, utiliser votre propre écran de connexion et également l'écran d'inscription par défaut. Mais si vous choisissez d'utiliser l'écran d'inscription par défaut, vous devez continuer à utiliser cet écran pendant l'intégralité du flux d'inscription, y compris la vérification de l'inscription.

### En quoi les flux sont-ils techniquement différents ?
{: #branded-technically}

Le service utilise des flux d'octroi d'autorisation OAuth 2.0 pour mapper le processus d'autorisation. Lorsque vous configurez des fournisseurs d'identité de réseaux sociaux tels que Facebook, le <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html" target="_blank">flux d'octroi d'autorisation <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> est utilisé pour appeler le widget de connexion. Lorsque vous utilisez vos propres écrans, le <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html" target="_blank">flux des données d'identification du mot de passe du propriétaire de la ressource <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> est utilisé pour fournir des jetons d'accès et d'identité qui vous permettent d'appeler vos écrans.



### Exemples
{: #branded-examples}

Oui ! Consultez l'un des exemples suivants pour voir Cloud Directory en action :

* <a href="https://www.ibm.com/cloud/blog/use-branded-ui-user-sign-app-id" target="_blank">Use your own branded UI for user sign-in with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
* <a href="https://www.ibm.com/cloud/blog/use-ui-flows-user-sign-sign-app-id" target="_blank">Use your own UI and Flows for User Sign-Up and Sign-in with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
* <a href="https://www.ibm.com/cloud/blog/custom-login-page-app-id-integration" target="_blank">Use a custom login page with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>


## Association d'une marque à votre application avec le logiciel SDK Android
{: #branded-ui-android}

Lorsque Cloud Directory est activé, vous pouvez appeler des écrans personnalisés avec le logiciel SDK Android. Vous pouvez choisir la combinaison d'écrans avec lesquels vos utilisateurs pourront interagir. <a href="https://www.ibm.com/cloud/blog/use-branded-ui-user-sign-app-id" target="blank">Consultez ce blogue <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour un exemple détaillé.
{: shortdesc}



### Connexion
{: #branded-android-sign-in}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique.
2. Ajoutez le code suivant à votre application. Le flux de connexion est déclenché lorsqu'un utilisateur clique sur le bouton de connexion sur votre écran personnalisé. Vous obtenez des jetons d'accès, d'identité et d'actualisation en fournissant le nom d'utilisateur et le mot de passe de l'utilisateur final.

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
  {: codeblock}

</br>
</br>

## Association d'une marque à votre application avec le logiciel SDK iOS Swift
{: #branded-ui-ios-swift}

Lorsque Cloud Directory est activé, vous pouvez appeler vos propres écrans de marque avec le logiciel [SDK Swift iOS](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

</br>

### Connexion
{: #branded-ios-sign-in}

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique.
2. Ajoutez le code suivant dans votre application. Lorsqu'un utilisateur tente de se connecter, votre écran de connexion est appelé et le processus d'autorisation et d'authentification commence par votre page de connexion personnalisée.

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
  {: codeblock}


## Association d'une marque à votre application avec le logiciel SDK Node.js
{: #branding-ui-nodejs}

Lorsque Cloud Directory est activé, vous pouvez appeler des écrans personnalisés avec le logiciel SDK Node.js.
{: shortdesc}

### Connexion
{: #branded-node-sign-in}

Avec `WebAppStrategy`, les utilisateurs peuvent se connecter à vos applications Web à l'aide de leur nom d'utilisateur et d'un mot de passe. Une fois qu'un utilisateur est connecté à votre application, son jeton d'accès est conservé dans une session HTTP tant qu'il est actif. Lorsque la session HTTP est fermée ou expire, le jeton d'accès est détruit.


1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique.
2. Ajoutez le code suivant dans votre application. Lorsqu'un utilisateur tente de se connecter, votre écran personnalisé est appelé et le processus d'autorisation et d'authentification commence.

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
      <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres de commande </th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>URL vers laquelle rediriger l'utilisateur lorsque l'authentification réussit.</td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>URL vers laquelle rediriger l'utilisateur si l'authentification échoue.</td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td>Lorsque la valeur est <code>true</code>, un message d'erreur est renvoyé depuis le service Cloud Directory. Par défaut, la valeur est <code>false</code>.</td>
      </tr>
    </tbody>
  </table>

**Remarque** : si vous soumettez la demande en HTML, vous pouvez utiliser le middleware <a href="https://www.npmjs.com/package/body-parser" target="blank">body parser <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Pour consulter le message d'erreur, vous pouvez utiliser <a href="https://www.npmjs.com/package/connect-flash" target="blank">connect-flash <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Pour voir le logiciel en action, consultez l'<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js" target="blank">exemple d'application Web <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


## Association d'une marque à votre application avec l'API
{: #branded-ui-api}

Vous pouvez afficher vos propres écrans et tirer parti des fonctions d'authentification et d'autorisation d'{{site.data.keyword.appid_short_notm}}. Si vous utilisez Cloud Directory comme fournisseur d'identité, vos utilisateurs peuvent interagir avec votre application avec peu d'aide de votre part. Ils peuvent se connecter, s'inscrire, réinitialiser leur mot de passe, etc., sans demander d'aide.
{: shortdesc}

Pour que ces opérations soient possibles, {{site.data.keyword.appid_short_notm}} expose des API REST. Vous pouvez utiliser les API REST pour générer un serveur back end dédié à vos applications Web ou pour interagir avec une application mobile avec vos propres écrans personnalisés.

L'API de gestion est sécurisée avec des jetons générés par IBM Cloud Identity and Access Management, de sorte que les propriétaires de compte peuvent spécifier le niveau d'accès de chaque membre de leur équipe pour chaque instance de service. Pour plus d'informations sur la façon dont IAM et {{site.data.keyword.appid_short_notm}} fonctionnent ensemble, voir [Gestion des accès de service](/docs/services/appid?topic=appid-service-access-management#service-access-management).

Après avoir configuré vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings), vous pouvez appeler les noeuds finaux ci-dessous pour afficher chaque écran.

### Inscription
{: #branded-api-signup}

Vous pouvez utiliser le noeud final `/sign_up` pour autoriser les utilisateurs à s'inscrire à votre application.
Indiquez les données suivantes dans le corps de demande :
  * Votre ID titulaire.
  * Données utilisateur Cloud Directory. Voir [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) pour plus de détails.
    * Un attribut `password`.
    * Le tableau d'adresses électroniques dont l'attribut `primary` a la valeur `true` doit comporter au moins une adresse électronique.

Selon votre [configuration de courrier électronique](/docs/services/appid?topic=appid-cd-messages#cd-messages), il est possible qu'un utilisateur reçoive une demande de vérification et/ou un courrier de bienvenue lorsqu'il se connecte à votre application. Ces deux types de courrier électronique sont déclenchés lorsqu'un utilisateur s'inscrit à votre application. L'e-mail de vérification contient un lien sur lequel l'utilisateur peut cliquer pour confirmer son identité, un écran qui s'affiche et remercie pour la vérification ou confirme que la vérification est terminée.  

Pour présenter votre propre page post-vérification :

1. Accédez au fournisseur d'identité Cloud Directory dans le tableau de bord {site.data.keyword.appid_short_notm}}.
2. Cliquez sur l'onglet **Vérification de l'adresse électronique**.
3. Dans **custom verification page URL**, entrez l'URL de votre page d'arrivée.

Si cette valeur est fournie, {{site.data.keyword.appid_short_notm}} appel l'URL au moyen d'une demande `context`. Lorsque vous appelez le noeud final `/sign_up/confirmation_result` et transmettez le paramètre `context` reçu, le résultat vous indique si l'utilisateur a vérifié son compte. Si tel est le cas, vous pouvez afficher votre page personnalisée.


### Mot de passe oublié
{: #branded-api-forgot-password}

Vous pouvez utiliser le noeud final `/forgot_password` pour autoriser les utilisateurs à récupérer leur mot de passe en cas d'oubli.

Indiquez les données suivantes dans le corps de demande :
  * Votre ID titulaire.
  * L'e-mail de l'utilisateur de Cloud Directory.

Lorsque le noeud final est appelé, un courrier électronique de réinitialisation de mot de passe est envoyé à l'utilisateur. Il contient un bouton **Réinitialiser**. Une fois que l'utilisateur a cliqué sur le bouton, {{site.data.keyword.appid_short_notm}} affiche un écran permettant à l'utilisateur de réinitialiser son mot de passe.

Vous pouvez présenter votre propre page post-réinitialisation de mot de passe :

1. Configurez vos [paramètres](/docs/services/appid?topic=appid-cloud-directory#cd-settings) Cloud Directory dans l'interface graphique. **Permettre aux utilisateurs de gérer leur compte à partir de votre application** doit être défini sur **Activé**.
2. Dans l'onglet **Réinitialiser le mot de passe** du tableau de bord du service, vérifiez que **E-mail d'oubli de mot de passe** est défini sur **Activé**.
3. Entrez l'URL de votre page d'arrivée dans la zone d'**URL pour la page de réinitialisation de mot de passe personnalisée**.  

Si cette valeur est fournie, {{site.data.keyword.appid_short_notm}} appel l'URL au moyen d'une demande `context`. Le paramètre `context` est utilisé pour recevoir le résultat lorsque le noeud final `/forgot_password/confirmation_result` est appelé. En cas de réussite, vous pouvez afficher votre page personnalisée.

Ajoutez une chaîne aléatoire à votre page de réinitialisation de mot de passe personnalisée et transmettez-la à votre système de back end lorsque la demande est soumise. Demandez à votre gestionnaire de valider la chaîne et appelez le noeud final `/change_password` uniquement si elle est valide. Ainsi, vous pouvez réduire la vulnérabilité de votre noeud final de réinitialisation de mot de passe sur le système de back end.
{: tip}


### Changement du mot de passe
{: #branded-api-change-password}

Vous pouvez utiliser le noeud final `/change_password` dans deux cas : lorsqu'un utilisateur soumet une demande de réinitialisation ou lorsqu'un utilisateur est connecté à votre application et souhaite mettre à jour son mot de passe.

Indiquez les informations suivantes dans le corps de demande pour mettre à jour le mot de passe après une demande de réinitialisation :
  * Votre ID titulaire.
  * Le nouveau mot de passe de l'utilisateur.
  * L'identificateur unique universel de l'utilisateur de Cloud Directory.
  * Facultatif : l'adresse IP à partir de laquelle a été effectuée la réinitialisation du mot de passe. Si vous choisissez de transmettre l'adresse IP, l'espace réservé `%{passwordChangeInfo.ipAddress}` est disponible pour le modèle de courrier électronique de changement de mot de passe.

En fonction de votre configuration, lorsqu'un mot de passe est changé, {{site.data.keyword.appid_short_notm}} envoie un courrier électronique à l'utilisateur pour lui signaler le changement.


Pour autoriser des utilisateurs à changer leur mot de passe lorsqu'ils sont connectés à votre application :

Indiquez les données suivantes dans le corps de demande :
  * Votre ID titulaire.
  * Le nouveau mot de passe de l'utilisateur.
  * L'identificateur unique universel de l'utilisateur de Cloud Directory.

Votre page de changement de mot de passe doit inviter l'utilisateur à entrer son mot de passe en cours et son nouveau mot de passe.
{: tip}

Votre système de back end valide le mot de passe en cours de l'utilisateur avec l'API ROP, et si celui-ci est valide, appelle le noeud final avec le nouveau mot de passe. En fonction de votre configuration, lorsqu'un mot de passe est changé, il est possible qu'{{site.data.keyword.appid_short_notm}} envoie un courrier électronique à l'utilisateur pour lui faire savoir qu'il y a eu un changement.


### Renvoyer
{: #branded-api-resend}

Vous pouvez utiliser `/resend/{templateName}` pour renvoyer un courrier électronique si un utilisateur ne l'a pas reçu pour une raison quelconque.

Indiquez les données suivantes dans le corps de demande :
  * L'ID titulaire.
  * Le nom de modèle.
  * L'identificateur unique universel de l'utilisateur de Cloud Directory.

### Changement des détails
{: #branded-api-change-details}

Lorsqu'un utilisateur est connecté à votre application, il peut mettre à jour certaines de ses informations. Vous pouvez utiliser le noeud final `/Users/{userId}` pour récupérer et mettre à jour ses informations.

Lorsque les détails de l'utilisateur sont mis à jour, le noeud final obtient les données utilisateur mises à jour dans le corps de demande au [format SCIM](https://tools.ietf.org/html/rfc7643#section-8.2). Veillez à modifier uniquement les détails pertinents.

L'adresse électronique des utilisateurs ne peut pas être changée.
{: tip}
