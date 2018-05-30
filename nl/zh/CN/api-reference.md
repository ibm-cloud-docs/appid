---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 使用 API 管理 {{site.data.keyword.appid_short_notm}}
{: manging-api}

您可以使用管理 API 进行 DevOps 自动化，定制和管理您的 {{site.data.keyword.appid_full}} 实例。
{: shortdesc}

管理 API 通过 IBM Cloud Identity and Access Management 生成的令牌进行保护。这意味着帐户所有者可以指定团队成员对每个服务实例的访问级别。有关 IAM 和 {{site.data.keyword.appid_short_notm}} 如何协作的更多信息，请参阅[服务访问管理](/docs/services/appid/iam.html)。

使用 API，您能够：
* 在您的 DevOps 流程应用程序中自动配置 {{site.data.keyword.appid_short_notm}}。
* 通过应用程序后端（例如，登录窗口小部件配置，注册过程和用户管理）设置和定制功能。


采用以下结构调用管理 API 端点：

```
appid-management.<region>.bluemix.net
```
{: codeblock}

您可以通过查看下表来找到区域。

<table>
  <tr>
    <th>{{site.data.keyword.Bluemix}} 区域</th>
    <th>端点</th>
  </tr>
  <tr>
    <td>英国</td>
    <td><code>appid-management.eu-gb.bluemix.net</code></td>
  </tr>
  <tr>
    <td>美国南部</td>
    <td><code>appid-management.ng.bluemix.net</code></td>
  </tr>
  <tr>
    <td>悉尼</td>
    <td><code>appid-management.au-syd.bluemix.net</code></td>
  </tr>
  <tr>
    <td>德国</td>
    <td><code>appid-management.eu-de.bluemix.net</code></td>
  </tr>
</table>



## 先决条件
{: #api-prereq}

<ul><ul><li>2018 年 3 月 15 日之后创建的服务实例。如果您的服务实例创建于该日期之前，请创建新实例并将其配置为与当前实例匹配。请确保更新应用程序以使用新实例。</li>
<li>已安装 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html)。</li></ul></ul>

## 用法示例
{: #api-example}

在以下示例中，您可以了解如何通过 Python 使用 API 来更改 {{site.data.keyword.appid_short_notm}} 租户徽标。

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


## 后续步骤
{: #api-try}

要亲自试用，请参阅 <a href="https://appid-management.ng.bluemix.net/swagger-ui/
" target="_blank">{{site.data.keyword.appid_short_notm}} 管理 Rest API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>
