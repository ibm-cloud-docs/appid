---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: Authentication, authorization, identity, app security, secure, application identity, app to app, access token

subcollection: appid

---

{:external: target="_blank" .external}
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

# API を使用した {{site.data.keyword.appid_short_notm}} の管理
{: #manging-api}

{{site.data.keyword.appid_full}} のインスタンスの DevOps 自動化、カスタマイズ、および管理に管理 API を使用できます。
{: shortdesc}

管理 API は、Identity and Access Management (IAM) で生成されたトークンにより保護されます。 IAM を使用して、アカウント所有者は、各サービス・インスタンスに対して自分のチームの誰がどのレベルのアクセス権限を持つかを指定できます。 IAM と {{site.data.keyword.appid_short_notm}} の連動方法について詳しくは、[サービス・アクセス管理](/docs/services/appid?topic=appid-service-access-management)を参照してください。


API の動作をご覧になりたいですか? 次のビデオ・チュートリアルをご覧ください。

<iframe class="embed-responsive-item" id="about-appid-api" title="{{site.data.keyword.appid_short_notm}} API の概要" type="text/html" width="640" height="390" src="//www.youtube.com/embed/b2ABxvAdGg0?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


API を使用して、以下の操作を行えます。
* DevOps プロセスのアプリで {{site.data.keyword.appid_short_notm}} の構成を自動化する。
* ログイン・ウィジェット構成、登録プロセス、ユーザー管理などの機能をアプリ・バックエンドを介して設定およびカスタマイズする。


管理 API エンドポイントの呼び出しには、以下の構造を使用します。

```
https://<region-endpoint>.appid.cloud.ibm.com/management
```
{: codeblock}


<table>
  <tr>
    <th>地域</th>
    <th>エンドポイント</th>
  </tr>
  <tr>
    <td>ダラス</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>フランクフルト</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>シドニー</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>ロンドン</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>東京</td>
    <td><code> jp-tok </code></td>
  </tr>
</table>



## 前提条件
{: #api-prereq}

<ul><ul><li>2018 年 3 月 15 日より後にサービス・インスタンスが作成されていること。 この日付より前にサービスのインスタンスが作成されている場合は、新しいインスタンスを作成し、現行インスタンスと合うように構成してください。 新しいインスタンスを使用するようにアプリを更新する必要があります。</li>
<li>[{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started) がインストールされていること。</li></ul></ul>

## 使用例
{: #api-example}

次の例は、Python で API を使用して {{site.data.keyword.appid_short_notm}} テナント・ロゴを変更する方法を示しています。

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


## 次のステップ
{: #api-try}

実際に試してみるには、[{{site.data.keyword.appid_short_notm}} 管理 Rest API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external} を参照してください
