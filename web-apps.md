---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}


# Adding App ID to your web apps
{: #adding-web}

With {{site.data.keyword.appid_full}}, you can quickly construct an authentication layer for your web applications.
{: shortdesc}

## Understanding the flow

**When would this flow be useful?**

When you are developing a web application, you can use the {{site.data.keyword.appid_short}} web flow to securely authenticate users. Users are then able to access your server-side protected content in your web apps.

**What is the flow's technical basis?**

Web apps often require users to authenticate in order to access protected content. {{site.data.keyword.appid_short_notm}} uses the OIDC authorization code flow to securely authenticate users. With this flow, when the user is authenticated, the app receives an authorization code. The code is then exchanged for an access, identity, and refresh token. In code exchange step the tokens are always sent via a secure backchannel between the app and the OIDC server. This provides an additional layer of security as the attacker is not able to intercept the tokens. These tokens can be sent directly to the web server hosting application for user authentication.

**How does this flow work?**

![{{site.data.keyword.appid_short_notm}} request flow](/docs/services/appid/images/web-flow.png)

1. A user initiates the authorization flow by sending a request to the `/authorization` endpoint via the {{site.data.keyword.appid_short_notm}} SDK or API.

2. If the user is unauthorized, the authentication flow is started with a redirect to {{site.data.keyword.appid_short_notm}}.

3. Depending on the user's `/authorization` request parameters or identity provider configuration, it launches the login widget in the users browser.

4. The user chooses an identity provider to authenticate with and completes the sign in process.

5. The identity provider redirects to the client app with the authorization code.

6. The {{site.data.keyword.appid_short_notm}} SDK exchanges the authorization code for access, identity, and optional refresh tokens from the {{site.data.keyword.appid_short_notm}} service.

7. The tokens are saved by the {{site.data.keyword.appid_short_notm}} SDK and a redirect to the client application occurs.

8. The user is granted access to the app.


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

### Initialize Node SDK

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
          <td><i>tenantID</i> </br> <i>clientID</i> </br> <i>secret</i> </br> <i>oauth-server-url</i> </br> </td>
          <td>You can find these values by clicking **View Credentials** in the **Service Credentials** tab of your service dashboard.</td>
      </tr>
      <tr>
        <td><i>redirectUri</i></td>
        <td>The redirect URI value can be supplied in three ways:</br>
            1. Manually in new `WebAppStrategy({redirectUri: "...."})`</br>
            2. As environment variable named `redirectUri`</br>
            3. If none of the above was supplied, the {{site.data.keyword.appid_short_notm}} SDK will try to retrieve `application_uri` of the application that is running on {{site.data.keyword.Bluemix_notm}} and append a default suffix `/ibm/cloud/appid/callback`.
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


## Configuring the Liberty for Java SDK
{: #configuring-liberty}

You can configure {{site.data.keyword.appid_short_notm}} to work with your Liberty for Java web applications.
{:shortdesc}

1. Add an <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect feature <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to your `server.xml`.

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. In your Open ID Connect Client feature, define the following placeholders. Use the service credentials to fill the placeholders.

  ```
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
      <td>Changes based on your region. It can be one of the following: </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
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

3. Define an authorization filter to specify protected resources. If a filter is not <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">defined <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, the service protects all resources.

  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

4. In your `server.xml` file, define your special subject type as `ALL_AUTHENTICATED_USERS`.

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

5. In your `<application-bnd>` element, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">define the roles <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> as found in your web app: `web.xml`.
  ```xml
  <security-role>
  <role-name>myrole</role-name>
  </security-role>
  <security-constraint>
  <web-resource-collection>
  <web-resource-name>ProtectedServlet</web-resource-name>
  <url-pattern>/ProtectedServlet/*</url-pattern>
  <http-method>GET</http-method>
  <http-method>PUT</http-method>
  <http-method>POST</http-method>
  <http-method>DELETE</http-method>
  </web-resource-collection>
  <auth-constraint>
  <role-name>myrole</role-name>
  </auth-constraint>
  <user-data-constraint>
  <transport-guarantee>NONE</transport-guarantee>
  </user-data-constraint>
  </security-constraint>
  ```
  {: codeblock}

## Using {{site.data.keyword.appid_short_notm}} with other languages

With an OIDC compliant client SDK, you can use {{site.data.keyword.appid_short_notm}} with other languages. Check out a list of <a href="https://openid.net/developers/certified/">certified libraries</a> for more information.
