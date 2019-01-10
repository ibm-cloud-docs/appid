---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}
{:codeblock: .codeblock}

# Ajout d'attributs avant la connexion de l'utilisateur
{: #sign-in}

Avec {{site.data.keyword.appid_full}}, vous pouvez commencer à créer un profil pour les utilisateurs pour lesquels vous savez qu'un accès à votre application sera nécessaire avant leur première connexion.
{: shortdesc}

Pour en savoir plus sur les types d'attributs, consultez [Compréhension des profils utilisateur](user-profile.html). Pour en savoir plus sur les attributs personnalisés et leurs impératifs de sécurité, consultez [Attributs personnalisés](custom-attributes.html).
{: tip}

**Pourquoi ajouter des informations sur un utilisateur à mon application avant qu'il ne se connecte pour la première fois ?**

Imaginez une application dans laquelle vous utilisez {{site.data.keyword.appid_short_notm}} pour fédérer des utilisateurs existants à partir de votre fournisseur d'identité SAML. Vous voudrez probablement que certains utilisateurs aient un accès `admin` immédiatement après leur première connexion à l'application. Pour ce faire, vous pouvez utiliser le noeud final de pré-enregistrement pour définir un attribut `admin` personnalisé pour ces utilisateurs et leur accorder l'accès à la console d'administration sans aucune autre action de votre part. Veillez à prendre en compte les [problèmes de sécurité](custom-attributes.html) pouvant survenir lors de la modification du paramètre par défaut.

**Comment les utilisateurs sont-ils identifiés ?**

Vous pouvez identifier vos utilisateurs à l'aide de l'un des éléments suivants :

* L'ID unique de l'utilisateur, appelé **identificateur global unique**, dans le fournisseur d'identité. Bien que cet identifiant existe toujours et qu'il soit garanti unique, il n'est pas toujours facilement disponible ou simple à comprendre. Par exemple, Cloud Directory utilise un identificateur global unique aléatoire de 16 octets.
* S'il est disponible, l'**e-mail** de l'utilisateur.

**Comment savoir quel fournisseur d'identité donne quelles informations ?**

Consultez le tableau suivant pour voir quel type d'informations d'identité vous pouvez utiliser.

<table>
  <thead>
    <tr>
      <th>Fournisseur
d'identité</th>
      <th>Identificateur global unique</th>
      <th>E-mail</th>
      <th>Sous</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cloud Directory</td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td></td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Personnalisé</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Fonction disponible" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

**Cloud Directory est-il géré différemment ?**

Pour garantir l'intégrité des attributs utilisateur pré-enregistrés, Cloud Directory impose des exigences supplémentaires à ses utilisateurs. Le pré-enregistrement ne peut avoir lieu que lorsque la validation du courrier électronique est activée et vérifiée. Si vous pré-enregistrez un utilisateur Cloud Directory avec des attributs spécifiques, ces attributs sont destinés à cette personne spécifique. Si l'e-mail n'est pas vérifié en premier, il est possible pour un autre utilisateur de réclamer l'adresse e-mail et tous les attributs qui lui sont attribués.

Comment faire ?

1. Configurez Cloud Directory en mode e-mail et mot de passe. Vous pouvez le faire via l'interface utilisateur dans les paramètres généraux sur l'onglet **Cloud Directory**. Vous pouvez également le configurer à l'aide des [API de gestion](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/createCloudDirectoryUser).

2. Vérifiez l'adresse électronique des utilisateurs pour confirmer leur identité de l'une des manières suivantes :

  * Pour vérifier l'identité d'un utilisateur par courrier électronique, définissez **Vérification de l'adresse électronique** sur **Activé** dans l'onglet **Cloud Directory** du tableau de bord du service. Si vous ajoutez un utilisateur et qu'il se connecte à votre application sans vérification préalable de son adresse électronique, la connexion aboutit mais son attribut prédéfini est supprimé.
  * Pour vérifier les utilisateurs manuellement, vous devez être administrateur et utiliser les [API de gestion](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/createCloudDirectoryUser) Cloud Directory. Lors de la création ou de la mise à jour d'un utilisateur, vous devez explicitement définir la zone `status` sur `CONFIRMED` dans votre contenu de données utilisateur.

**Dois-je faire quelque chose de particulier lorsque j'utilise un fournisseur d'identité personnalisé ?**

Lorsque vous ajoutez à l'avance des informations utilisateur à votre application, vous pouvez utiliser n'importe quel identificateur unique fourni par le flux d'authentification. L'identificateur doit _exactement_ correspondre à la valeur `sub` du jeton Web JSON qui est envoyé lors de la demande d'autorisation. Si l'identificateur ne correspond pas, la liaison du profil que vous souhaitez ajouter n'aboutit pas.



## Ajout d'informations utilisateur à votre application
{: #add}

Maintenant que vous connaissez le processus et vos implications en matière de sécurité, essayez d’ajouter un utilisateur.

**Avant de commencer :**

Vous devez connaître les informations suivantes pour ajouter des attributs personnalisés pour un utilisateur spécifique avec le noeud final d'API de gestion [/users](https://appid-management.ng.bluemix.net/swagger-ui/#!/Users/users_search_user_profile) :

* Le fournisseur d'identité dont l'utilisateur se servira pour se connecter.
* L'identificateur unique de l'utilisateur fourni par le fournisseur d'identité.

Lorsqu'un utilise se connecte à votre application pour la première fois, {{site.data.keyword.appid_short_notm}} recherche l'utilisateur. S'il est trouvé, l'utilisateur hérite de l'identité que vous avez affectée. S'il n'est pas trouvé, un nouvel utilisateur est créé en fonction des informations fournies par le fournisseur d'identité.

**Pour ajouter un utilisateur :**

1. Connectez-vous à IBM Cloud.
  ```
  ibmcloud login
  ```
  {: pre}

2. Recherchez votre jeton IAM en exécutant la commande suivante.
  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. Envoyez une requête POST au noeud final `/users` contenant une description de l'utilisateur et des attributs que vous souhaitez définir comme objet JSON.

  En-tête :
  ```
  POST {management-url}/management/v4/{tenantId}/users
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  Corps :
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes": {
             "mealPreference":"vegeterian"
           }
       }
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icône Idée"/> Description des composants</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>idp</em></code></td>
        <td>Fournisseur d'identité avec lequel l'utilisateur s'authentifiera. Les options comprennent : `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid`.</td>
      </tr>
      <tr>
        <td><code><em>idp-identity</em></code></td>
        <td>Identificateur unique fourni par le fournisseur d'identité.</td>
      </tr>
      <tr>
        <td><code><em>profile</em></code></td>
        <td>Profil utilisateur contenant le mappage JSON de l'attribut personnalisé.</td>
      </tr>
    </tbody>
  </table>

  Exemple de demande :
  ```
  $ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
  ```
  {: screen}

3. Vérifiez que l'enregistrement a réussi de l'une des manières suivantes :
  * Recherchez l'ID utilisateur dans la réponse.
    ```
    {
        "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
    }
    ```
    {: screen}
  * Recherchez le profil utilisateur qui a été créé.

N'oubliez pas que les attributs prédéfinis d'un utilisateur sont vides jusqu'à sa première authentification, mais que l'utilisateur est, à toutes fins utiles, entièrement authentifié. Vous pouvez utiliser son identifiant unique comme vous le feriez avec une personne déjà connectée. Par exemple, vous pouvez modifier, rechercher ou supprimer le profil.

Maintenant que vous avez associé un utilisateur à des attributs spécifiques, essayez d'[accéder aux attributs](/docs/services/appid/custom-attributes.html) !


</br>
