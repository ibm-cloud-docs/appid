---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}


# Configuration du SDK Swift iOS
{: #getting-started-ios}

Construisez vos applications Swift avec le SDK client d'{{site.data.keyword.appid_short}}, initialisez le SDK, authentifiez les utilisateurs et soumettez des demandes à des ressources protégées et non protégées.
{:shortdesc}


## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :
  * Une instance d'{{site.data.keyword.appid_short_notm}}.
  * Votre ID titulaire.
    * Dans l'onglet **Données d'identification pour le
service** de votre tableau de bord du service, cliquez sur **Afficher les données d'identification**. Votre ID titulaire est affiché dans la zone **TenantID**. Cette valeur est utilisée pour initialiser votre application.
  * Votre région {{site.data.keyword.Bluemix_notm}}.
  Vous pouvez identifier votre région en recherchant dans l'interface utilisateur. Cette valeur est utilisée pour initialiser votre application.
    <table> <caption> Tableau 1. Régions {{site.data.keyword.Bluemix_notm}} et valeurs de SDK correspondantes </caption>
    <tr>
      <th> Région Bluemix </th>
      <th> Valeur du SDK </th>
    </tr>
    <tr>
      <td> Sud des Etats-Unis </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> Royaume-Uni </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Projet Xcode (version 8.1 ou ultérieure).
  * CocoaPods (version 1.1.0 ou ultérieure).


## Installation du SDK client
{: #install-appid-sdk}

Le SDK client d'{{site.data.keyword.appid_short_notm}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets Swift et Cocoa Objective-C . CocoaPods télécharge des artefacts et les rend disponibles dans votre projet.

1. Créez un projet Xcode ou ouvrez un projet existant.
2. Ouvrez ou créez le fichier Pod dans le répertoire du projet.
3. Sous la cible de votre projet, ajoutez une dépendance pour le pod 'BluemixAppID'. Vérifiez que la commande `use_frameworks!` est également présente sous votre cible.

  Exemple :

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. Pour télécharger la dépendance `BluemixAppID`, exécutez la
commande ci-dessous.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Ouvrez votre projet Xcode et activez le partage de chaîne de certificats. Sous **Paramètres du projet**, cliquez sur **Fonctions** > **Partage de chaîne de certificats**.
7. Sous **Paramètres du projet** > **Information** > **Types d'URL**, ajoutez un type d'URL. Renseignez les deux zones de texte **Identificateur** et **Schéma d'URL** avec cette valeur : $(PRODUCT_BUNDLE_IDENTIFIER)


## Initialisation du SDK client
{: #initialize-client-sdk}

1. Ajoutez l'importation ci-dessous dans votre fichier
`AppDelegate.swift`.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Initialisez le SDK client en transmettant les paramètres d'ID titulaire et de région à la méthode initialize. Bien
que ce ne soit pas obligatoire, le code d'initialisation est souvent placé dans la
méthode application:didFinishLaunchingWithOptions: du fichier AppDelegate dans votre application Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * Remplacez tenantId par l'ID titulaire pour votre service App ID.
  * Remplacez AppID.REGION_UK par votre région {{site.data.keyword.appid_short_notm}}.

3. Ajoutez le code ci-dessous à votre fichier AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

## Authentification des utilisateurs à l'aide du widget de connexion
{: #authenticate-login}


Une fois que le SDK client d'{{site.data.keyword.appid_short_notm}} est initialisé, vous pouvez authentifier vos utilisateurs en exécutant le widget de connexion. La configuration par défaut du widget de connexion utilise Facebook et Google comme
options d'authentification. Si vous ne configurez qu'un seul fournisseur d'identité, le widget de
connexion ne démarre pas et l'utilisateur est redirigé vers l'écran d'authentification du
fournisseur d'identité (IDP) configuré.





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

## Accès aux attributs utilisateur
{: #accessing}

En obtenant un jeton d'accès, vous pouvez accéder au noeud final des attributs utilisateur protégés. Pour
ce faire, utilisez les méthodes d'API ci-dessous.

  ```swift
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {: codeblock}

Lorsqu'un jeton d'accès n'est pas transmis explicitement, {{site.data.keyword.appid_short_notm}} utilise le dernier jeton reçu.

Par exemple, vous pouvez utiliser le code ci-dessous pour définir un nouvel
attribut ou remplacer un attribut existant.

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributes received as a Dictionary
      } else {
          // An error has occurred
      }
  })
  ```
  {: codeblock}


### Connexion anonyme
{: #anonymous notoc}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez vous connecter de
manière [anonyme](/docs/services/appid/user-profile.html#anonymous).

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }
      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }
      public func onAuthorizationFailure(error: AuthorizationError) {
          //Error occurred
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {: codeblock}

### Authentification progressive
{: #progressive notoc}

S'il dispose d'un jeton d'accès anonyme, l'utilisateur peut devenir un
utilisateur identifié en transmettant le jeton à la méthode
`loginWidget.launch`.

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {: codeblock}

Après une connexion anonyme, une authentification progressive a lieu même si le widget de connexion est appelé sans transmission d'un jeton d'accès vu que le service a utilisé le dernier jeton d'accès reçu. Si vous voulez effacer les jetons que vous avez stockés, exécutez la commande ci-dessous.

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {: codeblock}



## Etapes suivantes
{: #next-steps}

{{site.data.keyword.appid_short_notm}} fournit une configuration par défaut lorsque vous mettez en place initialement vos fournisseurs d'identité. Vous ne pouvez utiliser la configuration par défaut qu'en mode développement. Avant de publier votre application, [mettez à jour la configuration par défaut avec vos propres données d'identification](/docs/services/appid/identity-providers.html).
