---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Configuration des fournisseurs d'identité
{: #troubleshooting-idp}

Si vous rencontrez des problèmes lorsque vous configurez des fournisseurs d'identité pour qu'ils fonctionnent avec {{site.data.keyword.appid_full}}, les techniques ci-après peuvent vous aider à les résoudre et à obtenir de l'aide.
{: shortdesc}


## Un utilisateur n'est pas redirigé vers le fournisseur d'identité
{: #ts-saml-redirect}

{: tsSymptoms}
Un utilisateur tente de se connecter à votre application, mais la page de connexion ne s'affiche pas à l'invite.

{: tsCauses}
Il est possible que le lancement du fournisseur d'identité échoue pour différentes raisons :

* L'URL de redirection que vous avez configurée  est incorrecte.
* Le fournisseur d'identité ne reconnaît pas la demande d'authentification.
* Le fournisseur d'identité attend une liaison HTTP-POST.
* Le fournisseur d'identité attend une demande authnRequest signée.

{: tsResolve}
Vous pouvez essayer les solutions suivantes :

* Mettez à jour votre URL de connexion. Cette URL est envoyée comme partie de la demande authnRequest et doit être exacte.
* Assurez-vous que vos métadonnées {{site.data.keyword.appid_short_notm}} sont correctement définies dans vos paramètres de fournisseur d'identité.
* Configurez votre fournisseur d'identité pour qu'il accepte la demande authnRequest dans HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} ne prend pas en charge la signature de demande authnRequest.

Si aucune des solutions ne résout le problème, il est possible que vous ayez un problème de connexion.
{: tip}


## Problèmes courants de langage SAML
{: #ts-common-saml}

Consultez le tableau suivant pour des explications et résolutions concernant les problèmes courants rencontrés lors de l'utilisation de SAML.

<table summary="Chaque ligne du tableau se lit de gauche à droite, avec l'état du cluster à la colonne 1 et une description à la colonne 2.">
  <thead>
    <th>Message</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td><code>Could not parse assertion xml.</code></td>
      <td>La réponse de SAML a été incorrectement formée.</td>
    </tr>
    <tr>
      <td><code>Invalid attribute without name. Contact your identity provider administrator.</code></td>
      <td>Il existe un attribut <code>&lt;saml:Attribute&gt;</code> sans valeur définie. Contactez votre administrateur de fournisseur d'identité.</td>
    </tr>
    <tr>
      <td><code>SAML response body must contain the RelayState parameter.</code></td>
      <td>Le paramètre n'a pas été inclus dans le corps de réponse SAML. {{site.data.keyword.appid_short_notm}} fournit le paramètre au fournisseur d'identité comme partie de la demande, et le paramètre exact doit être envoyé dans la réponse. Si le paramètre est modifié, vous pouvez contacter votre administrateur de fournisseur d'identité. </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>Le fournisseur d'identité SAML n'est pas <a href="/docs/services/appid?topic=appid-enterprise#enterprise" target="_blank">correctement configuré</a>. Validez votre configuration.</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>Une signature et un en-tête digest valides doivent être inclus dans l'assertion. La signature doit être créée en utilisant la clé privée qui est associée au certificat fourni dans la configuration SAML, qu'il s'agisse de la clé principale ou secondaire. <strong>Remarque</strong> : {{site.data.keyword.appid_short_notm}} ne prend pas en charge l'assertion chiffrée. Si votre fournisseur d'identité chiffre votre assertion SAML, désactivez le chiffrement.</td>
    </tr>
  </tbody>
</table>



## Erreurs de validation de réponse SAML
{: #ts-saml-response}

{{site.data.keyword.appid_short_notm}} impose les exigences de validité suivantes pour les assertions. Tous les attributs sont des noeuds XML de réponse SAML obligatoires, sauf indication contraire.
{: shortdesc}


<table summary="Chaque ligne du tableau se lit de gauche à droite, avec l'élément de réponse dans la colonne 1 et une description dans la colonne 2.">
  <thead>
    <th>Elément de réponse</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>L'élément de réponse doit être inclus dans le fichier XML de réponse.</td>
    </tr>
    <tr>
      <td><code>SAML version</code></td>
      <td>{{site.data.keyword.appid_short_notm}} accepte uniquement <code>SAML version 2.0</code>.</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>{{site.data.keyword.appid_short_notm}} vérifie que l'élément de réponse <code>InResponseTo</code> renvoyé dans l'assertion correspond à l'identificateur de demande enregistré à partir de la demande SAML.</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>L'émetteur spécifié dans une assertion doit correspondre à celui spécifié dans la configuration du fournisseur d'identité {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>Une signature et un en-tête digest valides doivent être inclus dans l'assertion. La signature doit être créée en utilisant la clé privée qui est associée au certificat fourni dans la configuration SAML. L'historique est validé à l'aide de la méthode de canonisation <code>CanonicalizationMethod</code> et des transformations <code>Transforms</code> spécifiées. <strong>Remarque</strong> : {{site.data.keyword.appid_short_notm}} ne valide pas l'expiration du certificat. Pour obtenir de l'aide pour la gestion de vos certificats, essayez [Certificate Manager](/docs/services/certificate-manager?topic=certificate-manager-getting-started#getting-started).</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>Le sujet ou <code>name_id</code> de l'assertion doit être le courrier électronique de la fédération de l'utilisateur.</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>Affirme que certains attributs sont associés à un utilisateur authentifié spécifique.</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>Facultatif</strong> : lorsqu'une instruction conditionnelle est incluse dans une assertion, elle doit également contenir un horodatage valide. {{site.data.keyword.appid_short_notm}} respecte la période de validité spécifiée dans une assertion. Pour vérifier, le service recherche les contraintes <code>NotBefore</code> et <code>NotOnOrAfter</code> qui doivent être définies et valides.</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}} ne prend pas en charge les assertions chiffrées. Si votre fournisseur d'identité est défini pour chiffrer votre assertion, désactivez-le. L'assertion doit être dans un format non chiffré.
{: tip}
