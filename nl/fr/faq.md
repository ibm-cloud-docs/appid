---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Foire aux questions

Cette foire aux questions fournit des réponses aux questions courantes sur le service {{site.data.keyword.appid_full}}.
{: shortdesc}


## Comment {{site.data.keyword.appid_short_notm}} calcule-t-il les prix ?
{: #pricing}

Avec {{site.data.keyword.appid_short_notm}}, plus vous utilisez de ressources, moins vous payez.
{: shortdesc}

Le plan à tranches graduées comprend deux parties : le nombre d'événements d'authentification et le nombre d'utilisateurs autorisés. Vous êtes facturé chaque mois sur la base d'une synthèse des deux parties. Le prix total
correspond aux frais cumulés pour chaque niveau d'utilisation, c'est-à-dire la quantité que vous utilisez multipliée par le prix unitaire de chaque tranche.

### Evénements d'authentification

Un événement d'authentification se produit lorsqu'un nouveau
jeton {{site.data.keyword.appid_short_notm}} est émis. Pour les utilisateurs identifiés,
chaque nouveau jeton est valide une heure. Pour les utilisateurs anonymes, les jetons sont
valides un mois. A l'expiration du jeton, vous devez en créer un nouveau pour accéder aux ressources protégées. Lorsque vous utilisez App ID pour l'authentification sur mobile,
les jetons des utilisateurs sont stockés dans `key-store/key-chain` et sont ajoutés à chaque
future demande. Ils sont accessibles via l'utilisation du SDK {{site.data.keyword.appid_short_notm}} pour Android ou iOS Swift. Lorsque vous utilisez le service pour l'authentification web, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">stockez le jeton de l'utilisateur <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> dans
les cookies de session.

### Utilisateurs autorisés

Un utilisateur autorisé est un utilisateur unique qui se connecte avec votre
service directement ou indirectement. Vous êtes facturé pour un utilisateur autorisé
chaque fois qu'un nouvel utilisateur se connecte depuis chaque fournisseur d'identité, y
compris dans le cas d'un utilisateur anonyme. Par exemple, si un utilisateur se connecte avec son identité Facebook, puis plus tard avec son profil Google,
deux utilisateurs autorisés distincts seront considérés.

Pour plus d'informations sur la tarification à tranches graduées, consultez les [documents de tarification {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>

## Quel type d'activité est surveillé par App ID ?
{: #activity-monitor}

Vous pouvez procéder au suivi de l'activité générée au sein de l'application liée à l'instance de service. Vous pouvez également surveiller l'activité d'administration effectuée dans App ID à l'aide du service Suivi de l'activité.

Pour afficher l'activité générée par votre application :

1. Connectez-vous à votre compte IBM Cloud.
2. Depuis le tableau de bord, sélectionnez votre instance d'App ID.
3. Cliquez sur l'onglet **Vue d'ensemble**.
4. Consultez l'activité répertoriée dans le **Journal d'activité**.

</br>
Pour surveiller l'activité d'administration :

1. Connectez-vous à votre compte IBM Cloud. Accédez à l'organisation et de l'espace dans lesquels votre instance d'App ID est mise à disposition.
2. Dans le catalogue, mettez à disposition une instance du service Suivi de l'activité. Veillez à vous trouver dans le même espace que votre instance d'App ID.
3. Dans le tableau de bord du service Suivi de l'activité, cliquez sur l'onglet **Gérer**.
4. Dans la liste déroulante, sélectionner les configurations suivantes afin de rechercher les événements qui ont été générés par l'App ID.
<table>
  <tr>
    <th> Zone </th>
    <th> Configuration </th>
  </tr>
  <tr>
    <td><i>Afficher les journaux</i></td>
    <td><b>Journaux d'espace</b></td>
  </tr>
  <tr>
    <td><i>Search</i></td>
    <td><b>target.name</b></td>
  </tr>
  <tr>
    <td>Filtrer</td>
    <td>appid</td>
  </tr>
</table>
5. Cliquez sur **Filtre**.

Pour plus d'informations sur le fonctionnement du service, voir la [documentation relative au suivi des activités](/docs/services/cloud-activity-tracker/index.html).
