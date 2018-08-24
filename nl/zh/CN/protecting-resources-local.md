---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}



#  配置本地开发服务器以用于 {{site.data.keyword.appid_short_notm}}
{: #protecting-local}

您可以将本地环境配置为使用 {{site.data.keyword.appid_short}} 服务。具体来说，您可以使用 {{site.data.keyword.appid_short_notm}} 服务器 SDK 在本地开发代码，以向开发服务器发送请求。
{:shortdesc}


## 开始之前
{: #begin}

确保[已安装服务器 SDK](/docs/services/appid/install.html#nodejs-setup)。


## 将 {{site.data.keyword.appid_short_notm}} 应用程序配置为使用本地开发服务器
{: #configuring-local}

要将应用程序配置为使用本地开发服务器，请在每个请求中使用本地主机。

1. 将租户标识替换为您的 {{site.data.keyword.appid_short_notm}} 租户标识。您可以在服务仪表板中找到此标识。
2. 将区域替换为相应的区域，如下表中所示。

<table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 区域及对应的 Android 和 iOS {{site.data.keyword.appid_short_notm}} 区域</caption>
<tr>
  <th> {{site.data.keyword.Bluemix_notm}} 区域</th>
  <th> Android 和 iOS </th>
</tr>
<tr>
  <td> 美国南部</td>
  <td> AppID.REGION_US_SOUTH</td>
</tr>
<tr>
  <td> 悉尼</td>
  <td> AppID.REGION_SYDNEY</td>
</tr>
<tr>
  <td> 英国</td>
  <td> AppID.REGION_UK</td>
</tr>
<tr>
  <td> 德国</td>
  <td> AppID.REGION_GERMANY </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //set to your server running port
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY, or AppID.REGION_UK.

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
 let region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, AppID.REGION_GERMANY, or AppID.REGION_UK.

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
