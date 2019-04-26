---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, user profiles, personalized apps, attributes, 

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

# Compréhension des profils utilisateur
{: #user-profile}

Avec {{site.data.keyword.appid_full}}, vous pouvez générer des expériences d'application personnalisées en accédant aux informations sur vos utilisateurs qui sont stockées par {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

## Concepts clés
{: #profile-concepts}

**Qu'est-ce qu'un profil utilisateur ?**

Un profil utilisateur est un ensemble d'attributs qui sont stockés par {{site.data.keyword.appid_short_notm}}. Les attributs sont des éléments d'information sur les utilisateurs qui interagissent avec votre application. Vous pouvez obtenir deux types d'attribut : des attributs `prédéfinis` et des attributs `personnalisés`.



**Que sont les attributs prédéfinis ?**

Les attributs prédéfinis sont renvoyés par le fournisseur d'identité lorsque votre utilisateur se connecte à votre application. Ils peuvent inclure le nom d'utilisateur, l'âge ou le sexe.



**Que sont les attributs personnalisés ?**

Les attributs personnalisés sont des informations apprises sur vos utilisateurs au fur et à mesure que ceux-ci interagissent avec votre application. Vous pouvez les définir avant que l'utilisateur ne se connecte à votre application pour la première fois. Par exemple, il peut s'agir de la taille de police favorite des utilisateurs, ou des articles qu'ils placent dans leur panier. Les attributs personnalisés peuvent être édités. Veillez à bien prendre connaissance des [implications pour la sécurité](/docs/services/appid?topic=appid-custom-attributes) que peut entraîner l'autorisation accordée aux utilisateurs de modifier leurs attributs avant de changer les valeurs par défaut.


## Accès aux attributs utilisateur
{: #profile-access}

Vous pouvez accéder aux attributs [prédéfinis](/docs/services/appid?topic=appid-predefined-attributes) et [personnalisés](/docs/services/appid?topic=appid-custom-attributes) de plusieurs façons. Après une authentification d'utilisateur réussie, votre application reçoit des jetons d'accès et d'identité. Le jeton d'identité contient un sous-ensemble normalisé d'attributs utilisateur qui sont renvoyés par un fournisseur d'identité. Vous pouvez obtenir la liste complète des attributs utilisateur via le noeud final OIDC [`/userinfo`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo). Pour gérer les attributs personnalisés, vous pouvez utiliser l'`API REST`. Le noeud final d'informations utilisateur et le noeud final des attributs personnalisés sont protégés par le jeton d'accès qui est généré par {{site.data.keyword.appid_short_notm}} à la fin du processus d'authentification.

Pour plus d'informations sur les jetons d'identité et d'accès, voir [Understanding tokens](/docs/services/appid?topic=appid-tokens#tokens) ou [Validating tokens](/docs/services/appid?topic=appid-token-validation).

Architecture de profil utilisateur ![{{site.data.keyword.appid_short_notm}}](images/user-profile1.png)

Figure. Flux d'informations d'un profil utilisateur

Pour consulter les attributs personnalisés, vous pouvez utiliser l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes" target="_blank">API REST<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

