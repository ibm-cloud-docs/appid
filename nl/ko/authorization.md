---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 권한 및 인증
{: authorization}

권한은 앱에 액세스를 부여하는 프로세스입니다. {{site.data.keyword.appid_short}} 서비스는 토큰, 필터 및 헤더를 사용하여 사용자를 인증합니다.
{: shortdesc}


## OAuth ID
{: #oauth}

서비스가 OAuth 로그인 API를 호출할 때 {{site.data.keyword.appid_short_notm}}에서는 OAuth 2.0 및 OIDC(OpenID Connect) 프로토콜을 사용하여 선택된 ID 제공자로 호출자에게 권한을 부여하고 인증합니다. 인증 후에는 ID가 {{site.data.keyword.appid_short_notm}} 사용자 레코드와 연관됩니다. {{site.data.keyword.appid_short_notm}}에서는 사용자의 속성에 액세스하는 데 사용할 수 있는 액세스 토큰 및 ID 제공자에서 제공하는 ID 정보가 들어 있는 ID 토큰을 리턴합니다. 이와 동일한 ID로 인증하는 클라이언트에서 동일한 사용자 레코드와 그 속성에 다시 액세스할 수 있습니다. 

## 액세스 및 ID 토큰

{{site.data.keyword.appid_short}}에서는 두 가지 유형의 토큰(액세스 및 ID)을 사용합니다.
{:shortdesc}

**참고**: 토큰은 <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>로 형식화됩니다. 

### 액세스 토큰
{: #access-tokens}

액세스 토큰을 사용하면 권한 필터로 보호되고 App ID로 설정되는 [백엔드 리소스](/docs/services/appid/protecting-resources.html)와의 통신이 가능합니다. 토큰은 JOSE(JavaScript Object Signing and Encryption) 스펙을 준수합니다. 

토큰 예제:

```
Header: {

    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": ["facebook"],
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "iat": "1495559064",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
}
```
{:screen}

<table>
<caption> 표 1. 액세스 토큰 컴포넌트 설명</caption>
  <tr>
    <th> 컴포넌트 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td><i> typ </i> </td>
    <td> 헤더 유형이며 "JOSE"로 지정됩니다. </td>
  </tr>
  <tr>
    <td><i> alg </i> </td>
    <td> 사용된 알고리즘이며 "RS256"으로 지정됩니다. </td>
  </tr>
  <tr>
    <td><i> iss </i> </td>
    <td> 토큰을 발행한 {{site.data.keyword.appid_short}} 서버이며 문자열 또는 URL로 지정됩니다. </td>
  </tr>
  <tr>
    <td><i> sub </i> </td>
    <td> 토큰이 발행된 사용자의 ID입니다. </td>
  </tr>
  <tr>
    <td><i> aud </i> </td>
    <td> 토큰이 대상으로 하는 클라이언트 ID입니다. </td>
  </tr>
  <tr>
    <td><i> exp </i> </td>
    <td> 시간소인이 만료되는 시간이며 epoch 시간으로 지정됩니다. </td>
  </tr>
  <tr>
    <td><i> iat </i> </td>
    <td> 시간소인이 발행된 시간이며 epoch 시간으로 지정됩니다. </td>
  </tr>
  <tr>
    <td><i> tenant </i> </td>
    <td> 토큰으로 발행된 고유 사용자 ID입니다. </td>
  </tr>
  <tr>
    <td><i> amr </i> </td>
    <td> 인증에 사용된 ID 제공자입니다. 이 변수는 <i>appid_facebook</i>,  <i>appid_google</i> 또는 <i>cloud_directory</i>일 수 있습니다. </td>
  </tr>
  <tr>
    <td><i> scope </i> </td>
    <td> 토큰이 발행된 범위입니다. </td>
  </tr>
</table>


### ID 토큰
{: #identity-tokens}

ID 토큰에는 사용자에 대한 정보가 포함됩니다. 이름, 이메일, 성 및 위치에 대한 정보를 제공합니다. 토큰은 사용자의 이미지에 대한 URL을 리턴할 수도 있습니다. 

토큰 예제:

```
Header: {

    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "exp: "1495562664",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "iat": "1495559064",
    "name": "John Smith",
    "email": "js@mail.com",
    "gender", "male",
    "locale": "en",
    "picture": "https://url.to.photo",
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "identities": [
        "provider": "facebook"
        "id": "377440159275659"
    ],
    "amr": ["facebook"],
    "oauth_client":{
      "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
}
```
{:screen}


<table>
<caption> 표 2. ID 토큰 컴포넌트 설명</caption>
  <tr>
    <th> 컴포넌트 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td> <i> name </i> </td>
    <td> ID 제공자가 보고한 사용자의 전체 이름입니다. 이는 리턴되어야 합니다. </td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> ID 제공자가 보고한 사용자의 이메일입니다. 사용 가능할 때만 리턴됩니다. </td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> 사용 가능한 경우 ID 제공자가 보고한 사용자의 성별입니다. </td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> ID 제공자가 보고한 사용자의 로케일입니다. </td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> 사용 가능한 경우 사용자의 사진에 대한 URL입니다. </td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id </ul></i></td>
    <td> </br><ul><li> 인증에 사용된 ID 제공자입니다. 이 변수는 <code>appid_facebook</code>, <code>appid_google</code> 또는 <code>cloud_directory</code> 중 하나일 수 있으며 반드시 리턴되어야 합니다. <li> ID 제공자가 보고한 고유 사용자 ID입니다. <li> ID 제공자가 리턴해야 하는 JSON 오브젝트입니다. </ul></li></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type </br><li> name <li> software_id <li> software_version<li> device_id <li>device_model<li>device_os<li>device_os_version </ul></i> </td>
    <td> </br><ul><li> 클라이언트 등록 중에 판별된 앱의 유형입니다. 변수는 <em>serverapp</em> 또는 <em>mobileapp</em>입니다. <li> 클라이언트 등록 중에 보고된 클라이언트 이름입니다. <li> 클라이언트 등록 중에 보고된 소프트웨어 ID입니다. <li> 클라이언트 등록 중에 사용된 소프트웨어의 버전입니다. <li> 모바일 클라이언트 디바이스 ID입니다. <li> 모바일 클라이언트 디바이스 모델입니다. <li> 모바일 클라이언트 디바이스 OS입니다. <li> 모바일 클라이언트 디바이스 OS 버전입니다. </ul></td>
  </tr>
</table>

## 헤더
{: #auth-header}

권한 헤더는 리턴된 토큰의 조합입니다. {{site.data.keyword.appid_short}}의 경우 권한 헤더는 운반자, 액세스 및 ID의 세 가지 다른 토큰으로 구성되며 공백으로 구분됩니다. 운반자 및 액세스 토큰은 앱에 액세스를 부여하는 데 필요합니다. ID 토큰은 선택사항이며 앱을 사용하는 사용자에 대한 정보를 저장하는 데 주로 사용됩니다. 

헤더 구조 예제:

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


## 필터
{: #auth-filter}

{{site.data.keyword.appid_short}} 서버 SDK는 두 가지 유형의 리소스(API 및 웹 애플리케이션)를 보호하기 위한 전략을 제공합니다.
{:shortdesc}

API 보호 전략은 인증되지 않은 클라이언트에 대한 권한을 확보하기 위해 범위의 목록이 있는 HTTP 401 응답을 리턴합니다. 웹 앱 보호 전략은 HTTP 302 경로 재지정을 리턴합니다. 구성에 따라서 경로 재지정이 인증되지 않은 클라이언트를 {{site.data.keyword.appid_short_notm}} 서비스에서 호스팅하는 사인인 페이지로 전송하거나 ID 제공자 로그인 페이지로 직접 전송합니다. 



### API 전략
{: #api}

API 전략은 요청에 올바른 액세스 토큰이 있는 권한 헤더가 포함될 것으로 예상합니다. 응답에도 ID 토큰이 포함될 수 있지만 필수는 아닙니다. 

토큰이 올바르지 않거나 만료된 경우, API 전략은 다음 정보가 포함된 HTTP 401 오류를 리턴합니다: Www-Authenticate=Bearer scope="{scope}" error="{error}". `error` 컴포넌트는 선택사항입니다. 

요청이 올바른 토큰을 리턴하는 경우, 제어가 다음 미들웨어에 전달되며 `appIdAuthorizationContext` 특성이 요청 오브젝트에 삽입됩니다. 이 특성에는 원래 액세스 및 ID 토큰, 일반 JSON 오브젝트로 디코딩된 페이로드 정보가 포함됩니다. 


### 웹 앱 전략
{: #web}

웹 앱 전략 클래스가 보호된 리소스에 액세스하려는 인증되지 않은 시도를 발견하면 사용자의 브라우저를 인증 페이지로 자동으로 경로 재지정합니다. 인증에 성공하면 사용자가 웹 앱의 콜백 URL로 리턴됩니다. 서비스는 웹 앱 전략 클래스를 사용하여 액세스 및 ID 토큰을 확보합니다. 해당 토큰을 확보한 후에 웹 앱 전략 클래스는 `WebAppStrategy.AUTH_CONTEXT` 아래의 HTTP 세션에 토큰을 저장합니다. 앱 데이터베이스에서 액세스 및 ID 토큰을 저장할 것인지 여부는 사용자가 결정합니다. 


## 점진적 인증
{: #oauth}

{{site.data.keyword.appid_short_notm}}는 OAuth 2.0 및 OIDC 프로토콜을 사용하여 사용자를 인증하고 권한을 부여합니다. 인증 후에는 ID가 사용자 레코드와 연관됩니다. 서비스에서는 사용자의 속성에 액세스하는 데 사용할 수 있는 액세스 토큰 및 ID 제공자에서 제공하는 사용자에 대한 정보가 포함된 ID 토큰을 리턴합니다. 동일한 ID로 인증하는 클라이언트에서 레코드와 그 속성에 다시 액세스할 수 있습니다. 

이제 사용자는 "선택적으로 사인인하려는 경우"에 대해 물을 수 있습니다. {{site.data.keyword.appid_short_notm}}에서는 익명인 경우에도 [사용자 프로파일](/docs/services/appid/user-profile.html)을 작성하기 위해 점진적 인증으로 알려진 것을 사용합니다. 그런 다음 사용자 사인인 후 알려진 사용자 프로파일에 대한 정보를 전송할 수 있습니다. 

![식별된 사용자가 되기 위한 경로를 표시하는 맵](/images/authenticationtrail.png)

그림 2. 식별된 사용자가 되기 위한 경로를 표시하는 맵

사용자가 익명으로 남아 있도록 선택한 경우 {{site.data.keyword.appid_short_notm}}는 임시 사용자 레코드를 작성하고 익명 액세스 및 ID 토큰을 리턴하는 OAuth 로그인 API를 호출합니다. 해당 토큰을 사용하여 앱은 사용자 레코드에 저장된 속성을 작성, 읽기, 업데이트, 삭제할 수 있습니다. 예를 들면, 사용자는 앱에 사인인하지 않고도 장바구니에 항목 추가하기를 즉각적으로 시작할 수 있습니다. 


사용자가 앱에 사인인하도록 선택한 경우 식별된 사용자가 됩니다. 사용자에 대한 정보는 사인인하도록 선택한 ID 제공자에서 제공됩니다. 사용자에 대한 정보가 포함된 액세스 권한 및 ID 토큰이 수신됩니다. 

익명 사용자는 식별된 사용자가 되도록 선택할 수 있습니다. 어떻게 수행됩니까?

익명 액세스 토큰은 로그인 API에 전달됩니다. 서비스가 ID 제공자로 호출을 인증합니다. 서비스는 익명 레코드를 찾기 위해 액세스 토큰을 사용하고 ID를 익명 레코드에 연결합니다. 새 액세스 ID 토큰에는 ID 제공자가 공유한 공용 정보가 포함됩니다. 사용자가 식별된 후 익명 토큰은 올바르지 않은 상태가 됩니다. 그러나 새 액세스 토큰으로 속성에 액세스할 수 있으므로 사용자가 계속해서 속성에 액세스할 수 있습니다. 

**참고**: ID가 다른 사용자에게 아직 지정되지 않은 경우 익명 레코드에만 ID를 지정할 수 있습니다. ID가 다른 {{site.data.keyword.appid_short_notm}} 사용자와 이미 연관되어 있는 경우, 토큰에 그 사용자 레코드의 정보가 포함되며 속성에 대한 액세스를 제공합니다. 이전 익명 사용자 속성은 새 토큰을 통해 액세스할 수 없습니다. 토큰이 만료될 때까지는 익명 액세스 토큰을 통해 정보에 계속 액세스할 수 있습니다. 개발 중에 익명 속성을 알려진 사용자에 병합하는 방식을 선택할 수 있습니다. 
