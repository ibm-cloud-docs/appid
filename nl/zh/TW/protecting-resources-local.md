---

copyright:
  years:  2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}



#  將本端開發伺服器配置為使用 {{site.data.keyword.appid_short_notm}}
{: #protecting-local}

您可以配置本端環境來使用 {{site.data.keyword.appid_short}} 服務。尤其，您可以在本端使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 來開發程式碼，將要求傳送至開發伺服器。
{:shortdesc}


## 開始之前
{: #begin}

確定您已完成[伺服器 SDK 安裝](/docs/services/appid/install.html#nodejs-setup)。


## 配置 {{site.data.keyword.appid_short_notm}} 應用程式以使用本端開發伺服器
{: #configuring-local}

若要配置應用程式來使用本端開發伺服器，請在每一個要求中使用本端主機。

1. 將承租戶 ID 取代為 {{site.data.keyword.appid_short_notm}} 承租戶 ID。您可以在服務儀表板中找到此 ID。
2. 將地區取代為適當的地區，如下表所示。

<table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地區及對應的 Android 和 iOS {{site.data.keyword.appid_short_notm}} 地區</caption>
<tr>
  <th> Bluemix 地區</th>
  <th> Android 及 iOS </th>
</tr>
<tr>
  <td> 美國南部</td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> 雪梨</td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> 英國</td>
  <td> AppID.REGION_UK </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //set to your server running port
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, or AppID.REGION_UK.

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
 let region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, or AppID.REGION_UK.

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
