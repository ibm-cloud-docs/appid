---

copyright:
  years: 2017
lastupdated: "2017-08-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Protecting Liberty for Java resources
{: #protecting-liberty}

You can use {{site.data.keyword.appid_short_notm}} to protect endpoints in your IBM Liberty for Java apps. Liberty for Java has the built in ability to handle Open ID Connect (OIDC) requests.

## Before you begin
{: #begin}

* You need an existing, unbound, [IBM Liberty for Java application](https://console.bluemix.net/catalog/starters/liberty-for-java). To become familiar with developing Liberty for Java apps, see [the docs](/docs/runtimes/liberty/index.html).
* Be sure you have [Apache Maven](https://maven.apache.org/download.cgi) installed.
* Learn about how OIDC works with Liberty for Java.

## Protecting resources in Liberty for Java
{: #protecting-liberty}

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


## Updating the Liberty for Java sample
{: #updating-liberty}

To make an update in the sample app, use the following instructions:

1. Create the servlets, jsp's, and html.
2. Define the protected resources and add them to the `web.xml` and `server.xml` authorization filters.
3. Create a war file and deploy it to Liberty for Java.

For more information about updating apps, see [adding {{site.data.keyword.appid_short_notm}} to an existing application](/docs/services/appid/existing.html#existing-liberty).
