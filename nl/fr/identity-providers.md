---

copyright:
  years: 2017
lastupdated: "2017-06-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Configuration des fournisseurs d'identité
{: #setting-up-idp}

Vous pouvez configurer Facebook, Google, IMBid (ou une combinaison des trois) pour
proposer une expérience de connexion unique à vos utilisateurs. En utilisant un fournisseur d'identité, les utilisateurs peuvent se connecter avec des
données d'identification qui leur sont déjà familières.
{:shortdesc}


## Configuration de l'authentification sur Facebook
{: #facebook}

Configurez le service {{site.data.keyword.appid_short}} pour utiliser Facebook comme fournisseur d'identité.


### Obtention d'un ID et d'une valeur confidentielle d'application auprès de Facebook
{: #getting-facebook-appid}

Pour utiliser Facebook comme fournisseur d'identité sur vos applications mobiles ou Web, vous devez ajouter et configurer la plateforme de site Web sur votre application Facebook.

1. Connectez-vous à votre compte sur le site <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for
Developers<img src="../../icons/launch-glyph.svg" alt="icône de lien externe"></a>.
2. Notez l'ID et la valeur confidentielle de l'application Facebook. Ces valeurs sont requises pour configurer votre projet Web pour l'authentification dans votre tableau de bord du service.
3. Ajoutez la plateforme Web et indiquez l'URL du site.
4. Dans la liste des produits, sélectionnez **Facebook Login**.
5. Dans la zone URL de redirection OAuth valides, entrez l'URL de noeud final de rappel du serveur d'autorisation. Vous
pouvez ajouter cette valeur après
avoir configuré votre instance de service. 
6. Cliquez sur **Sauvegarder les modifications**.

### Configuration d'{{site.data.keyword.appid_short_notm}} pour
l'authentification Facebook
{: #configuring-facebook-appid}

Une fois que vous disposez de votre ID et de votre valeur confidentielle d'application Facebook et que votre application Facebook for Developers est configurée pour servir des clients Web, vous pouvez éditer l'authentification Facebook depuis votre tableau de bord du service.

1. Depuis l'onglet **Gérer** de votre tableau de bord du service, sélectionnez **Facebook** et cliquez sur **Editer**.
2. Entrez l'ID et la valeur confidentielle d'application Facebook obtenus auprès du site Web Facebook for Developers.
3. Copiez l'URI mentionné dans la zone **URI de redirection pour Facebook for Developers**. 
Collez cet URI dans la zone **URI de redirection OAuth valides** dans
la
section **Facebook Login** du portail des développeurs Facebook.
4. Cliquez sur **Sauvegarder**.
5. Facultatif : pour les applications Web, entrez l'URL de redirection dans
la zone **URL de redirection d'application Web**. Cette valeur
définie par le développeur est utilisée pour accéder à l'URL de redirection une fois le processus d'autorisation terminé.


## Configuration de l'authentification Google
{: #google}

Configurez le service {{site.data.keyword.appid_short_notm}} pour utiliser Google comme fournisseur d'identité.


### Obtention d'un ID client et d'une valeur confidentielle auprès de Google
{: #google-client-id}

Pour utiliser Google comme fournisseur d'identité, procurez-vous un ID client et une valeur confidentielle Google, puis créez un projet dans la console de développeur Google.

1. Ouvrez votre application Google dans la <a href="https://console.developers.google.com/apis/library" target="_blank">console Google Developer<img src="../../icons/launch-glyph.svg" alt="icône de lien externe"></a>.
2. Ajoutez l'API Google+.
3. Créez des données d'identification à l'aide d'OAuth. Dans la zone **Type d'application**, sélectionnez **Application Web**. 
Dans la zone **URI de redirection autorisés**, entrez l'URI de
redirection {{site.data.keyword.appid_short_notm}}. Vous pouvez identifier l'URI
d'autorisation de redirection {{site.data.keyword.appid_short_notm}} depuis l'écran de configuration Google du tableau de
bord du service.
4. Prenez note de l'ID client et de la valeur confidentielle Google, puis
sauvegardez vos
modifications.



### Configuration d'{{site.data.keyword.appid_short_notm}} pour l'authentification Google
{: #google-client-appid}

Une fois que vous disposez de votre ID et de votre valeur confidentielle Google et que votre console Google Developers est configurée pour servir les clients Web, vous pouvez éditer l'authentification Google depuis votre tableau de bord du service.

1. Depuis l'onglet **Gérer** de votre tableau de bord du service, sélectionnez **Google** et cliquez sur **Editer**.
3. Entrez l'ID client et la valeur confidentielle Google obtenus dans la console Google Developers.
4. Copiez l'URI mentionné dans la zone **URI de redirection pour Google for Developers**. 
Collez cet URI dans la zone **URI de redirection autorisés** sous
l'entrée **Restrictions** de la section **ID client pour
application Web** du portail des développeurs Google.
5. Cliquez sur **Sauvegarder**.
6. Facultatif : pour les applications Web, entrez l'URI de redirection dans la
zone **URI de redirection d'application Web**. Cette valeur définie par le développeur est utilisée pour accéder à l'URI de redirection à l'issue du processus d'authentification.


## Configuration de l'authentification IBMid

Pour utiliser IBMid comme fournisseur d'identité,
consultez le
manuel <a href="https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide" target="_blank">IBMid-Federation-Guide
<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Si vous
possédez déjà une application BlueID, procurez-vous un ID client et une valeur
confidentielle BlueID.



### Obtention d'un ID client et d'une valeur confidentielle auprès d'IBMid


Pour obtenir un ID client et une valeur confidentielle, procédez comme suit.


1. Sur la page <a href="https://w3.innovate.ibm.com/tools/sso/home.html" target="_blank">SSO Self-Service Provisioner <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>, connectez-vous à votre compte BlueID. 
2. Enregistrez une application BlueID. Veillez à sélectionner
**preproduction** ou **production** pour le
fournisseur d'identité.

3. Dans la section des **détails sur le client**,
entrez l'URL de redirection App ID.
Vous pouvez obtenir l'URI d'autorisation de redirection sur l'écran de configuration
IBMid de votre tableau de bord du service.

4. Assurez-vous que l'option **Code d'autorisation** est sélectionnée.

5. Prenez note de votre ID client et de votre valeur confidentielle BlueID,
ainsi que du type de fournisseur d'identité de compte.
Cliquez sur **Continuer & Terminer**.

### Configuration d'App ID pour l'authentification IBMid 

Une fois que vous possédez un ID client et une valeur confidentielle BlueID et
que votre application BlueID est configurée avec l'URI de redirection approprié, vous
pouvez éditer la section d'authentification BlueID de votre tableau de bord du service.


1. Depuis l'onglet **Gérer** de votre tableau de bord du service, sélectionnez **IBMid** et cliquez sur
**Editer**.
2. Entrez votre ID client et votre valeur confidentielle BlueID.

3. Copiez l'URI indiqué dans la zone **URI de redirection pour IBMid
for Developers** et collez-le dans la zone **URI de
redirection**.
4. Sélectionnez **preproduction** ou
**production** pour le fournisseur d'identité et cliquez sur
**Sauvegarder**.
5. Facultatif : pour les applications Web, entrez l'URI de redirection dans la
zone **URI de redirection d'application Web**. Cette valeur
définie par le développeur est utilisée pour accéder à l'URI de redirection une fois
l'autorisation accordée.

