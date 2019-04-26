---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# Gestion des utilisateurs
{: #cd-users}

Lorsque vous activez Cloud Directory, les utilisateurs peuvent s'inscrire à votre application à l'aide d'une adresse électronique ou d'un nom d'utilisateur et d'un mot de passe.
{: shortdesc}


Un utilisateur Cloud Directory n'est pas un utilisateur {{site.data.keyword.appid_short_notm}}. Les utilisateurs peuvent s'inscrire à votre application en utilisant les différentes options de fournisseur d'identité que vous configurez. Les utilisateurs mentionnés dans cette rubrique sont ceux qui ont choisi d'utiliser l'option Cloud Directory lors de leur inscription à votre application.
{: note}


## Ajout et suppression d'utilisateurs
{: #add-delete-users}

Vous pouvez gérer vos utilisateurs Cloud Directory via le tableau de bord {{site.data.keyword.appid_short_notm}} ou à l'aide des API.
{: shortdesc}

Pour afficher l'intégralité des données relatives à un utilisateur particulier, vous pouvez utiliser les API afin de renvoyer les informations relatives à un utilisateur Cloud Directory sous forme d'objet JSON. Pour afficher l'ensemble complet des données utilisateur qu'{{site.data.keyword.appid_short_notm}} prend en charge, voir le [schéma principal SCIM](https://tools.ietf.org/html/rfc7643#section-8.2).

### Ajout d'utilisateurs
{: #add-users}

Pour ajouter un utilisateur via le tableau de bord {{site.data.keyword.appid_short_notm}}, procédez comme suit :

A des fins de test, vous pouvez ajouter un utilisateur via le tableau de bord {{site.data.keyword.appid_short_notm}}.

1. Accédez à l'onglet **Cloud Directory > Utilisateurs** du tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Cliquez sur **Ajouter un utilisateur**. Un écran s'affiche.

3. Entrez un **Prénom**, un **Nom**, une **adresse électronique** et un **Mot de passe**. Vérifiez que l'adresse électronique que vous voulez enregistrer n'est pas déjà utilisé par un autre utilisateur. Pour vous assurer que vous avez correctement entré votre mot de passe, confirmez-le dans la zone **Entrez à nouveau le mot de passe**.

4. Cliquez sur **Sauvegarder**. Un utilisateur Cloud Directory est créé.


### Suppression d'utilisateurs
{: #delete-users}

Vous pouvez supprimer un utilisateur de votre répertoire depuis l'interface graphique.

1. Accédez à l'onglet **Cloud Directory > Utilisateurs** du tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Cochez la case en regard de l'utilisateur à supprimer. Une boîte de dialogue s'affiche.

3. Dans la boîte de dialogue, cliquez sur **Supprimer**. Un écran s'affiche.

4. Confirmez que vous avez compris que la suppression d'un utilisateur ne peut pas être annulée en cliquant sur **Supprimer**. Si l'action était une erreur, vous pouvez ajouter de nouveau l'utilisateur à votre répertoire, mais toutes les informations le concernant ne sont plus disponibles.


## Migration des utilisateurs
{: #user-migration}

Il est parfois nécessaire de configurer une nouvelle instance d'{{site.data.keyword.appid_short_notm}}. Si vous utilisez Cloud Directory, vos utilisateurs devront être migrés vers la nouvelle instance. Vous pouvez utiliser les API de gestion pour faciliter la migration.
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
    <td>L'ID titulaire du service se trouve dans vos données d'identification du service. Vos données d'identification du service sont disponibles dans le tableau de bord {{site.data.keyword.appid_short_notm}}.</td>
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

Avant de commencer, assurez-vous de disposer des informations sur les paramètres suivantes :

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
    <td>Assurez-vous de disposer des droits <code>responsable</code> avant d'obtenir le jeton. Pour obtenir de l'aide sur le jeton IAM, consultez la <a href="https://cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">documentation <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.</td>
  </tr>
</table>

Pour exécuter le script :

1. Clonez le <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">référentiel <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
2. Ouvrez le terminal et accédez au dossier dans lequel vous avez cloné le référentiel.
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
