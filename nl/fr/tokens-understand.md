---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

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



# Comprendre les jetons
{: #tokens}

Lorsqu'un utilisateur est authentifié avec succès, l'application reçoit des jetons d'{{site.data.keyword.appid_short_notm}}. Le service utilise trois principaux types de jeton pour exécuter le processus d'authentification.
{: shortdesc}


## Accès aux jetons
{: #access}

Les jetons d'accès représentent une autorisation et permettent de communiquer avec des [ressources de back end](/docs/services/appid?topic=appid-backend) protégées par des filtres d'autorisation appliqués par {{site.data.keyword.appid_short}}. Le jeton est conforme aux spécifications JOSE (JavaScript Object Signing et Encryption). Les jetons sont formatés en tant que <a href="https://jwt.io/introduction/" target="blank">jetons Web JSON <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et sont signés avec une clé Web JSON qui utilise l'algorithme RS256.

Exemple de jeton :
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
  }
  ```
  {: screen}

## Que sont les jetons d'identité ?
{: #identity}

Les jetons d'identité représentent une authentification et contiennent des informations concernant l'utilisateur. Ils peuvent vous donner des informations sur son nom, son adresse électronique, son sexe et son emplacement. Ils peuvent également renvoyer une URL à une image de l'utilisateur. Les jetons sont formatés en tant que <a href="https://jwt.io/introduction/" target="blank">jetons Web JSON <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et sont signés avec une clé Web JSON qui utilise l'algorithme RS256.

Exemple de jeton :
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "exp": 1551903163,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "iat": 1551899553,
    "email": "appid155@mailinator.com",
    "name": "appid155@mailinator.com",
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "identities": [
      {
        "provider": "cloud_directory",
        "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
    ],
    "amr": [
      "cloud_directory"
    ]
  }
  ```
  {: screen}


Les jetons d'identité ne contiennent que des informations utilisateur partielles. Pour voir toutes les informations fournies par le fournisseur d'identité, vous pouvez utiliser le noeud final [/userinfo](/docs/services/appid?topic=appid-predefined-attributes#predefined-access-api).

## Que sont les jeton d'actualisation ?
{: #refresh}

{{site.data.keyword.appid_short}} permet d'acquérir de nouveaux jetons d'accès et d'identité sans nouvelle authentification, comme défini dans <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Un jeton d'actualisation peut être utilisé pour renouveler le jeton d'accès afin qu'un utilisateur n'ait à effectuer aucune action pour se connecter, telle que fournir des données d'identification. Similaires aux jetons d'accès, les jetons d'actualisation contiennent des données qui permettent à {{site.data.keyword.appid_short_notm}} de déterminer si vous êtes autorisé. Cependant, ces jetons sont opaques.

Les jetons d'actualisation sont configurés pour avoir une durée de vie supérieure à celle d'un jeton d'accès normal. Ainsi, lorsqu'un jeton d'accès expire, le jeton d'actualisation reste valide et peut être utilisé pour le renouveler. Les jetons d'actualisation d'{{site.data.keyword.appid_short_notm}} peuvent être configurés pour durer de 1 à 90 jours. Pour tirer le meilleur parti des jetons d'actualisation, conservez-les pendant toute leur durée de vie ou jusqu'à ce qu'ils soient renouvelés. Un utilisateur ne peut pas accéder directement à des ressources avec un simple jeton d'actualisation, ce qui rend ce jeton beaucoup plus sûr à conserver qu'un jeton d'accès. En tant que meilleure pratique, les jetons d'actualisation doivent être stockés de manière sécurisée par le client qui les a reçus et envoyés uniquement au serveur d'autorisation qui les a émis.

Pour plus de commodité, {{site.data.keyword.appid_short_notm}} renouvelle également son jeton d'actualisation — et sa date d'expiration — lorsque le jeton d'accès est renouvelé, permettant ainsi à l'utilisateur de rester connecté tant qu'il est actif à un moment donné avant l'expiration du jeton d'actualisation actuel. Par contre, si vous souhaitez utiliser des jetons d'actualisation tout en obligeant l'utilisateur à se connecter régulièrement, votre application ne pourra utiliser que les jetons d'actualisation renvoyés lorsque l'utilisateur se connecte en saisissant ses données d'identification. Nous vous recommandons cependant de toujours utiliser le dernier jeton d'actualisation reçu d'{{site.data.keyword.appid_short_notm}}, comme indiqué dans les <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">spécifications OAuth 2.0<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


Bien que ces jetons puissent simplifier le processus de connexion, votre application ne doit pas en dépendre, car ils peuvent être révoqués à tout moment, par exemple lorsque vous pensez que vos jetons d'actualisation ont été compromis. Il existe deux méthodes permettant de révoquer un jeton d'actualisation en cas de besoin. Si vous disposez d'un jeton d'actualisation, vous pouvez le révoquer selon la norme <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Sinon, si vous disposez de l'ID utilisateur, vous pouvez révoquer le jeton d'actualisation à l'aide de l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">API de gestion <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Pour plus d'informations sur l'accès à l'API de gestion, voir [Gestion de l'accès au service](/docs/services/appid?topic=appid-service-access-management#service-access-management).

Pour des exemples d'utilisation des jetons d'actualisation et de leur utilisation en vue d'implémenter une fonctionnalité remember-me, consultez [getting started samples](/docs/services/appid?topic=appid-getting-started#getting-started).


## D'où proviennent les jetons ?
{: #where}

Les jetons sont émis via le serveur OAuth {{site.data.keyword.appid_short_notm}} et sont formatés en tant que [jetons Web JSON (JWT)](https://jwt.io/introduction/). Ils sont signés avec une [clé Web JSON (JWK)](https://tools.ietf.org/html/rfc7517) à l'aide de l'algorithme RS256.

## Qu'advient-il des informations contenues dans le jeton ?
{: #contains}

Le jeton d'accès contient un ensemble de réclamations JWT standard et un ensemble de réclamations spécifiques à {{site.data.keyword.appid_short_notm}} telles qu'un ID titulaire. Le jeton d'identité contient des informations spécifiques à l'utilisateur. Les informations contenues dans les jetons sont stockées en tant que réclamations dans un [profil utilisateur](/docs/services/appid?topic=appid-user-profile#user-profile).

## Comment les jetons sont-ils reçus ?
{: #received}

Les jetons sont reçus par votre application après une authentification réussie. Votre application peut utiliser les jetons pour récupérer des informations sur l'autorisation et l'authentification de l'utilisateur. Le jeton d'accès peut être utilisé pour accéder aux ressources protégées en envoyant une demande à la ressource. Dans la demande, le jeton d'accès est décrit dans le [schéma d'authentification  Bearer](https://tools.ietf.org/html/rfc6750#page-5). Votre application doit analyser l'en-tête pour pouvoir extraire les jetons.

Exemple de demande :

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## Comment les jetons sont-ils définis ?
{: #set}

Les configurations des jetons peuvent être activées et désactivées via le tableau de bord {{site.data.keyword.appid_short_notm}}. Pour plus d'informations sur vos options de configuration, voir [Gestion des jetons](/docs/services/appid?topic=appid-managing-idp#managing-idp).
