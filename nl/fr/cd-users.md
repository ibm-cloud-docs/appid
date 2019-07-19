---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# Gestion des utilisateurs
{: #cd-users}

Avec Cloud Directory, vous pouvez gérer vos utilisateurs dans un registre évolutif en utilisant des fonctionnalités pré-installées qui améliorent la sécurité et le libre-service.
{: shortdesc}

Un utilisateur Cloud Directory n'est pas un utilisateur {{site.data.keyword.appid_short_notm}}. Les utilisateurs peuvent s'inscrire dans votre application en utilisant les différentes options de fournisseur d'identité que vous avez configurées, ou vous pouvez les ajouter à votre répertoire. Les utilisateurs mentionnés sur cette page sont ceux qui sont associés à Cloud Directory en tant que fournisseur d'identité.
{: note}

## Affichage des informations utilisateur
{: #cd-user-info}

Vous pouvez voir toutes les informations connues sur tous les utilisateurs de Cloud Directory sous forme d'objet JSON à l'aide des API ou du tableau de bord. 
{: shortdesc}


### Avec l'interface graphique

Vous pouvez utiliser le tableau de bord {{site.data.keyword.appid_short_notm}} pour afficher les détails sur les utilisateurs de votre application. 

1. Accédez à l'onglet **Cloud Directory > Utilisateurs ** de votre instance {{site.data.keyword.appid_short_notm}}.

2. Parcourez le tableau ou effectuez une recherche à l'aide d'une adresse e-mail pour trouver l'utilisateur dont vous voulez afficher les informations.

3. Dans le menu déroulant dynamique de la ligne de l'utilisateur, cliquez sur **Afficher les détails de l'utilisateur**. Une page contenant les informations de l'utilisateur s'ouvre. Consultez le tableau suivant pour voir quelles informations vous pouvez voir.

<table>
  <tr>
    <th colspan="2">Détails de l'utilisateur</th>
  </tr>
  <tr>
    <td>ID utilisateur</td>
    <td>L'ID utilisateur dépend du type d'inscription utilisateur que vous avez configuré. Si vous avez configuré un flux adresse e-mail/mot de passe, l'identifiant est l'adresse e-mail de l'utilisateur. Si vous utilisez le flux nom d'utilisateur/mot de passe, l'identifiant est le nom d'utilisateur qui est fourni lors de l'inscription.</td>
  </tr>
  <tr>
    <td>E-mail</td>
    <td>Adresse e-mail principale qui est associée à l'utilisateur.</td>
  </tr>
    <tr>
    <td>Prénom et nom de famille</td>
    <td>Prénom et nom de famille de l'utilisateur, tels qu'ils ont été fournis lors de la procédure d'inscription.</td>
  </tr>
  <tr>
    <td>Dernière connexion</td>
    <td>Horodatage de la dernière fois que l'utilisateur s'est connecté à votre application. Remarque : si vous avez ajouté votre utilisateur via le tableau de bord, les informations de connexion sont vides jusqu'à ce que l'utilisateur se connecte lui-même dans votre application. Lors de la connexion, il devient également un utilisateur App ID.</td>
  </tr>
  <tr>
    <td>ID</td>
    <td>ID attribué à l'utilisateur par {{site.data.keyword.appid_short_notm}}. Dans l'interface utilisateur, il n'est pas affiché mais vous pouvez copier la valeur et la coller dans un éditeur de texte pour la voir.</td>
  </tr>
  <tr>
    <td>Attributs prédéfinis</td>
    <td>Les attributs prédéfinis sont les choses qui sont connues d'un utilisateur grâce à SCIM.</td>
  </tr>
  <tr>
    <td>Attributs personnalisés</td>
    <td>Les attributs personnalisés sont des informations supplémentaires qui sont ajoutées à leur profil ou qui sont apprises sur les utilisateurs lorsqu'ils interagissent avec votre application.</td>
  </tr>
  <tr>
    <td>Récapitulatif</td>
    <td>Tous les attributs sont compilés pour former un profil qui vous donne un aperçu complet de votre utilisateur Cloud Directory. Pour plus d'informations, voir [Profils d'utilisateurs](/docs/services/appid?topic=appid-profiles).</td>
  </tr>
</table>

</br>

### Avec l'API

Vous pouvez utiliser l'API {{site.data.keyword.appid_short_notm}} pour afficher les détails sur les utilisateurs de votre application. 

1. Obtenez votre ID titulaire depuis votre instance du service.

2. Recherchez vos utilisateurs App ID à l'aide d'une requête d'identification, telle qu'une adresse e-mail, pour trouver l'ID d'utilisateur.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users?query={identifying-search-query}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  Exemple :

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@email.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. En utilisant l'ID que vous avez obtenu à l'étape précédente, envoyez une demande GET au noeud final `cloud_directory/users` pour voir le profil d'utilisateur complet.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-ID}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  Exemple de réponse :

  ```
  {
    sub: "c155c0ff-337a-46d3-a22a-a8f2cca08995",
    name: "Test User",
    email: "testuser@test.com",
    identities: [
      {
        provider: "cloud_directory",
        id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
        idpUserInfo: {
          displayName: "Test User",
          active: true,
          mfaContext: {},
          emails: [
            {
              value: "testuser@test.com",
              primary: true
            }
          ],
          meta: {
            lastLogin: "2019-05-20T16:33:20.699Z",
            created: "2019-05-20T16:25:13.019Z",
            location: "/v1/6b8ab644-1d4a-4b3e-bcd9-777ba8430a51/Users/f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            lastModified: "2019-05-20T16:33:20.707Z",
            resourceType: "User"
          },
          scemas: [
            "urn:ietf:params:scim:schemas:core:2.0:User"
          ],
          name: {
            givenName: "Test",
            familyName: "User",
            formatted: "Test User"
            },
          id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
          status: "CONFIRMED",
          idpType: "cloud_directory"
        }
      }
    ]
  }
  ```
  {: screen}

  Pour afficher l'ensemble complet des données utilisateur qu'{{site.data.keyword.appid_short_notm}} prend en charge, voir le [schéma principal SCIM](https://tools.ietf.org/html/rfc7643#section-8.2).
  {: tip}


## Ajout et suppression d'utilisateurs
{: #add-delete-users}

Vous pouvez gérer vos utilisateurs Cloud Directory via le tableau de bord {{site.data.keyword.appid_short_notm}} ou à l'aide des API.
{: shortdesc}

Lorsqu'un utilisateur s'inscrit dans votre application, il le fait par le biais d'un flux de travail de libre-service qui déclenche automatiquement des courriers électroniques tels qu'une demande de bienvenue ou de vérification. Lorsque vous, en tant qu'administrateur, ajoutez un utilisateur à votre application, aucun flux de libre-service n'est lancé, ce qui signifie que les utilisateurs ne reçoivent pas de courrier électronique de votre application. Si vous voulez que vos utilisateurs soient toujours avertis de leur ajout, vous pouvez déclencher les flux de messagerie par le biais de l'[API de gestion App ID](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher).


### Ajout d'utilisateurs
{: #add-users}

Lorsqu'un utilisateur s'inscrit dans votre application, il est ajouté en tant qu'utilisateur. A des fins de test, vous pouvez ajouter un utilisateur via le tableau de bord {{site.data.keyword.appid_short_notm}} ou via l'API.

Si vous désactivez l'inscription en libre-service ou si vous ajoutez un utilisateur en son nom, l'utilisateur ne reçoit pas d'e-mail de bienvenue ou de vérification lorsqu'il est ajouté.
{: tip}



**Pour ajouter un utilisateur via l'interface graphique :**

1. Accédez à l'onglet **Cloud Directory > Utilisateurs** du tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Cliquez sur **Ajouter un utilisateur**. Un formulaire s'affiche.

3. Entrez les données suivantes : **Prénom**, **Nom**, **Adresse électronique** et **Mot de passe**. Vérifiez que l'adresse électronique que vous voulez enregistrer n'est pas déjà utilisée par un autre utilisateur. Pour vous assurer que vous avez correctement entré votre mot de passe, saisissez-le dans la zone **Confirmer le mot de passe**.

4. Cliquez sur **Sauvegarder**. Un utilisateur Cloud Directory est créé.

</br>


**Pour ajouter un utilisateur via l'API :**

Le flux suivant montre comment ajouter un utilisateur avec une adresse e-mail et un mot de passe. Vous pouvez également choisir d'utiliser un flux nom d'utilisateur/mot de passe.

1. Obtenez votre ID titulaire (`tenantID`) à partir de vos données d'identification de service ou d'application.

2. Obtenez un jeton IAM {{site.data.keyword.cloud_notm}}.

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. Avec le jeton que vous avez obtenu à l'étape 2, envoyez une demande POST au noeud final `cloud-directory/users`. Cet exemple utilise le flux adresse e-mail/mot de passe. Vous pouvez également utiliser le flux nom d'utilisateur/mot de passe.

  ```
  curl --X POST "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users"
  -H "accept: application/json"
  -H "content-type: application/json"
  -H "authorization: Bearer {token}"
  -d {
    "displayName": "Test User",
    "password": "{App-ID-Cloud-Directory-User-Password}",
    "active": true,
    "emails": [
      {
        "value": "{App-ID-Cloud-Directory-User-Email}",
        "primary": true
      }
    ]
  }
  ```
  {: codeblock}

</br>


### Suppression d'utilisateurs
{: #delete-users}

Si vous voulez supprimer un utilisateur de votre répertoire, vous pouvez le supprimer de l'interface graphique ou à l'aide des API.
{: shortdesc}

**Pour supprimer un utilisateur via l'interface graphique :**

1. Accédez à l'onglet **Cloud Directory > Utilisateurs** du tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Cochez la case en regard de l'utilisateur à supprimer. Une boîte de dialogue s'affiche.

3. Dans la boîte de dialogue, cliquez sur **Supprimer**. Un écran s'ouvre.

4. Confirmez que vous avez compris que la suppression d'un utilisateur ne peut pas être annulée en cliquant sur **Supprimer**. Si l'action était une erreur, vous pouvez ajouter de nouveau l'utilisateur à votre répertoire, mais toutes les informations le concernant ne sont plus disponibles.

</br>

**Pour supprimer un utilisateur à l'aide de l'API :**

1. Obtenez votre ID titulaire.

2. A l'aide de l'adresse e-mail qui est associée à l'utilisateur, recherchez l'ID de l'utilisateur dans votre répertoire.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users?email={user-email}" -H "accept: application/json"
  ```
  {: codeblock}

3. Supprimez l'utilisateur.

  ```
  curl --X DELETE "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-GUID}"
  -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}



## Migration des utilisateurs
{: #user-migration}

Vous aurez parfois besoin d'ajouter une instance d'{{site.data.keyword.appid_short_notm}}. Lorsque vous utilisez Cloud Directory, vos utilisateurs doivent être migrés vers la nouvelle instance. Pour faciliter cette migration, vous pouvez utiliser les API de gestion.
{: shortdesc}


Vous devez avoir le [rôle IAM](/docs/iam?topic=iam-getstarted#getstarted) `Responsable` pour les deux instances {{site.data.keyword.appid_short_notm}}.
{: note}


### Exportation
{: cd-export}

Pour pouvoir ajouter vos utilisateurs à la nouvelle instance, vous devez les exporter à partir de votre instance actuelle. Pour ce faire, vous pouvez utiliser l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">API de gestion des exportations <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

Exemple de commande cURL :

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>Variable</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>Chaîne personnalisée utilisée pour chiffrer et déchiffrer le mot de passe haché d'un utilisateur.</td>
  </tr>
  <tr>
    <td><code> tenantID </code></td>
    <td>ID titulaire du service qui se trouve dans vos données d'identification du service. Vos données d'identification du service sont disponibles dans le tableau de bord {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
</table>

Seuls vos utilisateurs de Cloud Directory et leurs profils sont renvoyés. Les utilisateurs d'autres fournisseurs d'identité ne le sont pas.
{: note}


### Importation
{: #cd-import}

Maintenant que vos utilisateurs sont prêts, vous pouvez importer leurs informations dans la nouvelle instance. Pour ce faire, vous pouvez utiliser l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">API de gestion des importations <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


Exemple de commande cURL :

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}



### Script de migration
{: cd-migration-script}

{{site.data.keyword.appid_short_notm}} fournit un script de migration que vous pouvez utiliser via l'interface CLI pour accélérer le processus de migration.

Avant de commencer, assurez-vous de disposer des informations suivantes sur les paramètres :

<table>
  <tr>
    <th>Paramètre</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>ID titulaire de l'instance d'{{site.data.keyword.appid_short_notm}} à partir de laquelle vous prévoyez d'exporter des utilisateurs.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>ID titulaire de l'instance d'{{site.data.keyword.appid_short_notm}} vers laquelle vous prévoyez d'importer des utilisateurs.</td>
  </tr>
  <tr>
    <td>Région</td>
    <td>Les options de la région incluent : <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> et <code>us-south</code>.</td>
  </tr>
  <tr>
    <td>Jeton IAM</td>
    <td>Assurez-vous de disposer des droits de responsable (<code>manager</code>) avant d'obtenir le jeton. Pour obtenir de l'aide sur le jeton IAM, consultez la <a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">documentation <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.</td>
  </tr>
</table>

Pour exécuter le script :

1. Clonez le <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">référentiel <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
2. Ouvrez la console et accédez au dossier dans lequel vous avez cloné le référentiel.
3. Exécutez la commande suivante.

  ```
  npm install
  ```
  {: codeblock}

4. Exécutez la commande suivante avec vos paramètres.

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  Exemple de commande :

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}
