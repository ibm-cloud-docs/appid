---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-19"

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

</br>

**Que sont les attributs prédéfinis ?**

Les attributs prédéfinis sont renvoyés par le fournisseur d'identité lorsque votre utilisateur se connecte à votre application. Ils peuvent inclure le nom d'utilisateur, l'âge ou le sexe.

</br>

**Que sont les attributs personnalisés ?**

Les attributs personnalisés sont des informations apprises sur vos utilisateurs au fur et à mesure que ceux-ci interagissent avec votre application. Vous pouvez les définir avant que l'utilisateur ne se connecte à votre application pour la première fois. Par exemple, il peut s'agir de la taille de police favorite des utilisateurs, ou des articles qu'ils placent dans leur panier. Les attributs personnalisés peuvent être édités. Veillez à bien prendre connaissance des [implications pour la sécurité](custom-attributes.html) que peut entraîner l'autorisation accordée aux utilisateurs de modifier leurs attributs avant de changer les valeurs par défaut.

</br>
</br>

## Accès aux attributs utilisateur
{: #access}

Vous pouvez accéder aux attributs [prédéfinis](predefined.html) et [personnalisés](custom-attributes.html) de plusieurs façons. Après une authentification d'utilisateur réussie, votre application reçoit des jetons d'accès et d'identité. Le jeton d'identité contient un sous-ensemble normalisé d'attributs utilisateur qui sont renvoyés par un fournisseur d'identité. Vous pouvez obtenir la liste complète des attributs utilisateur via le noeud final OIDC [`/userinfo`](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/userInfo). Pour gérer les attributs personnalisés, vous pouvez utiliser l'`API REST`. Le noeud final d'informations utilisateur et le noeud final des attributs personnalisés sont protégés par le jeton d'accès qui est généré par {{site.data.keyword.appid_short_notm}} à la fin du processus d'authentification.

Pour plus d'informations sur les jetons d'identité et d'accès, voir [Understanding tokens](/docs/services/appid/authorization.html#tokens) ou [Validating tokens](/docs/services/appid/tokens.html).

Architecture d'un profil utilisateur ![{{site.data.keyword.appid_short_notm}}](images/user-profile1.png)

Figure. Flux d'informations d'un profil utilisateur

Pour consulter les attributs personnalisés, vous pouvez utiliser l'<a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API REST<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


</br>
</br>
