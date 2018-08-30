---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-30"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Securing app to app communication
{: #app}

With App ID, you can secure app to app communication by leveraging OAuth2.0 capabilities.
{: shortdesc}



## Understanding the communication flow
{: #understanding}


**How does the grant flow work?**

App ID leverages the OAuth2.0 client credentials grant flow to facilitate communication. After an app registers with App ID, the app itself obtains a client ID and secret. With this information, the app can request an access token from App ID and be authorized to access a protected resource or API. In the app-to-app flow, the application is granted only an access token. It does not obtain an identity token or a refresh token. For more information about tokens, see [Understanding tokens](tokens.html#tokens).

The application always holds the client secret. This work flow is meant to be used only with trusted applications where there is no risk of the secret being misused or leaked.
{: tip}

**What does the grant flow look like?**

In the following image, you can see the direction of communication between the service and your application.


![{{site.data.keyword.appid_short_notm}} app-to-app flow](/images/app-to-app-flow.svg)


1. A service registers with App iD to obtain a client ID and secret.
2. The application makes a request to App ID by sending the credentials retrieved in the previous step.
3. App ID validates the request, authenticates the app, and returns a response that contains an access token.
4. The application is now able to use the access token to send requests to a protected resource.

**When would this flow be useful?**
There are several reasons that you might want one application to communicate with another service or app without any user intervention. For example, a non-interactive app that needs to access a backend cloud-based service to store data that it uses to perform its work, rather than data that is specifically owned by an end-user. Other examples could include processes, CLIs, daemons, or an IoT device that monitors and reports environment variables to an upstream server. The specific use case is unique to each app, but the most important thing to remember is that the requests are exchanged on behalf of the app, not on an end user, and it is the app that is authenticated and authorized.




## Registering your app
{: #registering}

**Registering your app with the GUI**

1. In the **Application** tab of the App ID dashboard, click **Add Application**.
2. Add your application name and click **Save** to return to a list of your registered apps. The name of your application cannot exceed 50 characters.
3. From the list of registered apps, select the application that you added in the previous step. The row expands to show your credentials.

**Registering your app with the API**

1. Make a post request to the `/management/{tenantId}/applications` endpoint.

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


After your app is registered with App ID and you have obtained your credentials, you can make a request to the App ID authorization server to get an Access Token.

1. Make an HTTP POST request to the `/management/{tenantId}/token` endpoint. The authorization for the request is `Basic auth` with the client ID and secret being used as the username and password which are base 64 encoded.

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


