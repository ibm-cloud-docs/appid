---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-13"

keywords: authentication, authorization, identity, app security, secure, access, platform, management, permissions

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


# Gestion de l'accès au service
{: #service-access-management}

Avec {{site.data.keyword.appid_full}} et {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), les propriétaires de compte peuvent gérer l'accès utilisateur depuis leur compte.
{: shortdesc}

En tant que propriétaire de compte, vous pouvez définir des règles sur votre compte afin de créer des niveaux d'accès différents en fonction des utilisateurs. Par exemple, certains utilisateurs peuvent avoir un accès en **lecture seule** à une instance et un accès en **écriture** à une autre. Vous pouvez choisir qui est autorisé à créer, mettre à jour et supprimer des instances d'{{site.data.keyword.appid_short_notm}}.

Pour plus d'informations sur IAM, voir [Accès à IAM](/docs/iam?topic=iam-userroles).

## Rôles utilisateur
{: #iam-roles}

La portée d'une règle d'accès est basée sur un rôle affecté à des utilisateurs.
{: shortdesc}

Les règles activent l'accès à accorder à différents niveaux. Certaines des options sont les suivantes :
<ul><ul>
  <li>Accès à l'ensemble des instances du service sur votre compte</li>
  <li>Accès à une instance individuelle du service sur votre compte</li>
  <li>Accès à une ressource spécifique dans une instance</li>
  <li>Accès à tous les services activés pour IAM sur votre compte</li>
</ul></ul>

### Rôles de plateforme
{: #iam-platform-roles}

Les rôles de gestion de plateforme permettent aux utilisateurs d'effectuer des tâches sur des ressources de service au niveau de la plateforme. Par exemple, des rôles peuvent être affectés afin de déterminer qui peut créer ou supprimer des ID, créer des instances, ou encore lier des instances aux applications. Le tableau ci-dessous détaille la corrélation des actions aux rôles de gestion de plateforme.

<table>
  <tr>
    <th>Rôle plateforme</th>
    <th>Droits</th>
    <th>Exemples d'action</th>
  </tr>
  <tr>
    <td><i>Afficheur</i></td>
    <td>Afficher des instances {{site.data.keyword.appid_short_notm}}.</td>
    <td>Vous pouvez afficher les données d'un utilisateur Cloud Directory ou la configuration du fournisseur d'identité.</td>
  </tr>
  <tr>
    <td><i>Editeur</i></td>
    <td>Afficher et lier des instances d'{{site.data.keyword.appid_short_notm}}.</td>
    <td>Vous pouvez lier des applications à une instance d'{{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><i>Opérateur</i></td>
    <td>Créer, supprimer, éditer, interrompre, reprendre, afficher ou lier des instances d'{{site.data.keyword.appid_short_notm}}.</td>
    <td>Vous pouvez créer ou supprimer une instance d'{{site.data.keyword.appid_short_notm}} du catalogue.</td>
  </tr>
  <tr>
    <td><i>Administrateur</i></td>
    <td>Toutes les actions de gestion pour tous les services du compte.</td>
    <td>Vous pouvez effectuer toutes les actions d'opérateur et vous avez la possibilité d'affecter des règles à d'autres utilisateurs.</td>
  </tr>
</table>

### Rôles d'accès au service
{: #iam-service-roles}
Le tableau ci-dessous détaille les actions qui sont mappées aux rôles d'accès de service. Les rôles d'accès de service permettent aux utilisateurs d'accéder à {{site.data.keyword.appid_short_notm}} et d'appeler l'API {{site.data.keyword.appid_short_notm}}.


<table>
  <tr>
    <th>Rôle de service</th>
    <th>Droits</th>
    <th>Exemples d'action</th>
  </tr>
  <tr>
    <td><i>Lecteur</i></td>
    <td>Afficher les données d'instance d'{{site.data.keyword.appid_short_notm}}.</td>
    <td>Peut afficher les détails de l'instance de service tels que les données utilisateur ou les informations de fournisseur d'identité.</td>
  </tr>
  <tr>
    <td> <i>Rédacteur ou gestionnaire</i></td>
    <td>Afficher et modifier une instance d'{{site.data.keyword.appid_short_notm}}.</td>
    <td>Peut effectuer toutes les actions de lecteur, comme l'édition de la configuration de fournisseur d'identité. </li></ul></td>
  </tr>
</table>

Pour plus d'informations sur l'affectation de rôles utilisateur dans l'interface utilisateur, voir [Gestion de l'accès à IAM](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).


## Règles d'accès {{site.data.keyword.appid_short_notm}}
{: #iam-access}

Une règle d'accès avec un rôle utilisateur IAM doit être affectée à chaque utilisateur disposant d'un accès au service {{site.data.keyword.appid_short_notm}} sur votre compte. Cette règle détermine les actions que l'utilisateur peut effectuer dans le contexte du service ou de l'instance que vous sélectionnez.
{: shortdesc}

Les actions sont personnalisées et définies par le service {{site.data.keyword.cloud_notm}} en tant qu'opérations dont l'exécution est autorisée dans le service. Les actions sont ensuite mappées à des rôles utilisateur IAM. Vous pouvez assurer le suivi de certaines des actions effectuées avec le service {{site.data.keyword.cloudaccesstrailshort}}. Dans le tableau ci-dessous, les actions et les droits requis pour {{site.data.keyword.appid_short_notm}} sont mappés.

<table>
  <tr>
    <th>Action</th>
    <th>Explication</th>
    <th>Rôle requis</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>Afficher les URL de redirection post-authentification.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>Ajouter ou mettre à jour des URL de redirection post-authentification.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>Mettre à jour votre configuration de fournisseur d'identité.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>Afficher votre configuration de fournisseur d'identité.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>Afficher sous forme de liste les événements d'authentification récents.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>Afficher la configuration du widget de connexion, par exemple le logo et les couleurs.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>Mettre à jour la configuration du widget de connexion.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>Afficher la configuration de profil utilisateur.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>Modifier la configuration de profil utilisateur.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>Afficher la configuration de profil utilisateur.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>Ajouter de nouveaux utilisateurs au répertoire cloud.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>Mettre à jour les détails d'un utilisateur du répertoire cloud.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>Supprimer un utilisateur du répertoire cloud.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>Afficher les modèles de courrier électronique du répertoire cloud.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>Mettre à jour le modèle de courrier électronique avec votre propre contenu.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>Supprimer un modèle de courrier électronique de répertoire cloud.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>Afficher les métadonnées du fournisseur de services SAML du répertoire cloud.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>Définir ou mettre à jour l'image dans le widget de connexion pour le fournisseur d'identité SAML.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>Envoyer à un utilisateur un courrier électronique basé sur un modèle.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>Afficher les détails de l'expéditeur du courrier électronique.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>Mettre à jour les détails de l'expéditeur.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>Révoquer le jeton d'actualisation d'un utilisateur avec son ID utilisateur.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
</table>

</br>

## Exemple : autoriser un autre utilisateur à accéder à une instance d'{{site.data.keyword.appid_short_notm}}
{: #iam-example}

Dans ce scénario, un administrateur a créé une instance d'{{site.data.keyword.appid_short_notm}} et a besoin d'accorder l'accès afficheur à un autre membre de l'équipe.
{: shortdesc}

Avant de commencer :

* Installez l'[interface CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli).

Pour mettre à jour les droits d'accès, vous devez procédez comme suit en tant qu'administrateur :

1. Connectez-vous à la console {{site.data.keyword.cloud_notm}}.

2. Accordez à l'employé l'accès afficheur en suivant les étapes présentées dans la [documentation IAM](/docs/iam?topic=iam-iammanidaccser).

3. Accédez à l'onglet **Données d'identification pour le service** du tableau de bord {{site.data.keyword.appid_short_notm}}. Cliquez sur **Afficher les données d'identification** et copiez l'URL **tentantID**.

4. Connectez-vous à l'interface de ligne de commande d'{{site.data.keyword.cloud_notm}} depuis votre terminal.

    ```
    ibmcloud login -api -a https://api.{region}.cloud.ibm.com
    ```
    {: codeblock}

    <table>
      <tr>
        <th>Région</th>
        <th>Noeud final</th>
      </tr>
      <tr>
        <td>Dallas</td>
        <td><code>us-south</code></td>
      </tr>
      <tr>
        <td>Francfort</td>
        <td><code>eu-de</code></td>
      </tr>
      <tr>
        <td>Sydney</td>
        <td><code>au-syd</code></td>
      </tr>
      <tr>
        <td>Londres</td>
        <td><code>eu-gb</code></td>
      </tr>
      <tr>
        <td>Tokyo</td>
        <td><code>jp-tok</code></td>
      </tr>
    </table>

5. Obtenez un jeton IAM et notez-le.

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

6. Vérifiez que le membre d'équipe ne peut pas effectuer de modification.

    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/config/idps/facebook'
    ```
    {: codeblock}

    Le résultat est un message 403 indiquant que l'utilisateur n'est pas autorisé.

Pour afficher la configuration d'{{site.data.keyword.appid_short_notm}} depuis l'interface de ligne de commande, en tant que membre de l'équipe, vous devez procéder comme suit :

1. Connectez-vous depuis l'interface de ligne de commande d'{{site.data.keyword.cloud_notm}} dans votre terminal.

    ```
    ibmcloud login -a api.<region>.console.cloud.ibm.com
    ```
    {: codeblock}

2. Obtenez un jeton IAM et notez-le.

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

3. Affichez la configuration de fournisseur d'identité pour Facebook en utilisant cURL.

    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/facebook'
    ```
    {: codeblock}

    Le résultat est un message 200 qui contient les informations de fournisseur d'identité.
