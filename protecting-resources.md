---

copyright:
  years: 2017
lastupdated: "2017-11-29"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Protecting back-end resources

You can use the {{site.data.keyword.appid_short_notm}} server SDKs to protect endpoints in your applications.

## Protecting resources in Liberty for Java
{: #protecting-liberty}

You can use {{site.data.keyword.appid_short_notm}} to protect endpoints in your IBM Liberty for Java apps. Liberty for Java has the built in ability to handle Open ID Connect (OIDC) requests.

Before you begin:
* You need an existing, unbound, [IBM Liberty for Java application](https://console.bluemix.net/catalog/starters/liberty-for-java). To become familiar with developing Liberty for Java apps, see [the docs](/docs/runtimes/liberty/index.html).
* Be sure you have [Apache Maven](https://maven.apache.org/download.cgi) installed.
* Learn about how OIDC works with Liberty for Java.

To protect your resources:

1. Download the Liberty for Java sample from the UI. The sample contains a zip file with the standard Liberty files.
2. Open terminal at the directory where you extracted the sample.
3. Log in to {{site.data.keyword.Bluemix_notm}} by using the Cloud Foundry command line. When prompted, input your credentials.

  ```
  cf login
  ```
  {: codeblock}

4. Deploy the application. Running the following command creates a Liberty for Java instance with a name related to the tenantid.

  ```
  cf push
  ```
  {: codeblock}

5. Bind your service instance to the new Liberty for Java instance, and redeploy the application.
6. Open your application in a browser and login by using your credentials to review authentication activities.

## Protecting resources in Node.js
{: #protecting-resources-nodesdk}

The {{site.data.keyword.appid_short_notm}} server SDK provides an ApiStrategy passport strategy that is used in back-end applications that are deployed on {{site.data.keyword.Bluemix_notm}}. To protect your app from unauthorized access, you must instrument your Node.js server with the ApiStrategy. The `appid-serversdk-nodejs npm module` provides the ApiStrategy passport strategy and the verification method to validate the access token and ID token that are issued by {{site.data.keyword.appid_short_notm}}.

The {{site.data.keyword.appid_short_notm}} server SDK uses the <a href="http://passportjs.org/" target="_blank">Passport framework <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to enforce authorization.

The following snippet demonstrates how to use `APIStrategy` in a simple Express application to protect the `/protected` endpoint GET methods.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)    
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {: codeblock}
