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


#  Configurazione di un server di sviluppo locale per utilizzare {{site.data.keyword.appid_short_notm}}
{: #protecting-local}

Puoi configurare il tuo ambiente locale per utilizzare il servizio {{site.data.keyword.appid_short}}. Nello specifico, puoi sviluppare il codice localmente utilizzando l'SDK server {{site.data.keyword.appid_short_notm}} per inviare le richieste al server di sviluppo.
{:shortdesc}


## Prima di cominciare
{: #begin-local}

Installa l'[SDK server](/docs/services/appid?topic=appid-web-apps).


## Configurazione delle applicazioni {{site.data.keyword.appid_short_notm}} per lavorare con un server di sviluppo locale
{: #configuring-local}

Per configurare le tue applicazioni in modo che utilizzino un server di sviluppo locale, utilizza l'host locale in ognuna delle tue risposte.

1. Sostituisci l'ID tenant con il tuo ID tenant {{site.data.keyword.appid_short_notm}}. Puoi trovare questo ID nel tuo dashboard del servizio
2. Sostituisci la regione con la regione appropriata come descritto nella seguente tabella.

<table> <caption> Tabella 1. Regioni {{site.data.keyword.cloud_notm}} e regioni SDK Android e iOS {{site.data.keyword.appid_short_notm}} corrispondenti </caption>
<tr>
  <th> Regione {{site.data.keyword.cloud_notm}} </th>
  <th> Android e iOS </th>
</tr>
<tr>
  <td> Stati Uniti Sud </td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> Sydney </td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> Regno Unito </td>
  <td> AppID.REGION_UK </td>
</tr>
<tr>
  <td> Germania </td>
  <td> AppID.REGION_GERMANY </td>
</tr>
</table>



### Android
{: #android-local}


```java
String baseRequestUrl = "http://localhost:<port>"; //set to your server running port
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //set your {{site.data.keyword.appid_short_notm}} application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY, or AppID.REGION_UK.

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
 let region = AppID.REGION_UK; //set your {{site.data.keyword.appid_short_notm}} application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY, or AppID.REGION_UK.

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
