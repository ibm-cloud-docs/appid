---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}



#  Configurando um servidor de desenvolvimento local para trabalhar com o {{site.data.keyword.appid_short_notm}}
{: #protecting-local}

É possível configurar o seu ambiente local para usar o serviço do {{site.data.keyword.appid_short}}. Especificamente, é possível desenvolver o código
localmente usando o SDK do servidor {{site.data.keyword.appid_short_notm}} para enviar solicitações ao servidor de desenvolvimento.
{:shortdesc}


## Antes de iniciar
{: #begin}

Certifique-se de ter concluído a [instalação do SDK do servidor](/docs/services/appid/install.html#nodejs-setup).


## Configurando aplicativos {{site.data.keyword.appid_short_notm}} para trabalhar com um servidor de desenvolvimento local
{: #configuring-local}

Para configurar os seus apps para trabalharem com um servidor de desenvolvimento local, use o host local em cada uma de suas solicitações.

1. Substitua o ID do locatário pelo seu ID do locatário do {{site.data.keyword.appid_short_notm}}. É possível localizar esse ID em seu painel de
serviço.
2. Substitua a região pela região apropriada, conforme mostrado na tabela a seguir.

<table> <caption> Tabela 1. Regiões do {{site.data.keyword.Bluemix_notm}} e regiões do {{site.data.keyword.appid_short_notm}} correspondentes para Android e iOS </caption>
<tr>
  <th> Região do Bluemix </th>
  <th> Android e iOS </th>
</tr>
<tr>
  <td> Sul dos Estados Unidos </td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> Sydney </td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> United Kingdom </td>
  <td> AppID.REGION_UK </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //set to your server running port
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, or
AppID.REGION_UK.

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

 let baseRequestUrl = "http://localhost:<port>"; //set to your server running port
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, or
AppID.REGION_UK.

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
