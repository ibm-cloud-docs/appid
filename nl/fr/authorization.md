---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}




# Concepts clés
{: #key-concepts}

Vous êtes perdus entre autorisation et authentification ? Vous n'êtes pas seul. Consultez les informations de cette page pour en savoir plus sur la terminologie, les processus et la manière dont le service utilise les jetons.
{: shortdesc}


## Terminologie
{: #terms}


Ces termes clés peuvent vous aider à comprendre de quelle manière le service décompose le processus d'autorisation et d'authentification.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> est un protocole à norme ouverte utilisé pour fournir une autorisation d'application.</dd>
  <dt>OIDC (Open ID Connect)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> est une couche d'authentification qui opère au-dessus de OAuth 2.</p>
    <p>Lorsque vous utilisez OIDC et {{site.data.keyword.appid_short_notm}} ensemble, vos données d'identification du service permettent de configurer vos noeuds finaux OAuth. Lorsque vous utilisez le logiciel SDK, les URL des noeuds finaux sont générées automatiquement. Toutefois, vous pouvez aussi les générer vous-même en utilisant vos données d'identification du service. L'exemple et le tableau ci-dessous indiquent comment composer les URL.</p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
      "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
      "profilesUrl": "https://appid-profiles.ng.bluemix.net/"
    }</code></pre>
    <table>
      <tr>
        <th>Noeud final</th>
        <th>Format</th>
      </tr>
      <tr>
        <td>Authorization</td>
        <td>{oauthServerUrl}/authorization</td>
      </tr>
      <tr>
        <td>Token</td>
        <td>{oauthServerUrl}/token</td>
      </tr>
      <tr>
        <td>Userinfo</td>
        <td>{oauthServerUrl}/userinfo</td>
      </tr>
      <tr>
        <td>JWKS</td>
        <td>{oauthServerUrl}/publickeys</td>
      </tr>
    </table>
    <p><strong>Remarque</strong> : lorsque vous utilisez le logiciel SDK, les URL des noeuds finaux sont générées automatiquement.</p></dd>
  <dt>Jetons</dt>
    <dd>Le service utilise trois types de jeton différents. Les jetons d'accès représentent une autorisation et permettent de communiquer avec des [ressources de back end](/docs/services/appid/backend-apps.html) protégées par des filtres d'autorisation appliqués par {{site.data.keyword.appid_short}}. Les jetons d'identité représentent une authentification et contiennent des informations concernant l'utilisateur. Un jeton d'actualisation peut être utilisé pour obtenir un nouveau jeton d'accès sans nouvelle authentification de l'utilisateur. A l'aide des jetons d'actualisation, les utilisateurs peuvent autoriser l'application à mémoriser leurs informations. Ainsi, ils peuvent rester connectés. Pour plus d'informations sur les jetons et leur utilisation dans {{site.data.keyword.appid_short}}, consultez [Validation des jetons](tokens.html#remote-validation).
  </dd>
  <dt>En-têtes d'autorisation</dt>
    <dd><p>{{site.data.keyword.appid_short}} respecte la <a href="https://tools.ietf.org/html/rfc6750" target="blank">spécification de support de jeton <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et utilise une combinaison de jetons d'accès et d'identité envoyée sous forme d'en-tête d'autorisation HTTP. L'en-tête d'autorisation se compose de trois parties distinctes séparées par un espace. Les jetons sont codés en Base64. Le jeton d'identité est facultatif.</br>
    Exemple :</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>Stratégie d'API</dt>
    <dd><p>La stratégie d'API s'attend à ce que les demandes contiennent un en-tête d'autorisation avec un jeton d'accès valide. La demande peut également contenir un jeton d'identité, mais cela n'est pas obligatoire. Si un jeton n'est pas valide ou a expiré, la stratégie d'API renvoie une erreur HTTP 401 qui contient l'en-tête HTTP suivant :</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>Si la demande renvoie un jeton valide, le contrôle passe au middleware suivant et la propriété <code>appIdAuthorizationContext</code> est injectée dans l'objet de demande. Cette propriété contient les jetons d'accès et d'identité originaux, ainsi que les informations de contenu décodées sous forme d'objets JSON ordinaires.</dd>
  <dt>Stratégie d'application Web</dt>
    <dd>Lorsque la stratégie d'application Web détecte des tentatives non autorisées d'accès à une ressource protégée, elle redirige automatiquement le navigateur de l'utilisateur vers la page d'authentification, qui peut être fournie par {{site.data.keyword.appid_short}}. Si l'authentification aboutit, l'utilisateur est ramené à l'URL de rappel de l'application Web. La stratégie d'application Web obtient des jetons d'accès et d'identité et les stocke dans une session HTTP sous <code>WebAppStrategy.AUTH_CONTEXT</code>. Il revient à l'utilisateur de décider de stocker ou non les jetons d'accès et d'identité dans la base de données de l'application.</dd>
  <dt>Séparation et chiffrement des données</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} stocke et chiffre les attributs de profil utilisateur. Comme il s'agit d'un service partagé, chaque titulaire est associé à une clé de chiffrement dédiée et les données utilisateur de chaque titulaire sont chiffrées avec sa propre clé.</p>
    <p>{{site.data.keyword.appid_short_notm}} garantit que les informations privées soient chiffrées avant leur stockage.</p></dd>
