<staging>---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-18"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Adding App ID to your backend apps
{: #adding-backend}

You can use the IBM® Cloud {{site.data.keyword.appid_short_notm}} SDKs and APIs to protect your backend application endpoints/APIs.


## Understanding the flow
{: #understanding}

#### When would this flow be useful?

When you are developing backend applications and you need to secure its APIs from unauthorized access,
you can leverage the {{site.data.keyword.appid_short_notm}} SDKs and APIs to secure your protected resources.

#### What is the flow's technical basis?

{{site.data.keyword.appid_short_notm}} implements the [OAuth2](https://tools.ietf.org/html/rfc6749) and the OIDC spec, which uses bearer tokens for authentication and authorization. These tokens are formatted as  [JSON Web Tokens](https://tools.ietf.org/html/rfc7519), which are digitally signed and contain claims describing the subject being authenticated and the Identity Provider (IdP).
The APIs of your application are protected by Access and Identity tokens. Clients that need access to your APIs authenticate with the IdP through App ID in exchange for these tokens.
The claims in the tokens have to be validated in order to grant access to the protected APIs.

For more information about how tokens are used in App ID, see [Understanding tokens](authorization.html#tokens).
{: tip}

#### What does this flow look like?

![alt text](./images/securing-backend-apps.png)

1. A client obtains tokens from the App ID authorization server
2. The client invokes the protected resource passing the token in the authorization headers
3. The protected API then validates the token from the request before granting access to its protected resource

## Securing APIs with {{site.data.keyword.appid_short}} SDKs
{: #securing}

### Before you begin
{: #before-installation}

1. You need to an instance of {{site.data.keyword.appid_short_notm}}
2. Once you have an instance of App ID, generate service credentials from the Service Credentials tab on the {{site.data.keyword.appid_short_notm}} dashboard.
3. From the service credentials generated above, obtain the `tenant ID` and the `oauth server url`.


### Securing APIs with {{site.data.keyword.appid_short}} Node.js SDK
{: #node-sdk}

1. The App ID server SDK uses the [Passport framework](http://www.passportjs.org/) to enforce authentication and authorization. The SDK provides an `ApiStrategy` passport strategy to secure backend APIs
2. The `ApiStrategy` validates the Access and Identity tokens in the Authorization header of the request


#### Requirements

{: #requirements-node}

 * npm 4.+
 * node 6.+

#### Installing the SDK

{: #install-node}

1. Add the {{site.data.keyword.appid_short_notm}} node SDK as shown below, to your application's `package.json` and run `npm install`

```
"dependencies": {
    "ibmcloud-appid": "^4.0.0"
}
```
{: codeblock}

#### Initialize the SDK

{: #initialize-node}

Use the `tenant ID` and the `oauth server url` obtained earlier to initialize the {{site.data.keyword.appid_short_notm}} passport ApiStrategy as shown below.

```javascript
var express = require('express'); 
var passport = require('passport');
var APIStrategy = require('ibmcloud-appid').APIStrategy; 
passport.use(new APIStrategy({oauthServerUrl: "{oauth-server-url}",
	tenantId: "{tenant-id}")}); 
var app = express();
app.use(passport.initialize());
```
{: codeblock}

You are not required to provide the ApiStrategy configuration if your node.js application runs on IBM Cloud and is bound to the App ID service instance. In this case, the App ID configuration will be obtained using VCAP_SERVICES environment variable.
{: tip}


#### Securing the API

The following snippet demonstrates how to use `ApiStrategy` in a simple Express app to protect the `/protected` GET API.

```javascript
 app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }), function(request, response){
    console.log("Securty context", request.securityContext);
    response.send(200, "Success!");
    }
 );
```
{: codeblock}

1. In case the tokens are valid, the next middleware in the request chain is called and the `appIdAuthorizationContext` property is added to the request object
2. The `appIdAuthorizationContext` property will contain original access and identity tokens as well as decoded payload information


### Securing APIs in Java WebSphere Liberty
TBD

### Securing APIs in Spring Boot applications
TBD

## Securing APIs without the SDKs

Securing your backend APIs with tokens involves in validating the tokens on the request. There are
several ways to validate the {{site.data.keyword.appid_short_notm}} access and identity tokens. Refer to the [Validate Tokens](tokens.html) section
for detailed information.
