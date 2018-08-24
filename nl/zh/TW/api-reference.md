---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 使用 API 管理 {{site.data.keyword.appid_short_notm}}
{: manging-api}

您可以使用管理 API，對您的 {{site.data.keyword.appid_full}} 實例進行 DevOps 自動化、自訂及管理。
{: shortdesc}

管理 API 是使用 {{site.data.keyword.cloudaccesstraillong}} 產生的記號來保護。使用 IAM，帳戶擁有者可以指定其團隊成員對每個服務實例的存取層次。如需 IAM 與 {{site.data.keyword.appid_short_notm}} 如何合作的相關資訊，請參閱[服務存取管理](/docs/services/appid/iam.html)。

使用 API，您可以：
* 在 DevOps 處理程序的應用程式中自動配置 {{site.data.keyword.appid_short_notm}}。
* 透過應用程式後端設定及自訂功能，例如您的登入小組件配置、註冊處理程序及使用者管理。


呼叫管理 API 端點採用下列結構：

```
appid-management.<region>.bluemix.net
```
{: codeblock}

您可以在下表中尋找，以找出地區。

<table>
  <tr>
    <th>{{site.data.keyword.Bluemix}} 地區</th>
    <th>端點</th>
  </tr>
  <tr>
    <td>英國</td>
    <td><code>appid-management.eu-gb.bluemix.net</code></td>
  </tr>
  <tr>
    <td>美國南部</td>
    <td><code>appid-management.ng.bluemix.net</code></td>
  </tr>
  <tr>
    <td>雪梨</td>
    <td><code>appid-management.au-syd.bluemix.net</code></td>
  </tr>
  <tr>
    <td>德國</td>
    <td><code>appid-management.eu-de.bluemix.net</code></td>
  </tr>
</table>



## 必要條件
{: #api-prereq}

<ul><ul><li>一個在 2018 年 3 月 15 日之後建立的服務實例。如果您的服務實例是在該日期之前所建立，請建立新的實例，並將它配置為符合您的現行實例。請務必更新您的應用程式以使用新的實例。</li>
<li>已安裝 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html)。</li></ul></ul>

## 範例用法
{: #api-example}

在下列範例中，您可以看到如何使用 API 來變更含 Python 的 {{site.data.keyword.appid_short_notm}} 承租戶標誌。

```
import requests
import json

tenantId = '<App ID instance>'
Img = '<Logo file location>'
apiKey = '<IAM AI key>'

# get IAM token
headers = {'Content-Type': 'application/x-www-form-urlencoded', 'Accept':'application
/json'}
data = 'grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=' + apiKey;

r = requests.post("https://iam.ng.bluemix.net/oidc/token", data=data, headers=
headers);
token = 'Bearer ' + json.loads(r.text)['access_token'];

#  set login widget logo
headers = {'Authorization': token , 'Accept':'application/json'}
files = {'file': open(img,'rb')}

r = requests.post("https://appid-management.<region>.bluemix.net/management/v4/" + te
nantId + "/config/ui/media?mediaType=logo", files=files, headers=headers);

#  get login widget logo
headers = {'Authorization': token , 'Accept':'application/json'}

r = requests.get("https://appid-management.<region>.bluemix.net/management/v4/" + ten
antId + "/config/ui/media", headers=headers);

if (r.status_code >= 200) :
    print(r.text)
    print("success! the logo was changed")
```
{: screen}


## 後續步驟
{: #api-try}

若要自行嘗試，請參閱 <a href="https://appid-management.ng.bluemix.net/swagger-ui/
" target="_blank"> {{site.data.keyword.appid_short_notm}} Management Rest API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>
