---

copyright:
  years: 2017, 2022
lastupdated: "2022-02-07"

keywords: protected resource, backend apps, identity, tokens, identity provider, authentication, authorization, app security, oauth, 

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
{:release-note: data-hd-content-type='release-note'}

# Backend apps
{: #backend}

You can use the {{site.data.keyword.appid_full}} SDKs and APIs to protect your backend application endpoints and APIs.
{: shortdesc}


## Understanding the flow
{: #backend-understanding}

Part of developing backend apps is verifying that your APIs are protected from unauthorized access. The {{site.data.keyword.appid_short_notm}} SDKs help you protect your API endpoints and ensure the security of your app.


### What is the flow's technical basis?
{: #backend-technical-flow}

{{site.data.keyword.appid_short_notm}} implements the [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749){: external} and the OIDC spec, which uses bearer tokens for authentication and authorization. These tokens are formatted as [JSON Web Tokens](https://datatracker.ietf.org/doc/html/rfc7519){: external}, which are digitally signed and contain claims that describe the subject that is being authenticated and the identity provider. The APIs of your application are protected by access and identity tokens. Clients that need access to your APIs can authenticate with the identity provider through {{site.data.keyword.appid_short_notm}} in exchange for these tokens. The claims in the tokens must be validated to grant access to the protected APIs.

For more information about how tokens are used in {{site.data.keyword.appid_short_notm}}, see [Understanding tokens](/docs/appid?topic=appid-tokens).
{: tip}


### What does the flow look like?
{: #backend-flow}

![{{site.data.keyword.appid_short_notm}} backend flow](images/backend-flow.png){: caption="Figure 1. Backend application flow" caption-side="bottom"}

1. A client makes a POST request to the {{site.data.keyword.appid_short_notm}} authorization server to obtain an access token. A POST request generally takes the following form:

   ```sh
   POST /oauth/v4/{tenantId}/token HTTP/1.1
   Content_type: application/x-www-form-urlencoded
   Authorization header = "Basic" + base64encode({clientId}:{secret})
   FormData = {grant_type}
   ```
   {: screen}

2. If the client meets the qualifications, the authorization server returns an access token.

3. The client sends a request to the protected resource. Requests can be sent in multiple ways, depending on which HTTP client library you're using but a request generally takes the following form:

   ```sh
   curl -H 'Authorization: Bearer {access_token}' {https://my-protected-resource.com}
   ```
   {: screen}

4. The protected resource or API validates the token. If the token is valid, access to the resource is granted for the client. If the token cannot be validated, access is denied.

For information about how to configure your app to use Liberty for Java, see [Quick start: Liberty for Java backend apps tutorial](/docs/appid?topic=appid-backend-liberty).

## Protecting resources by using the Node.js SDK
{: #backend-secure}

You can use the {{site.data.keyword.appid_short_notm}} SDKs to enforce authentication and authorization for your server-side applications. The `ApiStrategy` works to secure your backend resources by requiring that access and identity tokens are validated as part of the request. The {{site.data.keyword.appid_short_notm}} Node.js SDK works with the [Passport framework](http://www.passportjs.org/){: external}.
{: shortdesc}

Check out the following video to learn about protecting backend Node applications with {{site.data.keyword.appid_short_notm}}. Then, try it out yourself by using a [simple Node sample app](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02b-simple-node-backend-app){: external}.

![Configuring your app to use the {{site.data.keyword.appid_short_notm}} Node.js SDK](https://www.youtube.com/embed/jJLSgkHpZwA){: video output="iframe" data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}


### Before you begin
{: #backend-secure-before}

Before you get started with the Node.js SDK, you must have the following prerequisites.
* An instance of {{site.data.keyword.appid_short_notm}}
* NPM version 4 or higher
* Node version 6 or higher

### Installing the Node.js SDK
{: #backend-secure-install}

1. Add the {{site.data.keyword.appid_short_notm}} Node.js SDK to your app's `package.json` file.

   ```sh
   "dependencies": {
      "ibmcloud-appid": "^6.0.0"
   }
   ```
   {: codeblock}

2. Run the following command.

   ```sh
   npm install
   ```
   {: codeblock}

### Initializing the Node.js SDK
{: #backend-secure-initialize-node}

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


### Securing the API with the API Strategy
{: #backend-secure-api-strategy}

The following snippet demonstrates how to use `ApiStrategy` in an Express app to protect the `/protected` GET API.

If your Node.js app runs on {{site.data.keyword.cloud_notm}} and is bound to your instance of {{site.data.keyword.appid_short_notm}}, there's no need to provide the API strategy configuration. The {{site.data.keyword.appid_short_notm}} configuration obtains the information by using the VCAP_SERVICES environment variable.
{: tip}

   ```javascript
    app.get('/protected_resource', passport.authenticate('APIStrategy.STRATEGY_NAME', { session: false }), function(request, response){
      console.log("Security context", request.appIdAuthorizationContext);
      response.send(200, "Success!");
      }
   );
   ```
   {: codeblock}


When the tokens are valid, the next middleware in the request chain is called and the `appIdAuthorizationContext` property is added to the request object. The property contains the original access and identity tokens and the decoded payload information of the tokens.

## Protecting resources by using the Swift SDK
{: #protect-resources-swift}

The {{site.data.keyword.appid_short_notm}} server-side Swift SDK provides an API protection middleware plug-in that is used to protect your backend apps. By associating your APIs with the middleware, you can protect your app from unauthorized access. After the API is protected, the middleware ensures that the tokens that are generated by {{site.data.keyword.appid_short_notm}} are validated. You can then modify the behavior of the API depending on the validation results.

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// setup routes
let router = Router()

// mandatory option to be passed in if app not deployed on IBM Cloud
let options = [
    "oauthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/d8438de6-c325-4956-ad34-abd49194affd",
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
                        "! You are logged in with " + userProfile.provider + "." +
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
{: #backend-secure-api}

To secure your backend apps and protected resources, you need to validate a token. When a client sends a request to your resource, you can verify that the token meets the defined specifications. The token might include identifying information, scope, or any other configuration that you have in place. You can validate {{site.data.keyword.appid_short_notm}} access and identity tokens in several ways. For help, check out [Validating tokens](/docs/appid?topic=appid-token-validation).


## Next steps
{: #backend-next}

With {{site.data.keyword.appid_short_notm}} installed in your application, you're almost ready to start authenticating users! Try doing one of the following activities next:

* Configure your [identity providers](/docs/appid?topic=appid-social)
* Customize and configure [the Login Widget](/docs/appid?topic=appid-login-widget)
* Learn more about the [Node.js SDK](https://github.com/ibm-cloud-security/appid-serversdk-nodejs){: external}
* Learn more about the [Swift SDK](https://github.com/ibm-cloud-security/appid-serversdk-swift){: external}


