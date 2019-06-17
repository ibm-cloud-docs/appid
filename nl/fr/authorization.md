---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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

# Concepts clés
{: #key-concepts}

Vous êtes perdus entre autorisation et authentification ? Vous n'êtes pas seul. Consultez les informations de cette page pour en savoir plus sur la terminologie, les processus et la manière dont le service utilise les jetons.
{: shortdesc}

Vous voulez en savoir plus sur les concepts de base de l'autorisation et de l'authentification ? Ne cherchez pas plus loin. Dans la vidéo suivante, vous pouvez en savoir plus sur OAuth 2.0, les types d'octroi, OIDC, et plus encore.

<iframe class="embed-responsive-item" id="about-appid-basics" title="A propos de {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/ndlk-ZhKGXM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


## Terminologie
{: #terms}

Ces termes clés peuvent vous aider à comprendre de quelle manière le service décompose le processus d'autorisation et d'authentification.

### OAuth 2
{: #term-oauth}
<a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> est un protocole à norme ouverte utilisé pour fournir une autorisation d'application.


### OIDC (Open ID Connect)
{: #term-oidc}

<a href="https://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> est une couche d'authentification qui fonctionne sur OAuth 2. Lorsque vous utilisez OIDC et {{site.data.keyword.appid_short_notm}} ensemble, les données d'identification de votre application permettent de configurer vos noeuds finaux. Lorsque vous utilisez le logiciel SDK, les URL des noeuds finaux sont générées automatiquement. Toutefois, vous pouvez aussi les générer vous-même en utilisant vos données d'identification du service. L'URL est au format suivant : noeud final du service {{site.data.keyword.appid_short_notm}} + "/oauth/v4" + /ID titulaire.

Exemple :

```
{
  "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
  "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
  "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
  "name":testing",
  "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
  "profilesUrl": "https://us-south.appid.cloud.ibm.com",
  "discoveryEndpoint": "https://us-south.appid.ibm.cloud.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
}
```
{: screen}

Sur la base de cet exemple, l'URL sera `https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0`. Vous y ajoutez ensuite le noeud final auquel vous voulez envoyer une demande. Consultez le tableau suivant pour quelques exemples de noeud final.

<table>
  <tr>
    <th>Noeud final</th>
    <th>Format</th>
  </tr>
  <tr>
    <td>Autorisation</td>
    <td>{oauthServerUrl}/authorization</td>
  </tr>
  <tr>
    <td>Token</td>
    <td>{oauthServerUrl}/token</td>
  </tr>
  <tr>
    <td>Informations utilisateur</td>
    <td>{oauthServerUrl}/userinfo</td>
  </tr>
  <tr>
    <td>JWKS</td>
    <td>{oauthServerUrl}/publickeys</td>
  </tr>
</table>

Lorsque vous utilisez le logiciel SDK, les URL des noeuds finaux sont générées automatiquement.
{: note}

### Jetons
{: #term-token}

Le service utilise trois types de jeton différents. Les jetons d'accès représentent une autorisation et permettent de communiquer avec des [ressources de back end](/docs/services/appid?topic=appid-backend) protégées par des filtres d'autorisation appliqués par {{site.data.keyword.appid_short}}. Les jetons d'identité représentent une authentification et contiennent des informations concernant l'utilisateur. Un jeton d'actualisation peut être utilisé pour obtenir un nouveau jeton d'accès sans nouvelle authentification de l'utilisateur. A l'aide des jetons d'actualisation, les utilisateurs peuvent autoriser l'application à mémoriser leurs informations. Ainsi, ils peuvent rester connectés. Les jetons sont définis dans **Fournisseurs d'identité > Gérer** du tableau de bord {{site.data.keyword.appid_short}}. Pour plus d'informations sur les jetons et leur utilisation dans {{site.data.keyword.appid_short}}, voir [Gestion des jetons](/docs/services/appid?topic=appid-tokens#tokens).

### En-têtes d'autorisation
{: #term-auth-header}

{{site.data.keyword.appid_short}} respecte la <a href="https://tools.ietf.org/html/rfc6750" target="blank">spécification du jeton du porteur<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et utilise une combinaison de jetons d'accès et d'identité envoyée sous forme d'en-tête d'autorisation HTTP. L'en-tête d'autorisation se compose de trois parties distinctes séparées par un espace. Les jetons sont codés en Base64. Le jeton d'identité est facultatif.

Exemple :

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


### Stratégie d'API
{: #term-api-strategy}

La stratégie d'API s'attend à ce que les demandes contiennent un en-tête d'autorisation avec un jeton d'accès valide. La demande peut également contenir un jeton d'identité, mais cela n'est pas obligatoire. Si un jeton n'est pas valide ou a expiré, la stratégie d'API renvoie une erreur HTTP 401 qui contient l'en-tête HTTP suivant :
```
Www-Authenticate=Bearer scope="{scope}" error="{error}"
```
{: screen}

Si la demande renvoie un jeton valide, le contrôle passe au middleware suivant et la propriété `appIdAuthorizationContext` est injectée dans l'objet de demande. Cette propriété contient les jetons d'accès et d'identité originaux, ainsi que les informations de contenu décodées sous forme d'objets JSON ordinaires.

### Stratégie d'application Web
{: #term-web-strategy}

Lorsque la stratégie d'application Web détecte des tentatives non autorisées d'accès à une ressource protégée, elle redirige automatiquement le navigateur de l'utilisateur vers la page d'authentification, qui peut être fournie par {{site.data.keyword.appid_short}}. Si l'authentification aboutit, l'utilisateur est ramené à l'URL de rappel de l'application Web. La stratégie d'application Web obtient des jetons d'accès et d'identité et les stocke dans une session HTTP sous `WebAppStrategy.AUTH_CONTEXT`. Il revient à l'utilisateur de décider de stocker ou non les jetons d'accès et d'identité dans la base de données de l'application.

### Séparation et chiffrement des données
{: #term-data-encryption}

{{site.data.keyword.appid_short_notm}} stocke et chiffre les attributs de profil utilisateur. Comme il s'agit d'un service partagé, chaque titulaire est associé à une clé de chiffrement dédiée et les données utilisateur de chaque titulaire sont chiffrées avec sa propre clé.

{{site.data.keyword.appid_short_notm}} garantit que les informations privées soient chiffrées avant leur stockage.
{: note}


### URI de redirection
{: #term-redirect}

{{site.data.keyword.appid_short_notm}} utilise une liste d'URI qualifiés complet approuvés pour rediriger vos utilisateurs après une interaction avec votre application. Par exemple, lorsque l'utilisateur a réussi à se connecter, {{site.data.keyword.appid_short_notm}} le redirige vers la page d'accueil de votre application ou toute autre page que vous avez désignée. Le format de votre URI peut changer en fonction de votre application. Pour plus d'informations, voir [Ajout d'URI de redirection](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).


### Jeu de clés Web JSON (JWKS)
{: #term-jwks}

Un jeu de clés JWKS représente un ensemble de clés cryptographiques. {{site.data.keyword.appid_short_notm}} utilise un jeu de clés JWKS pour vérifier l'authenticité des jetons que génère le service. En utilisant l'ID de clé pour vérifier la signature vous pouvez vous assurer que le jeton a été émis par une source digne de confiance, {{site.data.keyword.appid_short_notm}}, et que les informations qu'il contient n'ont jamais été modifiées.


