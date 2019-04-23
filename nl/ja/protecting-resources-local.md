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


#  {{site.data.keyword.appid_short_notm}} と連携するローカル開発サーバーの構成
{: #protecting-local}

ローカル環境を、{{site.data.keyword.appid_short}} サービスを使用するように構成できます。 具体的には、{{site.data.keyword.appid_short_notm}} Server SDK を使用してコードをローカルで開発し、要求を開発サーバーに送信できます。
{:shortdesc}


## 開始する前に
{: #begin-local}

[サーバー SDK](/docs/services/appid?topic=appid-web-apps) をインストールします。


## ローカル開発サーバーで作業するための {{site.data.keyword.appid_short_notm}} アプリケーションの構成
{: #configuring-local}

ローカルの開発サーバーで機能するようにアプリを構成するには、各要求でローカル・ホストを使用します。

1. テナント ID を {{site.data.keyword.appid_short_notm}} テナント ID に置き換えます。 この ID は、サービスのダッシュボードで確認できます。
2. 地域を、以下の表に示している該当地域に置き換えます。

<table> <caption> 表 1。{{site.data.keyword.cloud_notm}} 地域と対応する Android および iOS の {{site.data.keyword.appid_short_notm}} 地域 </caption>
<tr>
  <th> {{site.data.keyword.cloud_notm}} 地域 </th>
  <th> Android と iOS </th>
</tr>
<tr>
  <td> 米国南部 </td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> シドニー </td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> 英国 </td>
  <td> AppID.REGION_UK </td>
</tr>
<tr>
  <td> ドイツ </td>
  <td> AppID.REGION_GERMANY </td>
</tr>
</table>



### Android
{: #android-local}


```java
String baseRequestUrl = "http://localhost:<port>"; //サーバーの実行ポートを設定
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //{{site.data.keyword.appid_short_notm}} アプリケーションの地域をここで設定。 現在使用可能な値は AppID.REGION_US_SOUTH、AppID.REGION_SYDNEY、 AppID.REGION_GERMANY、または AppID.REGION_UK。

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

 let baseRequestUrl = "http://localhost:<port>"; //サーバーの実行ポートを設定
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.REGION_UK; //{{site.data.keyword.appid_short_notm}} アプリケーションの地域をここで設定。 現在使用可能な値は AppID.REGION_US_SOUTH、AppID.REGION_SYDNEY、 AppID.REGION_GERMANY、または AppID.REGION_UK。

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
