---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-09"

keywords: authentication, authorization, identity, app security, secure, development, sso, directory, users, registry, multiple apps

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


# Connexion unique
{: #cd-sso}

Avec la connexion unique pour Cloud Directory, vous pouvez offrir une expérience d'authentification fluide entre plusieurs applications Web. Si la connexion unique est activée lorsqu'un utilisateur se connecte pour la première fois, il n'aura pas à entrer de nouveau ses données d'identification à sa prochaine connexion. Il sera automatiquement connecté à toutes les applications protégées par la même instance {{site.data.keyword.appid_short_notm}}.


## Fonctionnement
{: #cd-sso-how-it-works}

Examinez le diagramme suivant pour voir comment fonctionne la connexion unique.

![Diagramme de connexion unique](images/sso.png)

1. Un utilisateur Cloud Directory se connecte à votre application pour la première fois.
2. Il est invité à s'authentifier en fournissant un nom d'utilisateur ou une adresse de courrier électronique et un mot de passe.
3. Si les données d'identification sont valides, l'utilisateur est connecté à votre application. En parallèle, {{site.data.keyword.appid_short_notm}} crée une session et définit un cookie sur le navigateur de l'utilisateur.
4. Si un utilisateur tente de se connecter à l'une de vos autres applications, {{site.data.keyword.appid_short_notm}} détecte le cookie de session et connecte automatiquement l'utilisateur à votre application. Les cookies de session {{site.data.keyword.appid_short_notm}} sont propres à une instance et signés à l'aide de la clé privée unique de l'instance.

Si votre instance est configurée de manière à utiliser, en plus de Cloud Directory, des fournisseurs d'identité tels que SAML ou Facebook, le widget de connexion est toujours affiché. Les utilisateurs sont invités à entrer leurs données d'identification Cloud Directory ou à sélectionner l'un des autres fournisseurs, même s'ils disposent d'une session de connexion unique valide.
{: note}


## Configuration de la connexion unique
{: #cd-sso-configure}

Vous pouvez configurer la connexion unique à l'aide du tableau de bord {{site.data.keyword.appid_short_notm}} ou des API.
{: shortdesc}


### Avec l'interface graphique
{: #cd-sso-configure-gui}


Vous pouvez configure la connexion unique via l'interface graphique.

1. Accédez à l'onglet **Cloud Directory > Connexion unique** du tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Dans la zone **Activer la connexion unique** basculez Connexion unique sur **Activé**.

3. Définissez la durée d'inaction dont dispose un utilisateur avant expiration de la session de connexion unique. Lorsqu'elle expire, l'utilisateur doit se reconnecter. La durée est indiquée en minutes et le temps d'inactivité maximum autorisé est de 10 080 minutes (soit 7 jours). La durée par défaut est de 1440 minutes ce qui équivaut à 1 jour.

4. Ajoutez vos URI de redirection dans la zone **URI de redirection après déconnexion**, puis cliquez sur le signe **+**. Veillez à n'enregistrer que des applications en lesquelles vous avez confiance. En enregistrant l'URI, vous autoriser {{site.data.keyword.appid_short_notm}} à l'inclure dans le flux de travaux d'autorisation.

5. Cliquez sur **Sauvegarder**.



### Avec l'API
{: #cd-sso-configure-api}

Vous pouvez activer la fonction en utilisant l'API admin de configuration de la connexion unique pour définir trois paramètres.

Exemple d'appel :

```json
{
  "isActive": true,
  "inactivityTimeoutSeconds": 86400,
  "logoutRedirectUris": [
    "http://my-first-app.com/after_logout",
    "http://my-second-app.com/after_logout"
  ]
}
```
{: screen}

<table>
  <tr>
    <th>Paramètre</th>
    <th>Définition</th>
  </tr>
  <tr>
    <td><code>isActive</code></td>
    <td>Pour activer la connexion unique, définissez cette valeur sur <code>true</code>. Le paramétrage par défaut est <code>false</code>.</td>
  </tr>
  <tr>
    <td><code>inactivityTimeoutSeconds</code></td>
    <td>Durée maximale d'activité accordée à l'utilisateur avant que celui-ci soit obligé d'entrer de nouveau ses données d'identification. Cette valeur est indiquée en secondes avec un maximum de <code>604800 secondes</code> (7 jours). Le paramétrage par défaut est <code>86400 secondes</code> (1 jour).</td>
  </tr>
  <tr>
    <td><code>logoutRedirectUris</code></td>
    <td>Liste des URI autorisés, séparés par des virgules, vers lesquels {{site.data.keyword.appid_short_notm}} peut rediriger vos utilisateurs une fois qu'ils sont connectés.</td>
  </tr>
</table>



## Configuration de la déconnexion
{: #cd-sso-log-out}

Avec {{site.data.keyword.appid_short_notm}} vous pouvez mettre fin à la session de connexion unique d'un utilisateur pour son navigateur en cours. Si le noeud final d'API est accédé par le navigateur de l'utilisateur, la session est interrompue et l'utilisateur est invité à entrer ses données d'identification lors de sa prochaine tentative de connexion dans ce navigateur, et ce pour toutes vos applications.
{: shortdesc}


Lorsqu'un flux de travail de changement, réinitialisation ou renouvellement de mot de passe est lancé, les sessions de tous les clients sont automatiquement interrompues pour l'utilisateur.
{: note}


### Avec l'API
{: #cd-sso-log-out-api}

Pour déconnecter un utilisateur, redirigez son navigateur en utilisant vos informations pour effectuer l'appel d'API suivant.

```
https://<region>.appid.cloud.ibm.com/oauth/v4/<tenant-id>/cloud_directory/sso/logout?redirect_uri=<redirect_uri>&client_id=<clientId>
```
{: codeblock}

<table>
  <tr>
    <th>Variable</th>
    <th>Valeur</th>
  </tr>
  <tr>
    <td><code>Région</code></td>
    <td>Région dans laquelle votre instance {{site.data.keyword.appid_short_notm}} est mise à disposition. Les options incluent <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> et <code>us-south</code>.</td>
  </tr>
  <tr>
    <td><code>tenant-id</code></td>
    <td>Identificateur unique de votre instance {{site.data.keyword.appid_short_notm}}. Cette valeur figure dans l'onglet <em>Données d'identification pour le service</em> du tableau de bord {{site.data.keyword.appid_short_notm}}. Si vous ne disposez pas d'un ensemble de données d'identification du service, vous pouvez en créer un et en extraire la valeur.</td>
  </tr>
  <tr>
    <td><code>redirect_uri</code></td>
    <td>URI indiqué dans votre configuration de connexion unique via le tableau de bord {{site.data.keyword.appid_short_notm}}. Pour des raisons de sécurité, si vous n'indiquez pas de valeur, la redirection ne peut pas s'effectuer et une erreur est signalée.</td>
  </tr>
</table>

Même si la session de connexion unique est interrompue, un utilisateur qui dispose d'un jeton d'accès valide stocké dans sa session peut ne pas avoir à entrer de nouveau ses données d'identification tant que son jeton n'a pas expiré. Par défaut, le jeton expire au bout d'une heure.
{: note}


### Accès avec le logiciel SDK de serveur Node.JS
{: #cd-sso-log-out-nodejs}

Vous pouvez également utiliser le logiciel SDK de serveur Node.js {{site.data.keyword.appid_short_notm}} pour gérer automatiquement la redirection.

Exemple :

```javascript
app.get('/logoutSSO', (req, res) => {
  res.clearCookie("refreshToken");
  webAppStrategy.logoutSSO(req,res, { "redirect_uri": "https://my-app.com/after_logout" });
  });
```
{: screen}


## Fin de toutes les sessions d'un utilisateur
{: cd-sso-ending-all-sessions}

En tant qu'administrateur, vous pouvez mettre fin à toutes les sessions de connexion unique de n'importe quel utilisateur à l'aide des API admin d'{{site.data.keyword.appid_short_notm}}. Les API sont protégées par un jeton IAM de cloud.

Exemple de demande d'API :

```
POST https://<region>.appid.cloud.ibm.com/management/v4/{tenant-id}/cloud_directory/Users/{user-id}/sso/logout
Headers:
Authorization: <IAM TOKEN>
```
{: codeblock}

<table>
  <tr>
    <th>Variable</th>
    <th>Valeur</th>
  </tr>
  <tr>
    <td><code>Région</code></td>
    <td>Région dans laquelle votre instance {{site.data.keyword.appid_short_notm}} est mise à disposition. Les options incluent <code>us-south</code>, <code>eu-gb</code> et <code>eu-de</code>.</td>
  </tr>
  <tr>
    <td><code>tenant-id</code></td>
    <td>Identificateur unique de votre instance {{site.data.keyword.appid_short_notm}}. Cette valeur figure dans l'onglet <em>Données d'identification pour le service</em> du tableau de bord {{site.data.keyword.appid_short_notm}}. Si vous ne disposez pas d'un ensemble de données d'identification du service, vous pouvez en créer un et en extraire la valeur.</td>
  </tr>
  <tr>
    <td><code>user-id</code></td>
    <td>Identificateur unique d'un utilisateur Cloud Directory. Vous pouvez obtenir cet identificateur à l'aide des [API utilisateur Cloud Directory](https://us-south.appid.cloud.ibm.com/swagger-ui/#/) ou en affichant le jeton d'identité de l'utilisateur.</td>
  </tr>
</table>

Lorsque vous appelez cette API, toutes les sessions de connexion unique de l'utilisateur spécifié sont invalidées. Cela signifie que la prochaine fois que l'utilisateur tente de se connecter à l'une de vos applications, à partir de n'importe quel navigateur ou appareil, il est invité à entrer de nouveau ses données d'identification.

