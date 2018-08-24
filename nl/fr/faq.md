---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# Foire aux questions

Cette foire aux questions fournit des réponses aux questions courantes sur le service {{site.data.keyword.appid_full}}.
{: shortdesc}


## Comment {{site.data.keyword.appid_short_notm}} calcule-t-il les prix ?
{: #pricing}

Avec {{site.data.keyword.appid_short_notm}}, plus vous utilisez de ressources, moins vous payez.
{: shortdesc}

Le plan à tranches graduées comprend deux parties : le nombre d'événements d'authentification et le nombre d'utilisateurs autorisés. Vous êtes facturé chaque mois sur la base d'une synthèse des deux parties. Le prix total correspond aux frais cumulés pour chaque niveau d'utilisation, c'est-à-dire la quantité que vous utilisez multipliée par le prix unitaire de chaque tranche.

### Evénements d'authentification

Un événement d'authentification survient lorsqu'un nouveau jeton d'accès, ordinaire ou anonyme, est émis. Pour les utilisateurs identifiés, chaque nouveau jeton d'accès est valide par défaut pendant une heure (par le biais d'une authentification d'utilisateur réelle ou de jetons d'actualisation). Les jetons anonymes sont valides par défaut pendant un mois. A l'expiration du jeton, vous devez en créer un nouveau pour accéder aux ressources protégées. Vous pouvez mettre à jour l'heure d'expiration des jetons {{site.data.keyword.appid_short_notm}} dans la page d'**expiration de la connexion** du tableau de bord {{site.data.keyword.appid_short_notm}}. 

Lorsque vous utilisez {{site.data.keyword.appid_short_notm}} dans des applications mobiles, les jetons sont stockés dans un magasin de clés ou une chaîne de certificats et ajoutés à chaque demande effectuée. Les jetons sont accessibles à l'aide du logiciel SDK Android ou iOS d'App ID. Lorsque vous utilisez {{site.data.keyword.appid_short_notm}} dans des applications Web, il est recommandé de stocker les jetons dans des cookies de session d'application. 


### Utilisateurs autorisés

Un utilisateur autorisé est un utilisateur unique qui se connecte avec votre service directement ou indirectement. Vous êtes facturé pour un utilisateur autorisé chaque fois qu'un nouvel utilisateur se connecte depuis un fournisseur d'identité, y compris dans le cas d'un utilisateur anonyme. Par exemple, si un utilisateur se connecte avec son identité Facebook, puis plus tard avec son profil Google, ils seront considérés comme deux utilisateurs autorisés distincts. 

Pour plus d'informations sur la tarification à tranches graduées, consultez les [documents de tarification {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>


## Fonctionnement du chiffrement dans {{site.data.keyword.appid_short_notm}} 
{: #encryption}

Consultez le tableau ci-dessous pour obtenir des réponses aux questions fréquemment posées sur le chiffrement. 

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Pourquoi utilisez-vous le chiffrement ?</td>
      <td>Le service chiffre les données client au repos. </td>
    </tr>
    <tr>
      <td>Avez-vous généré vos propres algorithmes ? Lesquels utilisez-vous dans votre code ? </td>
      <td>Nous n'avons pas généré nos propres algorithmes, mais le service utilise les algorithmes <code>AES</code> et <code>SHA-256</code> associés au salage. </td>
    </tr>
    <tr>
      <td>Utilisez-vous des fournisseurs ou des modules de chiffrement publics ou open source ? Vous arrive-t-il d'exposer les fonctions de chiffrement ? </td>
      <td>Le service utilise des bibliothèques Java <code>javax.crypto</code> mais n'expose jamais les fonctions de chiffrement. </td>
    </tr>
    <tr>
      <td>Comment stockez-vous les clés ? </td>
      <td>Les clés sont générées puis stockées localement une fois chiffrées à l'aide d'une clé principale propre à chaque région. Les clés principales sont stockées dans {{site.data.keyword.keymanagementserviceshort}}.</td>
    </tr>
    <tr>
      <td>Quel niveau de chiffrement de la clé utilisez-vous ? </td>
      <td>Le service utilise un niveau de chiffrement de 16 octets. </td>
    </tr>
    <tr>
      <td>Appelez-vous des API distantes qui exposent les fonctions de chiffrement ? </td>
      <td>Non. </td>
    </tr>
  </tbody>
</table>

</br>

## Pour {{site.data.keyword.appid_short_notm}}, aspect attendu d'une assertion SAML
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

</br>

## Types d'algorithme pris en charge pour les signatures SAML
{: #saml-signatures}

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
