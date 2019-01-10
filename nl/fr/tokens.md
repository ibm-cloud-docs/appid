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


# Validation des jetons
{: #token-validation}

La validation des jetons est une partie importante dans le processus de développement des applications modernes. Elle vous permet de protéger votre application ou vos API des utilisateurs non autorisés. {{site.data.keyword.appid_full}} utilise des jetons d'accès et d'identité pour s'assurer qu'un utilisateur ou une application est authentifié avant de lui accorder un droit d'accès. Si vous utilisez l'un des logiciels SDK fournis par {{site.data.keyword.appid_short_notm}}, l'obtention et la validation de vos jetons sont effectuées pour vous !
{: shortdesc}

Pour plus d'informations sur l'utilisation des jetons dans {{site.data.keyword.appid_short_notm}}, voir [Understanding tokens](authorization.html#tokens).
{: tip}

**Qu'est-ce que la validation des jetons ?**

Les jetons sont utilisés pour vérifier qu'une personne est bien qui elle dit être. Ils confirment toutes les autorisations d'accès éventuellement détenues par l'utilisateur pour une durée déterminée. Lorsqu'un utilisateur se connecte à votre application et se voit attribuer un jeton, votre application doit valider l'utilisateur avant que l'accès ne lui soit accordé.

</br>

**Que faire si j'utilise une langue dans laquelle {{site.data.keyword.appid_short_notm}} ne dispose pas de logiciel SDK ?**

Ne vous inquiétez pas ! Trois options s'offrent à vous :

* Travailler avec les API {{site.data.keyword.appid_short_notm}}
* Implémenter votre propre logique de validation
* Utiliser n'importe quel logiciel SDK open source compatible OIDC

D'après les commentaires reçus, l'option 1 est généralement le moyen le plus simple.
{: tip}

</br>
</br>

## Utilisation des API {{site.data.keyword.appid_short_notm}}
{: #remote-validation}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} pour valider vos jetons à l'aide de l'introspection.
{: shortdesc}

1. Envoyez une requête POST au noeud final de l'API [/introspect](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/introspect) pour valider votre jeton. La demande doit fournir le jeton et un en-tête d'autorisation de base contenant l'ID client et la valeur confidentielle.

  Exemple de demande :

    ```
    POST /oauth/v3/{tenant_id}/introspect HTTP/1.1
    Host: appid-oauth.ng.bluemix.net
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. Le serveur vérifie la date d'expiration et la signature du jeton et renvoie un objet JSON indiquant si le jeton est actif ou inactif.

  Exemple de réponse :

    ```
    {
      "active": true
    }
    ```
    {: screen}


## Validation manuelle des jetons
{: #local-validation}

Vous pouvez valider vos jetons localement en les analysant, en vérifiant leur signature et en validant les réclamations qui y sont stockées.
{: shortdesc}


1. Analysez les jetons. Le [jeton Web JSON (JWT)](https://tools.ietf.org/html/rfc7519) est un moyen standard de transmettre des informations en toute sécurité. Il comporte trois parties principales, l'en-tête, le contenu et la signature, qui sont codées au format base64URL et séparées par des points(.). Vous pouvez utiliser n'importe quel décodeur base64URL disponible pour analyser le jeton. Vous pouvez également utiliser l'une des [bibliothèques répertoriées](https://jwt.io/#libraries-io) pour analyser le jeton.

  Exemple de jeton codé :

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  Exemple d'en-tête décodé :

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  Contenu décodé :

    ```
    {
      "iss": "appid-oauth",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. Appelez le [noeud final /publickeys](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/publicKeys) pour extraire vos clés publiques. Les clés publiques renvoyées sont au format [JSON Web Keys (JWK)](https://tools.ietf.org/html/rfc7517).

  Exemple de demande :

    ```
    GET /oauth/v3/{tenant_id}/publickeys HTTP/1.1
    Host: appid-oauth.ng.bluemix.net
    Cache-Control: no-cache
    ```
    {: screen}

3. Stockez les clés dans le cache de votre application pour une utilisation ultérieure. Le stockage des clés accélère le processus et évite les retards sur le réseau si un autre appel est passé.

4. Importez les paramètres de clé publique.

  Exemple de réponse :

    ```]
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres de clé publique </th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>Définit l'algorithme utilisé.</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>Définit le but de la clé.</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>Définit l'ID unique de la clé.</td>
      </tr>
      <tr>
        <td>Autre</td>
        <td>Il peut y avoir d'autres paramètres spécifiques à votre algorithme qui doivent également être importés.</td>
      </tr>
    </tbody>
  </table>

5. Vérifiez la signature du jeton. L'en-tête du jeton contient l'algorithme qui a été utilisé pour signer le jeton et l'ID de clé ou la réclamation `kid` de la clé publique correspondante. Comme les clés publiques ne changent pas souvent, vous pouvez les mettre en cache dans votre application et les actualiser de temps en temps. Si votre clé en cache ne contient pas la réclamation `kid`, vous pouvez valider les jetons en local.

  1. Demandez à votre application de vérifier que le contenu de l'en-tête du jeton entrant correspond aux paramètres de la clé publique.
  2. Vérifiez tout particulièrement que les mêmes algorithmes ont été utilisés et que votre cache de clé publique contient une clé avec l'ID de clé approprié.
  3. Assurez-vous que votre valeur hachée est identique à la signature du formulaire PEM de la clé publique. Votre valeur hachée peut être obtenue en combinant et en hachant l'en-tête du contenu du jeton. Ce processus pouvant être complexe à implémenter manuellement, il peut être utile d'utiliser l'une des [bibliothèques répertoriées](https://jwt.io/) pour valider la signature.

6. Validez les réclamations stockées dans les jetons. Pour vérifier les futures vérifications, vous pouvez utiliser [cette liste](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Réclamations devant être validées </th>
    </thead>
    <tbody>
      <tr>
        <td><code>iss</code></td>
        <td>L'émetteur doit être identique à celui du serveur OAuth {{site.data.keyword.appid_short_notm}}.</td>
      </tr>
      <tr>
        <td><code>exp</code></td>
        <td>L'heure actuelle doit être antérieure à l'heure d'expiration.</td>
      </tr>
      <tr>
        <td><code>aud</code></td>
        <td>L'audience doit contenir l'ID client de votre application.</td>
      </tr>
      <tr>
        <td><code>tenant</code></td>
        <td>Le titulaire doit contenir l'ID titulaire de votre application.</td>
      </tr>
      <tr>
        <td><code>scope</code></td>
        <td>Portée des droits accordés à l'utilisateur. Spécifique au jeton d'accès.</td>
      </tr>
    </tbody>
  </table>

</br>
</br>
