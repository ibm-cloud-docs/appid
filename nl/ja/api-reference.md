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

# API を使用した {{site.data.keyword.appid_short_notm}} の管理
{: manging-api}

{{site.data.keyword.appid_full}} のインスタンスの DevOps 自動化、カスタマイズ、および管理に管理 API を使用できます。
{: shortdesc}

管理 API は、IBM Cloud Identity and Access Management で生成されたトークンにより保護されます。つまり、アカウント所有者は、各サービス・インスタンスに対して自分のチームの誰がどのレベルのアクセス権限を持つかを指定できます。IAM と {{site.data.keyword.appid_short_notm}} の連動方法について詳しくは、[サービス・アクセス管理](/docs/services/appid/iam.html)を参照してください。

API を使用して、以下の操作を行えます。
* DevOps プロセスのアプリで {{site.data.keyword.appid_short_notm}} の構成を自動化する。
* ログイン・ウィジェット構成、登録プロセス、ユーザー管理などの機能をアプリ・バックエンドを介して設定およびカスタマイズする。


管理 API エンドポイントの呼び出しには、以下の構造を使用します。

```
appid-management.<region>.bluemix.net
```
{: codeblock}

地域については、以下の表を参照してください。

<table>
  <tr>
    <th>{{site.data.keyword.Bluemix}} 地域</th>
    <th>エンドポイント</th>
  </tr>
  <tr>
    <td>英国 </td>
    <td><code>appid-management.eu-gb.bluemix.net</code></td>
  </tr>
  <tr>
    <td>米国南部 </td>
    <td><code>appid-management.ng.bluemix.net</code></td>
  </tr>
  <tr>
    <td>シドニー </td>
    <td><code>appid-management.au-syd.bluemix.net</code></td>
  </tr>
  <tr>
    <td>ドイツ</td>
    <td><code>appid-management.eu-de.bluemix.net</code></td>
  </tr>
</table>



## 前提条件
{: #api-prereq}

<ul><ul><li>2018 年 3 月 15 日より後にサービス・インスタンスが作成されていること。この日付より前にサービスのインスタンスが作成されている場合は、新しいインスタンスを作成し、現行インスタンスと合うように構成してください。新しいインスタンスを使用するようにアプリを更新する必要があります。</li>
<li>[{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html) がインストールされていること。</li></ul></ul>

## 使用例
{: #api-example}

次の例は、Python で API を使用して {{site.data.keyword.appid_short_notm}} テナント・ロゴを変更する方法を示しています。

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


## 次のステップ
{: #api-try}

これを実際に試してみるには、<a href="https://appid-management.ng.bluemix.net/swagger-ui/
" target="_blank">{{site.data.keyword.appid_short_notm}} 管理 Rest API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください
