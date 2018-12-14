---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}
{:codeblock: .codeblock}


# Web apps
{: #adding-web}

With {{site.data.keyword.appid_full}}, you can quickly construct an authentication layer for your web applications.
{: shortdesc}

## Understanding the flow
{: #understanding}

**When would this flow be useful?**

When you are developing a web application, you can use the {{site.data.keyword.appid_short}} web flow to securely authenticate users. Users are then able to access your server-side protected content in your web apps.

**What is the flow's technical basis?**

Web apps often require users to authenticate in order to access protected content. {{site.data.keyword.appid_short_notm}} uses the OIDC authorization code flow to securely authenticate users. With this flow, when the user is authenticated, the app receives an authorization code. The code is then exchanged for an access, identity, and refresh token. In code, exchange step the tokens are always sent via a secure backchannel between the app and the OIDC server. This provides an extra layer of security as the attacker is not able to intercept the tokens. These tokens can be sent directly to the web server hosting application for user authentication.

**How does this flow work?**

![{{site.data.keyword.appid_short_notm}} request flow](images/web-flow.png)

1. A user initiates the authorization flow by sending a request to the `/authorization` endpoint via the {{site.data.keyword.appid_short_notm}} SDK or API.

2. If the user is unauthorized, the authentication flow is started with a redirect to {{site.data.keyword.appid_short_notm}}.

3. Depending on the user's `/authorization` request parameters or identity provider configuration, it launches the login widget in the users browser.

4. The user chooses an identity provider to authenticate with and completes the sign in process.

5. The identity provider redirects to the client app with the authorization code.

6. The {{site.data.keyword.appid_short_notm}} SDK exchanges the authorization code for access, identity, and optional refresh tokens from the {{site.data.keyword.appid_short_notm}} service.

7. The tokens are saved by the {{site.data.keyword.appid_short_notm}} SDK and a redirect to the client application occurs.

8. The user is granted access to the app.

</br>
</br>

## Configuring the Node.js SDK
{: #configuring-nodejs}

You can configure {{site.data.keyword.appid_short_notm}} to work with your Node.js web applications.
{: shortdesc}

**Before you begin**

You must have the following prerequisites:

* An instance of the {{site.data.keyword.appid_short_notm}} service
* A set of service credentials
* NPM version 4 or higher
* Node version 6 or higher
* Your redirect URI set in the {{site.data.keyword.appid_short_notm}} service dashboard


### Installing the Node.js SDK

1. By using the command line, change to the directory that contains your Node.js app.

2. Install the {{site.data.keyword.appid_short_notm}} service.
  ```bash
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### Initializing the Node.js SDK

1. Add the following `require` definitions to your `server.js` file.

    ```javascript
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. Set up your express app to use express-session middleware. **Note**: You must configure the middleware with the proper session storage for production environments. For more information see the <a href="https://github.com/expressjs/session" target="_blank"> expressjs docs <img src="../icons/launch-glyph.svg" alt="External link icon"></a>.

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

3. Pass your service credentials to initialize the SDK.

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

   <table summary="Command components: Node.js apps">
      <caption>Command components for Node.js apps</caption>
        <tr>
          <th>Components</th>
          <th>Description</th>
        </tr>
      <tr>
          <td><i>tenantId</i> </br> <i>clientId</i> </br> <i>secret</i> </br> <i>oauth-server-url</i> </br> </td>
          <td>You can find these values by clicking **View Credentials** in the **Service Credentials** tab of your service dashboard.</td>
      </tr>
      <tr>
        <td><i>redirectUri</i></td>
        <td>The redirect URI value can be supplied in three ways:</br>
            1. Manually in new `WebAppStrategy({redirectUri: "...."})`</br>
            2. As environment variable named `redirectUri`</br>
            3. If neither of those options is supplied, the {{site.data.keyword.appid_short_notm}} SDK tries to retrieve the `application_uri` of the application that is running on {{site.data.keyword.Bluemix_notm}} and append a default suffix `/ibm/cloud/appid/callback`.
        </td>
      </tr>
    </table>

4. Configure passport with serialization and deserialization. This configuration step is required for authenticated session persistence across HTTP requests. For more information, see the <a href="http://passportjs.org/docs" target="_blank">passport docs <img src="../icons/launch-glyph.svg" alt="External link icon"></a>.

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

6. Register your protected endpoint.

   ```javascript
   app.get(‘/protected’, passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res) res.json(req.user); });
   ```
   {: codeblock}

For more information, see the <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub repository <img src="../icons/launch-glyph.svg" alt="External link icon"></a>.

</br>
</br>

## Configuring the Liberty for Java SDK
{: #configuring-liberty}

You can configure {{site.data.keyword.appid_short_notm}} to work with your Liberty for Java web applications.
{:shortdesc}

**Before you begin**

You must have the following prerequisites:
* An instance of the {{site.data.keyword.appid_short_notm}} service
* A set of service credentials
* Apache Maven 3.5 or higher
* Java 1.8
* A Liberty for Java web application

### Installing the Liberty for Java SDK

1. Add an OpenID Connect feature to your `server.xml`.

  ```xml
  <featureManager>
      <feature>ssl-1.0</feature>
      <feature>appSecurity-2.0</feature>
      <feature>openidConnectClient-1.0</feature>
  </featureManager>
  ```
  {: codeblock}

2. Create an Open ID Connect Client feature and define the following placeholders. Use the service credentials to fill the placeholders.

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
  <caption>Table. OIDC element variables for Liberty for Java apps</caption>
    <tr>
      <th> Component </th>
      <th> Description </th>
    </tr>
    <tr>
    <td><code>clientID</code> </br> <code>secret</code> </br> <code>oauth-server-url</code> </br></td>
    <td>You can find these values by clicking **View credentials** in the **service credentials** tab of your service dashboard.</td>
    </tr>
    <tr>
      <td><code>authorizationEndpointURL</code></td>
      <td> Add `/authorization` to the end of your oauthServerURL.</td>
    </tr>
    <tr>
      <td><code>tokenEndpointUrl</code></td>
      <td>Add `/token` to the end of your oauthServerURL.</td>
    </tr>
    <tr>
      <td><code>jwkEndpointUrl</code></td>
      <td>Add `/publickeys` to the end of your oauthServerURL.</td>
    </tr>
    <tr>
      <td><code>issuerIdentifier</code></td>
      <td>Changes based on your region. It can be one of the following: </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.appid.cloud.ibm.com"</ul></td>
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

1. In your `server.xml` file, define an authorization filter to specify protected resources. If a filter is not <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">defined <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, the service protects all resources.

  ```xml
  <authFilter id="myAuthFilter">
      <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
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

3. Download the `libertySample-1.0.0.war` file from <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/liberty-for-java" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and place it in your server's apps folder. For example, if your server is named defaultServer, the war file would go here `target/liberty/wlp/usr/servers/defaultServer/apps/`.

4. Configure SSL by adding the following to your `server.xml` file. You will also need to create a truststore.

```xml
  <keyStore id="defaultKeyStore" password="myPassword"/>
  <keyStore id="appidtruststore" password="Liberty" location="${server.config.dir}/mytruststore.jks"/>
  <ssl id="defaultSSLConfig" keyStoreRef="defaultKeyStore" trustStoreRef="appidtruststore"/>
```
{: codeblock}

By default SSL configuration requires the truststore be configured for OpenID Connect. Learn more about <a href="https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_config_oidc_rp.html" target="_blank">configuring an OpenID Connect Client in Liberty <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
{: tip}

</br>
</br>

## Configuring Spring Boot for Java SDK
{: #configuring-spring-boot}

You can configure {{site.data.keyword.appid_short_notm}} to work with your Spring Boot applications.
{:shortdesc}

**Before you begin**

You must have the following prerequisites:

* An instance of the {{site.data.keyword.appid_short_notm}} service
* A set of service credentials
* A Java + Maven project
* Apache Maven 3.5 or higher
* Java 1.8
* Spring Boot 2.0 and Security OAuth 2.0 or higher


### Initializing the Spring Boot framework

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

3. In the same file, include the Maven plugin.

  ```xml
  <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
  </plugin>
  ```
  {: codeblock}

### Initializing OAuth2

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
                .antMatchers("/protectedResource").authenticated()
                .and().logout().logoutSuccessUrl("/").permitAll();
    }
  ```
  {: codeblock}


### Adding credentials

1. Add an `application.yml` configuration file to the `/springbootsample/src/main/resources/` directory. You can complete your configuration with the information from your service credentials.

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


For a step-by-step example, check out <a href="https://www.ibm.com/blogs/bluemix/2018/06/creating-spring-boot-applications-app-id/" target="_blank">this blog</a>!

</br>
</br>

## Using {{site.data.keyword.appid_short_notm}} with other languages
{: #other}

With an OIDC compliant client SDK, you can use {{site.data.keyword.appid_short_notm}} with other languages. Check out a list of <a href="https://openid.net/developers/certified/">certified libraries</a> for more information.


</br>
</br>

## Next steps
{: #next}

With {{site.data.keyword.appid_short_notm}} installed in your application, you're almost ready to start authenticating users! Try doing one of the following activities next:

* Configure your [identity providers](/docs/services/appid/identity-providers.html)
* Customize and configure [the Login Widget](/docs/services/appid/login-widget.html)
* Learn more about the <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
