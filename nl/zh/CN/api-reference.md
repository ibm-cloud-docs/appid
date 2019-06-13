---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-13"

keywords: authentication, authorization, identity, app security, secure, application identity, app to app, access token

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

# 使用 API 管理 {{site.data.keyword.appid_short_notm}}
{: #manging-api}

您可以使用管理 API 进行 DevOps 自动化，定制和管理您的 {{site.data.keyword.appid_full}} 实例。
{: shortdesc}

管理 API 通过 Identity and Access Management (IAM) 生成的令牌进行保护。使用 IAM，帐户所有者可以指定团队成员对每个服务实例的访问级别。有关 IAM 和 {{site.data.keyword.appid_short_notm}} 如何协作的更多信息，请参阅[服务访问管理](/docs/services/appid?topic=appid-service-access-management)。


要了解 API 的工作方式？请查看以下视频教程！

<iframe class="embed-responsive-item" id="about-appid-api" title="关于 {{site.data.keyword.appid_short_notm}} API" type="text/html" width="640" height="390" src="//www.youtube.com/embed/b2ABxvAdGg0?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


使用 API，您能够：
* 在您的 DevOps 流程应用程序中自动配置 {{site.data.keyword.appid_short_notm}}。
* 通过应用程序后端（例如，登录窗口小部件配置，注册过程和用户管理）设置和定制功能。


对管理 API 端点的调用采用以下结构：

```
https://<region-endpoint>.appid.cloud.ibm.com/management
```
{: codeblock}


<table>
  <tr>
    <th>区域</th>
    <th>端点</th>
  </tr>
  <tr>
    <td>达拉斯</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>法兰克福</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>悉尼</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>伦敦</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>东京</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



## 先决条件
{: #api-prereq}

<ul><ul><li>2018 年 3 月 15 日之后创建的服务实例。如果您的服务实例创建于该日期之前，请创建新实例并将其配置为与当前实例匹配。请确保更新应用程序以使用新实例。</li>
<li>已安装 [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli)。</li></ul></ul>

## 用法示例
{: #api-example}

在以下示例中，您可以了解如何通过 Python 使用 API 来更改 {{site.data.keyword.appid_short_notm}} 租户徽标。

```
import requests
import json

tenantId = '<{{site.data.keyword.appid_short_notm}} instance>'
Img = '<Logo file location>'
apiKey = '<IAM API key>'

# get an IAM token
headers = {'Content-Type': 'application/x-www-form-urlencoded', 'Accept':'application
/json'}
data = 'grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=' + apiKey;

r = requests.post("https://iam.cloud.ibm.com/oidc/token", data=data, headers=
headers);
token = 'Bearer ' + json.loads(r.text)['access_token'];

#  set the Login Widget logo
headers = {'Authorization': token , 'Accept':'application/json'}
files = {'file': open(img,'rb')}

r = requests.post("https://<region>.appid.cloud.com/management/v4/" + tenantId + "/config/ui/media?mediaType=logo", files=files, headers=headers);

#  get login widget logo
headers = {'Authorization': token , 'Accept':'application/json'}

r = requests.get("https://<region>.appid.cloud.com/management/v4/" + tenantId + "/config/ui/media", headers=headers);

if (r.status_code >= 200) :~
    print(r.text)
    print("success! the logo was changed")
```
{: screen}


## 后续步骤
{: #api-try}

要亲自试用，请参阅 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">{{site.data.keyword.appid_short_notm}} 管理 Rest API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>
