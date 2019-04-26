---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-14"

keywords: authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

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

# Traitement général des incidents
{: #troubleshooting}

Si vous rencontrez des problèmes lorsque vous utilisez {{site.data.keyword.appid_full}}, les techniques suivantes peuvent vous aider à les résoudre et à obtenir de l'aide.
{: shortdesc}

## Aide et assistance
{: #ts-gettinghelp}

Vous pouvez obtenir de l'aide en recherchant des informations précises ou en posant des questions via un forum. Vous pouvez aussi ouvrir un ticket de demande de service. Lorsque vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de façon à ce qu'elle soit vue par les équipes de développement {{site.data.keyword.cloud_notm}}.
  * Posez toute question d'ordre technique sur {{site.data.keyword.appid_short_notm}} sur le forum <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> en indiquant balise "ibm-appid".
  * Posez toute question relative au service et aux instructions de mise en route sur le forum <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> Incluez la balise `appid`.

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
Vous pouvez recevoir une erreur "too many requests" si vous effectuez un test automatisé avec un seul utilisateur virtuel. Chaque utilisateur est limité à cinq tentatives de connexion dans un délai d'une minute. Les tentatives de connexion sont limitées de manière à éviter les attaques en force DDOS et autres types d'attaques similaires.

{: tsResolve}
Pour résoudre le problème, vous pouvez utiliser plusieurs utilisateurs virtuels lorsque vous effectuez le test.
</br>
