---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione esistente

Puoi utilizzare {{site.data.keyword.appid_full}} con la tua applicazione esistente per autenticare e archiviare le informazioni sul profilo per i tuoi utenti.


## Prerequisiti

* Un'applicazione iOS Swift, Android, Node.js, Swift o Liberty for Java esistente.
* Un'istanza esistente di {{site.data.keyword.appid_short_notm}}.


## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione Android esistente
{: #existing-android}

Puoi aggiungere il servizio {{site.data.keyword.appid_short_notm}} alle tue applicazioni Android esistenti.

1. Aggiungi JitPack al tuo file `build.gradle` della root.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: codeblock}

2. Apri il file `build.gradle` per la tua applicazione, trova la sezione delle dipendenze del file e aggiungi una dipendenza di compilazione all'SDK client {{site.data.keyword.appid_short_notm}}.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

3. Trova la sezione defaultConfig e aggiungi la seguente riga di codice.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. Sincronizza il tuo progetto con Gradle.
5. Inizializza l'SDK client passando i parametri contesto, ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo onCreate dell'attività principale nella tua applicazione Android.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

    <table>
    <caption> Tabella 1. Componenti del comando spiegati </caption>
      <tr>
        <th> Componenti </th>
        <th> Descrizione </th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> Puoi trovare questo valore facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio. </td>
      </tr>
      <tr>
        <td> <i> AppID.REGION </i> </td>
        <td> Puoi trovare la tua regione nella IU. Le opzioni sono `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` o `AppID.REGION_Sydney`. </td>
      </tr>
    </table>

6. Dopo che l'SDK client {{site.data.keyword.appid_short_notm}} è stato inizializzato, puoi autenticare i tuoi utenti eseguendo il widget di accesso.

  ```Java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

          @Override
          public void onAuthorizationCanceled () {
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
        });
  ```
  {: codeblock}

    <table>
    <caption> Tabella 2. Componenti del comando spiegati </caption>
      <tr>
        <th> Componenti </th>
        <th> Descrizione </th>
      </tr>
      <tr>
        <td> <i> onAuthorizationFailure </i> </td>
        <td> Si è verificata un'eccezione. </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationCanceled </i> </td>
        <td> Il processo di autenticazione è stata annullato dall'utente. </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationSuccess </i> </td>
        <td> L'utente è stato autenticato. </td>
      </tr>
    </table>

## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione iOS Swift esistente
{: #existing-ios}

1. Apri il podfile nella directory del progetto.
2. Nella tua destinazione del progetto, aggiungi una dipendenza per il pod 'BluemixAppID'. Assicurati che anche il comando `use_frameworks!` sia nella tua destinazione.
3. Per scaricare la dipendenza `BluemixAppID`, esegui il seguente comando.

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. Apri il tuo progetto Xcode e abilita Keychain Sharing. In **Project Settings**, fai clic su **Capabilities** > **Keychain Sharing**.
5. In **Project Settings** > **Info** > **URL Types** aggiungi un **URL Type**. Riempi le caselle di testo **Identifier** e **URL Scheme** con il seguente valore.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. Aggiungi la seguente importazione al tuo file `AppDelegate.swift`.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: codeblock}

7. Inizializza l'SDK client passando i parametri ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo application:didFinishLaunchingWithOptions: di AppDelegate nella tua applicazione.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: codeblock}

    <table>
    <caption> Tabella 3. Componenti del comando spiegati </caption>
      <tr>
        <th> Componenti </th>
        <th> Descrizione </th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> Puoi trovare questo valore facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio. </td>
      </tr>
      <tr>
        <td> <i> AppID.REGION </i> </td>
        <td> Puoi trovare la tua regione nella IU. Le opzioni sono `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` o `AppID.REGION_Sydney`. </td>
      </tr>
    </table>

