---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}



#  Configuring a local development server to work with {{site.data.keyword.appid_short_notm}}
{: #protecting-local}

You can configure your local environment to use the {{site.data.keyword.appid_short}} service. Specifically, you can develop code locally by using the {{site.data.keyword.appid_short_notm}} server SDK to send requests to the development server.
{:shortdesc}


## Before you begin
{: #begin}

Install the [server SDK](web-apps.html).


## Configuring {{site.data.keyword.appid_short_notm}} applications to work with a local development server
{: #configuring-local}

To configure your apps to work with a local development server, use the local host in each of your requests.

1. Replace the tenant ID with your {{site.data.keyword.appid_short_notm}} tenant ID. You can find this ID in your service dashboard.
2. Replace the region with the appropriate region as shown in the following table.

<table> <caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding {{site.data.keyword.appid_short_notm}} regions for Android and iOS </caption>
<tr>
  <th> {{site.data.keyword.Bluemix_notm}} Region </th>
  <th> Android and iOS </th>
</tr>
<tr>
  <td> US South </td>
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
  <td> Germany </td>
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
