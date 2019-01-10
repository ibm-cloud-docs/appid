---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}

# Configuration des fournisseurs d'identité
{: #troubleshooting-idp}

Si vous rencontrez des problèmes lorsque vous configurez des fournisseurs d'identité pour qu'ils fonctionnent avec {{site.data.keyword.appid_full}}, les techniques ci-après peuvent vous aider à les résoudre et à obtenir de l'aide.
{: shortdesc}


## Un utilisateur n'est pas redirigé vers l'application après connexion
{: #signin-fail}

{: tsSymptoms}
Un utilisateur se connecte à votre application via une page de connexion d'un fournisseur d'identité et, soit rien ne se passe, soit la connexion échoue.

{: tsCauses}
Il est possible que la connexion échoue pour les raisons suivantes :

* Votre URL de redirection n'a pas été correctement ajoutée à la [liste blanche](faq.html#redirect).
* L'utilisateur n'est pas autorisé.
* L'utilisateur a tenté de se connecter avec de mauvaises données d'identification.

{: tsResolve}
Pour que la redirection ait lieu :

* Vérifiez que votre URL de redirection est correcte. Elle doit être exacte pour que la redirection ait lieu.
* Veillez à ce que votre utilisateur se connecte avec les données d'identification appropriées.
* Vérifiez que ces données sont configurées dans vos paramètres utilisateur de fournisseur d'identité.

</br>

## Problèmes courants de langage SAML
{: #common-saml}

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
      <td>Le fournisseur d'identité SAML n'est pas <a href="enterprise.html" target="_blank">correctement configuré</a>. Validez votre configuration.</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>Une signature et un en-tête digest valides doivent être inclus dans l'assertion. La signature doit être créée en utilisant la clé privée qui est associée au certificat fourni dans la configuration SAML, qu'il s'agisse de la clé principale ou secondaire. <strong>Remarque</strong> : {{site.data.keyword.appid_short_notm}} ne prend pas en charge l'assertion chiffrée. Si votre fournisseur d'identité chiffre votre assertion SAML, désactivez le chiffrement.</td>
    </tr>
  </tbody>
</table>

</br>

## Un utilisateur n'est pas redirigé vers le fournisseur d'identité
{: #saml-redirect}

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

## Un attribut affiche une valeur erronée
{: #saml-attribute}

{: tsSymptoms}
Une valeur d'attribut existe dans un profil utilisateur mais n'est pas associée à l'attribut approprié.

{: tsCauses}
L'attribut de profil utilisateur n'est pas correctement mappé.

{: tsResolve}
Mappez les attributs des paramètres de votre fournisseur d'identité. {{site.data.keyword.appid_short_notm}} attend les attributs suivants :
* `name`
* `email`
* `locale`
* `picture`

</br>

## Erreurs de validation de réponse SAML
{: #saml-response}

{{site.data.keyword.appid_short_notm}} impose les exigences de validité suivantes pour les assertions. Tous les attributs sont des noeuds XML SAMLResponse obligatoires, sauf indication contraire.
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
      <td>Une signature et un en-tête digest valides doivent être inclus dans l'assertion. La signature doit être créée en utilisant la clé privée qui est associée au certificat fourni dans la configuration SAML. L'historique est validé à l'aide de la méthode de canonisation <code>CanonicalizationMethod</code> et des transformations <code>Transforms</code> spécifiées. <strong>Remarque</strong> : {{site.data.keyword.appid_short_notm}} ne valide pas l'expiration du certificat. Pour obtenir de l'aide pour la gestion de vos certificats, essayez [Certificate Manager](/docs/services/certificate-manager/index.html).</td>
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
