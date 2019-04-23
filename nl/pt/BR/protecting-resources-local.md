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


#  Configurando um servidor de desenvolvimento local para trabalhar com o {{site.data.keyword.appid_short_notm}}
{: #protecting-local}

É possível configurar o seu ambiente local para usar o serviço do {{site.data.keyword.appid_short}}. Especificamente, é possível desenvolver o código
localmente usando o SDK do servidor {{site.data.keyword.appid_short_notm}} para enviar solicitações ao servidor de desenvolvimento.
{:shortdesc}


## Antes de iniciar
{: #begin-local}

Instale o [SDK do servidor](/docs/services/appid?topic=appid-web-apps).


## Configurando aplicativos {{site.data.keyword.appid_short_notm}} para trabalhar com um servidor de desenvolvimento local
{: #configuring-local}

Para configurar os seus apps para trabalharem com um servidor de desenvolvimento local, use o host local em cada uma de suas solicitações.

1. Substitua o ID do locatário pelo seu ID do locatário do {{site.data.keyword.appid_short_notm}}. É possível localizar esse ID em seu painel de
serviço.
2. Substitua a região pela região apropriada, conforme mostrado na tabela a seguir.

<table> <caption> Tabela 1. Regiões do {{site.data.keyword.cloud_notm}} e regiões do {{site.data.keyword.appid_short_notm}} correspondentes para Android e iOS </caption>
<tr>
  <th> {{site.data.keyword.cloud_notm}} Região </th>
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
<tr>
  <td> Alemanha </td>
  <td> AppID.REGION_GERMANY </td>
</tr>
</table>



### Android
{: #android-local}


```java
String baseRequestUrl = "http://localhost: < port>"; // configurado para a porta de execução do servidor
String tenantId = "service-AppID-service-tenantID";
Cadeia region = AppID.REGION_UK; // configura a região do aplicativo { {site.data.keyword.appid_short_notm } } aqui. Atualmente, os valores possíveis são AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY ou AppID.REGION_UK.

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
 let region = AppID.REGION_UK; //set your {{site.data.keyword.appid_short_notm}} application region here. Atualmente, os valores possíveis são AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY ou AppID.REGION_UK.

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
