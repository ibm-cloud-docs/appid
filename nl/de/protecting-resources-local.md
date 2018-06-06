---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}



#  Lokalen Entwicklungsserver für die Verwendung mit {{site.data.keyword.appid_short_notm}} konfigurieren
{: #protecting-local}

Sie können Ihre lokale Umgebung so konfigurieren, dass sie den {{site.data.keyword.appid_short}}-Service verwendet. Insbesondere können Sie Code lokal entwickeln, indem Sie das {{site.data.keyword.appid_short_notm}}-Server-SDK verwenden, um Anforderungen an den Entwicklungsserver senden.
{:shortdesc}


## Vorbereitungen
{: #begin}

Die [Server-SDK-Installation](/docs/services/appid/install.html#nodejs-setup) muss abgeschlossen sein.


## {{site.data.keyword.appid_short_notm}}-Anwendungen zur Arbeit mit einem lokalen Entwicklungsserver konfigurieren
{: #configuring-local}

Um Ihre Apps so zu konfigurieren, dass sie mit einem lokalen Entwicklungsserver arbeiten, verwenden Sie den lokalen Host in jeder Anforderung.

1. Ersetzen Sie die Tenant-ID durch Ihre {{site.data.keyword.appid_short_notm}}-Tenant-ID. Diese ID befindet sich in Ihrem Service-Dashboard.
2. Ersetzen Sie die Region durch die richtige Region, wie in der folgenden Tabelle dargestellt.

<table> <caption> Tabelle 1. {{site.data.keyword.Bluemix_notm}}-Regionen und entsprechende {{site.data.keyword.appid_short_notm}}-Regionen für Android und iOS </caption>
<tr>
  <th> Bluemix-Region </th>
  <th> Android und iOS </th>
</tr>
<tr>
  <td> Vereinigte Staaten (Süden) </td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> Sydney </td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> Vereinigtes Königreich </td>
  <td> AppID.REGION_UK </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //set to your server running port
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //set your App ID application region here. Aktuell mögliche Werte sind AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY oder AppID.REGION_UK.

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
{: #swift}
```swift

 let baseRequestUrl = "http://localhost:<port>"; //auf Server festgelegt, der den Port ausführt
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.REGION_UK; //Region der App ID-Anwendung hier festlegen. Aktuell mögliche Werte sind AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY oder AppID.REGION_UK.

BMSClient.sharedInstance.initialize(bluemixRegion: region)
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
