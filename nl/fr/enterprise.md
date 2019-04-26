---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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

SAML (Security Assertion Markup Language) est une norme ouverte pour l'échange de données d'authentification et d'autorisation entre un fournisseur d'identité qui produit une assertion de l'identité de l'utilisateur et un fournisseur de services qui consomme les informations d'identité de l'utilisateur.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} fonctionne en tant que fournisseur de services et initie une connexion unique à un fournisseur tiers tel que l'outil ADFS (Active Directory Federation Services). Le protocole <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> prend en charge différents profils et options de liaison. {{site.data.keyword.appid_short_notm}} prend en charge le profil SSO de navigateur Web, avec liaison HTTP Post.

Pour apprendre à utiliser un fournisseur d'identité SAML spécifique, consultez les articles de blogue relatifs à la configuration d'{{site.data.keyword.appid_short_notm}} avec [Ping One ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [Azure Active Directory ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) ou [Active Directory Federation Services ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}



## Comprendre les assertions
{: #saml-assertions}

Une assertion SAML es similaire à un [attribut utilisateur](/docs/services/appid?topic=appid-user-profile#user-profile). C'est une instruction ou un élément d'information relatif à un utilisateur qui est renvoyé à {{site.data.keyword.appid_short_notm}} par un fournisseur d'identité lorsqu'un utilisateur se connecte avec succès à votre application. Selon la configuration de votre application et le fournisseur d'identité que vous utilisez, les informations peuvent porter sur le nom d'utilisateur, l'adresse électronique, ou tout autre zone que vous voulez voir renseignée.
{: shortdesc}

Lorsque les assertions sont renvoyées à {{site.data.keyword.appid_short_notm}}, le service fédère l'identité de l'utilisateur. Si l'assertion SAML correspond à l'une des réclamations OIDC suivantes, elle est automatiquement ajoutée au jeton d'identité.  Si une ou plusieurs de ces valeurs changent côté fournisseur, les nouvelles valeurs ne sont disponibles qu'après la reconnexion de l'utilisateur.

 * `name`
 * `email`
 * `locale`
 * `picture`

Les assertions qui ne correspondent à aucun des noms standard sont par défaut ignorées, mais si votre fournisseur SAML renvoie d'autres assertions, il est possible d'obtenir les informations lorsqu'un utilisateur se connecte. En créant un tableau des assertions que vous voulez utiliser, vous pouvez [injecter les informations dans vos jetons](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Mais, veillez à ne pas ajouter plus d'informations que nécessaires à vos jetons. Les jetons sont généralement envoyés dans des en-têtes http et les en-têtes sont limités en taille.
{: tip}

### Pour {{site.data.keyword.appid_short_notm}}, aspect attendu d'une assertion SAML
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




## Fourniture de métadonnées à votre fournisseur d'identité
{: #saml-provide-idp}

Pour configurer votre application, vous devez fournir des informations à un fournisseur d'identité compatible SAML. Ces informations sont échangées via un fichier XML de métadonnées qui comporte égaiement des données de configuration utilisées pour établir le caractère de fiabilité.
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
      <td>Façon dont le fournisseur d'identité détermine le format d'identificateur qu'il doit envoyer dans l'objet d'une assertion. Façon dont {{site.data.keyword.appid_short_notm}} identifie des utilisateurs.</td>
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

## Fourniture de métadonnées à {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

Vous pouvez obtenir des données de votre fournisseur d'identité et les fournir à {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Fourniture de métadonnées à l'aide de l'interface graphique
{: #saml-provide-gui}

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


### Fourniture de métadonnées avec l'API
{: #saml-provide-api}

1. Obtenez vos métadonnées SAML en envoyant une demande GET au [noeud final d'API /getSamlMetadata](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

  Exemple de code :
  ```
  <?xml version="1.0"?>
  <getSamlMetadata>
    <?xml version="1.0"?> <EntityDescriptor> <SPSSODescriptor> <NameIDFormat> </NameIDFormat> <AssertionConsumerService /> </SPSSODescriptor>
   </EntityDescriptor>
    </getSamlMetadata>
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
    },
    "validation_data": {
      "certificates": [
        {
          "certificate_index": 0,
          "expiration_timestamp": 1674473996,
          "warning": "Your certificate will expire in 18 days."
        }
      ]
    }
  }
  ```
  {: screen}

2. Configurez votre requête POST sur le [noeud final d'API /set_saml_idp](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

  1. Dans l'exemple de métadonnées suivant, remplacez les variables par vos propres informations.

    ```
    Put {Management URI}/config/idps/saml
    Content-Type: application/json
    {
      "isActive": true,
      "config": {
        "entityID": "https://example.com/saml2/metadata/706634",
        "signInUrl": "https://example.com/saml2/sso-redirect/706634",
        "certificates": [
          "primary-certificate-example-pem-format"
        ],
        "displayName": "my saml example"
      }
    }
    ```
    {: codeblock}

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

  2. Facultatif : ajoutez un certificat secondaire au tableau de certificats après le certificat principal. Le certificat secondaire est utilisé si la validation de la signature échoue avec le certificat principal. Si la clé de signature reste la même, {{site.data.keyword.appid_short_notm}} ne bloque pas l'authentification de certificats arrivés à expiration.

    Exemple :
    ```
    {
      "isActive": true,
      "config": {
        ...
        "certificates": [
          "primary-certificate-example-pem-format",
          "secondary-certificate-example-pem-format"
        ],
        ...
      }
    }
    ```
    {: screen}
  {: #configuring-saml-new}
  3. Facultatif : ajoutez un contexte d'authentification en ajoutant un tableau de classe et une chaîne de comparaison à votre code. Veillez à mettre à jour les paramètres `class` et `comparison` avec vos valeurs. Un contexte d’authentification permet de vérifier la qualité de l'authentification et des assertions SAML.

    Exemple :
    ```
    {
      "isActive": true,
      "config": {
        ...
        "authnContext": {
          "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
          "comparison": "sampleComparisonValue"
        }
      }
    }
    ```
    {: screen}

3. Envoyez la demande. Si vous avez choisi d'ajouter les valeurs facultatives, votre demande doit ressembler à l'exemple suivant.

  ```
  Put {Management URI}/config/idps/saml
  Content-Type: application/json
  {
    "isActive": true,
    "config": {
      ...
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
        "comparison": "sampleComparisonValue"
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
      "displayName": "my saml example"
    }
  }
  ```
  {: codeblock}


## Test de votre configuration
{: #saml-testing}

Vous pouvez tester la configuration entre votre fournisseur d'identité SAML et {{site.data.keyword.appid_short_notm}}.

1. Veillez à sauvegarder votre configuration.
2. Accédez à l'onglet **SAML 2.0** du tableau de bord {{site.data.keyword.appid_short_notm}} et cliquez sur **Test**. Un nouvel onglet s'ouvre.
3. Connectez-vous à l'aide d'un utilisateur que votre fournisseur d'identité a déjà authentifié.
4. Une fois le formulaire complété, vous êtes redirigé vers une autre page.
  * Authentification réussie : La connexion entre {{site.data.keyword.appid_short_notm}} et le fournisseur d'identité fonctionne correctement. La page affiche des [jetons d'accès et d'identité](/docs/services/appid?topic=appid-tokens#tokens) valides.
  * Echec de l'authentification : La connexion est interrompue. La page affiche les erreurs et le fichier XML de réponse SAML.


Vous rencontrez des problèmes ? Consultez [Troubleshooting identity provider configurations](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}
