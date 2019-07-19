---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: Authentication, authorization, identity, app security, secure, application identity, app to app, access token, activity

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


# Evénements {{site.data.keyword.cloudaccesstrailshort}}
{: #at-events}

Vous pouvez afficher, gérer et analyser les activités initiées par l'utilisateur et effectuées dans votre instance de service {{site.data.keyword.appid_full}} en utilisant le service {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}





Pour plus d'informations sur le fonctionnement de ce service, voir la [documentation {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started).






## Affichage des événements d'administration
{: #at-monitor-admin}

Vous pouvez afficher, gérer et analyser l'activité de configuration effectuée dans votre instance d'{{site.data.keyword.appid_short_notm}} à l'aide du service {{site.data.keyword.at_short}}.
{: shortdesc}

Pour surveiller l'activité d'administration :

1. Connectez-vous à votre compte {{site.data.keyword.cloud_notm}}.
2. Depuis le catalogue, mettez à disposition une instance du service {{site.data.keyword.cloudaccesstrailshort}} sur le même compte que votre instance d'{{site.data.keyword.appid_short_notm}}.
3. Dans le tableau de bord {{site.data.keyword.cloudaccesstrailshort}}, cliquez sur l'onglet **Gérer**.
4. Dans la liste déroulante, effectuez les configurations suivantes afin de rechercher des événements qui sont générés par {{site.data.keyword.appid_short_notm}} :
    * Pour **Afficher les journaux**, sélectionnez **Journaux de compte**.
    * Pour **Rechercher**, sélectionnez **target.Management**.
    * Pour **Filtrer**, entrez `appid`.
5. Cliquez sur **Filtrer**.

</br>

## Liste des événements d'administration
{: #at-events-admin}

Consultez le tableau ci-dessous pour la liste des événements qui sont envoyés à {{site.data.cloudaccesstrailshort}}.

<table>
  <tr>
    <th>Action</th>
    <th>Description</th>
    <th>Emplacement dans l'interface utilisateur</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>Afficher l'activité récente.</td>
    <td>Disponible dans la boîte <strong>Journal d'activité</strong> de l'onglet <strong>Présentation</strong>.</td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>Afficher la configuration de fournisseur d'identité.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Gérer</strong>.</td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>Mettre à jour la configuration de fournisseur d'identité.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Gérer</strong>.</td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>Afficher la configuration de l'expiration de jeton.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Expiration du jeton</strong>.</td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>Afficher la configuration de stockage de profil utilisateur.</td>
    <td>Disponible dans la boîte <strong>Journal d'activité</strong> de l'onglet <strong>Présentation</strong>.</td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>Mettre à jour la configuration de stockage de profil utilisateur.</td>
    <td>Disponible dans l'onglet <strong>Profils</strong>.</td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>Afficher la couleur de thème de l'en-tête du widget de connexion.</td>
    <td>Disponible dans l'onglet <strong>Personnalisation de la connexion</strong>.</td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>Mettre à jour la couleur de thème de l'en-tête du widget de connexion.</td>
    <td>Disponible dans l'onglet <strong>Personnalisation de la connexion</strong>.</td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>Afficher l'image affichée dans le widget de connexion.</td>
    <td>Disponible dans l'onglet <strong>Personnalisation de la connexion</strong>.</td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>Mettre à jour l'image affichée dans le widget de connexion.</td>
    <td>Disponible dans l'onglet <strong>Personnalisation de la connexion</strong>.</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>Afficher la configuration de l'interface utilisateur du widget de connexion, qui comprend la couleur de l'en-tête et l'image.</td>
    <td>Disponible dans l'onglet <strong>Personnalisation de la connexion</strong>.</td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>Afficher la liste des langues prises en charge.</td>
    <td>Doit être affichée depuis l'API.</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>Mettre à jour la liste des langues prises en charge.</td>
    <td>Doit être mise à jour depuis l'API.</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>Afficher les métadonnées SAML d'{{site.data.keyword.appid_short_notm}}.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > SAML 2.0 Federation</strong>.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>Afficher un utilisateur du Cloud Directory.</td>
    <td>Disponible dans l'onglet <strong>Utilisateurs</strong>.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>Mettre à jour un utilisateur Cloud Directory.</td>
    <td>Disponible dans l'onglet <strong>Utilisateurs</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>Supprimer un utilisateur Cloud Directory.</td>
    <td>Disponible dans l'onglet <strong>Utilisateurs</strong>.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>Afficher la liste de vos utilisateurs Cloud Directory.</td>
    <td>Disponible dans l'onglet <strong>Utilisateurs</strong>.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>Mettre à jour la liste de vos utilisateurs Cloud Directory.</td>
    <td>Disponible dans l'onglet <strong>Utilisateurs</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>Supprimer la liste des utilisateurs Cloud Directory.</td>
    <td>Disponible dans l'onglet <strong>Utilisateurs</strong>.</td>
  </tr>
  <tr>
    <td><code>read.emailTemplate</code></td>
    <td>Afficher un modèle de courrier électronique.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Modèles</strong>.</td>
  </tr>
  <tr>
    <td><code>update.emailTemplate</code></td>
    <td>Mettre à jour un modèle de courrier électronique.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Modèles</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.emailTemplate</code></td>
    <td>Supprimer un modèle de courrier électronique pour réinitialiser les valeurs par défaut.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Modèles</strong>.</td>
  </tr>
  <tr>
    <td><code>read.senderDetails</code></td>
    <td>Afficher les détails de l'expéditeur.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Paramètres</strong>.</td>
  </tr>
  <tr>
    <td><code>update.senderDetails</code></td>
    <td>Mettre à jour les détails de l'expéditeur.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Paramètres</strong>.</td>
  </tr>
  <tr>
    <td><code>update.resendNotification</code></td>
    <td>Renvoyer des notifications d'utilisateur.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Paramètres</strong>.</td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>Mettre à jour le processus en cas d'oubli du mot de passe.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Paramètres</strong>.</td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>Afficher le résultat de la confirmation d'oubli du mot de passe.</td>
    <td>Doit être effectuée via l'API.</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>Mettre à jour le processus d'inscription.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Paramètres</strong>.</td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>Afficher la confirmation du résultat de l'inscription.</td>
    <td>Doit être effectuée via l'API.</td>
  </tr>
  <tr>
    <td><code>read.action_url</code></td>
    <td>Afficher l'URL personnalisée qui est appelée lorsqu'une action est effectuée.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Pages d'arrivée personnalisées</strong>.</td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>Mettre à jour l'URL personnalisée qui est appelée lorsqu'une action est effectuée.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Paramètres</strong>.</td>
  </tr>
  <tr>
    <td><code>update.changePassword</code></td>
    <td>Changer le mot de passe de l'utilisateur Cloud Directory.</td>
    <td>Disponible dans l'onglet <strong>Fournisseurs d'identité > Cloud Directory > Paramètres</strong>.</td>
  </tr>
  <tr>
    <td><code>read.loginWidgetConfig</code></td>
    <td>Afficher votre configuration de widget de connexion.</td>
    <td>Disponible dans l'onglet <strong>Personnalisation de la connexion</strong>.</td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>Mettre à jour votre configuration de widget de connexion.</td>
    <td>Disponible dans l'onglet <strong>Personnalisation de la connexion</strong>.</td>
  </tr>
</table>



