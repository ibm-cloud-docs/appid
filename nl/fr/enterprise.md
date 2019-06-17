---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

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

# SAML
{: #enterprise}

Lorsque vous avez un fournisseur d'identité basé sur SAML, vous pouvez configurer {{site.data.keyword.appid_short_notm}} pour agir en tant que fournisseur de services qui initie une connexion unique (SSO) à un fournisseur tiers. Pendant le flux de connexion, vos utilisateurs peuvent être facilement authentifiés et peuvent obtenir des jetons de sécurité {{site.data.keyword.appid_short_notm}} qui leur permettent d'accéder à vos applications et à vos API protégées.
{: shortdesc}

 
Vous travaillez avec un fournisseur d'identité SAML spécifique ? Jetez un coup d'oeil à l'un de ces articles de blogue sur la configuration de {{site.data.keyword.appid_short_notm}} avec [Ping One ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-ping-one), [Azure Active Directory ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory) ou [Active Directory Federation Service ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service).
{: tip}


## Compréhension de SAML
{: #saml-understanding}

SAML (Security Assertion Markup Language) est une norme ouverte pour l'échange de données d'authentification et d'autorisation entre un fournisseur d'identité qui produit une assertion de l'identité de l'utilisateur et un fournisseur de services qui consomme les informations d'identité de l'utilisateur.
{: shortdesc}

Le protocole <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> prend en charge différents profils et options de liaison. {{site.data.keyword.appid_short_notm}} prend en charge le profil SSO de navigateur Web, avec liaison HTTP Post.

### Quelle est la base technique des flux ?
{: #saml-tech-basis}

SAML 2.0 est l'une des infrastructures les plus établies pour les normes d'authentification et d'autorisation. Il s'agit d'un protocole XML entre un fournisseur de services ({{site.data.keyword.appid_short_notm}}) et un fournisseur d'identité. Lorsqu'un fournisseur d'identité authentifie un utilisateur, il crée des jetons SAML, qui contiennent des assertions, ou des instructions, sur l'utilisateur. Les instructions peuvent contenir :

- des informations d'authentification telles que la manière dont l'utilisateur a été authentifié - un mot de passe, une authentification multi-facteur, etc.
- des attributs associés à l'utilisateur - à quel groupe ils appartiennent.
- des décisions d'autorisation qui indiquent si l'utilisateur est autorisé à effectuer une action particulière sur une ressource particulière.

Lorsque les assertions sont renvoyées à {{site.data.keyword.appid_short_notm}}, le service fédère l'identité de l'utilisateur et les jetons correspondants sont générés. Si l'assertion SAML correspond à l'une des réclamations OIDC suivantes, elle est automatiquement ajoutée au jeton d'identité.  Si une ou plusieurs de ces valeurs changent côté fournisseur, les nouvelles valeurs ne sont disponibles qu'après la reconnexion de l'utilisateur.

 * `name`
 * `email`
 * `locale`
 * `picture`

Les assertions qui ne correspondent à aucun des noms standard sont par défaut ignorées, mais si votre fournisseur SAML renvoie d'autres assertions, il est possible d'obtenir les informations lorsqu'un utilisateur se connecte. En créant un tableau des assertions que vous voulez utiliser, vous pouvez [injecter les informations dans vos jetons](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Mais, veillez à ne pas ajouter plus d'informations que nécessaires à vos jetons. Les jetons sont généralement envoyés dans des en-têtes http et les en-têtes sont limités en taille.
{: tip}

### A quoi ressemble le flux ?
{: #saml-flow}

Bien que {{site.data.keyword.appid_short_notm}} et votre fournisseur d'identité utilisent l'infrastructure SAML pour authentifier l'utilisateur, {{site.data.keyword.appid_short_notm}} utilise l'infrastructure plus moderne OAuth 2.0/ OIDC pour échanger les clés de sécurité avec l'application. Jetez un coup d'oeil à l'image suivante pour voir un flux d'information détaillé.

![Flux d'authentification d'entreprise SAML](/images/ibmid-flow.png)

1. Un utilisateur accède à la page de connexion ou à la ressource restreinte sur son application, ce qui déclenche une requête sur le noeud final {{site.data.keyword.appid_short_notm}} `/authorization` via un SDK {{site.data.keyword.appid_short_notm}} ou une API. Si l'utilisateur n'est pas autorisé, le flux d'authentification commence par une redirection vers {{site.data.keyword.appid_short_notm}}.
2. {{site.data.keyword.appid_short_notm}} génère une demande d'authentification SAML (AuthNRequest) et le navigateur redirige automatiquement l'utilisateur vers le fournisseur d'identité SAML.
3. Le fournisseur d'identité analyse la requête SAML, authentifie l'utilisateur et génère une réponse SAML avec ses assertions.
4. Le fournisseur d'identité redirige l'utilisateur et la réponse vers {{site.data.keyword.appid_short_notm}} avec la réponse SAML.
5. Si l'authentification réussit, {{site.data.keyword.appid_short_notm}} crée des jetons d'accès et d'identité qui représentent l'autorisation et l'authentification d'un utilisateur et les renvoit à l'application. Si l'authentification échoue, {{site.data.keyword.appid_short_notm}} renvoie le code d'erreur du fournisseur d'identité à l'application.
6. L'utilisateur a accès à l'application ou aux ressources protégées.



### Le SSO modifie-t-il le débit ?
{: #saml-sso-flow}

Le profil SSO du navigateur Web que {{site.data.keyword.appid_short_notm}} implémente est initié par le fournisseur de services, ce qui signifie que {{site.data.keyword.appid_short_notm}} doit envoyer une requête SAML au fournisseur d'identité pour lancer la session d'authentification. 

Actuellement, {{site.data.keyword.appid_short_notm}} ne prend pas en charge les flux initiés par le fournisseur d'identité et ils ne doivent pas être utilisés avec le service pour le moment.
{: note}

Si votre fournisseur d'identité prend en charge la connexion unique, il est possible que l'authentification SAML utilise la session SSO déjà établie pour authentifier l'utilisateur. Si ce n'est pas le cas, l'utilisateur est redirigé vers une page de connexion. Il peut être redirigé si votre fournisseur d'identité ne peut pas répondre aux exigences d'authentification définies dans la demande d'authentification d'{{site.data.keyword.cloud_notm}} avec les éléments utilisés pour établir la connexion unique. Par exemple, si votre fournisseur d'identité établit une session SSO utilisateur en utilisant la biométrie, alors le contexte d'authentification par défaut de {{site.data.keyword.appid_short_notm}} doit changer. Par défaut, {{site.data.keyword.appid_short_notm}} s'attend à ce que les utilisateurs soient authentifiés par mot de passe via HTTPS : `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.



## Configuration de SAML pour fonctionner avec {{site.data.keyword.appid_short_notm}}
{: #saml-configure}

Vous pouvez configurer SAML pour fonctionner avec {{site.data.keyword.appid_short_notm}} en fournissant les métadonnées d'{{site.data.keyword.appid_short_notm}} à votre fournisseur d'identité et les métadonnées de celui-ci à {{site.data.keyword.appid_short_notm}}.



### Fourniture de métadonnées à votre fournisseur d'identité
{: #saml-provide-idp}

Pour configurer votre application, vous devez fournir des informations à un fournisseur d'identité compatible avec SAML. Ces informations sont échangées via un fichier XML de métadonnées qui comporte égaiement des données de configuration utilisées pour établir le caractère de fiabilité.
{: shortdesc}

Vous ne pouvez pas activer SAML tant que vous ne l'avez pas configuré comme fournisseur d'identité.
{: tip}

1. Dans l'onglet **Gérer** du tableau de bord {{site.data.keyword.appid_short_notm}}, cliquez sur **Editer** dans la ligne **SAML** pour configurer vos paramètres.
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
      <td>Méthode par laquelle le fournisseur d'identité détermine le format d'identificateur qu'il doit envoyer dans l'objet d'une assertion et comment {{site.data.keyword.appid_short_notm}} identifie les utilisateurs. L'ID doit avoir le format suivant : <code><saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"/></code></td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>Méthode, pour un fournisseur d'identité, de vérifier s'il a besoin de signer l'assertion. Le service attend une assertion signée mais ne prend pas en charge les assertions chiffrées.</td>
    </tr>
  </table>

3. Indiquez les données nécessaires à votre fournisseur d'identité. Si ce dernier prend en charge le téléchargement du fichier de métadonnées, vous pouvez procéder de la sorte. Si ce n'est pas le cas, configurez manuellement les propriétés. Les fournisseurs d'identité n'utilisant pas tous les mêmes propriétés, il est possible que vous ne les utilisiez pas toutes.

  Les noms de propriété peuvent varier d'un fournisseur d'identité à un autre.
  {: tip}

4. Basculez **SAML 2.0 Federation** sur **Activé**.



### Fourniture de métadonnées à {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

Vous pouvez obtenir des données de votre fournisseur d'identité et les fournir à {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

**Fourniture de métadonnées à l'aide de l'interface graphique** 

1. Accédez à l'onglet **SAML 2.0** du tableau de bord {{site.data.keyword.appid_short_notm}}. Entrez les métadonnées suivantes, obtenues du fournisseur d'identité à la section **Provide Metadata from SAML IdP**.
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

Vous souhaitez définir un contexte d'authentification ? Vous pouvez le faire à l'aide de l'API.
{: tip}

</br>

**Fourniture de métadonnées avec l'API**

1. Examinez votre configuration SAML actuelle, y compris votre contexte d'authentification et vos certificats, en lançant une requête GET sur le noeud final d'API [`/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

  Exemple de code :
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
  ```
  {: codeblock}

  Exemple de sortie :
  ```
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    }
  }
  ```
  {: screen}

2. Créez votre configuration SAML en remplaçant les valeurs de l'exemple suivant par les informations de votre fournisseur. Les valeurs indiquées dans l'exemple sont obligatoires, mais vous pouvez choisir d'inclure d'autres informations, comme indiqué dans le tableau.

  ```
  "config": {
    "authnContext": {
      "class": [
        "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
      ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
    ],
    "displayName": "my saml example",
  }
  ```
  {: codeblock}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> Variable </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>URL vers laquelle l'utilisateur est redirigé pour l'authentification. Elle est hébergée par votre fournisseur d'identité SAML.</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>Nom global unique d'un fournisseur d'identité SAML.</td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>Nom que vous attribuez à votre configuration SAML.</td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>Certificat émis par votre fournisseur d'identité SAML. Utilisé pour la signature et la validation des assertions SAML. Tous les fournisseurs sont différents, mais vous devriez pouvoir télécharger le certificat signataire depuis votre fournisseur d'identité. Le certificat doit être au format <code>.pem</code>.</td>
    </tr>
    <tr>
      <td>Facultatif : <code>secondary-certificate-example-pem-format</code></td>
      <td>Certificat de sauvegarde émis par votre fournisseur d'identité SAML. Il est utilisé si la validation de la signature échoue avec le certificat principal. <strong>Remarque</strong> : si la clé de signature reste la même, {{site.data.keyword.appid_short_notm}} ne bloque pas l'authentification des certificats expirés.</td>
    </tr>
    <tr>
      <td>Facultatif : <code>authnContext</code></td>
      <td>Le contexte d'authentification est utilisé pour vérifier la qualité de l'authentification et des assertions SAML. Vous pouvez ajouter un contexte d'authentification en ajoutant un tableau de classes et une chaîne de comparaison à votre code. Assurez-vous d'actualiser les paramètres <code>class</code> et <code>comparison</code> avec vos valeurs. Par exemple, un paramètre <code>class</code> pourrait ressembler à <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code>.</td>
    </tr>
  </table>

3. Effectuez une requête PUT sur le [noeud final d'API `/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) pour fournir la configuration que vous avez créée à l'étape 2 à {{site.data.keyword.appid_short_notm}}. Consultez l'exemple suivant pour voir à quoi pourrait ressembler votre demande.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
      ],
      "displayName": "my saml example",
    }
  }
  ```
  {: screen}



## Test de votre configuration
{: #saml-testing}

Vous pouvez tester la configuration entre votre fournisseur d'identité SAML et {{site.data.keyword.appid_short_notm}}.

1. Veillez à sauvegarder votre configuration.
2. Accédez à l'onglet **SAML 2.0** du tableau de bord {{site.data.keyword.appid_short_notm}} et cliquez sur **Test**. Un nouvel onglet s'ouvre.
3. Connectez-vous à l'aide d'un utilisateur que votre fournisseur d'identité a déjà authentifié.
4. Une fois le formulaire complété, vous êtes redirigé vers une autre page.
  * Authentification réussie : La connexion entre {{site.data.keyword.appid_short_notm}} et le fournisseur d'identité fonctionne correctement. La page affiche des [jetons d'accès et d'identité](/docs/services/appid?topic=appid-tokens#tokens) valides.
  * Echec de l'authentification : La connexion est interrompue. La page affiche les erreurs et le fichier XML de réponse SAML.


Vous rencontrez des problèmes ? Voir [Dépannage : SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}




## Foire aux questions sur SAML
{: #saml-assertions}

Les assertions SAML peuvent être renvoyées de différentes manières. Consultez les exemples suivants pour voir le format de réponse attendu par {{site.data.keyword.appid_short_notm}}.
{: shortdesc}


### Quelle est le format attendu par {{site.data.keyword.appid_short_notm}} pour une assertion SAML ?
{: #saml-example}

Le service s'attend à ce qu'une assertion SAML ressemble à l'exemple ci-dessous.

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}


### Quels types d'algorithme sont pris en charge par {{site.data.keyword.appid_short_notm}} ?
{: #saml-signatures}

{{site.data.keyword.appid_short_notm}} utilise l'algorithme <a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour traiter les signatures numériques XML.

