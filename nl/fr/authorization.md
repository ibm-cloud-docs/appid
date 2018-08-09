---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-2"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Autorisation et authentification
{: #authorization}

Avec {{site.data.keyword.appid_full}}, les utilisateurs peuvent optimiser l'usage des jetons et des filtres d'autorisation de manière à garantir la protection de leurs applications. Avant qu'un utilisateur ne puisse accorder d'autorisation à une application, un fournisseur d'identité doit en authentifier l'identité.
{: shortdesc}


## Concepts clés
{: #key-concepts}

Ces termes clés peuvent vous aider à comprendre de quelle manière le service décompose le processus d'autorisation et d'authentification.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> est un protocole à norme ouverte utilisé pour fournir une autorisation d'application.</dd>
  <dt>OIDC (Open ID Connect)</dt>
    <dd><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> est une couche d'authentification qui opère au-dessus de OAuth 2.</dd>
  <dt>Jetons d'accès</dt>
    <dd><p>Les jetons d'accès représentent une autorisation et permettent de communiquer avec des [ressources de back end](/docs/services/appid/protecting-resources.html) protégées par des filtres d'autorisation appliqués par {{site.data.keyword.appid_short}}. Ils sont conformes aux spécifications JOSE (JavaScript Object Signing and Encryption). Les jetons sont au format <a href="https://jwt.io/introduction/" target="blank">Jeton Web JSON<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.</br>
    Exemple :</p>
    <pre><code>Header: {
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
    </code></pre></dd>
  <dt>Jetons d'identité</dt>
    <dd><p>Les jetons d'identité représentent une authentification et contiennent des informations concernant l'utilisateur. Ces informations peuvent être son nom, son adresse e-mail, son sexe et son emplacement. Le jeton peut aussi contenir une URL pointant sur une image de l'utilisateur.</br>
    Exemple :</p>
    <pre><code>Header: {
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
    </pre></code></dd>
  <dt>Jeton d'actualisation</dt>
      <dd><p>{{site.data.keyword.appid_short}} prend en charge la possibilité d'acquérir de nouveaux jetons d'accès et d'identité sans nouvelle authentification, comme défini dans <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
      Lorsqu'un utilisateur se connecte à l'aide d'un jeton d'actualisation, il n'a pas besoin d'effectuer une action, comme fournir des donnée d'identification. En règle générale, les jetons d'actualisation sont configurés pour avoir un cycle de vie supérieur à celui d'un jeton d'accès classique.</p><p>
      Pour tirer pleinement parti des jetons d'actualisation, conservez les jetons durant leur cycle de vie complet. Un utilisateur ne peut pas accéder directement à des ressources avec juste un jeton d'actualisation, ce qui rend sa conservation plus sûre que celle d'un jeton d'accès. Pour des exemples d'utilisation de jetons d'actualisation, notamment pour implémenter une fonctionnalité *remember me*, consultez les exemples d'initiation.</p><p>En tant que pratique recommandée, les jetons d'actualisation doivent être stockés de manière sécurisée par le client qui les reçoit et doivent être envoyés uniquement au serveur d'autorisations qui les a émis.</p></dd>
  <dt>En-têtes d'autorisation</dt>
    <dd><p>{{site.data.keyword.appid_short}} respecte la <a href="https://tools.ietf.org/html/rfc6750" target="blank">spécification de support de jeton <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et utilise une combinaison de jetons d'accès et d'identité envoyée sous forme d'en-tête d'autorisation HTTP. L'en-tête d'autorisation se compose de trois parties distinctes séparées par un espace. Les jetons sont codés en Base64. Le jeton d'identité est facultatif.</br>
    Exemple :</p>
    <pre><code>Authorization=Bearer {jeton_accès} [{jeton_identité}]</pre></code></dd>
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

## Fonctionnement du processus
{: #process}

Lors du codage d'applications, la principale préoccupation est la sécurité. Comment garantir que seuls les utilisateurs dotés de l'accès requis utilisent votre application ? Vous pouvez faire appel à un processus d'autorisation. Dans la plupart des processus, l'autorisation et l'authentification sont couplées, ce qui peut compliquer les modifications au niveau de vos politiques de sécurité et fournisseurs d'identité. Avec {{site.data.keyword.appid_short}}, autorisation et authentification sont des processus séparés.
{: shortdesc}

Lorsque vous configurez des fournisseurs d'identité de réseaux sociaux tels que Facebook, le [flux d'octroi d'autorisation Oauth2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) est utilisé pour appeler le widget de connexion. Avec un répertoire cloud comme fournisseur d'identité, le [flux des données d'identification du mot de passe du propriétaire de la ressource](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) est utilisé pour fournir des jetons d'accès et d'identité.

![Trajet d'un utilisateur inconnu devenant un utilisateur identifié.](/images/authenticationtrail.png)

Lorsqu'un utilisateur choisit de se connecter, il devient un utilisateur identifié. Le fournisseur d'identité renvoie à {{site.data.keyword.appid_short}} des jetons d'accès et d'identité qui contiennent ces informations. Le service prend les jetons fournis et détermine si l'utilisateur détient les données d'identification appropriées pour accéder à une application. Si les jetons sont validés, le service autorise l'accès de l'utilisateur. Les informations d'authentification sont associées à l'enregistrement de l'utilisateur une fois qu'elles ont été autorisées. Un nouvel accès à cet enregistrement d'utilisateur et à ses attributs peut être effectué par n'importe quel client qui s'authentifie avec cette même identité.

### Authentification progressive

Avec {{site.data.keyword.appid_short_notm}}, un utilisateur anonyme peut choisir de devenir un utilisateur identifié.

Mais comment cela fonctionne-t-il ?

Lorsqu'un utilisateur choisit de ne pas se connecter immédiatement, il est considéré comme étant un utilisateur anonyme. Ainsi, un utilisateur peut commencer immédiatement à ajouter des articles à un panier sans se connecter. Pour les utilisateurs anonymes, {{site.data.keyword.appid_short_notm}} crée un enregistrement utilisateur ad hoc et appelle l'API de connexion OAuth, qui renvoie des jetons d'accès et d'identité anonymes. Grâce à ces jetons, l'application peut créer, lire, mettre
à jour et supprimer les attributs stockés dans l'enregistrement
d'utilisateur.

![Trajet d'un utilisateur identifié lorsqu'il démarre en tant qu'anonyme.](/images/anon-authenticationtrail.png)

Lorsqu'un utilisateur anonyme se connecte, son jeton d'accès est transmis à l'API de connexion. Le service authentifie l'appel auprès d'un fournisseur d'identité. Le service utilise le jeton d'accès pour trouver l'enregistrement d'utilisateur anonyme, puis il lui associe l'identité. Les nouveaux jetons d'accès et d'identité contiennent les informations publiques partagées par le fournisseur d'identité. Une fois l'utilisateur identifié, son jeton d'accès anonyme n'est plus valide. L'utilisateur garde toutefois la faculté d'accéder à ses attributs, car ceux-ci sont accessibles avec le nouveau jeton.

Une identité peut être affectée à un enregistrement anonyme uniquement si elle n'est pas déjà affectée à un autre utilisateur.
{: tip}

Si l'identité est déjà associée à un autre utilisateur {{site.data.keyword.appid_short_notm}}, les jetons contiennent les informations de l'enregistrement de cet autre utilisateur et donnent accès à ses attributs. Les utilisateurs anonymes précédents et leurs attributs ne sont pas
accessibles via le nouveau jeton. Jusqu'à l'expiration du jeton, les informations sont toujours accessibles via le jeton d'accès anonyme. Pendant le développement,
vous pouvez choisir comment fusionner les attributs de l'utilisateur anonyme avec ceux de l'utilisateur
connu.
