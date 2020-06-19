---

copyright:
  years: 2017, 2020
lastupdated: "2020-06-19"

keywords: obtain tokens, return tokens, authorized, authorization, access management, client id, secret, tenant id, app security, identity token

subcollection: appid

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
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




# Obtaining tokens
{: #obtain-tokens}

When users or backend services interact with your app, they might need to be authorized to perform specific actions. {{site.data.keyword.appid_short_notm}} verifies that the entity that makes the request is authorized and returns access and identity tokens to your app. If the entity making the request is an end user, the tokens might contain information about the user such as the scope of their permissions and their name. If it is a backend service, then only an access token is returned.
{: shortdesc}


## Getting your client ID and secret
{: #obtain-clientid-secret}

In order to obtain tokens, you must have your client ID and secret. The credentials are specific to every application and are used to help identify and validate the users that a token might be assigned to. 
{: shortdesc}


### By using the GUI
{: #credentials-gui}

1. Navigate to the **Applications** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. If you already have a set of credentials listed, you can skip to step 3. If you do not, create one.
    1. On the **Applications** tab, click **Add application**.
    2. Give your application a name and click **Save** to return to a list of your registered apps. The name of your application cannot exceed 50 characters.

3. From the list of registered apps, select the application that you want to work with. The row expands to show your credentials.

4. Copy your client ID and secret.


### By using the API
{: #credentials-api}

1.  Make a POST request to the [`/management/v4/{tenantId}/applications` endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication).

  Request:

  ```sh
  curl -X POST https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <IAM_TOKEN>' \
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



## Obtaining access and identity tokens
{: #obtain-access-id-tokens}

With a client ID and secret, you can obtain access and identity tokens by using the following steps.
{: shortdesc}


### Obtaining tokens by using an SDK
{: obtain-token-sdk}

1. Obtain your tenant ID, client ID, secret, and OAuth Server URL from your credentials.

2. Using the information from step 1, update the following code snippet and add it into your application. The default code is for Node.js. If you're working with another language, you can choose the one that applies to you at the beginning of this topic.

  Node:
  {: ph data-hd-programlang='javascript'}

  ```javascript
  const config = {
    tenantId: "{tenant-id}",
    clientId: "{client-id}",
    secret: "{secret}",
    oauthServerUrl: "{oauth-server-url}"
  };

  const TokenManager = require('ibmcloud-appid').TokenManager;

  const tokenManager = new TokenManager(config);

  async function getAppIdentityToken() {
    try {
        const tokenResponse = await tokenManager.getApplicationIdentityToken();
        console.log('Token response : ' + JSON.stringify(tokenResponse));

        //the token response contains the access_token, expires_in, token_type
    } catch (err) {
        console.log('err obtained : ' + err);
    }
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

  Java:
  {: ph data-hd-programlang='java'}

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
  {: ph data-hd-programlang='java'}

iOS Swift:
{: ph data-hd-programlang='swift'}

  ```swift
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
  {: ph data-hd-programlang='swift'}

Server Swift:
{: ph data-hd-programlang='swift'}

  ```swift
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
  {: ph data-hd-programlang='swift'}


</br>

### Obtaining tokens by using the API
{: #obtain-tokens-api}

1. Obtain your tenant ID, client ID, secret, and OAuth Server URL from your credentials.

2. Encode your client ID and secret.

    1. Copy your client ID and secret using the steps from the previous section.
    2. Use a base64 encoder to encode your authorization information.
    3. Copy the output.

3. Make a request to the API to obtain a token. The data section of your request varies depending on the type of grant type that you're using. 

  ```sh
  curl -X GET https://<region>.appid.cloud.ibm.com/oauth/v4/<tenant_id>/token \
  -H 'Authorization: Basic base64Encoded{{client-ID}:{client-secret}}' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H 'Accept: application/json' \
  -F grant_type=password \
  -F username=testuser@test.com \
  -F password=testuser
  ```
  {: codeblock}

  If you don't have an application, you can use the same command but replace `GET` with `POST`.
  {: tip}

The type of grant type that you use to obtain your token can differ depending on the type of authorization that you're working with. For a detailed list of options, check out the [swagger documentation](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token).
