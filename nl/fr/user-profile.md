---

copyright:
  years: 2017
lastupdated: "2017-12-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Accès aux attributs utilisateur
{: #user-profile}

Vous pouvez gérer les données sur l'utilisateur final que vous utilisez pour construire une expérience personnalisée.
{:shortdesc}

Un attribut d'utilisateur est un segment d'information d'une entité stockée et gérée par {{site.data.keyword.appid_full}}.
Le profil contient les attributs et l'identité d'un utilisateur et peut être anonyme ou lié à une identité gérée par un fournisseur d'identité.

{{site.data.keyword.appid_short_notm}} fournit une API pour la connexion, anonyme ou bien avec authentification, via un [fournisseur d'identité](/docs/services/appid/identity-providers.html) OpenId Connect (OIDC). Le noeud final d'API d'attribut de profil utilisateur est une ressource qui est protégée
par
le jeton d'accès généré par {{site.data.keyword.appid_short_notm}} au cours du
processus de connexion et d'authentification.


## Stockage, lecture et suppression d'attributs utilisateur
{: #storing-data}

{{site.data.keyword.appid_short_notm}} fournit une
<a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API
REST <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> permettant
d'effectuer des opérations de création, d'extraction, de mise à jour et de suppression
des attributs d'un utilisateur. Le service fournit également un logiciel SDK pour
les
clients
mobiles <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android
<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
et
<a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift
<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

## Accès aux attributs d'utilisateur avec le SDK Android

{: #accessing}

En obtenant un jeton d'accès, vous pouvez accéder au noeud final des attributs utilisateur protégés. Vous
pouvez y accéder avec les méthodes ci-dessous.

  ```java
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {: codeblock}

Lorsqu'un jeton d'accès n'est pas transmis explicitement, {{site.data.keyword.appid_short_notm}} utilise le dernier jeton reçu.

Par exemple, vous pouvez utiliser le code ci-dessous pour définir un nouvel
attribut ou remplacer un attribut existant.

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//attributes received in JSON format on successful response 		}

		@Override 		public
void onFailure(UserAttributesException e) {
			//Exception occurred 		}
	});
  ```
  {: codeblock}

### Connexion anonyme
{: #anonymous notoc}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez vous connecter de
manière [anonyme](/docs/services/appid/user-profile.html#anonymous).

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred 		}

		@Override
		public void onAuthorizationCanceled() {
			//Authentication canceled by the user 		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//User authenticated 		}
	});
  ```
  {: codeblock}

### Authentification progressive
{: #progressive notoc}

Lorsqu'il dispose d'un jeton d'accès anonyme, l'utilisateur peut devenir un utilisateur identifié en transmettant ce jeton à la méthode `loginWidget.launch`.

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {: codeblock}

Après une connexion anonyme, une authentification progressive a lieu même si le widget de connexion est appelé sans transmission d'un jeton d'accès vu que le service a utilisé le dernier jeton d'accès reçu. Si vous voulez effacer les jetons que vous avez stockés, exécutez la commande ci-dessous.

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {: codeblock}


## Accès aux attributs d'utilisateur avec le SDK iOS

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

## Séparation et chiffrement des données
{: #data}

{{site.data.keyword.appid_short_notm}} stocke et chiffre les attributs de profil utilisateur. Etant donné qu'il s'agit d'un service partagé, chaque titulaire est associé à une clé de chiffrement dédiée et les données utilisateur de chaque titulaire sont chiffrées avec sa propre clé.

{{site.data.keyword.appid_short_notm}} garantit que les informations privées soient chiffrées avant leur stockage.