8. Aggiungi il seguente codice al tuo file AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
         	return AppID.sharedInstance.application(application, open: url, options: options)
      }
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
     }

     public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

    <table>
    <caption> Tabella 4. Componenti del comando spiegati </caption>
      <tr>
        <th> Componenti </th>
        <th> Descrizione </th>
      </tr>
      <tr>
        <td> <i> onAuthorizationSuccess </i> </td>
        <td> L'utente è stato autenticato. </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationCanceled </i> </td>
        <td> Il processo di autenticazione è stata annullato dall'utente. </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationFailure </i> </td>
        <td> Si è verificata un'eccezione. </td>
      </tr>
    </table>

## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione web Node.js esistente
{: #existing-node}

1. Aggiungi il modulo `bluemix-appid` alla tua applicazione Node.js.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: codeblock}

2. Installa i seguenti moduli se non sono già stati installati.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. Aggiungi il seguente codice al tuo file `app.js` per:
    * Configurare la tua applicazione Express per utilizzare il middleware della sessione Express. **Nota**: devi configurare il middleware con l'archivio della sessione appropriato per gli ambienti di produzione. Per ulteriori informazioni consulta <a href="https://github.com/expressjs/session" target="_blank">expressjs docs <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
    * Configurare passportjs con la serializzazione e la deserializzazione. Questo è obbligatorio per la persistenza della sessione autenticata attraverso le richieste HTTP. Per ulteriori informazioni, visita il <a href="http://passportjs.org/docs" target="_blank">passportjs docs <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.  
    * Richiamare i token di accesso e identità dal servizio {{site.data.keyword.appid_short_notm}} eseguendo un comando get per il callback dell'URL.

  ```javaScript
  const express = require("express");
  const session = require("express-session");
  const passport = require("passport");
  const WebAppStrategy = require("bluemix-appid").WebAppStrategy;
  const app = express();
  const CALLBACK_URL = "/ibm/bluemix/appid/callback";
  app.use(session({
      secret: "123456",
      resave: true,
      saveUninitialized: true
    }));
  app.use(passport.initialize());
    app.use(passport.session());

    passport.use(new WebAppStrategy());
  passport.serializeUser(function(user, cb) {
      cb(null, user);
    });

    passport.deserializeUser(function(obj, cb) {
      cb(null, obj);
    });
  app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
    		res.json(req.user);
    });
  ```
  {: codeblock}

    **Nota**: il servizio reindirizza nel seguente ordine:
    1. L'URL originale della richiesta che ha attivato il processo di autenticazione, come persistente nella sessione HTTP nella chiave `WebAppStrategy.ORIGINAL_URL`.
    2. Un reindirizzamento con esito positivo, come specificato in `passport.authenticate(name, {successRedirect: "...."}).`
    3. La root dell'applicazione ("/")

4. Ridistribuire l'applicazione.


## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione web Swift esistente
{: #existing-swift}

1. Apri il file `Package.swift` nella directory della tua applicazione Swift e aggiungi la dipendenza `appid-serversdk-swift`.
  Ad esempio:

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
    )
    ```
    {: codeblock}

2. Aggiungi il seguente codice alla tua applicazione Swift per:
    * Configurare Kitura per utilizzare il middleware della sessione. **Nota**: devi configurare Kitura con l'archivio della sessione appropriato per gli ambienti di produzione. Per ulteriori informazioni consulta <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura docs <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
    * Richiamare i token di accesso e identità dal servizio {{site.data.keyword.appid_short_notm}} eseguendo un comando get per il callback dell'URL.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  router.get(CALLBACK_URL,
    handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
      successRedirect: LANDING_PAGE_URL,
      failureRedirect: LANDING_PAGE_URL
      ))
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
    let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]
    guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
      response.status(.unauthorized)
          return next()
      }
    response.send(json: identityTokenPayload!)
    next()
    })
  ```
  {: codeblock}

  <table>
  <caption> Tabella 5. Componenti del comando spiegati </caption>
    <tr>
      <th> Componenti </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td> <i> var CALLBACK_URL </i> </td>
      <td> /ibm/bluemix/appid/callback </td>
    </tr>
    <tr>
      <td> <i> var LANDING_PAGE_URL </i> </td>
      <td> /index.html </td>
    </tr>
    </table>

