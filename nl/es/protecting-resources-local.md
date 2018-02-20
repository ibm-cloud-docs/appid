---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}



#  Configuración de un servidor de desarrollo local para trabajar con {{site.data.keyword.appid_short_notm}}
{: #protecting-local}

Puede configurar su entorno local para que utilice el servicio {{site.data.keyword.appid_short}}. Específicamente, puede desarrollar código de forma local utilizando el SDK de servidor de {{site.data.keyword.appid_short_notm}} para enviar solicitudes al servidor de desarrollo.
{:shortdesc}


## Antes de empezar
{: #begin}

Asegúrese de que ha completado la [instalación del SDK de servidor](/docs/services/appid/install.html#nodejs-setup).


## Configuración de aplicaciones de {{site.data.keyword.appid_short_notm}} para que funcionen con un servidor de desarrollo local
{: #configuring-local}

Para configurar sus apps para trabajar con un servidor de desarrollo local, utilice el host local en cada una de las solicitudes.

1. Sustituya el ID de arrendatario por su ID de arrendatario de {{site.data.keyword.appid_short_notm}}. Encontrará este ID en su panel de control del servicio.
2. Sustituya la región por la región adecuada, como se muestra en la tabla siguiente.

<table> <caption> Tabla 1. Regiones de {{site.data.keyword.Bluemix_notm}} y regiones de {{site.data.keyword.appid_short_notm}} correspondientes para Android e iOS </caption>
<tr>
  <th> Región Bluemix </th>
  <th> Android e iOS </th>
</tr>
<tr>
  <td> Sur de EE.UU. </td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> Sídney </td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> Reino Unido </td>
  <td> AppID.REGION_UK </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //defina el puerto de ejecución del servidor
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //defina aquí su región de aplicación App ID. Los valores posibles son AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY o AppID.REGION_UK.

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

 let baseRequestUrl = "http://localhost:<port>"; //defina el puerto de ejecución del servidor
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.REGION_UK; //defina aquí su región de aplicación App ID. Los valores posibles son AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY o AppID.REGION_UK.

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
