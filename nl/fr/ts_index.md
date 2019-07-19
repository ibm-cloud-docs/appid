---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

subcollection: appid

---

{:external: target="_blank" .external}
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

# Dépannage général
{: #troubleshooting}

Si vous rencontrez des problèmes lorsque vous utilisez {{site.data.keyword.appid_full}}, les techniques suivantes peuvent vous aider à les résoudre et à obtenir de l'aide.
{: shortdesc}

## Aide et assistance
{: #ts-gettinghelp}

Vous pouvez obtenir de l'aide en recherchant des informations précises ou en posant des questions via un forum. Vous pouvez aussi ouvrir un ticket de demande de service. Lorsque vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de façon à ce qu'elle soit vue par les équipes de développement {{site.data.keyword.cloud_notm}}.
  * Posez toute question d'ordre technique sur {{site.data.keyword.appid_short_notm}} sur le forum <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> en indiquant la balise "ibm-appid".
  * Posez toute question relative au service et aux instructions de mise en route sur le forum <a href="https://developer.ibm.com/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> Incluez la balise `appid`.

Pour plus d'informations sur l'obtention de support, voir [Comment obtenir le support dont j'ai besoin ?](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).


## Un utilisateur n'est pas redirigé vers l'application après connexion
{: #ts-signin-fail}

{: tsSymptoms}
Un utilisateur se connecte à votre application via une page de connexion d'un fournisseur d'identité et, soit rien ne se passe, soit la connexion échoue.

{: tsCauses}
Il est possible que la connexion échoue pour les raisons suivantes :

* Votre URL de redirection n'a pas été correctement ajoutée à la [liste blanche](/docs/services/appid?topic=appid-faq#faq-redirect).
* L'utilisateur n'est pas autorisé.
* L'utilisateur a tenté de se connecter avec de mauvaises données d'identification.

{: tsResolve}
Pour que la redirection ait lieu :

* Vérifiez que votre URL de redirection est correcte. Elle doit être exacte pour que la redirection ait lieu.
* Veillez à ce que votre utilisateur se connecte avec les données d'identification appropriées.
* Vérifiez que ces données sont configurées dans vos paramètres utilisateur de fournisseur d'identité.



## Un identificateur URI personnalisé est rejeté
{: #ts-custom-uri}

{: tsSymptoms}
Lorsque vous entrez une URL de redirection Web qui utilise un schéma URL personnalisé, elle est rejetée par la console {{site.data.keyword.appid_short_notm}}.

{: tsCauses}
Il est possible que votre URL soit rejetée pour les raisons suivantes :

* L'URL ne suit pas un schéma `http` ou `https`
* L'URL se termine par `://`
* Votre URL comporte une erreur typographique

Les limitations sont en place pour des raisons de sécurité.

{: tsResolve}
Pour résoudre le problème, vérifiez que l'URL est correcte. Si votre URL ne répond pas aux exigences, vous pouvez créer un noeud final HTTPS dans votre application pour rediriger le code d'octroi reçu vers votre URL personnalisée. Indiquez le noeud final créé comme votre URL de redirection dans la console {{site.data.keyword.appid_short_notm}}. Pour plus d'informations sur les URI de redirection, voir [Ajout d'URI de redirection](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)

## Un utilisateur n'est pas redirigé vers le fournisseur d'identité
{: #ts-redirect}

{: tsSymptoms}
Un utilisateur tente de se connecter à votre application, mais la page de connexion ne s'affiche pas à l'invite.

{: tsCauses}
Il est possible que le lancement du fournisseur d'identité échoue pour différentes raisons :

* L'URL de redirection que vous avez configurée  est incorrecte.
* Le fournisseur d'identité ne reconnaît pas la demande d'authentification.
* Le fournisseur d'identité attend une liaison HTTP-POST.
* Le fournisseur d'identité attend une demande AuthnRequest signée.

{: tsResolve}
Vous pouvez essayer les solutions suivantes :

* Mettez à jour votre URL de connexion. Cette URL est envoyée comme partie de la demande AuthnRequest et doit être exacte.
* Assurez-vous que vos métadonnées {{site.data.keyword.appid_short_notm}} sont correctement définies dans vos paramètres de fournisseur d'identité.
* Configurez votre fournisseur d'identité pour qu'il accepte la demande AuthnRequest dans la redirection HTTP.
* {{site.data.keyword.appid_short_notm}} ne prend pas en charge la signature des demandes AuthnRequest.

Si aucune des solutions ne résout le problème, il est possible que vous ayez un problème de connexion.
{: tip}


## Un attribut affiche une valeur erronée
{: #ts-saml-attribute}

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



## Erreur : Trop de demandes
{: #ts-requests}

{: tsSymptoms}
Vous tentez d'afficher la page d'accueil de votre application mais vous recevez l'erreur suivante :

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
Vous pouvez recevoir une erreur "too many requests" si vous effectuez un test automatisé avec un seul utilisateur virtuel. Chaque utilisateur est limité à cinq tentatives de connexion dans un délai d'une minute. Les tentatives de connexion sont limitées de manière à éviter les attaques en force DDoS et autres types d'attaques similaires.

{: tsResolve}
Pour résoudre le problème, vous pouvez utiliser plusieurs utilisateurs virtuels lorsque vous effectuez le test.
</br>
