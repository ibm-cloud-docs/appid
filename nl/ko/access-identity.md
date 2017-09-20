---

copyright:
  years: 2017
lastupdated: "2017-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 액세스 및 ID 토큰
{: #access-and-identity}

{{site.data.keyword.appid_short}}에서는 두 가지 유형의 토큰(액세스 및 ID)을 사용합니다. 토큰은 <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>으로 형식화됩니다.
{:shortdesc}


## 액세스 토큰
{: #access-tokens}

액세스 토큰을 사용하면 {{site.data.keyword.appid_short_notm}} 권한 부여 필터로 보호되는 [백엔드 리소스](/docs/services/appid/protecting-resources.html)와의 통신이 가능합니다. 토큰은 JOSE(JavaScript Object Signing and Encryption) 스펙을 준수하며 형식은 다음과 같습니다. 

```
Header: {

    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": "facebook",
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
    <td> <i> typ </i> </td>
    <td> 헤더 유형이며 "JOSE"로 지정됩니다. </td>
  </tr>
  <tr>
    <td> <i> alg </i> </td>
    <td> 사용된 알고리즘이며 "RS256"으로 지정됩니다. </td>
  </tr>
  <tr>
    <td> <i> iss </i> </td>
    <td> 토큰을 발행한 {{site.data.keyword.appid_short}} 서버이며 문자열 또는 URL로 지정됩니다. </td>
  </tr>
  <tr>
    <td> <i> sub </i> </td>
    <td> 토큰이 발행된 사용자의 ID입니다. </td>
  </tr>
  <tr>
    <td> <i> aud </i> </td>
    <td> 토큰이 대상으로 하는 클라이언트 ID입니다. </td>
  </tr>
  <tr>
    <td> <i> exp </i> </td>
    <td> 시간소인이 만료되는 시간이며 epoch 시간으로 지정됩니다. </td>
  </tr>
  <tr>
    <td> <i> iat </i> </td>
    <td> 시간소인이 발행된 시간이며 epoch 시간으로 지정됩니다. </td>
  </tr>
  <tr>
    <td> <i> tenant </i> </td>
    <td> 토큰이 발행된 테넌트 ID입니다. </td>
  </tr>
  <tr>
    <td> <i> amr </i> </td>
    <td> 인증에 사용된 ID 제공자입니다. 이 변수는 <i>appid_facebook</i> 또는 <i>appid_google</i>일 수 있습니다. </td>
  </tr>
  <tr>
    <td> <i> scope </i> </td>
    <td> 토큰이 발행된 범위입니다. </td>
  </tr>
</table>


## ID 토큰
{: #identity-tokens}

ID 토큰에는 이름, 이메일, 성별, 사진 및 위치를 포함하는 사용자에 대한 정보가 포함됩니다. 

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
        "id": "377440159275659",
        "amr: "facebook",
    ],
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
    <td> <i> identities: </br> <ul><li> provider <li> id <li> amr </ul></i></td>
    <td> </br><ul><li> 인증에 사용된 ID 제공자입니다. 이 변수는 <code>appid_facebook</code>, <code>appid_google</code> 또는 <code>appid_ibmid</code>가 가능하며 리턴되어야 합니다. <li> ID 제공자가 보고한 고유 사용자 ID입니다. <li> ID 제공자가 리턴해야 하는 JSON 오브젝트입니다. </ul></i></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type <li> name <li> software_id <li> software_version</ul></i> </td>
    <td> </br><ul><li> 클라이언트 등록 중에 판별된 애플리케이션의 유형입니다. 변수는 <i>serverapp</i> 또는 <i>mobileapp</i>입니다. <li> 클라이언트 등록 중에 보고된 클라이언트 이름입니다. <li> 클라이언트 등록 중에 보고된 소프트웨어 ID입니다. <li> 클라이언트 등록 중에 사용된 소프트웨어의 버전입니다. </ul></td>
  </tr>
</table>
