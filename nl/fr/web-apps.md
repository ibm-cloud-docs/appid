---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}
{:codeblock: .codeblock}


# Applications Web
{: #adding-web}

Avec {{site.data.keyword.appid_full}}, vous pouvez rapidement construire une couche d'authentification pour vos applications Web.
{: shortdesc}

## Comprendre le flux
{: #understanding}

**Dans quelles circonstances ce flux est-il utile ?**

Lorsque vous développez une application Web, vous pouvez utiliser le flux Web {{site.data.keyword.appid_short}} pour authentifier les utilisateurs en toute sécurité. Les utilisateurs peuvent ensuite accéder au contenu protégé côté serveur de vos applications Web.

**Quelle est la base technique du flux ?**

Les applications Web exigent souvent que les utilisateurs s'authentifient pour pouvoir accéder au contenu protégé. {{site.data.keyword.appid_short_notm}} utilise le flux de code d'autorisation OIDC pour authentifier les utilisateurs de manière sécurisée. Avec ce flux, l'application reçoit un code d'autorisation lorsqu'un utilisateur est authentifié. Ce code est ensuite échangé contre des jetons d'accès, d'identité et d'actualisation. Lors de l'étape d'échange de code, les jetons sont toujours envoyés via un canal de retour sécurisé entre l'application et le serveur OIDC. Cela permet d'avoir une couche de sécurité supplémentaire et empêche les pirates d'intercepter les jetons. Ces jetons peuvent être envoyés directement à l'application d'hébergement du serveur Web pour l'authentification d'utilisateur.

**Comment fonctionne ce flux ?**

![{{site.data.keyword.appid_short_notm}} - Flux d'une demande](images/web-flow.png)

1. Un utilisateur lance le flux d'autorisation en envoyant une demande au noeud final `/authorization` via le logiciel SDK ou l'API {{site.data.keyword.appid_short_notm}}.

2. Si l'utilisateur n'est pas autorisé, le flux d'authentification est démarré et redirigé vers {{site.data.keyword.appid_short_notm}}.

3. Selon les paramètres de demande `/authorization` ou la configuration du fournisseur d'identité de l'utilisateur, il lance le widget de connexion dans le navigateur de l'utilisateur.

4. L'utilisateur choisit un fournisseur d'identité pour l'authentification et effectue le processus de connexion.

5. Le fournisseur d'identité redirige vers l'application client avec le code d'autorisation.

6. Le logiciel SDK {{site.data.keyword.appid_short_notm}} échange le code d'autorisation contre des jetons d'accès et d'identité ainsi que des jetons d'actualisation facultatifs à partir du service {{site.data.keyword.appid_short_notm}}.

7. Les jetons sont sauvegardés par le logiciel SDK {{site.data.keyword.appid_short_notm}} et redirigés vers l'application client.

8. L'utilisateur est autorisé à accéder à l'application.

</br>
</br>

## Configuration du logiciel SDK Node.js
{: #configuring-nodejs}

Vous pouvez configurer {{site.data.keyword.appid_short_notm}} pour qu'il fonctionne avec vos applications Web Node.js.
{: shortdesc}

**Avant de commencer**

Vous devez disposer des prérequis suivants :

* Une instance du service {{site.data.keyword.appid_short_notm}}
* Un ensemble de données d'identification du service
* NPM version 4 ou ultérieure
* Noeud version 6 ou ultérieure
* Votre URI de redirection défini dans le tableau de bord du service {{site.data.keyword.appid_short_notm}}


### Installation du logiciel SDK Node.js

1. A l'aide de la ligne de commande, accédez au répertoire contenant votre application Node.js.

2. Installez le service {{site.data.keyword.appid_short_notm}}.
  ```bash
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### Initialisation du logiciel SDK Node.js

1. Ajoutez les définitions `require` suivantes à votre fichier `server.js` :

    ```javascript
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. Configurez votre application Express pour qu'elle utilise le middleware express-session. **Remarque** : vous devez configurer le middleware avec le stockage de session approprié pour les environnements de production. Pour plus d'informations, consultez
la <a href="https://github.com/expressjs/session" target="_blank">documentation expressjs <img src="../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

    ```javascript
    const app = express();
    app.use(session({
        secret: "123456",
        resave: true,
        saveUninitialized: true
        }));
    app.use(passport.initialize());
    app.use(passport.session());
    ```
    {: codeblock}

3. Transmettez vos données d'identification du service pour initialiser le logiciel SDK.

  ```javascript
    passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: codeblock}

   <table summary="Composantes de commande : applications Node.js">
      <caption>Composantes de commande pour les applications Node.js</caption>
        <tr>
          <th>Composantes</th>
          <th>Description</th>
        </tr>
      <tr>
          <td><i>tenantId</i> </br> <i>clientId</i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
          <td>Vous pouvez trouver ces valeurs en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service.</td>
      </tr>
      <tr>
        <td><i>redirectUri</i></td>
        <td>La valeur de l'URI de redirection peut être fournie de trois façons : </br>
            1. Manuellement, dans la nouvelle valeur `WebAppStrategy({redirectUri: "...."})`</br>
            2. Sous forme de variable d'environnement nommée `redirectUri`</br>
            3. Si aucune de ces options n'est fournie, le logiciel SDK {{site.data.keyword.appid_short_notm}} tente d'extraire l'URI `application_uri` de l'application s'exécutant sous {{site.data.keyword.Bluemix_notm}} et d'ajouter le suffixe par défaut `/ibm/cloud/appid/callback`.
        </td>
      </tr>
    </table>

4. Configurez passport avec la sérialisation et la désérialisation. Cette étape de configuration est requise pour la persistance de session authentifiée dans les demandes HTTP. Pour plus d'informations, voir la <a href="http://passportjs.org/docs" target="_blank">documentation de passport <img src="../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

  ```javascript
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. Ajoutez le code suivant à votre fichier `server.js` pour émettre les redirections de service.

   ```javascript
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   ```
   {: codeblock}

6. Enregistrez votre noeud final protégé.

   ```javascript
   app.get(‘/protected’, passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res) res.json(req.user); });
   ```
   {: codeblock}

Pour plus d'informations, voir le <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">référentiel GitHub Node.js pour {{site.data.keyword.appid_short_notm}} <img src="../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

</br>
</br>

## Configuration du logiciel SDK Liberty for Java
{: #configuring-liberty}

Vous pouvez configurer {{site.data.keyword.appid_short_notm}} pour qu'il fonctionne avec vos applications Web Liberty for Java.
{:shortdesc}

**Avant de commencer**

Vous devez disposer des prérequis suivants :
* Une instance du service {{site.data.keyword.appid_short_notm}}
* Un ensemble de données d'identification du service
* Apache Maven version 3.5 ou ultérieure
* Java 1.8
* Application Web Liberty for Java

### Installation du logiciel SDK Liberty for Java

1. Ajoutez une fonction OpenID Connect à votre fichier `server.xml`.

  ```xml
  <featureManager>
      <feature>ssl-1.0</feature>
      <feature>appSecurity-2.0</feature>
      <feature>openidConnectClient-1.0</feature>
  </featureManager>
  ```
  {: codeblock}

2. Créez une fonction Open ID Connect Client et définissez les espaces réservés suivants. Utilisez les données d'identification du service pour remplir les espaces réservés.

  ```xml
  <openidConnectClient
    clientId='App ID client_ID'
    clientSecret='App ID Secret'
    authorizationEndpointUrl='oauthServerUrl/authorization'
    tokenEndpointUrl='oauthServerUrl/token'
    jwkEndpointUrl='oauthServerUrl/publickeys'
    issuerIdentifier='Changed according to the region'
    tokenEndpointAuthMethod="basic"
    signatureAlgorithm="RS256"
    authFilterid="myAuthFilter"
    trustAliasName="my.bluemix.certificate"
  />
  ```
  {: codeblock}

  <table>
  <caption>Tableau. Variables d'élément OIDC pour les applications Liberty for Java</caption>
    <tr>
      <th> Composant</th>
      <th> Description </th>
    </tr>
    <tr>
    <td><code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
    <td>Vous pouvez trouver ces valeurs en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service.</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td>
      <td> Ajoutez `/authorization` à la fin de oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td>
      <td>Ajoutez `/token` à la fin de oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td>
      <td>Ajoutez `/publickeys` à la fin de oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td>
      <td>Varie en fonction de votre région. Il peut s'agir de l'une des valeurs suivantes : </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td>
      <td>Spécifié en tant que "basic".</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td>
      <td>Spécifié en tant que "RS256".</td>
    </tr>
    <tr>
      <td><code> authFilterid </code></td>
      <td>Liste des ressources à protéger.</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td>
      <td>Nom de votre certificat dans le magasin de clés de confiance.</td>
    </tr>
  </table>

### Initialisation du logiciel SDK Liberty for Java

1. Dans votre fichier `server.xml`, définissez un filtre d'autorisation pour spécifier des ressources protégées. Si aucun filtre n'est <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">défini <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>, le service protège toutes les ressources.

  ```xml
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

2. Définissez votre type de sujet spécial en tant que `ALL_AUTHENTICATED_USERS`.

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample"
  location="${server.config.dir}/apps/libertySample-1.0.0.war">
    <application-bnd>
        <security-role name="myrole">
        <special-subject type="ALL_AUTHENTICATED_USERS"/>
        </security-role>
            </application-bnd>
        </application>
  ```
  {: codeblock}

3. Téléchargez le fichier `libertySample-1.0.0.war` depuis <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/liberty-for-java" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et placez-le dans le dossier des applications de votre serveur. Par exemple, si votre serveur s'appelle defaultServer, le fichier war se trouvera ici `target/liberty/wlp/usr/servers/defaultServer/apps/`.

4. Configurez SSL en ajoutant ce qui suit à votre fichier `server.xml`. Vous devrez également créer un magasin de clés de confiance.

```xml
  <keyStore id="defaultKeyStore" password="myPassword"/>
  <keyStore id="appidtruststore" password="Liberty" location="${server.config.dir}/mytruststore.jks"/>
  <ssl id="defaultSSLConfig" keyStoreRef="defaultKeyStore" trustStoreRef="appidtruststore"/>
```
{: codeblock}

Par défaut, la configuration SSL nécessite que le magasin de clés de confiance soit configuré pour OpenID Connect. En savoir plus sur la <a href="https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_config_oidc_rp.html" target="_blank">configuration d'un client OpenID Connect dans Liberty <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
{: tip}

</br>
</br>

## Configuration du logiciel SDK Spring Boot for Java
{: #configuring-spring-boot}

Vous pouvez configurer {{site.data.keyword.appid_short_notm}} pour qu'il fonctionne avec vos applications Spring Boot.
{:shortdesc}

**Avant de commencer**

Vous devez disposer des prérequis suivants :

* Une instance du service {{site.data.keyword.appid_short_notm}}
* Un ensemble de données d'identification du service
* Un projet Java + Maven
* Apache Maven version 3.5 ou ultérieure
* Java 1.8
* Spring Boot version 2.0 et Security OAuth version 2.0 ou ultérieure


### Initialisation de l'infrastructure Spring Boot

1. Ajoutez ce qui suit entre les balises `<project> </project>` dans votre fichier Maven `pom.xml`.

  ```xml
  <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.2.RELEASE</version>
      <relativePath/>
  </parent>
  ```
  {: codeblock}

2. Ajoutez les dépendances suivantes à votre fichier Maven `pom.xml`.

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-web</artifactId>
      </dependency>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-security</artifactId>
      </dependency>
      <dependency>
          <groupId>org.springframework.security.oauth.boot</groupId>
          <artifactId>spring-security-oauth2-autoconfigure</artifactId>
          <version>2.0.0.RELEASE</version>
      </dependency>
  </dependencies>
  ```
  {: codeblock}

3. Dans le même fichier, incluez le plug-in Maven.

  ```xml
  <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
  </plugin>
  ```
  {: codeblock}

### Initialisation d'OAuth2

1. Ajoutez les annotations suivantes à votre fichier Java.

  ```java
  @SpringBootApplication
  @EnableOAuth2Sso
  ```
  {: codeblock}

2. Etendez la classe avec `WebSecurityConfigurerAdapter`.
3. Remplacez toutes les configurations de sécurité et enregistrez votre noeud final protégé.

  ```java
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .antMatchers("/protectedResource").authenticated()
                .and().logout().logoutSuccessUrl("/").permitAll();
    }
  ```
  {: codeblock}


### Ajout de données d'identification

1. Ajoutez un fichier de configuration `application.yml` au répertoire `/springbootsample/src/main/resources/`. Vous pouvez compléter votre configuration avec les informations provenant de vos données d'identification du service.

  ```
  security:
  oauth2:
    client:
      clientId: {client ID}
      clientSecret: {client Secret}
      accessTokenUri: {oauthServerUrl}/token
      userAuthorizationUri: {oauthServerUrl}/authorization
    resource:
      userInfoUri: {oauthServerUrl}/userinfo
  ```
  {: codeblock}


Pour un exemple étape par étape, consultez <a href="https://www.ibm.com/blogs/bluemix/2018/06/creating-spring-boot-applications-app-id/" target="_blank">ce blogue </a>!

</br>
</br>

## Utilisation d'{{site.data.keyword.appid_short_notm}} dans d'autres langues
{: #other}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} dans d'autres langues avec un logiciel SDK client compatible OIDC. Pour plus d'informations, consultez la liste des <a href="https://openid.net/developers/certified/">bibliothèques certifiées</a>.


</br>
</br>

## Etapes suivantes
{: #next}

{{site.data.keyword.appid_short_notm}} est installé dans votre application ? Vous êtes pratiquement prêt à commencer l'authentification des utilisateurs ! Essayez d'effectuer l'une des activités suivantes :

* Configurer vos [fournisseurs d'identité](/docs/services/appid/identity-providers.html)
* Personnaliser et configurer [le widget de connexion](/docs/services/appid/login-widget.html)
* En savoir plus sur le <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">logiciel SDK Node.js<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
