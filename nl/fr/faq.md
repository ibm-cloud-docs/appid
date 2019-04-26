---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: authentication, authorization, identity, app security, secure

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
{:faq: data-hd-content-type='faq'}


# Foire aux questions
{: #faq}

Cette foire aux questions fournit des réponses aux questions courantes sur le service {{site.data.keyword.appid_full}}.
{: shortdesc}


## Comment {{site.data.keyword.appid_short_notm}} calcule-t-il les prix ?
{: #faq-pricing}
{: faq}

Avec {{site.data.keyword.appid_short_notm}}, plus vous utilisez de ressources, moins vous payez.
{: shortdesc}

Le plan à tranches graduées comprend trois parties : le nombre d'événements d'authentification, la sécurité régulière et la sécurité avancée et le nombre d'utilisateurs autorisés. Vous êtes facturé chaque mois sur la base d'une synthèse des deux parties. Le prix total correspond aux frais cumulés pour chaque niveau d'utilisation, c'est-à-dire la quantité que vous utilisez multipliée par le prix unitaire de chaque tranche.

Vos 1000 premiers événements d'authentification et les 1000 premiers utilisateurs autorisés de chaque mois sont gratuits, à l'exception des événements de sécurité avancée. Tous les événements de sécurité avancée entraînent des frais supplémentaires.

### Evénements d'authentification
{: #faq-authentication}

Un événement d'authentification survient lorsqu'un nouveau jeton d'accès, ordinaire ou anonyme, est émis. Les jetons peuvent être émis en réponse à une demande de connexion initiée par un utilisateur, ou par une application pour l'utilisateur. Par défaut, les jetons d'accès sont valables pendant une heure et les jetons anonymes pendant 30 jours. A l'expiration du jeton, vous devez en créer un nouveau pour accéder aux ressources protégées. Vous pouvez mettre à jour l'heure d'expiration de vos jetons {{site.data.keyword.appid_short_notm}} sur la page **Fournisseurs d'identité > Gérer > Paramètres d'authentification** du tableau de bord du service.

#### Fonctions de sécurité avancée

Les fonctions de sécurité avancée vous permettent de renforcer la sécurité de votre application.
{: shortdesc}

<table>
  <tr>
    <th>Fonction</th>
    <th>Avantage</th>
  </tr>
  <tr>
    <td>Authentification multi-facteur</td>
    <td>[MFA for Cloud Directory](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) confirme l'identité d'un utilisateur en lui demandant d'entrer un code d'accès unique qui lui est envoyé par courrier électronique, en plus de son adresse électronique et de son mot de passe.</td>
  </tr>
  <tr>
    <td>Gestion des règles sur les mots de passe</td>
    <td>En tant que propriétaire de compte, vous pouvez imposer des mots de passe plus sécurisés pour Cloud Directory en configurant un ensemble de règles auxquelles les mots de passe utilisateur doivent se conformer. Par exemple, ces règles incluent le nombre de tentatives de connexion avant verrouillage, les délais d'expiration, le délai minimum entre les mises à jour de mot de passe ou le nombre de fois avant lesquelles un mot de passe ne peut pas être répété. Pour obtenir la liste complète des options et des informations de configuration, voir [Advanced password management](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password).</td>
  </tr>
</table>

Par défaut, les fonctions de sécurité avancée sont désactivées. L'activation de l'authentification multi-facteur ou de la gestion des règles sur les mots de passe entraîne la facturation de frais supplémentaires. Si vous désactivez toutes les fonctions avancées, votre compte revient à la politique à moindre coût. Par exemple, si vous avez obtenu 10 000 jetons d'accès, puis vous avez activé la gestion des règles sur les mots de passe et obtenu 10 000 jetons supplémentaires, vous paierez pour 20 000 événements d'authentification et 10 000 événements de sécurité avancée.

Ces fonctions ne sont disponibles que pour les instances figurant sur le plan de tarification à tranches graduées et créées après le 15 mars 2018.
{: note}

### Utilisateurs autorisés
{: #faq-authorized}

Les utilisateurs autorisés sont des utilisateurs uniques qui se connectent à votre service, directement ou indirectement, notamment des utilisateurs anonymes. Vous êtes facturé pour un utilisateur autorisé à chaque fois qu'un nouvel utilisateur, y compris un utilisateur anonyme, se connecte à votre application. Par exemple, si un utilisateur se connecte avec son profil Facebook, puis plus tard avec son profil Google, il est pris en compte comme s'il s'agissait de deux utilisateurs autorisés distincts.

Pour les toutes dernières informations de tarification, vous pouvez créer une estimation de coût en cliquant sur **Ajouter à l'estimation** dans la section {{site.data.keyword.appid_short_notm}} du [catalogue {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/catalog/services/app-id).
{: tip}



## Pourquoi dois-je ajouter mon URI de redirection à la liste blanche ?
{: #faq-redirect}
{: faq}

Une URI de redirection est le noeud final de rappel de votre application. Pour empêcher les attaques par hameçonnage, {{site.data.keyword.appid_short_notm}} valide l'URI par rapport à la liste blanche des URI de redirection. En cas d'hameçonnage, il est possible qu'un pirate puisse accéder à vos jetons utilisateur. Pour plus d'informations sur les URI de redirection, voir [Ajout d'URI de redirection](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).

N'incluez pas de paramètres de demande dans votre URL. Ils sont ignorés lors du processus de validation. Exemple d'URL : `http://hôte:[port]/chemin`
{: tip}



## Fonctionnement du chiffrement dans {{site.data.keyword.appid_short_notm}}
{: #faq-encryption}
{: faq}

Consultez le tableau ci-dessous pour obtenir des réponses aux questions fréquemment posées sur le chiffrement.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Pourquoi utilisez-vous le chiffrement ?</td>
      <td>L'un des moyens de protéger les informations de nos utilisateurs consiste à chiffrer les données client inactives. Le service chiffre les données client inactives à l'aide de clés par titulaire.</td>
    </tr>
    <tr>
      <td>Avez-vous généré vos propres algorithmes ? Lesquels utilisez-vous dans votre code ?</td>
      <td>Nous n'avons pas généré nos propres algorithmes, mais le service utilise les algorithmes <code>AES</code> et <code>SHA-256</code> associés au salage.</td>
    </tr>
    <tr>
      <td>Utilisez-vous des fournisseurs ou des modules de chiffrement publics ou open source ? Vous arrive-t-il d'exposer les fonctions de chiffrement ? </td>
      <td>Le service utilise des bibliothèques Java <code>javax.crypto</code> mais n'expose jamais les fonctions de chiffrement.</td>
    </tr>
    <tr>
      <td>Comment stockez-vous les clés ?</td>
      <td>Les clés sont générées, chiffrées avec une clé principale spécifique à chaque région, puis stockées localement. Les clés principales sont stockées dans {{site.data.keyword.keymanagementserviceshort}}. Au niveau du stockage et du middleware, il existe un chiffrement de niveau de service qui signifie qu'il existe une clé unique pour tous les clients. Au niveau de l'application, chaque client dispose de sa propre clé de chiffrement.</td>
    </tr>
    <tr>
      <td>Quel niveau de chiffrement de la clé utilisez-vous ?</td>
      <td>Le service utilise un niveau de chiffrement de 16 octets.</td>
    </tr>
    <tr>
      <td>Appelez-vous des API distantes qui exposent les fonctions de chiffrement ?</td>
      <td>Non.</td>
    </tr>
  </tbody>
</table>

