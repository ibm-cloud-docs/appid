---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Securing app to app communication
{: #app}

With {{site.data.keyword.appid_short_notm}}, you can secure app to app communication by leveraging OAuth2.0 capabilities.
{: shortdesc}


## Understanding the communication flow
{: #understanding}

**When would this flow be useful?**

There are several reasons that you might want one application to communicate with another service or app without any user intervention. For example, a non-interactive app that needs to access another application to perform its work. This could include processes, CLIs, daemons, or an IoT device that monitors and reports environment variables to an upstream server. The specific use case is unique to each application, but the most important thing to remember is that the requests are exchanged on behalf of the app, not on an end user, and it is the app that is authenticated and authorized.

</br>

**How does the app to app flow work?**

{{site.data.keyword.appid_short_notm}} leverages the OAuth2.0 client credentials  flow to protect communication. After an app registers with {{site.data.keyword.appid_short_notm}}, the app obtains a client ID and secret. With this information, the app can request an access token from {{site.data.keyword.appid_short_notm}} and be authorized to access a protected resource or API. In the app to app flow, the application is granted only an access token. It does not obtain an identity token or a refresh token. For more information about tokens, see [Understanding tokens](tokens.html#tokens).

This flow should be used only with trusted web apps. It will not work for mobile apps.

The application always holds the client secret. This work flow is meant to be used only with trusted applications where there is no risk of the secret being misused or leaked.
{: tip}

</br>

**What does the flow look like?**

In the following image, you can see the direction of communication between the service and your application.

![{{site.data.keyword.appid_short_notm}} app to app flow](/images/app-to-app-flow.svg)
Figure. App to app flow

1. A service registers with {{site.data.keyword.appid_short_notm}} to obtain a client ID and secret.
2. Application A makes a request to {{site.data.keyword.appid_short_notm}} by sending the credentials retrieved in the previous step.
3. {{site.data.keyword.appid_short_notm}} validates the request, authenticates the app, and returns a response to Application A that contains an access token.
4. Application A is now able to use the access token to send requests to Application B such as object storage or another protected resource.

</br>

## Registering your app
{: #registering}

</br>

**Registering your app with the GUI**

1. In the **Application** tab of the {{site.data.keyword.appid_short_notm}} dashboard, click **Add Application**.
2. Add your application name and click **Save** to return to a list of your registered apps. The name of your application cannot exceed 50 characters.
3. From the list of registered apps, select the application that you added in the previous step. The row expands to show your credentials.

</br>

**Registering your app with the API**

1. Make a POST request to the [`/management/v4/{tenantId}/applications` endpoint](https://appid-management.ng.bluemix.net/swagger-ui/#!/Applications/getAllApplications).

  Request:
  ```
  curl -X POST \  https://appid-management.ng.bluemix.net/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
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
   "oAuthServerUrl": "https://appid-oauth.eu-gb.bluemix.net/oauth/v3/39a37f57-a227-4bfe-a044-93b6e6060b61"
   }
  ```
  {: codeblock}



## Obtaining an access token
{: #obtain-token}

After your app is registered with {{site.data.keyword.appid_short_notm}} and you have obtained your credentials, you can make a request to the {{site.data.keyword.appid_short_notm}} authorization server to get an Access Token.

1. Make an HTTP POST request to the [`/oauth/v3/{tenantId}/token` endpoint](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/token). The authorization for the request is `Basic auth` with the client ID and secret being used as the username and password which are base64 encoded.

  Request :
  ```
  curl -X POST \
    http://localhost:6002/oauth/v3/39a37f57-a227-4bfe-a044-93b6e6060b61/token \
    -H 'Authorization: Basic base64Encoded{clientId:secret}' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    -d grant_type=client_credentials
  ```
  {: codeblock}

  Example response:
  ```
  {
  "access_token": "eyJhbGciOiJS...F9A",
  "expires_in": "3600",
  "token_type": "Bearer"
  }
  ```
  {: codeblock}


## Tutorial: End-to-end flow with the Node.js SDK
{: tutorial-node}

1. Obtain an [access token](authorization.html#tokens) in one of the following ways:
  * From the {{site.data.keyword.appid_short_notm}} Node.js SDK by using the token manager. Initialize the token manager with your app credentials and make a call to the `getAppIdentityToken()` method to obtain the token.

    ```
    const TokenManager = require('ibmcloud-appid').TokenManager;
    const config = {
     clientId: "29a19759-aafb-41c7-9ef7-ee7b0ca88818",
     tenantId: "39a37f57-a227-4bfe-a044-93b6e6060b61",
     secret: "ZTEzZTA2MDAtMjljZS00MWNlLTk5NTktZDliMjY3YzUxZTYx",
     oauthServerUrl: "https://appid-oauth.eu-gb.bluemix.net/oauth/v3/39a37f57-a227-4bfe-a044-93b6e6060b61"
    };


    const tokenManager = new TokenManager(config);


    tokenManager.getAppIdentityToken().then((appIdAuthContext) => {
     console.log(' Access tokens from SDK : ' + JSON.stringify(appIdAuthContext));
    }).catch((err) => {
     //console.error('Error retrieving tokens : ' + err);
    });
    ```
    {: codeblock}

  * From the {{site.data.keyword.appid_short_notm}} authorization server. **Note**: The `oauthServerUrl` in the request is obtained when you register your application. If you registered your app with the management APIs, the server URL is in the response body. If you registered your app by binding it with the IBM Cloud console, the URL can be found in your VCAP_SERVICES JSON object or through your Kubernetes secrets.

    ```
    var request = require('request');

    function getAccessToken() {
      let options = {
          method: 'POST',
          url: oauthServerUrl + '/token',
          headers: { 'content-type': 'application/x-www-form-urlencoded',
              'Authorization': 'Basic ' +Buffer.from('clientId: secret').toString('base64')
          },
          form: {
              grant_type: 'client_credentials'
          }
      };

      return new Promise((resolve, reject) => {
          request(options, function (error, response, body) {
              if (error) {
                  return reject(error);
              }

              let data = JSON.parse(body);
              if(data.access_token) {
                  resolve(data.access_token);
              } else {
                  reject(data);
              }
          })
      });

    }
    ```
    {: codeblock}

2. Make a request to your protected resource by using the access token that you obtained in the previous step.

  ```
  let options = {
      method: 'GET',
      url: 'http://localhost:8081/protected_resource',
      headers: { authorization : 'Bearer ' + accessToken}
  }

  request(options, function (error, response, body) {
      if (error) {
       console.log(error)
      } else {
          res.status(response.statusCode).send({
      console.log(JSON.stringify(body));
          });
      }
  });
  ```
  {: codeblock}

3. Secure your protected resources by using the API strategy from the {{site.data.keyword.appid_short_notm}} Node SDK.

  ```
  const express = require('express'),
    passport = require('passport');

  var app = express();
  app.use(passport.initialize());

  passport.use(new APIStrategy({
      oauthServerUrl: "https://appid-oauth.eu-gb.bluemix.net/oauth/v3/398ec248-5e93-48b8-a122-ccabc714fe85",
      tenantId:"398ec248-5e93-48b8-a122-ccabc714fe85"
  }));


  app.get('/protected_resource',
      passport.authenticate(APIStrategy.STRATEGY_NAME, {session: false}),
      (req, res) => {

          res.send("Hello from protected resource");
  });
  ```
  {: codeblock}
