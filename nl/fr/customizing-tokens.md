---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-25"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Personnalisation des jetons
{: #customizing-tokens}

Vous pouvez configurer vos jetons {{site.data.keyword.appid_short_notm}} pour répondre aux besoins spécifiques de votre application.
{: shortdesc}

**Quels types de jetons existe-t-il ?**

{{site.data.keyword.appid_short_notm}} propose différents types de jetons pour protéger vos applications.

* Jetons d'accès : permettent la communication avec les ressources d'arrière-plan qui sont protégées par des filtres d'autorisation. Si un jeton d'accès n'est pas associé à un utilisateur spécifique, ses capacités sont limitées.
* Jetons d'identité : contiennent des informations personnelles et sont utilisés pour authentifier un utilisateur. Selon la configuration de votre application, des jetons d'identité peuvent être émis avant l'authentification d'un utilisateur. Cela vous permet d'associer des attributs à vos utilisateurs avant qu'ils ne se connectent à votre application.
* Jetons d'actualisation : peuvent être utilisés pour prolonger la durée pendant laquelle un utilisateur peut rester sans s'authentifier à nouveau.

Vous souhaitez en savoir plus sur les jetons ? Consultez la rubrique [Understanding tokens](authorization.html#tokens).
{: tip}

</br>

**Quelles sont mes options de personnalisation ?**

Vous pouvez personnaliser vos jetons en définissant la validité de la durée de vie ou en y ajoutant des revendications personnalisées. Consultez le tableau suivant pour voir comment la durée de vie est configurée ou continuez à lire pour en savoir plus sur le mappage d'attributs personnalisés.

<table>
  <tr>
    <th>Type de jeton</th>
    <th>Type de valeur</th>
    <th>Valeur par défaut</th>
    <th>Options</th>
  </tr>
  <tr>
    <td>Accès</td>
    <td>Minutes</td>
    <td>60</td>
    <td>Toute valeur comprise entre 5 et 1440</td>
  </tr>
  <tr>
    <td>Identité</td>
    <td>Minutes</td>
    <td>60</td>
    <td>Toute valeur comprise entre 5 et 1440</td>
  </tr>
  <tr>
    <td>Actualiser</td>
    <td>Jours</td>
    <td>30</td>
    <td>Toute valeur comprise entre 1 et 9</td>
  </tr>
  <tr>
    <td>Anonyme</td>
    <td>Jours</td>
    <td>30</td>
    <td>Toute valeur comprise entre 1 et 9</td>
  </tr>
</table>

</br>

**Pourquoi ajouter des réclamations à mes jetons ?**

Vous pouvez souhaiter procéder au suivi d'attributs supplémentaires pour plusieurs raisons. Lorsque vous travaillez avec les développeurs de vos applications, vous pouvez mapper des rôles et des droits. Ou, lorsque vous créez des profils pour vos utilisateurs finaux, vous pouvez contrôler des informations supplémentaires qui vous aident à créer des expériences personnalisées.

</br>

**Existe-t-il des considérations de sécurité ?**

Oui. Les jetons servant à identifier les utilisateurs et à sécuriser vos ressources, leur durée de vie affecte plusieurs éléments différents. En personnalisant votre configuration de jeton, vous pouvez vous assurer que vos besoins en matière de sécurité et d'expérience utilisateur sont satisfaits. Toutefois, si un jeton devait être compromis, un utilisateur malveillant aurait plus de temps pour affecter votre application.

Vous voulez en savoir plus sur les considérations de sécurité à prendre en compte ? Consultez la rubrique [Attributs personnalisés](custom-attributes.html).
{: tip}

</br>
</br>

## Comprendre les attributs personnalisés et les réclamations
{: #custom-claims}

Vous pouvez mapper les attributs de profil utilisateur sur vos réclamations de jetons d'accès et d'identité. Cela signifie que vous n'avez pas à accéder au [noeud final /userinfo](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/userInfo) ou à extraire des attributs personnalisés par la suite ; ils sont déjà stockés dans les jetons !
{: shortdesc}


**Pourquoi ajouter des attributs à mes réclamations ?**

Sans avoir à faire d'appels réseau supplémentaires, tout ce que votre application peut avoir besoin de savoir sur un utilisateur ou sur les actions qu'ils peut exécuter est déjà dans le jeton ! Si vous ne disposez pas de quantités massives de données, cela vous rendra plus efficace. Vous pouvez également assurer l'intégrité de ces attributs mappés lorsqu'ils sont envoyés sur le réseau, car ils sont stockés dans un jeton signé.

</br>

**Quels types de réclamation puis-je définir ?**

Les réclamations fournies par {{site.data.keyword.appid_short_notm}} appartiennent à plusieurs catégories qui se différencient par leur niveau de personnalisation.

*Réclamations enregistrées *: certaines réclamations dans les jetons d'accès et d'identité sont définies par {{site.data.keyword.appid_short_notm}} et ne peuvent pas être remplacées par des mappages personnalisés. Si votre réclamation est restreinte, elle est ignorée par le service. Les réclamations sont les suivantes : `iss`, `aud`, `sub`, `iat`, `exp`, `amr` et `tenant`.

*Réclamations restreintes *: selon le jeton vers lequel les réclamations sont mappées, certaines d'entre elles peuvent avoir des possibilités de personnalisation limitées. Pour un jeton d'accès, la seule réclamation restreinte est `scope`. Elle ne peut pas être remplacée par des mappages personnalisés, mais peut être étendue selon vos propres portées. Lorsque la réclamation de portée est mappée à un jeton d'accès, la valeur doit être une chaîne et ne peut pas être préfixée par `appid_`, sinon elle sera ignorée. Dans les jetons d'identité, les réclamations `identities` et `oauth_clients` ne peuvent pas être modifiées ou remplacées.

*Réclamations normalisées *: chaque jeton d'identité contient un ensemble de réclamations qui sont reconnues par {{site.data.keyword.appid_short_notm}} comme étant des réclamations normalisées. Lorsqu'elles sont disponibles, elles sont directement mappées de votre fournisseur d'identité vers le jeton. Ces réclamations ne peuvent pas être explicitement omises mais peuvent être remplacées par des mappages de réclamations personnalisés. Les réclamations comprennent `name`, `email`, `picture`, `local` et `gender`.

</br>

**Comment les réclamations sont-elles définies ?**

Chaque mappage est défini par un objet de source de données et une clé qui est utilisée pour extraire la réclamation. Chaque réclamation personnalisée est définie pour chaque jeton séparément et est appliquée de manière séquentielle. Vous pouvez enregistrer jusqu'à 100 réclamations par chaque jeton avec un contenu maximal de 100 Ko.

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Icône Idée"/> Comprendre les objets de mappage de réclamation</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>Obligatoire</td>
        <td>Définit la source de la réclamation. Peut faire référence aux informations utilisateur du fournisseur d'identité ou aux attributs personnalisés {{site.data.keyword.appid_short_notm}} de l'utilisateur. </br> </br> Les options comprennent `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid` et `attributes`.</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>Obligatoire</td>
        <td>Définit la réclamation des données source. </td>
      </tr>
    </tbody>
  </table>

Vous pouvez référencer des réclamations imbriquées dans vos mappages en utilisant la syntaxe dot. Exemple : `nested.attribute`
{:tip}

</br>

## Configuration de jetons {{site.data.keyword.appid_short_notm}}
{: #configuring-tokens}

Vous pouvez configurer vos jetons {{site.data.keyword.appid_short_notm}} à l'aide de l'interface graphique ou des API de gestion.
{: shortdesc}

### Configuration de la durée de vie des jetons à l'aide de l'interface graphique
{: #configuring-tokens-ui}

1. Accédez à votre tableau de bord du service.
2. Dans la section **Fournisseurs d'identité** de la navigation, sélectionnez la page **Gérer**.
3. Dans l'onglet **Paramètres**, configurez vos jetons.
  1. Pour autoriser la connexion sans interaction de l'utilisateur, définissez les **jetons d'actualisation** sur **On**.
  2. Définissez la durée de vie de votre jeton d'actualisation. L'expiration est définie en jours et peut être n'importe quelle valeur comprise entre 1 et 90. Plus le nombre est petit, plus l'utilisateur doit s'inscrire souvent.
  3. Définissez la durée de vie de votre jeton d'accès. L'expiration est définie en minutes et peut être comprise entre 5 et 1440. Plus la valeur est petite, plus la protection est importante en cas de vol de jetons.
  4. Définissez la durée de vie de votre jeton anonyme. Un [jeton anonyme](/docs/services/appid/progressive.html#anonymous) est affecté aux utilisateurs à partir du moment où ils commencent à interagir avec votre application. Lorsqu'un utilisateur se connecte, les informations contenues dans le jeton anonyme sont alors transférées au jeton associé à l'utilisateur. L'expiration est définie en jours et peut être n'importe quelle valeur comprise entre 1 et 90. 

</br>

### Configuration de jetons à l'aide des API de gestion
{: #configuring-tokens-api}

**Avant de commencer**

Assurez-vous de disposer des prérequis suivants :

* Votre ID titulaire d'instance {{site.data.keyword.appid_short_notm}}. Il est disponible dans la section **Données d'identification pour le service** de l'interface graphique.
* Votre jeton IAM (Identity and Access Management). Pour obtenir de l'aide sur le jeton IAM, consultez la [documentation IAM](/docs/iam/apikey_iamtoken.html).

**Mappage de vos réclamations**

1. Envoyez une requête PUT au noeud final `/config/tokens` avec votre configuration de jeton.

  En-tête :
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  Corps :
  ```
   {
       "access": {
           "expires_in": 3600,
       },
       "refresh": {
           "expires_in": 2592000,
           "enabled": true
       },
       "anonymous": {
           "expires_in": 2592000,
           "enabled": true
       },
       "accessTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "name_id"
           }
       ],
       "idTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "attributes.uid"
           }
       ]
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Icône Idée"/> Comprendre la configuration des jetons</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>Facultatif</td>
        <td>Objet contenant le délai d'expiration de vos jetons d'accès et d'identité, `expires_in`, exprimé en minutes. </br> </br> Le délai d'expiration par défaut est de 60 minutes. </td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>Facultatif</td>
          <td>Objet contenant le délai d'expiration de votre jeton d'actualisation, `expires_in`, exprimé en jours. </br> </br> Le délai d'expiration par défaut est de 30 jours. </td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>Facultatif</td>
          <td>Objet contenant le délai d'expiration de vos jetons d'accès anonyme et d'identité, `expires_in`, exprimé en jours. </br> </br> Le délai d'expiration par défaut est de 30 jours. </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>Facultatif</td>
          <td>Tableau contenant les objets qui sont créés lorsque des réclamations associées à des jetons d'accès sont mappées.</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>Facultatif</td>
          <td>Tableau contenant les objets qui sont créés lorsque des réclamations associées à des jetons d'identité sont mappées.</td>
      </tr>
    </tbody>
  </table>

  Exemple de demande :
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
            }
          ],
          "idTokenClaims": [
            {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
  }' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
