---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: authentication, authorization, identity, app security, secure

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}


#  Configuration d'un serveur de développement local pour {{site.data.keyword.appid_short_notm}}
{: #protecting-local}

Vous pouvez configurer votre environnement local afin d'utiliser le service {{site.data.keyword.appid_short}}. Plus précisément, vous pouvez développer le code en local à
l'aide du logiciel SDK serveur d'{{site.data.keyword.appid_short_notm}} pour envoyer des demandes au serveur de développement.
{:shortdesc}


## Avant de commencer
{: #begin-local}

Installez le [logiciel SDK serveur](/docs/services/appid?topic=appid-web-apps).


## Configuration d'applications {{site.data.keyword.appid_short_notm}} pour leur utilisation avec un serveur de développement local
{: #configuring-local}

Pour configurer vos applications afin d'utiliser un serveur de développement local, utilisez l'hôte local dans chaque demande.

1. Remplacez l'ID titulaire par votre ID titulaire {{site.data.keyword.appid_short_notm}}. Vous pouvez localiser cet ID dans votre tableau de bord du service.
2. Remplacez la région par la région appropriée comme indiqué dans le tableau ci-dessous.

<table> <caption> Tableau 1. Régions {{site.data.keyword.cloud_notm}} et régions {{site.data.keyword.appid_short_notm}} correspondantes pour Android et iOS </caption>
<tr>
  <th> Région {{site.data.keyword.cloud_notm}} </th>
  <th> Android et iOS </th>
</tr>
<tr>
  <td> Sud des Etats-Unis </td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> Sydney </td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> Royaume-Uni </td>
  <td> AppID.REGION_UK </td>
</tr>
<tr>
  <td> Allemagne </td>
  <td> AppID.REGION_GERMANY </td>
</tr>
</table>



### Android
{: #android-local}


```java
String baseRequestUrl = "http://localhost:<port>"; //set to your server running port
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //set your {{site.data.keyword.appid_short_notm}} application region here. Les valeurs actuellement admises sont AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY et AppID.REGION_UK.

BMSClient bmsClient= BMSClient.getInstance();
bmsClient.initialize(getApplicationContext(), region);
AppID appId = AppID.getInstance();
appId.initialize(getApplicationContext(), tenantId, region);

AppIDAuthorizationManager appIDAuthorizationManager = new AppIDAuthorizationManager(appId);
bmsClient.setAuthorizationManager(appIDAuthorizationManager);

Request request = new Request(baseRequestUrl + "/resource/path", Request.GET);
request.send(this, new ResponseListener() {
    @Override
		public void onSuccess (Response response) {
        Log.d("Myapp", "onSuccess :: " + response.getResponseText());
		}
    @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
        if (null != t) {
            Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
            Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
            Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
    }
});
```
{: codeblock}

### iOS - Swift
{: #swift-local}
```swift

 let baseRequestUrl = "http://localhost:<port>"; //set to your server running port
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.REGION_UK; //set your {{site.data.keyword.appid_short_notm}} application region here. Les valeurs actuellement admises sont AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY et AppID.REGION_UK.

BMSClient.sharedInstance.initialize(region: AppID.<region>)
BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)

var request:Request =  Request(url: baseRequestUrl + "/resource/path", method: HttpMethod.GET)
request.send(completionHandler: {(response:Response?, error:Error?) in
    if let error = error {
            print("Connection failure")
     		print("Error :: \(error)");
     		print("Status :: \(response?.statusCode)");
    	} else {
            print("Connection success")
            print("Response :: \(response?.responseText)")
        }
});
```
{: codeblock}
