---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Configuration de fournisseurs d'identité d'entreprise
{: #enterprise}

Si vous disposez déjà d'un référentiel d'utilisateurs et d'un moyen certifié d'authentifier les utilisateurs sur votre système interne, vous pouvez configurer le service {{site.data.keyword.appid_full}} pour utiliser un fournisseur d'identité d'entreprise.
{: shortdesc}

## Comprendre le langage SAML
{: #saml}

SAML est une norme ouverte pour l'échange de données d'authentification et d'autorisation entre un fournisseur d'identité qui produit une assertion de l'identité de l'utilisateur et un fournisseur de services qui consomme les informations d'identité de l'utilisateur.
{: shortdesc}

Principes de fonctionnement

{{site.data.keyword.appid_short_notm}} fonctionne en tant que fournisseur de services et initie une ouverture de session unique de type SSO (Single Sign On) à un fournisseur tiers tel que l'outil Active Directory Federation Services (ADFS). Le protocole <a href="http://saml.xml.org/saml-specifications" target="_blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> prend en charge différents profils et options de liaison. {{site.data.keyword.appid_short_notm}} prend en charge le profil SSO de navigateur Web, avec liaison HTTP Post.

### Assertions SAML et réclamations de jeton d'identité

Une assertion SAML est un package d'informations comportant une ou plusieurs instructions. L'assertion contient la décision d'autorisation et peut comporter des informations d'identité relatives à l'utilisateur.

Quand un utilisateur se connecte avec un fournisseur d'identité, ce fournisseur envoie une assertion à {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} propage à votre application les informations d'identité utilisateur renvoyées dans l'assertion SAML en tant que réclamations de jeton OIDC. L'attribut SAML doit correspondre à l'une des réclamations OIDC suivantes pour être ajouté au jeton d'identité. 

Les réclamations suivantes peuvent être ajoutées :
* `name`
* `email`
* `locale`
* `picture`

Les éléments d'attribut SAML restants qui ne correspondent pas à un nom standard sont ignorés.

## Configuration de votre application pour une utilisation d'un fournisseur d'identité SAML externe
{: #configuring-saml}

Vous pouvez configurer le service {{site.data.keyword.appid_short_notm}} pour qu'il utilise un fournisseur d'identité SAML.
{: shortdesc}

### Fourniture de métadonnées à votre fournisseur d'identité

Pour configurer votre application, vous devez fournir des informations à un fournisseur d'identité compatible SAML. Ces informations sont échangées via un fichier XML de métadonnées qui comporte égaiement des données de configuration utilisées pour établir le caractère de fiabilité.

1. Dans l'onglet **Gérer** du tableau de bord {{site.data.keyword.appid_short_notm}}, définissez **SAML 2.0** sur **Activé**. Cliquez ensuite sur **Editer** pour configurer vos paramètres SAML.
2. Cliquez sur **Télécharger le fichier de métadonnées SAML**. Votre fournisseur d'identité attend les informations suivantes du fichier.
  <table>
    <tr>
      <th> Variable </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>Identificateur permettant au fournisseur d'identité de savoir que {{site.data.keyword.appid_short_notm}} est l'émetteur de la demande SAML.</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>Emplacement où le fournisseur d'identité envoie les assertions SAML après que l'authentification d'un utilisateur a abouti.</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>Instructions sur la procédure d'envoi, par le fournisseur d'identité, de la réponse SAML.</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>Façon dont le fournisseur d'identité détermine le format d'identificateur qu'il doit envoyer dans l'objet d'une assertion. Façon dont {{site.data.keyword.appid_short_notm}} identifie des utilisateurs.</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>Méthode, pour un fournisseur d'identité, de vérifier s'il a besoin de signer l'assertion. Le service attend une assertion signée mais ne prend pas en charge les assertions chiffrées.</td>
    </tr>
  </table>

3. Indiquez les données nécessaires à votre fournisseur d'identité. Si ce dernier prend en charge le téléchargement du fichier de métadonnées, vous pouvez procéder de la sorte. Si ce n'est pas le cas, configurez manuellement les propriétés. Tous les fournisseurs d'identité n'utilisant pas les mêmes propriétés, il n'est donc pas forcément nécessaire de toutes les utiliser.

Les noms de propriété peuvent varier d'un fournisseur d'identité à un autre.
{: tip}

### Fourniture de métadonnées à {{site.data.keyword.appid_short_notm}}

Vous aurez besoin de données du fournisseur d'identité que vous devrez fournir à {{site.data.keyword.appid_short_notm}}.

1. Accédez à l'onglet **SAML 2.0** du tableau de bord {{site.data.keyword.appid_short_notm}}. Entrez les métadonnées suivantes, provenant du fournisseur d'identité, à la section **Provide Metadata from SAML IdP**.
  <table>
    <tr>
      <th> Variable </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>URL vers laquelle l'utilisateur est redirigé pour l'authentification. Elle est hébergée par votre fournisseur d'identité SAML.</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>Nom global unique d'un fournisseur d'identité SAML.</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>Certificat émis par votre fournisseur d'identité SAML. Utilisé pour la signature et la validation des assertions SAML. Tous les fournisseurs sont différents, mais vous devriez pouvoir télécharger le certificat signataire depuis votre fournisseur d'identité. Le certificat doit être au format <code>.pem</code>.</td>
    </tr>
  </table>

2. Facultatif : Indiquez un **certificat secondaire** à utiliser en cas d'échec de validation de la signature pour le certificat principal. Si la clé de signature reste la même, {{site.data.keyword.appid_short_notm}} ne bloque pas l'authentification de certificats arrivés à expiration.

3. Mettez à jour le **nom du fournisseur** et cliquez sur **Sauvegarder**. Nom par défaut : SAML.


### Test de votre configuration

Vous pouvez tester la configuration entre votre fournisseur d'identité SAML et {{site.data.keyword.appid_short_notm}}.

1. Veillez à sauvegarder votre configuration.
2. Accédez à l'onglet **SAML 2.0** du tableau de bord {{site.data.keyword.appid_short_notm}} et cliquez sur **Test**. Un nouvel onglet s'ouvre.
3. Connectez-vous à l'aide d'un utilisateur que votre fournisseur d'identité a déjà authentifié. 
4. Une fois le formulaire complété, vous êtes redirigé vers une autre page.
  * Authentification réussie : La connexion entre {{site.data.keyword.appid_short_notm}} et le fournisseur d'identité fonctionne correctement. La page affiche des [jetons d'accès et d'identité](/docs/services/appid/authorization.html#key-concepts) valides.
  * Echec de l'authentification : La connexion est interrompue. La page affiche les erreurs et le fichier XML de réponse SAML.
