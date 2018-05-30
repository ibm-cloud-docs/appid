---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Gestion de l'accès au service
{: #service-access-management}

Avec {{site.data.keyword.appid_full}} et {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM), les propriétaires de compte peuvent gérer l'accès utilisateur depuis leur compte.
{: shortdesc}

En tant que propriétaire de compte, vous pouvez définir des règles au sein de votre compte afin de créer des niveaux d'accès différents en fonction des utilisateurs. Par exemple, certains utilisateurs peuvent avoir un accès à une instance en **Lecture seule** mais un accès en **Ecriture** à un autre. Vous pouvez choisir qui est autorisé à créer, mettre à jour et supprimer des instances d'{{site.data.keyword.appid_short_notm}}.

Pour plus d'informations sur IAM, voir [Accès à IAM](/docs/iam/users_roles.html).

## Rôles utilisateur
{: #roles}

La portée d'une politique d'accès est basée sur un rôle affecté à des utilisateurs.
{: shortdesc}

Les politiques activent l'accès à accorder à différents niveaux. Certaines des options sont les suivantes :
<ul><ul>
  <li>Accès à l'ensemble des instances du service dans votre compte</li>
  <li>Accès à une instance individuelle du service dans votre compte</li>
  <li>Accès à une ressource spécifique au sein d'une instance</li>
  <li>Accès à tous les services activés pour IAM dans votre compte</li>
</ul></ul>

Les rôles de gestion de plateforme permettent aux utilisateurs d'effectuer des tâches sur des ressources de service au niveau plateforme. Des rôles peuvent, par exemple, être affectés afin de déterminer qui peut créer ou supprimer des ID, créer des instances, ou encore lier des instances aux applications. Le tableau suivant détaille les actions corrélées aux rôles de gestion de plateforme.

<table>
  <tr>
    <th>Rôle plateforme</th>
    <th>Droits</th>
    <th>Exemples d'action</th>
  </tr>
  <tr>
    <td><i>Afficheur</i></td>
    <td>Afficher des instances {{site.data.keyword.appid_short_notm}}.</td>
    <td>Vous pouvez voir les données d'un utilisateur Cloud Directory (Répertoire cloud) ou la configuration du fournisseur d'identité.</td>
  </tr>
  <tr>
    <td><i>Editeur</i></td>
    <td>Afficher et lier des instances {{site.data.keyword.appid_short_notm}}.</td>
    <td>Vous pouvez lier des applications à une instance d'{{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><i>Opérateur</i></td>
    <td>Créer, supprimer, éditer, interrompre, reprendre, afficher ou lier des instances {{site.data.keyword.appid_short_notm}}.</td>
    <td>Vous pouvez créer ou supprimer une instance {{site.data.keyword.appid_short_notm}} du catalogue.</td>
  </tr>
  <tr>
    <td><i>Administrateur</i></td>
    <td>Toutes les actions de gestion pour tous les services du compte.</td>
    <td>Vous pouvez effectuer toutes les actions d'opérateur et vous avez la possibilité d'affecter des politiques à d'autres utilisateurs.</td>
  </tr>
</table>

</br>
</br>
Le tableau suivant détaille les actions mappées aux rôles d'accès de service. Les rôles d'accès de service permet aux utilisateurs d'accéder à {{site.data.keyword.appid_short_notm}}, ainsi que la possibilité d'appeler l'API {{site.data.keyword.appid_short_notm}}.


<table>
  <tr>
    <th>Rôle de service</th>
    <th>Droits</th>
    <th>Exemples d'action</th>
  </tr>
  <tr>
    <td><i>Lecteur</i></td>
    <td>Afficher les données d'instance {{site.data.keyword.appid_short_notm}}.</td>
    <td>Peut afficher les détails de l'instance de service tels que les données utilisateur ou les informations de fournisseur d'identité.</td>
  </tr>
  <tr>
    <td> <i>Rédacteur ou gestionnaire</i></td>
    <td>Afficher et modifier une instance {{site.data.keyword.appid_short_notm}}.</td>
    <td>Peut effectuer toutes les actions de lecteur, comme l'édition de la configuration de fournisseur d'identité.</li></ul></td>
  </tr>
</table>

Pour plus d'informations sur l'affectation de rôles utilisateur dans l'interface utilisateur, voir [Gestion de l'accès à IAM](/docs/iam/mngiam.html#iammanidaccser).

## Règles d'accès {{site.data.keyword.appid_short_notm}}
{: #access}

Une règle d'accès avec un rôle utilisateur IAM doit être affectée à chaque utilisateur disposant d'un accès au service {{site.data.keyword.appid_short_notm}} de votre compte. Cette règle détermine les actions que l'utilisateur peut effectuer dans le contexte du service ou de l'instance que vous sélectionnez.
{: shortdesc}

Les actions sont personnalisées et définies par le service {{site.data.keyword.Bluemix_notm}} en tant qu'opérations dont l'exécution est autorisée dans le service. Les actions sont ensuite mappées à des rôles utilisateur IAM. Pour {{site.data.keyword.appid_short_notm}}, les actions suivantes existent :

<table>
  <tr>
    <th>Commande</th>
    <th>Explication </th>
    <th>Rôle</th>
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
    <td>Afficher votre configuration du fournisseur d'identité.</td>
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
    <td>Afficher les modèles d'e-mail du répertoire cloud.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>Mettre à jour le modèle d'e-mail avec votre propre contenu.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>Supprimer un modèle d'e-mail de répertoire cloud.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>Envoyer à un utilisateur un e-mail basé sur un modèle.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>Afficher les détails de l'expéditeur de l'e-mail.</td>
    <td>Lecteur, rédacteur, gestionnaire</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>Mettre à jour les détails de l'expéditeur.</td>
    <td>Rédacteur, gestionnaire</td>
  </tr>
</table>




## Exemple : Donner à un autre utilisateur l'accès à une instance d'{{site.data.keyword.appid_short_notm}}
{: #example}

Dans ce scénario, un administrateur a créé une instance d'{{site.data.keyword.appid_short_notm}} et a besoin d'accorder l'accès afficheur à un autre membre d'équipe.
{: shortdesc}

Avant de commencer :
* Installez l'interface de ligne de commande [{{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/get_started.html).

Pour mettre à jour les droits d'accès, l'administrateur exécute la procédure suivante :

1. Connectez-vous à la console {{site.data.keyword.Bluemix_notm}}.
2. Donnez à l'employé l'accès afficheur en suivant les étapes exposées dans la [documentation IAM](/docs/iam/iamusermanage.html#iamusermanage).
3. Accédez à l'onglet **Données d'identification du service** du tableau de bord {{site.data.keyword.appid_short_notm}}. Cliquez sur **Afficher les données d'identification** et copiez l'URL **tentantID**.
4. Connectez-vous à l'interface CLI {{site.data.keyword.Bluemix_notm}} depuis votre terminal.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. Obtenez un jeton IAM et notez-le.
    ```
    bx iam oauth-tokens
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
    'https://appid-management.stage1.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    Le résultat est un message de type 403 (non autorisé).

Pour afficher la configuration {{site.data.keyword.appid_short_notm}} depuis l'interface CLI, le membre d'équipe doit exécuter la procédure suivante :

1. A l'aide de l'interface CLI {{site.data.keyword.Bluemix_notm}}, connectez-vous sur votre terminal.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. Obtenez un jeton IAM et notez-le.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. Affichez la configuration de fournisseur d'identité pour Facebook en utilisant cURL.
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    Le résultat est un message 200 qui contient les informations de fournisseur d'identité.
