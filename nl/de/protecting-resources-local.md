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


#  Lokalen Entwicklungsserver für Verwendung mit {{site.data.keyword.appid_short_notm}} konfigurieren
{: #protecting-local}

Sie können Ihre lokale Umgebung so konfigurieren, dass sie den {{site.data.keyword.appid_short}}-Service verwendet. Insbesondere können Sie Code lokal entwickeln, indem Sie das {{site.data.keyword.appid_short_notm}}-Server-SDK verwenden, um Anforderungen an den Entwicklungsserver zu senden.
{:shortdesc}


## Vorbereitungen
{: #begin-local}

Installieren Sie das [Server-SDK](/docs/services/appid?topic=appid-web-apps).


## {{site.data.keyword.appid_short_notm}}-Anwendungen zur Arbeit mit einem lokalen Entwicklungsserver konfigurieren
{: #configuring-local}

Um Ihre Apps so zu konfigurieren, dass sie mit einem lokalen Entwicklungsserver arbeiten, verwenden Sie den lokalen Host in jeder Anforderung.

1. Ersetzen Sie die Tenant-ID durch Ihre {{site.data.keyword.appid_short_notm}}-Tenant-ID. Diese ID befindet sich in Ihrem Service-Dashboard.
2. Ersetzen Sie die Region durch die richtige Region, wie in der folgenden Tabelle dargestellt.

<table> <caption> Tabelle 1. {{site.data.keyword.cloud_notm}}-Regionen und entsprechende {{site.data.keyword.appid_short_notm}}-Regionen für Android und iOS </caption>
<tr>
  <th> {{site.data.keyword.cloud_notm}}-Region </th>
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
<tr>
  <td> Deutschland </td>
  <td> AppID.REGION_GERMANY </td>
</tr>
</table>



### Android
{: #android-local}


```java
String baseRequestUrl = "http://localhost:<port>"; // Auf den aktiven Port Ihres Servers festlegen.
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; // Hier die {{site.data.keyword.appid_short_notm}}-Anwendungsregion festlegen. Derzeit sind folgende Werte möglich: AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY und AppID.REGION_UK.

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

 let baseRequestUrl = "http://localhost:<port>"; // Auf den aktiven Port Ihres Servers festlegen.
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.REGION_UK; // Hier die {{site.data.keyword.appid_short_notm}}-Anwendungsregion festlegen. Derzeit sind folgende Werte möglich: AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY und AppID.REGION_UK.

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
