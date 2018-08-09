---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

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

Un événement d'authentification se produit lorsqu'un nouveau jeton {{site.data.keyword.appid_short_notm}} est émis. Pour les utilisateurs identifiés, chaque nouveau jeton est valide une heure. Les jetons sont valides pour une durée d'un mois. A l'expiration du jeton, vous devez en créer un nouveau pour accéder aux ressources protégées. Lorsque vous utilisez {{site.data.keyword.appid_short_notm}} pour l'authentification sur mobile, les jetons des utilisateurs sont stockés dans `key-store/key-chain` et sont ajoutés à chaque future demande. Ils sont accessibles via l'utilisation du SDK {{site.data.keyword.appid_short_notm}} pour Android ou iOS Swift. Lorsque vous utilisez le service pour l'authentification Web, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">stockez le jeton de l'utilisateur <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> dans les cookies de session.

### Utilisateurs autorisés

Un utilisateur autorisé est un utilisateur unique qui se connecte avec votre service directement ou indirectement. Vous êtes facturé pour un utilisateur autorisé chaque fois qu'un nouvel utilisateur se connecte depuis chaque fournisseur d'identité, y compris dans le cas d'un utilisateur anonyme. Par exemple, si un utilisateur se connecte avec son identité Facebook, puis plus tard avec son profil Google, deux utilisateurs autorisés distincts seront considérés.

Pour plus d'informations sur la tarification à tranches graduées, consultez les [documents de tarification {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>

## Type d'activité surveillé par {{site.data.keyword.appid_short_notm}}
{: #activity-monitor}

Vous pouvez procéder au suivi de l'activité générée au sein de l'application liée à l'instance de service. Vous pouvez également surveiller l'activité d'administration effectuée dans {{site.data.keyword.appid_short_notm}} à l'aide du service {{site.data.keyword.cloudaccesstrailshort}}.

Pour afficher l'activité générée par votre application :

1. Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}.
2. Depuis le tableau de bord, sélectionnez votre instance d'{{site.data.keyword.appid_short_notm}}.
3. Cliquez sur l'onglet **Vue d'ensemble**.
4. Consultez l'activité répertoriée dans le **Journal d'activité**.

</br>
Pour surveiller l'activité d'administration :

1. Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}. Accédez à l'organisation et de l'espace dans lesquels votre instance d'{{site.data.keyword.appid_short_notm}} est mise à disposition.
2. Dans le catalogue, mettez à disposition une instance du service {{site.data.keyword.cloudaccesstrailshort}}. Veillez à vous trouver dans le même espace que votre instance d'{{site.data.keyword.appid_short_notm}}.
3. Dans le tableau de bord {{site.data.keyword.cloudaccesstrailshort}}, cliquez sur l'onglet **Gérer**.
4. Dans la liste déroulante, sélectionnez les configurations suivantes afin de rechercher les événements générés par {{site.data.keyword.appid_short_notm}}.
<table>
  <tr>
    <th> Zone </th>
    <th> Configuration </th>
  </tr>
  <tr>
    <td>Affichage des journaux </td>
    <td>Journaux d'espace</td>
  </tr>
  <tr>
    <td>Rechercher</td>
    <td>target.name</td>
  </tr>
  <tr>
    <td>Filtrer</td>
    <td>appid</td>
  </tr>
</table>
5. Cliquez sur **Filtre**.

Pour plus d'informations sur le fonctionnement du service, voir la [documentation {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html).

</br>

## Pour {{site.data.keyword.appid_short_notm}}, aspect attendu d'une assertion SAML
{: #saml-example}

Le service s'attend à ce qu'une assertion SAML ressemble à l'exemple suivant.

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

Vous pouvez utiliser l'un des algorithmes suivants pour traiter les signatures numériques XML.

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
