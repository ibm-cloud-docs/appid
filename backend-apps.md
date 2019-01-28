---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Backend apps
{: #adding-backend}

You can use the {{site.data.keyword.appid_full}} SDKs and APIs to protect your backend application endpoints and APIs.
{: shortdesc}


## Understanding the flow
{: #understanding}

**When would this flow be useful?**

Part of developing backend apps is verifying that your APIs are protected from unauthorized access. The {{site.data.keyword.appid_short_notm}} SDKs make it easy to protect your API endpoints and ensure the security of your app.

**What is the flow's technical basis?**

{{site.data.keyword.appid_short_notm}} implements the [OAuth2](https://tools.ietf.org/html/rfc6749) and the OIDC spec, which uses bearer tokens for authentication and authorization. These tokens are formatted as  [JSON Web Tokens](https://tools.ietf.org/html/rfc7519), which are digitally signed and contain claims that describe the subject that is being authenticated and the identity provider. The APIs of your application are protected by access and identity tokens. Clients that need access to your APIs can authenticate with the identity provider through {{site.data.keyword.appid_short_notm}} in exchange for these tokens. The claims in the tokens have to be validated in order to grant access to the protected APIs.

For more information about how tokens are used in {{site.data.keyword.appid_short_notm}}, see [Understanding tokens](/docs/services/appid/authorization.html#tokens).
{: tip}

**What does this flow look like?**

![{{site.data.keyword.appid_short_notm}} backend flow. Steps are listed in order in the following the image.](/docs/services/appid/images/backend-flow.png)

1. A client makes a POST request to the {{site.data.keyword.appid_short_notm}} authorization server to obtain an access token. A POST request generally takes the following form:

  ```
  POST/oauth/v3/{tenantId}/token HTTP/1.1
  Content_type: application/x-www-form-urlencoded
  Authorization header = "Basic" + base64encode({clientId}:{secret})
  FormData = {grant_type}
  ```
  {: screen}

2. If the client meets the qualifications, the authorization server returns an access token.

3. The client sends a request to the protected resource.

4. The protected resource or API validates the token. If the token is valid, access to the resource is granted for the client. If the token cannot be validated, access is denied.


## Protecting resources with the Node.js SDK
{: #secure-node}

The {{site.data.keyword.appid_short_notm}} server SDK enforces authentication and authorization with the [Passport framework](http://www.passportjs.org/). With the `ApiStrategy`, you can secure your backed resources by requiring that access and identity tokens are validated in the authorization header as part of the request.
{: shortdesc}

**Before you begin**

You must have the following prerequisites before you can get started:
 * An instance of {{site.data.keyword.appid_short_notm}}
 * NPM version 4 or higher
 * Node version 6 or higher

**Installing the SDK**

1. Add the {{site.data.keyword.appid_short_notm}} Node.js SDK to your app's `package.json` file.

  ```
  "dependencies": {
      "ibmcloud-appid": "^4.0.0"
  }
  ```
  {: codeblock}

2. Run the following command.

  ```
  npm install
  ```
  {: codeblock}

**Initializing the SDK**

You can initialize the SDK by using an `oauth server url`.

1. Obtain your `oauth server url`.
  1. Navigate to the **Service Credentials** tab of the {{site.data.keyword.appid_short_notm}} dashboard.
  2. If you don't already have a set of credentials, click **New credential** and then click **Add** to create a new set. If you do, skip this step.
  3. Click the **View credentials** toggle to see your information.
  4. Copy your `oauth server url` to use in the next step.

2. Initialize the {{site.data.keyword.appid_short_notm}} passport strategy as shown in the following example.

  ```javascript
  var express = require('express'); 
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy; 
  passport.use(new APIStrategy({ oauthServerUrl: "{oauth-server-url}" })); 
  var app = express();
  app.use(passport.initialize());
  ```
  {: codeblock}


If your Node.js app runs on {{site.data.keyword.Bluemix_notm}} and is bound to your instance of {{site.data.keyword.appid_short_notm}}, there's no need to provide the API strategy configuration. The {{site.data.keyword.appid_short_notm}} configuration obtains the information by using the VCAP_SERVICES environment variable.
{: tip}

**Securing the API**

The following snippet demonstrates how to use `ApiStrategy` in an Express app to protect the `/protected` GET API.

  ```javascript
   app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', { session: false }), function(request, response){
      console.log("Security context", request.appIdAuthorizationContext);
      response.send(200, "Success!");
      }
   );
   ```
  {: codeblock}

When the tokens are valid, the next middleware in the request chain is called and the `appIdAuthorizationContext` property is added to the request object. The property contains the original access and identity tokens, as well as the decoded payload information of the respective tokens.


## Protecting resources with the Swift SDK
{: #secure-swift}

You can use {{site.data.keyword.appid_short_notm}} to protect your server-side resources by using the Swift SDK.
{: shortdesc}

The {{site.data.keyword.appid_short_notm}} [Swift server SDK](https://github.com/ibm-cloud-security/appid-serversdk-swift) provides an API protection middleware plug-in that is used to protect your back-end apps. By associating your APIs with the middleware, you can protect your app from unauthorized access. After the API is protected, the middleware ensures that the tokens that are generated by {{site.data.keyword.appid_short_notm}} are validated. You can then modify the behavior of the API depending on the validation results.

See the following code snippet for an example of how to protect the `/protectedendpoint` API.

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// setup routes
let router = Router()

// mandatory option to be passed in if app not deployed on IBM Cloud
let options = [
    "oauthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v3/d8438de6-c325-4956-ad34-abd49194affd",
]
let apiCreds = Credentials()

// Minimum macOS version required
if #available(OSX 10.12, *) {

    // setup API protection
    let apiKituraCredentialsPlugin = APIKituraCredentialsPlugin(options: options)
    apiCreds.register(plugin: apiKituraCredentialsPlugin)

    // associate route with API protection
    router.all(middleware: apiCreds)

    // create protected API
    router.get("/protectedendpoint") { request, response, next in

        response.headers["Content-Type"] = "text/html; charset=utf-8"
        do {
            if let userProfile = request.userProfile  {
                try response.status(.OK).send(
                    "<!DOCTYPE html><html><body>" +
                        "Welcome " + userProfile.displayName  +
                        "! You are logged in with " + userProfile.provider + ".
" +
                    "</body></html>\n\n").end()
                next()
                return
            }
            try response.status(.unauthorized).send(
                "<!DOCTYPE html><html><body>” + “You are not authorized!" +
                "</body></html>\n\n").end()
        }
        catch {}
        next()
    }

    // Start server
    Kitura.addHTTPServer(onPort: 8090, with: router)

    Kitura.run()  
}
```
{: codeblock}

## Protecting resources manually
{: secure-api}

Securing your backend apps and protected resources involves validating tokens. You can validate {{site.data.keyword.appid_short_notm}} access and identity tokens in several ways. For help validating tokens, check out [Validating tokens](/docs/services/appid/tokens.html).


## Next steps
{: #next}

With {{site.data.keyword.appid_short_notm}} installed in your application, you're almost ready to start authenticating users! Try doing one of the following activities next:

* Configure your [identity providers](/docs/services/appid/identity-providers.html)
* Customize and configure [the Login Widget](/docs/services/appid/login-widget.html)
* Learn more about the <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
* Learn more about the <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">Swift SDK<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