</dl>

</br>
</br>


## Comprendre les jetons
{: #tokens}

Lorsqu'un utilisateur est authentifié avec succès, l'application reçoit des jetons d'{{site.data.keyword.appid_short_notm}}. Le service utilise trois principaux types de jeton pour exécuter le processus d'authentification.
{: shortdesc}


**Qu'est-ce qu'un jeton d'accès ?**

Les jetons d'accès représentent une autorisation et permettent de communiquer avec des [ressources de back end](/docs/services/appid/backend-apps.html) protégées par des filtres d'autorisation appliqués par {{site.data.keyword.appid_short}}. Le jeton est conforme aux spécifications JOSE (JavaScript Object Signing et Encryption). Les jetons sont formatés en tant que <a href="https://jwt.io/introduction/" target="blank">jetons Web JSON <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et sont signés avec une clé Web JSON qui utilise l'algorithme RS256.

Exemple de jeton :
  ```
  Header: {
      "typ": "JOSE",
      "alg": "RS256",
  }
  Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "exp": "1495562664",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "amr": ["facebook"],
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "iat": "1495559064",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
  ```
  {: screen}

**Qu'est-ce qu'un jeton d'identité ?**

Les jetons d'identité représentent une authentification et contiennent des informations concernant l'utilisateur. Ils peuvent vous donner des informations sur son nom, son adresse électronique, son sexe et son emplacement. Ils peuvent également renvoyer une URL à une image de l'utilisateur. Les jetons sont formatés en tant que <a href="https://jwt.io/introduction/" target="blank">jetons Web JSON <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et sont signés avec une clé Web JSON qui utilise l'algorithme RS256.

Exemple de jeton :
  ```
  Header: {
      "typ": "JOSE",
      "alg": "RS256",
  }
  Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "exp: "1495562664",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "iat": "1495559064",
      "name": "John Smith",
      "email": "js@mail.com",
      "gender", "male",
      "locale": "en",
      "picture": "<URL-to-photo>",
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "identities": [
          "provider": "facebook"
          "id": "377440159275659"
      ],
      "amr": ["facebook"],
      "oauth_client":{
        "name": "BluemixApp",
        "type": "serverapp",
        "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
        "software_version": "1.0.0",
      }
  }
  ```
  {: screen}

Les jetons d'identité ne contiennent que des informations utilisateur partielles. Pour voir toutes les informations fournies par le fournisseur d'identité, vous pouvez utiliser le [noeud final user info](/docs/services/appid/predefined.html#api).

**Qu'est-ce qu'un jeton d'actualisation ?**

{{site.data.keyword.appid_short}} permet d'acquérir de nouveaux jetons d'accès et d'identité sans nouvelle authentification, comme défini dans <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Un jeton d'actualisation peut être utilisé pour renouveler le jeton d'accès afin qu'un utilisateur n'ait à effectuer aucune action pour se connecter, telle que fournir des données d'identification. Similaires aux jetons d'accès, les jetons d'actualisation contiennent des données qui permettent à {{site.data.keyword.appid_short_notm}} de déterminer si vous êtes autorisé. Cependant, ces jetons sont opaques.

Les jetons d'actualisation sont configurés pour avoir une durée de vie supérieure à celle d'un jeton d'accès normal. Ainsi, lorsqu'un jeton d'accès expire, le jeton d'actualisation reste valide et peut être utilisé pour le renouveler. Les jetons d'actualisation d'{{site.data.keyword.appid_short_notm}} peuvent être configurés pour durer de 1 à 90 jours. Pour tirer le meilleur parti des jetons d'actualisation, conservez-les pendant toute leur durée de vie ou jusqu'à ce qu'ils soient renouvelés. Un utilisateur ne peut pas accéder directement à des ressources avec un simple jeton d'actualisation, ce qui rend ce jeton beaucoup plus sûr à conserver qu'un jeton d'accès. En tant que meilleure pratique, les jetons d'actualisation doivent être stockés de manière sécurisée par le client qui les a reçus et envoyés uniquement au serveur d'autorisation qui les a émis.

Pour plus de commodité, {{site.data.keyword.appid_short_notm}} renouvelle également son jeton d'actualisation — et sa date d'expiration — lorsque le jeton d'accès est renouvelé, permettant ainsi à l'utilisateur de rester connecté tant qu'il est actif à un moment donné avant l'expiration du jeton d'actualisation actuel. Par contre, si vous souhaitez utiliser des jetons d'actualisation tout en obligeant l'utilisateur à se connecter régulièrement, votre application ne pourra utiliser que les jetons d'actualisation renvoyés lorsque l'utilisateur se connecte en saisissant ses données d'identification. Nous vous recommandons cependant de toujours utiliser le dernier jeton d'actualisation reçu de l'ID d'application, comme indiqué dans les <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">spécifications Oauth <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


Bien que ces jetons puissent simplifier le processus de connexion, votre application ne doit pas en dépendre, car ils peuvent être révoqués à tout moment, par exemple lorsque vous pensez que vos jetons d'actualisation ont été compromis. Il existe deux méthodes permettant de révoquer un jeton d'actualisation en cas de besoin. Si vous disposez d'un jeton d'actualisation, vous pouvez le révoquer selon la norme <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Sinon, si vous disposez de l'ID utilisateur, vous pouvez révoquer le jeton d'actualisation à l'aide de l'<a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="_blank">API de gestion <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Pour plus d'informations sur l'accès à l'API de gestion, voir [Gestion de l'accès au service](iam.html#service-access-management).

Pour des exemples d'utilisation des jetons d'actualisation et de leur utilisation en vue d'implémenter une fonctionnalité remember-me, consultez [getting started samples](index.html).


**D'où proviennent les jetons ?**

Les jetons sont émis via le serveur OAuth {{site.data.keyword.appid_short_notm}} et sont formatés en tant que [jetons Web JSON (JWT)](https://jwt.io/introduction/). Ils sont signés avec une [clé Web JSON (JWK)](https://tools.ietf.org/html/rfc7517) à l'aide de l'algorithme RS256.

**Qu'advient-il des informations contenues dans le jeton ?**

Le jeton d'accès contient un ensemble de réclamations JWT standard et un ensemble de réclamations spécifiques à {{site.data.keyword.appid_short_notm}} telles qu'un ID titulaire. Le jeton d'identité contient des informations spécifiques à l'utilisateur. Les informations contenues dans les jetons sont stockées en tant que réclamations dans un [profil utilisateur](/docs/services/appid/user-profile.html).

**Comment les jetons sont-ils reçus ?**

Les jetons sont reçus par votre application après une authentification réussie. Votre application peut utiliser les jetons pour récupérer des informations sur l'autorisation et l'authentification de l'utilisateur. Le jeton d'accès peut être utilisé pour accéder aux ressources protégées en envoyant une demande à la ressource. Dans la demande, le jeton d'accès est décrit dans le [schéma d'authentification Bearer](https://tools.ietf.org/html/rfc6750#page-5). Votre application doit analyser l'en-tête pour pouvoir extraire les jetons.

Exemple de demande :

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

</br>
</br>
