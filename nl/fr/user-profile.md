---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Compréhension des profils utilisateur 
{: #user-profile}

Avec {{site.data.keyword.appid_full}}, vous pouvez générer des expériences d'application personnalisées en accédant aux informations sur vos utilisateurs qui sont stockées par {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

## Concepts clés
{: #key-concepts}

**Qu'est-ce qu'un profil utilisateur ?**

Un profil utilisateur est un ensemble d'attributs qui sont stockés par {{site.data.keyword.appid_short_notm}}. Les attributs sont des éléments d'information sur les utilisateurs qui interagissent avec votre application. Vous pouvez obtenir deux types d'attribut : des attributs `prédéfinis` et des attributs `personnalisés`.

**Que sont les attributs prédéfinis ?**

Les attributs prédéfinis sont renvoyés par le fournisseur d'identité lorsque votre utilisateur se connecte à votre application. Ils peuvent inclure le nom d'utilisateur, l'âge ou le sexe. 

**Que sont les attributs personnalisés ?**

Les attributs personnalisés sont des informations apprises sur vos utilisateurs au fur et à mesure que ceux-ci interagissent avec votre application. Il peut s'agir de la taille de police qu'ils utilisent ou des articles qu'ils ont placé dans leur panier. Les attributs personnalisés peuvent être édités. 

## Accès aux attributs utilisateur
{: #access}

Vous pouvez accéder aux informations de profil utilisateur de plusieurs façons. Après une authentification d'utilisateur réussie, votre application reçoit des jetons d'accès et d'identité. Le jeton d'identité contient un sous-ensemble normalisé d'attributs utilisateur qui sont renvoyés par un fournisseur d'identité. Vous pouvez obtenir la liste complète des attributs utilisateur via le noeud final OIDC `/userinfo`. Pour gérer les attributs personnalisés, vous pouvez utiliser l'`API REST`. Le noeud final userinfo et le noeud final des attributs personnalisés sont protégés par le jeton d'accès qui est généré par {{site.data.keyword.appid_short_notm}} à la fin du processus d'authentification. 



![Architecture d'un profil utilisateur {{site.data.keyword.appid_short_notm}}](/images/user-profile1.png)

Figure. Flux d'informations d'un profil utilisateur 

Pour consulter les attributs personnalisés, vous pouvez utiliser l'<a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API REST<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. 

</br>
</br>