5. Ridistribuire l'applicazione.



## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione Liberty for Java esistente
{: #existing-liberty}

Puoi configurare {{site.data.keyword.appid_short_notm}} per utilizzare le tue applicazioni web Liberty for Java esistenti.

1. Aggiungi una <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> al tuo `server.xml`.

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. Nella tua funzione Open ID Connect Client, definisci i seguenti segnaposto. Vengono riempiti automaticamente da {{site.data.keyword.Bluemix_notm}} successivamente. La variabile del nome dell'istanza deve corrispondere esattamente al tuo nome dell'istanza {{site.data.keyword.appid_short_notm}}.

  ```
  clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
  clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
  authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
  tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
  jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
  issuerIdentifier='appid-oauth.ng.bluemix.net'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  ```
  {: codeblock}

  **Nota**: la variabile issuerIdentifier è diversa a seconda della tua regione. Può essere una delle seguenti variabili:
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. Definisci un filtro di autorizzazione per specificare le risorse protette. Se non viene <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">definito un filtro <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>, il servizio proteggerà tutte le risorse.
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

3. Nel tuo file `server.xml`, definisci il tuo tipo di oggetto speciale come ALL_AUTHENTICATED_USERS.

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

4. Nel tuo elemento `<application-bnd>`, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">definisci i ruoli <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> come trovati nella tua applicazione web: `web.xml`.

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

5. Ottieni un certificato.

    a. Nel tuo dashboard {{site.data.keyword.appid_short_notm}}, fai clic sulle credenziali del servizio.

    b. Fai clic su **View credentials** e copia `oauthServerUrl`.

    c. Aggiungi `/token` all'URL. Utilizza Firefox per aprire l'URL di output e ottenere il certificato. Puoi utilizzare il seguente URL come esempio.

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Nella barra degli indirizzi di Firefox, fai clic sull'icona di blocco > **right arrow** > **more information** > **view certificate**.

    e. Nella scheda **Security**, fai clic su **View certificate** > **details**.

    f. Esporta il certificato e salvalo nella tua unità locale come un file PEM.

6. Aggiungi il certificato alla tuo file truststore.jks Liberty for Java utilizzando <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e aggiungi un riferimento all'alias del certificato nell'elemento OIDC. Il tuo `.jks file` è ubicato nella tua directory del server: **resources** > **security** > **<i>truststore file name</i>** > **`.jks file`**. Puoi utilizzare una delle seguenti opzioni per aggiungere il tuo certificato al file.

    * Nel terminale, passa alla tua cartella di sicurezza Liberty for Java: wlp > usr > servers > <i>servername</i> > resources > security e utilizza il seguente comando per aggiungere il certificato.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Nota**: `~/Documents/[certificatename].cer` illustra l'ubicazione del file nella tua unità locale.

    * Puoi utilizzare <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per aggiungere il certificato. Apri KeyStore Explorer e seleziona **Open an existing KeyStore**.

7. Nel tuo file `manifest.yml`, definisci la tua istanza {{site.data.keyword.appid_short_notm}}.

  ```yml
  services:
  - <appid service name>

  Manifest.yml file example:
  applications:
  - name: LibertyExampl
  buildpack: liberty-for-java
  instances: 1
  random-route: true
  memory: 512M
  disk_quota: 1024M
  timeout: 180
  services:
  - AppID-Instance-Name
  ```
  {: codeblock}

    Un file `server.xml` di esempio configurato per {{site.data.keyword.appid_short_notm}}:

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <server description="sample server">

      <featureManager>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>  
      </featureManager>

      <openidConnectClient id="MyDefaultRP"
         clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
         clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
         authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
         tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
         jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
         issuerIdentifier='${cloud.services.AppID-Instance-Name.credentials.appid-oauth.ng.bluemix.net}'
         tokenEndpointAuthMethod="basic"
         signatureAlgorithm="RS256"
         authFilterid="myAuthFilter"
         trustAliasName="my.bluemix.certificate "
      />
      <authFilter id="myAuthFilter">
               <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
      </authFilter>

      <application type="war" id="ProtectedServlet" context-root="/appidSample" location="${server.config.dir}/apps/libertySample-1.0.0.war">
          <application-bnd>
              <security-role name="myrole">
                  <special-subject type="ALL_AUTHENTICATED_USERS" />
              </security-role>
          </application-bnd>
      </application>

   <applicationManager autoExpand="true"/>

  <keyStore id="defaultKeyStore" password="Password"/>
  <keyStore id="defaulttrustore" password="Liberty" location="<FileContainingCertificated>.jks"/>

  <ssl id="defaultSSLSettings" keyStoreRef="defaultKeyStore" trustStoreRef="defaulttrustore"/>
  <sslDefault sslRef="defaultSSLSettings"/>

      <httpEndpoint id="defaultHttpEndpoint" httpPort="9080" host="*" httpsPort="9443" />

      
      <applicationManager autoExpand="true"/>

  </server>
  ```
  {: codeblock}



## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione esistente non in esecuzione in {{site.data.keyword.Bluemix_notm}}
{: #existing}

Se disponi di un'applicazione Node.js o Swift non in esecuzione in {{site.data.keyword.Bluemix_notm}}, puoi configurare WebAppStrategy o WebAppKituraCredentialsPlugin per lavorare in remoto. Per un'applicazione Liberty for Java non in esecuzione in Bluemix, configura le variabili dell'elemento OIDC.


Nella tua applicazione Node.js, sostituisci `passport.use(new WebAppStrategy());` con il seguente codice.

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: codeblock}

Nella tua applicazione Swift, sostituisci `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` con il seguente codice.

  ```swift
  let options = [
        "clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
    let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  ```
  {: codeblock}

  <table>
  <caption> Tabella 6. Componenti per il comando per le applicazioni Swift e Node.js spiegati </caption>
    <tr>
      <th> Componenti </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td> Puoi trovare questi valori facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio. </td>
    </tr>
    <tr>
      <td> <i> app-url </i> </td>
      <td> Il tuo URL dell'applicazione. </td>
    </tr>
    <tr>
      <td> <i> CALLBACK_URL </i> </td>
      <td> L'URL che gli utenti della pagina visualizzano dopo il login. </td>
    </tr>
  </table>

Nelle tue applicazioni Liberty for Java, completa la seguente procedura in [Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione Liberty for Java esistente](/docs/services/appid/existing.html#existing-liberty), ma sostituisci le variabili dell'elemento client OIDC con il seguente codice.

  ```
  clientId='App ID client_ID'
  clientSecret='App Id Secret'      
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
  <caption> Tabella 7. Variabili dell'elemento OIDC per le applicazioni Liberty for Java non in esecuzione in Bluemix </caption>
    <tr>
      <th> Componente </th>
      <th> Descrizione </th>
    </tr>
    <tr>
    <td> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> Puoi trovare questi valori facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio. </td>
    </tr>
    <tr>
      <td> <i> authorizationEndpointURL </i> </td>
      <td> Aggiungi `/authorization` alla file di oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> tokenEndpointUrl </i> </td>
      <td> Aggiungi `/token` alla file di oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> jwkEndpointUrl </i> </td>
      <td> Aggiungi `/publickeys` alla file di oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> issuerIdentifier </i> </td>
      <td> Diversa a seconda della regione. Può essere uno dei seguenti valori: </br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net" </ul></td>
    </tr>
    <tr>
      <td> <i> tokenEndpointAuthMethod </i> </td>
      <td> Specificata come "basic". </td>
    </tr>
    <tr>
      <td> <i> signatureAlgorithm </i> </td>
      <td> Specificata come "RS256". </td>
    </tr>
    <tr>
      <td> <i> authFilterid </i> </td>
      <td> L'elenco delle risorse da proteggere. </td>
    </tr>
    <tr>
      <td> <i> trustAliasName </i> </td>
      <td> Il nome del tuo certificato nel tuo truststore. </td>
    </tr>
  </table>
