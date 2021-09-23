---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-23"

keywords: obtain tokens, return tokens, authorized, authorization, access management, client id, secret, tenant id, app security, identity token

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



# Obtaining tokens
{: #obtain-tokens}

When users or backend services interact with your app, they might need to be authorized to perform specific actions. {{site.data.keyword.appid_short_notm}} verifies that the entity that makes the request is authorized and returns access and identity tokens to your app. If the entity making the request is an end user, the tokens might contain information about the user such as the scope of their permissions and their name. If it is a backend service, then only an access token is returned.
{: shortdesc}


## Getting your client ID and secret with the GUI
{: #obtain-clientid-secret}
{: ui}

In order to obtain tokens, you must have your client ID and secret. The credentials are specific to every application and are used to help identify and validate the users that a token might be assigned to. 
{: shortdesc}

1. Navigate to the **Applications** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. If you already have a set of credentials listed, you can skip to step 3. If you do not, create one.
    1. On the **Applications** tab, click **Add application**.
    2. Give your application a name and click **Save** to return to a list of your registered apps. The name of your application cannot exceed 50 characters.

3. From the list of registered apps, select the application that you want to work with. The row expands to show your credentials.

4. Copy your client ID and secret.


## Getting your client ID and secret with the API
{: #credentials-api}
{: api}

In order to obtain tokens, you must have your client ID and secret. The credentials are specific to every application and are used to help identify and validate the users that a token might be assigned to. 
{: shortdesc}

1.  Make a POST request to the [`/management/v4/{tenantId}/applications` endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication).

  Request:

  ```sh
  curl -X POST https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {IAM_TOKEN}' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  Example response:

  ```json
  {
    "clientId": "c90830bf-11b0-4b65-bffe-9773f8703bad",
    "tenantId": "b42f7429-fc24-48ds-b4f9-616bcc31cfd5",
    "secret": "YWQyNjdkZjMtMGRhZC00ZWRkLThiOTQtN2E3ODEyZjhkOWQz",
    "name": "testing",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48ds-b4f9-616bcb31cfd5",
    "profilesUrl": "https://us-south.appid.cloud.ibm.com",
    "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48ds-b4f9-616bcb31cfd5/.well-known/openid-configuration"
  }
  ```
  {: screen}

2. Copy the client ID and secret.


## Obtaining access and identity tokens with the GUI
{: #obtain-access-id-tokens}
{: #ui}

With a client ID and secret, you can obtain access and identity tokens by using the API or an SDK. The following examples show how to obtain a token by using the Resource Owner Password (ROP) flow.

This action can be done through the API only. To see the steps, switch to the API instructions.
{: note}

## Obtaining access and identity tokens with the API
{: #obtain-access-id-tokens}
{: api}

With a client ID and secret, you can obtain access and identity tokens by using the API or an SDK. The following examples show how to obtain a token by using the Resource Owner Password (ROP) flow.


1. Obtain your tenant ID, client ID, secret, and OAuth Server URL from your credentials.

2. Encode your client ID and secret by using a base64 encoder.

3. Use the following code examples to retrieve your tokens. The grant type that you use to obtain your token can differ depending on the type of authorization that you're working with. For a detailed list of options, check out the [swagger documentation](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token){: external}.

  
  ```sh
  curl -X POST 'https://{region}.appid.cloud.ibm.com/oauth/v4/{tenant_id}/token' \
  -H 'Authorization: Basic base64Encoded{{client-ID}:{client-secret}}' \
  -H 'Accept: application/json' \
  -F 'grant_type=password' \
  -F 'username=testuser@test.com' \
  -F 'password=testuser'
  ```
  {: codeblock}
  {: curl}

  
  ```swift
  // iOS Swift example

  class delegate : TokenResponseDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
    //User authenticated
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
    //Exception occurred
    }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}
  {: swift}

  
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password, new TokenResponseListener() {
    @Override
    public void onAuthorizationFailure (AuthorizationException exception) {
        //Exception occurred
    }

    @Override
    public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
        //User authenticated
    }
  });
  ```
  {: codeblock}
  {: java}

  

  ```javascript
  // Declare the API you want to protect
  app.get("/api/protected",

    passport.authenticate(APIStrategy.STRATEGY_NAME, {
      session: false
    }),
    function(req, res) {
      // Get full appIdAuthorizationContext from request object
      var appIdAuthContext = req.appIdAuthorizationContext;

      appIdAuthContext.accessToken; // Raw access_token
      appIdAuthContext.accessTokenPayload; // Decoded access_token JSON
      appIdAuthContext.identityToken; // Raw identity_token
      appIdAuthContext.identityTokenPayload; // Decoded identity_token JSON
      appIdAuthContext.refreshToken; // Raw refresh_token
      ...
    }
  );
  ```
  {: codeblock}
  {: javascript}

  
  ```swift
  // Server-side swift example

  let options = [
    "clientId": "{client-id}",
    "secret": "{secret}",
    "tenantId": "{tenant-id}",
    "oauthServerUrl": "{oauth-server-url}",
    "redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  ```
  {: codeblock}
  {: swift}


