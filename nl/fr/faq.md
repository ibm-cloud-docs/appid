---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:faq: data-hd-content-type='faq'}


# Foire aux questions
{: #faq}

Cette foire aux questions fournit des réponses aux questions courantes sur le service {{site.data.keyword.appid_full}}.
{: shortdesc}


## Comment {{site.data.keyword.appid_short_notm}} calcule-t-il les prix ?
{: #pricing}
{: faq}

Avec {{site.data.keyword.appid_short_notm}}, plus vous utilisez de ressources, moins vous payez.
{: shortdesc}

Le plan à tranches graduées comprend trois parties : le nombre d'événements d'authentification, la sécurité régulière et la sécurité avancée et le nombre d'utilisateurs autorisés. Vous êtes facturé chaque mois sur la base d'une synthèse des deux parties. Le prix total correspond aux frais cumulés pour chaque niveau d'utilisation, c'est-à-dire la quantité que vous utilisez multipliée par le prix unitaire de chaque tranche.

Vos 1000 premiers événements d'authentification et les 1000 premiers utilisateurs autorisés de chaque mois sont gratuits, à l'exception des événements de sécurité avancée. Tous les événements de sécurité avancée entraînent des frais supplémentaires.

### Evénements d'authentification

Un événement d'authentification survient lorsqu'un nouveau jeton d'accès, ordinaire ou anonyme, est émis. Les jetons peuvent être émis en réponse à une demande de connexion initiée par un utilisateur, ou par une application pour l'utilisateur. Par défaut, les jetons d'accès sont valables pendant une heure et les jetons anonymes pendant 30 jours. A l'expiration du jeton, vous devez en créer un nouveau pour accéder aux ressources protégées. Vous pouvez mettre à jour l'heure d'expiration de vos jetons {{site.data.keyword.appid_short_notm}} sur la page d'**expiration de la connexion** du tableau de bord du service.

#### Fonctions de sécurité avancée

Les fonctions de sécurité avancée vous permettent de renforcer la sécurité de votre application.
{: shortdesc}

<table>
  <tr>
    <th>Fonction</th>
    <th>Avantage</th>
  </tr>
  <tr>
    <td>Authentification multi-facteur</td>
    <td>[MFA for Cloud Directory](mfa.html) confirme l'identité d'un utilisateur en lui demandant d'entrer un code d'accès unique qui lui est envoyé par courrier électronique, en plus de son adresse électronique et de son mot de passe.</td>
  </tr>
  <tr>
    <td>Gestion des règles sur les mots de passe</td>
    <td>En tant que propriétaire de compte, vous pouvez imposer des mots de passe plus sécurisés pour Cloud Directory en configurant un ensemble de règles auxquelles les mots de passe utilisateur doivent se conformer. Par exemple, ces règles incluent le nombre de tentatives de connexion avant verrouillage, les délais d'expiration, le délai minimum entre les mises à jour de mot de passe ou le nombre de fois avant lesquelles un mot de passe ne peut pas être répété. Pour obtenir la liste complète des options et des informations de configuration, voir [Advanced password management](cloud-directory.html#advanced-password).</td>
  </tr>
</table>

Par défaut, les fonctions de sécurité avancée sont désactivées. L'activation de l'authentification multi-facteur ou de la gestion des règles sur les mots de passe entraîne la facturation de frais supplémentaires. Si vous désactivez toutes les fonctions avancées, votre compte revient à la politique à moindre coût. Par exemple, si vous avez obtenu 10 000 jetons d'accès, puis avez activé l'authentification multi-facteur et la gestion des règles sur les mots de passe et en avez obtenu 10 000 autres, vous paierez pour 20 000 événements d'authentification et 10 000 événements de sécurité avancée.

Ces fonctions ne sont disponibles que pour les instances figurant sur le plan de tarification à tranches graduées et créées après le 15 mars 2018.
{: note}

### Utilisateurs autorisés

Les utilisateurs autorisés sont des utilisateurs uniques qui se connectent à votre service, directement ou indirectement, notamment des utilisateurs anonymes. Vous êtes facturé pour un utilisateur autorisé à chaque fois qu'un nouvel utilisateur, y compris un utilisateur anonyme, se connecte à votre application. Par exemple, si un utilisateur se connecte avec son profil Facebook, puis plus tard avec son profil Google, il est pris en compte comme s'il s'agissait de deux utilisateurs autorisés distincts.

Pour obtenir les dernières informations de tarification d'{{site.data.keyword.appid_short_notm}}, voir la [calculatrice de prix](https://console.cloud.ibm.com/pricing/configure/service/AdvancedMobileAccess-d6aece47-d840-45b0-8ab9-ad15354deeea).
{: important}

</br>


## Pourquoi dois-je ajouter mon URL de redirection à la liste blanche ?
{: #redirect}
{: faq}

Une URL de redirection est le noeud final de rappel de votre application. Pour empêcher les attaques par hameçonnage, {{site.data.keyword.appid_short_notm}} valide l'URL par rapport à la liste blanche des URL de redirection. En cas d'hameçonnage, il est possible qu'un pirate puisse accéder à vos jetons utilisateur.

Pour ajouter votre URL à la liste blanche :

1. Accédez à **Fournisseurs d'identité > Gérer**.
2. Dans la zone **Ajouter une URL de redirection Web**, entrez l'URL et cliquez sur **+**.

N'incluez pas de paramètres de demande dans votre URL. Ils sont ignorés lors du processus de validation. Exemple d'URL : `http://hôte:[port]/chemin`
{: tip}

</br>

## Fonctionnement du chiffrement dans {{site.data.keyword.appid_short_notm}}
{: #encryption}
{: faq}

Consultez le tableau ci-dessous pour obtenir des réponses aux questions fréquemment posées sur le chiffrement.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Pourquoi utilisez-vous le chiffrement ?</td>
      <td>L'un des moyens de protéger les informations de nos utilisateurs consiste à chiffrer les données client inactives. Le service chiffre les données client inactives à l'aide de clés par titulaire.</td>
    </tr>
    <tr>
      <td>Avez-vous généré vos propres algorithmes ? Lesquels utilisez-vous dans votre code ?</td>
      <td>Nous n'avons pas généré nos propres algorithmes, mais le service utilise les algorithmes <code>AES</code> et <code>SHA-256</code> associés au salage.</td>
    </tr>
    <tr>
      <td>Utilisez-vous des fournisseurs ou des modules de chiffrement publics ou open source ? Vous arrive-t-il d'exposer les fonctions de chiffrement ? </td>
      <td>Le service utilise des bibliothèques Java <code>javax.crypto</code> mais n'expose jamais les fonctions de chiffrement.</td>
    </tr>
    <tr>
      <td>Comment stockez-vous les clés ?</td>
      <td>Les clés sont générées, chiffrées avec une clé principale spécifique à chaque région, puis stockées localement. Les clés principales sont stockées dans {{site.data.keyword.keymanagementserviceshort}}. Au niveau du stockage et du middleware, il existe un chiffrement de niveau de service qui signifie qu'il existe une clé unique pour tous les clients. Au niveau de l'application, chaque client dispose de sa propre clé de chiffrement.</td>
    </tr>
    <tr>
      <td>Quel niveau de chiffrement de la clé utilisez-vous ?</td>
      <td>Le service utilise un niveau de chiffrement de 16 octets.</td>
    </tr>
    <tr>
      <td>Appelez-vous des API distantes qui exposent les fonctions de chiffrement ?</td>
      <td>Non.</td>
    </tr>
  </tbody>
</table>

</br>

## Pour {{site.data.keyword.appid_short_notm}}, aspect attendu d'une assertion SAML
{: #saml-example}
{: faq}

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

</br>

## Types d'algorithme pris en charge pour les signatures SAML
{: #saml-signatures}
{: faq}

Vous pouvez utiliser l'un des algorithmes ci-dessous pour traiter les signatures numériques XML.

<table>
  <tr>
    <th> Type d'algorithme </th>
    <th> Options d'algorithme </th>
  </tr>
  <tr>
    <td>Algorithmes de canonisation et de transformation avec ou sans commentaires</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">Canonicalization <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">Exclusive Canonicalization with and without comments <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">Enveloped Signature transform <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li></ul></td>
  </tr>
  <tr>
    <td>Algorithmes de hachage</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">SHA1 digests <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">SHA256 digests <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">SHA512 digests <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li></ul></td>
  </tr>
  <tr>
    <td>Algorithmes de signature</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></li></ul></td>
  </tr>
</table>

Pour plus d'informations sur l'utilisation d'un fournisseur d'identité SAML, voir [Configuration de fournisseurs d'identité d'entreprise](enterprise.html).
