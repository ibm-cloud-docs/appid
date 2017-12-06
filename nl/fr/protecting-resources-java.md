---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Protection des ressources Liberty for Java
{: #protecting-liberty}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} pour protéger des noeuds finaux dans vos applications IBM Liberty for Java. Liberty for Java intègre des capacités de gestion des demandes OIDC (Open ID Connect).

## Avant de commencer
{: #begin}

* Vous devez disposer d'une [application IBM Liberty for Java](https://console.bluemix.net/catalog/starters/liberty-for-java) existante, non liée. Pour vous familiariser avec le développement d'applications Liberty for Java, voir la documentation [](/docs/runtimes/liberty/index.html).
* Assurez-vous que [Apache Maven](https://maven.apache.org/download.cgi) est installé.
* Découvrez comment OIDC fonctionne avec Liberty for Java.

## Protection des ressources dans Liberty for Java
{: #protecting-liberty}

1. Téléchargez le modèle Liberty for Java depuis l'interface utilisateur. Il contient un fichier zip qui inclut les fichiers Liberty standard.

2. Ouvrez le terminal et accédez au répertoire dans lequel vous avez extrait le modèle.

3. Connectez-vous à {{site.data.keyword.Bluemix_notm}} à l'aide de la ligne de commande Cloud Foundry. A l'invite, entrez vos données d'identification.

  ```
  cf login
  ```
  {: codeblock}

4. Déployez l'application. L'exécution de la commande suivante crée une instance Liberty for Java nommée d'après l'ID titulaire.

  ```
  cf push
  ```
  {: codeblock}

5. Liez votre instance de service à la nouvelle instance Liberty for Java et redéployez l'application.

6. Ouvrez votre application dans un navigateur et connectez-vous à l'aide de vos données d'identification pour passer en revue les activités d'authentification.


## Mise à jour du modèle Liberty for Java
{: #updating-liberty}

Pour mettre à jour le modèle d'application, procédez comme suit :

1. Créez les servlets, jsp et html.
2. Définissez les ressources protégées et ajoutez-les aux filtres d'autorisation `web.xml` et `server.xml`.
3. Créez un fichier WAR et déployez-le dans Liberty for Java.

Pour plus d'informations sur la mise à jour des applications, voir [ajout d'{{site.data.keyword.appid_short_notm}} à une application existante](/docs/services/appid/existing.html#existing-liberty).
