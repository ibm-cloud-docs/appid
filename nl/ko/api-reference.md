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

# API로 {{site.data.keyword.appid_short_notm}} 관리
{: #manging-api}

관리 API를 {{site.data.keyword.appid_full}} 인스턴스의 DevOps 자동화, 사용자 정의 및 관리에 사용할 수 있습니다.
{: shortdesc}

관리 API는 IAM(Identity and Access Management)에서 생성한 토큰으로 보호됩니다. IAM을 사용하면 계정 소유자가 자체 팀의 어떤 구성원이 각 서비스 인스턴스에 대해 어떤 액세스 레벨을 보유하는지를 지정할 수 있습니다. IAM 및 {{site.data.keyword.appid_short_notm}}가 함께 작동되는 방법에 대한 자세한 정보는 [서비스 액세스 관리](/docs/services/appid?topic=appid-service-access-management)를 참조하십시오.


작동 중인 API를 보고 싶으십니까? 다음 동영상 튜토리얼을 확인하십시오.

<iframe class="embed-responsive-item" id="about-appid-api" title="{{site.data.keyword.appid_short_notm}} API 정보" type="text/html" width="640" height="390" src="//www.youtube.com/embed/b2ABxvAdGg0?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


API로 다음을 수행할 수 있습니다.
* DevOps 프로세스의 앱에서 {{site.data.keyword.appid_short_notm}}의 구성 자동화
* 앱 백엔드를 통해 기능 설정 및 사용자 정의(예: 로그인 위젯 구성, 등록 프로세스 및 사용자 관리)


관리 API 엔드포인트에 대한 호출의 구조는 다음과 같습니다.

```
https://<region-endpoint>.appid.cloud.ibm.com/management
```
{: codeblock}


<table>
  <tr>
    <th>Region</th>
    <th>엔드포인트</th>
  </tr>
  <tr>
    <td>Dallas</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>프랑크푸르트</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>시드니</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>런던</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>토쿄</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



## 전제조건
{: #api-prereq}

<ul><ul><li>2018년 3월 15일 이후 작성된 서비스 인스턴스. 해당 날짜 이전에 작성된 서비스의 인스턴스가 있는 경우에는 새 인스턴스를 작성하고 현재 인스턴스와 일치하도록 이를 구성하십시오. 반드시 새 인스턴스를 사용하도록 앱을 업데이트하십시오.</li>
<li>설치된 [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started).</li></ul></ul>

## 사용 예제
{: #api-example}

다음 예제에서는 API를 사용하여 Python으로 {{site.data.keyword.appid_short_notm}} 테넌트 로고를 변경하는 방법을 볼 수 있습니다.

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


## 다음 단계
{: #api-try}

직접 사용해 보려면 [{{site.data.keyword.appid_short_notm}} Management Rest API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}를 참조하십시오.
