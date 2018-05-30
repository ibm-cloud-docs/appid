---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Traitement des incidents
{: #troubleshooting}

Si vous rencontrez des problèmes lorsque vous utilisez {{site.data.keyword.appid_full}}, les techniques suivantes peuvent vous aider à les résoudre et à obtenir de l'aide.
{: shortdesc}


## Aide et assistance
{: #gettinghelp}

Vous pouvez obtenir de l'aide en recherchant des informations précises ou en posant des questions via un forum. Vous pouvez aussi ouvrir un ticket de demande de service. Lorsque vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de façon à ce qu'elle soit vue par les équipes de développement {{site.data.keyword.Bluemix_notm}}.
  * En cas de questions d'ordre technique sur {{site.data.keyword.appid_short_notm}}, posez votre question sur le forum <a href="http://stackoverflow.com/search?q=ibm+" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>, accompagnée de la balise "ibm-appid".
  * Pour des questions relatives au service et aux instructions de mise en route, utilisez le forum <a href="https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=appid%20[bluemix]" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Incluez la balise `appid`.

Pour plus d'informations sur l'obtention de support, voir [Comment obtenir l'aide dont j'ai besoin ?](/docs/get-support/howtogetsupport.html#getting-customer-support).

</br>

## Impossible d'être redirigé vers l'application une fois connecté
{: #signin-fail}

{: tsSymptoms}
Un utilisateur se connecte à votre application via une page de connexion d'un fournisseur d'identité et, soit rien ne se passe, soit la connexion échoue.

{: tsCauses}
Il est possible que la connexion échoue pour les raisons suivantes :

* Votre URL de redirection n'a pas été correctement ajoutée à la [liste blanche](identity-providers.html#redirect).
* L'utilisateur n'est pas autorisé.
* L'utilisateur a tenté de se connecter avec de mauvaises données d'identification.

{: tsResolve}
Pour que la redirection ait lieu :

* Vérifiez que votre URL de redirection est correcte. Elle doit être exacte pour que la redirection ait lieu.
* Veillez à ce que votre utilisateur se connecte avec les données d'identification appropriées.
* Vérifiez que ces données sont configurées dans vos paramètres utilisateur de fournisseur d'identité.

</br>

## Problèmes courants lors de l'utilisation du langage SAML
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
      <td>Il existe un <code><saml:Attribute</code> sans valeur définie. Contactez votre administrateur de fournisseur d'identité.</td>
    </tr>
    <tr>
      <td><code>SAML response body must contain RelayState.</code></td>
      <td>Le paramètre RelayState n'a pas été inclus dans le corps de réponse SAML. {{site.data.keyword.appid_short_notm}} fournit le paramètre au fournisseur d'identité comme partie de la demande, et le paramètre exact doit être envoyé dans la réponse. Si le paramètre est modifié, vous pouvez contacter votre administrateur de fournisseur d'identité.</td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>Le fournisseur d'identité SAML n'est pas correctement configuré. Validez votre configuration. Pour obtenir de l'aide, voir <a href="enterprise.html#configuring-saml" target="_blank">Configuration de votre application pour une utilisation d'un fournisseur d'identité SAML externe</a>.</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>Une signature et un en-tête digest valides doivent être inclus dans l'assertion. La signature doit être créée en utilisant la clé privée associée au certificat fourni dans la configuration SAML, qu'il s'agisse de la clé principale ou secondaire. <em>Remarque</em> : {{site.data.keyword.appid_short_notm}} ne prend pas en charge l'assertion chiffrée. Si votre fournisseur d'identité chiffre votre assertion SAML, désactivez le chiffrement. </td>
    </tr>
  </tbody>
</table>


## Pas de redirection vers le fournisseur d'identité lors de l'utilisation de SAML
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

Si aucune de ces solutions ne résout le problème, il est possible que vous ayez un problème de connexion. 

</br>

## Un attribut affiche une valeur erronée lors de l'utilisation de SAML
{: #saml-attribute}

{: tsSymptoms}
Une valeur d'attribut existe dans un profil utilisateur mais n'est pas connectée à l'attribut approprié.

{: tsCauses}
L'attribut de profil utilisateur n'est pas correctement mappé.

{: tsResolve}
Mappez les attributs des paramètres de votre fournisseur d'identité. {{site.data.keyword.appid_short_notm}} attend les attributs suivants :
* `name`
* `email`
* `locale`
* `picture`
