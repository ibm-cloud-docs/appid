---

copyright:
  years: 2017, 2021
lastupdated: "2021-07-12"

keywords: web apps, authorization code, authentication, nodejs, javascript, app access, application credentials, login, redirect uri, protected endpoint, video

subcollection: appid

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}


# Web apps
{: #web-apps}

When you are developing a web application, you can use the {{site.data.keyword.appid_full}} web flow to securely authenticate users. Users are then able to access your server-side protected content in your web apps.
{: shortdesc}

## Understanding the flow
{: #understanding-web-flow}


Web apps often require users to authenticate in order to access protected content. {{site.data.keyword.appid_short_notm}} uses the OIDC authorization code flow to securely authenticate users. With this flow, when the user is authenticated, the app receives an authorization code. The code is then exchanged for an access, identity, and refresh token. In code, exchange step the tokens are always sent via a secure backchannel between the app and the OIDC server. This provides an extra layer of security as the attacker is not able to intercept the tokens. These tokens can be sent directly to the web server hosting application for user authentication.


![{{site.data.keyword.appid_short_notm}} web app request flow](images/web-flow.png){: caption="Figure 1. {{site.data.keyword.appid_short_notm}} web app request flow" caption-side="bottom"}

1. A user initiates the authorization flow by sending a request to the `/authorization` endpoint via the {{site.data.keyword.appid_short_notm}} SDK or API.

2. If the user is unauthorized, the authentication flow is started with a redirect to {{site.data.keyword.appid_short_notm}}.

3. Depending on the user's `/authorization` request parameters or identity provider configuration, it starts the Login Widget in the user's browser.

4. The user chooses an identity provider to authenticate with and completes the sign-in process.

5. The identity provider redirects to the client app with the authorization code.

6. The {{site.data.keyword.appid_short_notm}} SDK exchanges the authorization code for access, identity, and optional refresh tokens from the {{site.data.keyword.appid_short_notm}} service.

7. The tokens are saved by the {{site.data.keyword.appid_short_notm}} SDK and a redirect to the client application occurs.

8. The user is granted access to the app.


## Configuring the Node.js SDK
{: #web-configuring-nodejs}

You can configure {{site.data.keyword.appid_short_notm}} to work with your Node.js web applications.
{: shortdesc}

### Before you begin
{: #web-configure-node-begin}

You must have the following prerequisites:

* An instance of the {{site.data.keyword.appid_short_notm}} service
* A set of service credentials
* NPM version 4 or higher
* Node version 6 or higher
* Your redirect URI set in the {{site.data.keyword.appid_short_notm}} service dashboard


Check out the following video to learn about protecting Node applications with {{site.data.keyword.appid_short_notm}}. Then, try it out yourself by using a [simple Node sample app](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02a-simple-node-web-app){: external}.

![About {{site.data.keyword.appid_short_notm}}](https://www.youtube.com/embed/6roa1ZOvwtw){: video output="iframe" data-script="none" id="about-appid" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

### Installing the Node.js SDK
{: #web-nodejs-install}

1. By using the command line, change to the directory that contains your Node.js app.

2. Install the {{site.data.keyword.appid_short_notm}} service.

  ```bash
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### Initializing the Node.js SDK
{: #web-nodejs-initialize}

1. Add the following `require` definitions to your `server.js` file.

  ```javascript
  const express = require('express');
  const session = require('express-session')
  const passport = require('passport');
  const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
  const CALLBACK_URL = "/ibm/cloud/appid/callback";
  ```
  {: codeblock}

2. Set up your express app to use express-session middleware.

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

  You must configure the middleware with the proper session storage for production environments. For more information, see the [express.js](https://expressjs.com/){: external}.
  {: note}

3. Obtain your credentials in one of the following ways.

  * By navigating to the **Applications** tab of the {{site.data.keyword.appid_short_notm}} dashboard. If you don't have an application in the list, you can click **Add application** to create a one.

  * By making a POST request to the [`/management/v4/{tenantId}/applications` endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication){: external}.

    Request format:
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer <IAM_TOKEN>' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    Example response:
    ```
    {
    "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
    "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
    "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
    "name": "ApplicationName",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61"
    }
    ```
    {: screen}

4. Optional: Decide how to format your redirect URI. The redirect can be formatted in two different ways.

  * Manually in a new `WebAppStrategy({redirectUri: "...."})`
  * As an environment variable named `redirectUri`

  If neither are provided, the {{site.data.keyword.appid_short_notm}} SDK tries to retrieve the `application_uri` of the app that is running on {{site.data.keyword.cloud_notm}} and append a default suffix `/ibm/cloud/appid/callback`.

5. By using the information obtained in the previous steps, initialize the SDK.

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

6. Configure passport with serialization and deserialization. This configuration step is required for authenticated session persistence across HTTP requests. For more information, see the <a href="http://www.passportjs.org/docs/" target="_blank">passport docs <img src="../icons/launch-glyph.svg" alt="External link icon"></a>.

  ```javascript
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. Add the following code to your `server.js` file to issue the service redirects.

   ```javascript
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   ```
   {: codeblock}

6. Register your protected endpoint by adding the following code snippet into your `app.js` file.

   ```javascript
   app.get(‘/protected_resource’, passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res) {res.json(req.user); });
   ```
   {: codeblock}

For more information, see the <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub repository <img src="../icons/launch-glyph.svg" alt="External link icon"></a>.



## Configuring the Liberty for Java SDK
{: #web-configuring-liberty}

You can configure {{site.data.keyword.appid_short_notm}} to work with your Liberty for Java web applications.
{:shortdesc}

### Before you begin
{: #web-configure-liberty-before}

You must have the following prerequisites:
* An instance of the {{site.data.keyword.appid_short_notm}} service
* A set of service credentials
* Apache Maven 3.5 or higher
* Java 1.8
* A Liberty for Java web application


Check out the following video to learn about protecting Liberty for Java applications with {{site.data.keyword.appid_short_notm}}. Then, try it out yourself by using a [simple Liberty for Java sample app](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02c-simple-liberty-web-app).


![About {{site.data.keyword.appid_short_notm}}](https://www.youtube.com/embed/o_Er69YUsMQ){: video output="iframe" data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}


### Installing the Liberty for Java SDK
{: #web-liberty-install}

1. Add an OpenID Connect feature to your `server.xml`.

  ```xml
  <featureManager>
      <feature>ssl-1.0</feature>
      <feature>appSecurity-2.0</feature>
      <feature>openidConnectClient-1.0</feature>
  </featureManager>
  ```
  {: codeblock}

2. Obtain your credentials in one of two ways.

  * By navigating to the **Applications** tab of the {{site.data.keyword.appid_short_notm}} dashboard. If you don't already have one, you can click **Add application** to create a new one.

  * By making a POST request to the [`/management/v4/{tenantId}/applications` endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication){: external}.

    Request format:
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    Example response:
    ```
    {
    "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
    "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
    "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
    "name": "ApplicationName",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61"
    }
    ```
    {: screen}

3. Create an Open ID Connect Client feature and define the following placeholders. Use the service credentials to fill the placeholders.

  ```xml
  <openidConnectClient
    clientId='{{site.data.keyword.appid_short_notm}} client_ID'
    clientSecret='{{site.data.keyword.appid_short_notm}} Secret'
    authorizationEndpointUrl='oauthServerUrl/authorization'
    tokenEndpointUrl='oauthServerUrl/token'
    jwkEndpointUrl='oauthServerUrl/publickeys'
    issuerIdentifier='Changed according to the region'
    tokenEndpointAuthMethod="basic"
    signatureAlgorithm="RS256"
    authFilterid="myAuthFilter"
    trustAliasName="ibm.com"
  />
  ```
  {: codeblock}

  <table>
  <caption>Table. OIDC element variables for Liberty for Java apps</caption>
    <tr>
      <th> Component </th>
      <th> Description </th>
    </tr>
    <tr>
    <td><code>clientID</code> </br> <code>secret</code> </br> <code>oauth-server-url</code> </br></td>
    <td>Complete step two to obtain your service credentials.</td>
    </tr>
    <tr>
      <td><code>authorizationEndpointURL</code></td>
      <td> Add <code>/authorization</code> to the end of your <code>oauthServerURL</code>.</td>
    </tr>
    <tr>
      <td><code>tokenEndpointUrl</code></td>
      <td>Add <code>/token</code> to the end of your <code>oauthServerURL</code>.</td>
    </tr>
    <tr>
      <td><code>jwkEndpointUrl</code></td>
      <td>Add <code>/publickeys</code> to the end of your <code>oauthServerURL</code>.</td>
    </tr>
    <tr>
      <td><code>issuerIdentifier</code></td>
      <td>The issuer identifier takes the following form: <code>&lt;region>&gt;.cloud.ibm.com</code>. Learn more about the <a href="/docs/appid?topic=appid-regions-endpoints">available regions</a>.</td>
    </tr>
    <tr>
      <td><code>tokenEndpointAuthMethod</code></td>
      <td>Specified as "basic".</td>
    </tr>
    <tr>
      <td><code>signatureAlgorithm</code></td>
      <td>Specified as "RS256".</td>
    </tr>
    <tr>
      <td><code>authFilterid</code></td>
      <td>The list of resources to protect.</td>
    </tr>
    <tr>
      <td><code>trustAliasName</code></td>
      <td>The name of your certificate within your truststore.</td>
    </tr>
  </table>

### Initializing the Liberty for Java SDK
{: #web-liberty-initialize}

1. In your `server.xml` file, define an authorization filter to specify protected resources. If a filter is not [defined](https://www.ibm.com/docs/en/was-liberty/core?topic=liberty-authentication-filters){: external}, the service protects all resources.

  ```xml
  <authFilter id="myAuthFilter">
      <requestUrl id="myRequestUrl" urlPattern="/protected_resource" matchType="contains"/>
  </authFilter>
  ```
  {: codeblock}

2. Define your special subject type as `ALL_AUTHENTICATED_USERS`.

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample" location="${server.config.dir}/apps/libertySample-1.0.0.war">
      <application-bnd>
          <security-role name="myrole">
              <special-subject type="ALL_AUTHENTICATED_USERS"/>
          </security-role>
      </application-bnd>
  </application>
  ```
  {: codeblock}

3. Download the `libertySample-1.0.0.war` file from [GitHub](https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/liberty-for-java){: external} and place it in your server's apps folder. For example, if your server is named `defaultServer`, the war file would go here `target/liberty/wlp/usr/servers/defaultServer/apps/`.

4. Configure SSL by adding the following to your `server.xml` file. You also need to create a truststore.

  ```xml
    <keyStore id="defaultKeyStore" password="myPassword"/>
    <keyStore id="appidtruststore" password="Liberty" location="${server.config.dir}/mytruststore.jks"/>
    <ssl id="defaultSSLConfig" keyStoreRef="defaultKeyStore" trustStoreRef="appidtruststore"/>
  ```
  {: codeblock}

By default SSL configuration requires the truststore be configured for OpenID Connect. Learn more about [configuring an OpenID Connect Client in Liberty](https://www.ibm.com/docs/en/was-liberty/base?topic=connect-configuring-openid-client-in-liberty){: external}.
{: tip}



## Configuring Spring Boot for Java SDK
{: #web-configuring-spring-boot}

You can configure {{site.data.keyword.appid_short_notm}} to work with your Spring Boot applications.
{:shortdesc}

### Before you begin
{: #web-configure-spring-boot-before}

You must have the following prerequisites:

* An instance of the {{site.data.keyword.appid_short_notm}} service
* A set of service credentials
* A Java + Maven project
* Apache Maven 3.5 or higher
* Java 1.8
* Spring Boot 2.0 and Security OAuth 2.0 or higher


### Initializing the Spring Boot framework
{: #web-spring-boot-initialize}

1. Add the following between the `<project> </project>` tags in your Maven `pom.xml` file.

  ```xml
  <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.2.RELEASE</version>
      <relativePath/>
  </parent>
  ```
  {: codeblock}

2. Add the following dependencies to your Maven `pom.xml` file.

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

3. In the same file, include the Maven plug-in.

  ```xml
  <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
  </plugin>
  ```
  {: codeblock}

### Initializing OAuth2
{: #web-oauth-initialize}

1. Add the following annotations to your Java file.

  ```java
  @SpringBootApplication
  @EnableOAuth2Sso
  ```
  {: codeblock}

2. Extend the class with `WebSecurityConfigurerAdapter`.
3. Override any security configuration and register your protected endpoint.

  ```java
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .antMatchers("/protected_Resource").authenticated()
                .and().logout().logoutSuccessUrl("/").permitAll();
    }
  ```
  {: codeblock}


### Adding credentials
{: #web-spring-boot-credentials}

1. Obtain your credentials in one of the following ways.

  * By navigating to the **Applications** tab of the {{site.data.keyword.appid_short_notm}} dashboard. If you don't already have one, you can click **Add application** to create a new one.

  * By making a POST request to the [`/management/v4/{tenantId}/applications` endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication).

    Request format:
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    Example response:
    ```
    {
    "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
    "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
    "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
    "name": "ApplicationName",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61"
    }
    ```
    {: screen}

2. Add an `application.yml` configuration file to the `/springbootsample/src/main/resources/` directory. You can complete your configuration with the information from your service credentials.

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

For a step-by-step example, check out <a href="https://www.ibm.com/cloud/blog/creating-spring-boot-applications-app-id" target="_blank">this blog</a>!


## Using {{site.data.keyword.appid_short_notm}} with other languages
{: #web-other-languages}

With an OIDC-compliant client SDK, you can use {{site.data.keyword.appid_short_notm}} with other languages. Check out the list of <a href="https://openid.net/developers/certified/">certified libraries</a> for more information.

## Next steps
{: #web-next}

With {{site.data.keyword.appid_short_notm}} installed in your application, you're almost ready to start authenticating users! Try doing one of the following activities next:

* Configure your [identity providers](/docs/appid?topic=appid-social)
* Customize and configure [the Login Widget](/docs/appid?topic=appid-login-widget)
* Learn more about the [Node.js SDK](https://github.com/ibm-cloud-security/appid-serversdk-nodejs){: external}

