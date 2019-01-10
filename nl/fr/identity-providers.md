---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{: tip: .tip}

# Réseau social
{: #setting-up-idp}

Avec {{site.data.keyword.appid_full}}, vous pouvez configurer des fournisseurs d'identité de réseau social pour définir une expérience de connexion unique pour votre application. La possibilité pour un utilisateur de se connecter avec ses profils sociaux, lui permet de ne pas avoir à se souvenir de plusieurs mots de passe pour différentes applications.
{: shortdesc}


## Configuration par défaut
{: #default}

{{site.data.keyword.appid_short_notm}} fournit une configuration par défaut pour vous aider à être rapidement opérationnel avec le service.
{: shortdesc}

Les données d'identification par défaut sont définies pour Facebook et Google. Ces données d'identification sont limitées à 100 utilisations par instance, par jour. Comme il s'agit de données d'identification IBM, elles sont destinées à un usage en mode développement uniquement. Avant de publier votre application, mettez à jour la configuration avec vos propres données d'identification.


## Configuration de Facebook
{: #facebook}

Vous pouvez configurer le service {{site.data.keyword.appid_short}} pour utiliser Facebook comme fournisseur d'identité.
{: shortdesc}

### Obtention d'un ID et d'une valeur confidentielle d'application auprès de Facebook

Pour utiliser Facebook comme fournisseur d'identité, vous devez ajouter et configurer la plateforme de site Web sur votre application Facebook.

1. Connectez-vous à votre compte sur le <a href="https://developers.facebook.com/docs/apps/register" target="_blank">site Facebook for Developers <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
2. Notez l'ID et la valeur confidentielle de l'application Facebook. Ces valeurs sont requises pour configurer votre projet Web pour l'authentification dans votre tableau de bord du service.
3. Ajoutez la plateforme Web et indiquez l'URL du site.
4. Dans la liste des produits, sélectionnez **Facebook Login**.
5. Dans la zone **URL de redirection OAuth valides**, entrez l'URL du noeud final de rappel du serveur d'autorisation.
6. Cliquez sur **Sauvegarder les modifications**.


### Configuration d'{{site.data.keyword.appid_short_notm}} pour l'authentification Facebook

Une fois que vous disposez de votre ID et de votre valeur confidentielle d'application Facebook et que votre application Facebook for Developers est configurée pour servir des clients Web, vous pouvez éditer l'authentification Facebook depuis votre tableau de bord du service.

1. Depuis l'onglet **Gérer** de votre tableau de bord du service, sélectionnez **Facebook** et cliquez sur **Editer**.
2. Entrez l'ID et la valeur confidentielle d'application Facebook obtenus auprès du site Web Facebook for Developers.
3. Copiez l'URI mentionné dans la zone **URI de redirection pour Facebook for Developers**. Collez cet URI dans la zone **URI de redirection OAuth valides** dans la section **Facebook Login** du portail des développeurs Facebook.
4. Cliquez sur **Sauvegarder**.
5. Facultatif : pour les applications Web, entrez l'URL de redirection dans la zone **URL de redirection d'application Web**. Cette valeur définie par le développeur est utilisée pour accéder à l'URL de redirection une fois le processus d'autorisation terminé. L'URL doit suivre un schéma `http` ou `https`. Pour un niveau de sécurité renforcé, utilisez un schéma `https`.


## Configuration de Google
{: #google}

Configurez le service {{site.data.keyword.appid_short}} pour utiliser Google comme fournisseur d'identité.
{: shortdesc}

### Obtention d'un ID client et d'une valeur confidentielle auprès de Google

Créez un projet dans la <a href="https://developers.google.com/" target="_blank">console Google Developers <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>, configurez le projet pour servir des clients Web et obtenez un identificateur et une valeur confidentielle de client.

1. Créez un projet.
2. Ajoutez l'API Google+ à votre projet Google.
3. Ajoutez les données d'identification à l'API Google+.
    1. Sélectionnez API Google+ comme type d'API.
    2. Sélectionnez **Navigateur Web** comme emplacement d'appel de l'API.
    3. Sélectionnez **Données utilisateur**.
    4. Renseignez les zones requises pour créer un ID client. Une valeur confidentielle est créée en parallèle.
4. Notez l'ID client et la valeur confidentielle Google. Dans l'onglet des données d'identification, sélectionnez l'ID que vous avez créé pour obtenir votre identificateur et votre valeur confidentielle de client.

### Configuration d'{{site.data.keyword.appid_short}} pour l'authentification Google

Une fois que vous avez configuré votre projet Google et obtenu votre identificateur et votre valeur confidentielle de client, vous pouvez éditer votre tableau de bord du service pour l'authentification Google.

1. Sur la page **Gérer** de votre tableau de bord du service, sélectionnez **Google** et cliquez sur **Editer**.
2. Entrez l'ID client et la valeur confidentielle client obtenus dans la console Google Developers.
3. Autorisez l'URL d'{{site.data.keyword.appid_short}}.
    1. Copiez l'**URL de redirection pour la console Google Developer** à partir des détails du fournisseur d'identité Google.
    2. Sur la page des données d'identification de votre projet Google, sélectionnez l'ID client créé pour cette intégration.
    3. Collez l'URL depuis {{site.data.keyword.appid_short}} dans la zone **URI de redirection autorisés**, puis cliquez sur**Sauvegarder**.
4. Cliquez sur **Sauvegarder** pour mettre à jour votre configuration Google dans {{site.data.keyword.appid_short}}.
5. Pour les applications Web, entrez l'URL de redirection dans l'onglet **Gérer**. Une fois le processus d'autorisation terminé, un utilisateur est envoyé à cette adresse URL. L'URL doit suivre un schéma `http` ou `https`. Pour un niveau de sécurité renforcé, utilisez un schéma `https`.
