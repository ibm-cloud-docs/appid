---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, tokens, access, claim, attributes

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


# 토큰 사용자 정의
{: #customizing-tokens}

애플리케이션의 특정 요구사항을 충족하도록 {{site.data.keyword.appid_short_notm}} 토큰을 구성할 수 있습니다.
{: shortdesc}

## 사용자 정의에 대한 정보
{: #understanding-customization}

{{site.data.keyword.appid_short_notm}}는 다양한 유형의 토큰을 사용하여 애플리케이션을 보호합니다.

* 액세스 토큰: 권한 필터를 통해 보호되는 백엔드 리소스와 통신할 수 있도록 해줍니다. 액세스 토큰이 특정 사용자와 연관되지 않을 경우 해당 토큰의 기능이 제한됩니다.
* ID 토큰: 개인 정보가 포함되어 있으며 사용자를 인증하기 위해 사용됩니다. 앱 구성에 따라 사용자가 인증되기 전에 ID 토큰이 발행될 수 있습니다. 이 경우 사용자가 애플리케이션에 사인인하기 전에 속성을 해당 사용자와 연관시키는 작업을 시작할 수 있습니다.
* 새로 고치기 토큰: 사용자가 재인증 없이 진행할 수 있는 시간을 연장하기 위해 사용할 수 있습니다.

토큰에 대한 자세한 정보를 확인하시겠습니까? [토큰에 대한 정보](/docs/services/appid?topic=appid-tokens#tokens)를 자세히 읽어 보십시오.
{: tip}


[GUI](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-ui)에서 또는 [API](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-api)를 사용하여 토큰에 유효 기간을 설정하거나 사용자 정의 청구를 추가하여 토큰을 사용자 정의할 수 있습니다. 수명을 구성하는 방법에 대해 확인하거나 사용자 정의 속성을 맵핑하는 방법에 대해 읽어 보려면 다음 표를 참조하십시오.

<table>
  <tr>
    <th>토큰 유형</th>
    <th>값 유형</th>
    <th>기본값</th>
    <th>옵션</th>
  </tr>
  <tr>
    <td>액세스</td>
    <td>분</td>
    <td>60</td>
    <td>5 - 1440 사이의 값</td>
  </tr>
  <tr>
    <td>ID</td>
    <td>분</td>
    <td>60</td>
    <td>5 - 1440 사이의 값</td>
  </tr>
  <tr>
    <td>새로 고치기</td>
    <td>일</td>
    <td>30</td>
    <td>1 - 9 사이의 값</td>
  </tr>
  <tr>
    <td>익명</td>
    <td>일</td>
    <td>30</td>
    <td>1 - 9 사이의 값</td>
  </tr>
</table>


토큰은 사용자를 식별하고 리소스에 보안을 설정하기 위해 사용되기 때문에 토큰의 수명은 여러가지 다양한 항목에 영향을 미치게 됩니다. 토큰 구성을 사용자 정의하여 보안 및 사용자 환경(experience) 요구사항이 충족되도록 할 수 있습니다. 하지만 토큰이 손상되는 경우 악성 사용자가 애플리케이션에 영향을 미칠 수 있는 추가적인 시간을 확보하게 됩니다. [사용자 정의 속성](/docs/services/appid?topic=appid-custom-attributes)에서 보안 고려사항에 대한 자세한 정보를 확인할 수 있습니다.
{: important}


## 사용자 정의 속성 및 청구에 대한 정보
{: #custom-claims}

사용자 프로파일 속성을 액세스 및 ID 토큰 청구에 맵핑할 수 있습니다. 즉, 이미 토큰에 저장되어 있기 때문에 나중에 [/userinfo 엔드포인트](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo)로 이동하거나 사용자 정의 속성을 가져올 필요가 없습니다!
{: shortdesc}

### 청구가 무엇입니까?
{: #custom-claims-defined}

청구는 엔티티가 자신에 대해 또는 다른 사용자 대신 작성하는 내역서입니다. 예를 들어 ID 제공자를 사용하여 애플리케이션에 사인인한 경우 해당 제공자는 이미 사용자에 대해 알고 있는 정보로 그룹화할 수 있도록 애플리케이션에 청구 그룹을 전송하거나 앱에 사용자에 대한 내역서를 전송합니다. 이 방법을 통해 사인인할 때 앱이 해당 정보로(사용자가 구성한 방식으로) 설정됩니다. JSON 오브젝트를 형식화하는 방법에 대한 정보는 다음 예제를 참조하십시오.

```
{
  "accessTokenClaims": [
            {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
       "idTokenClaims": [
           {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
  "access": {
    "expires_in": 3600
  },
  "refresh": {
    "expires_in": 2592000,
    "enabled": true
  },
  "anonymousAccess": {
    "expires_in": 2592000,
    "enabled": true
  }
}
```
{: screen}

토큰에 대한 사용자 정의 만기 정보가 존재하는 경우 모든 요청에서 해당 정보를 설정해야 합니다. 설정하지 않을 경우 해당 요청에서 현재 구성을 대체하며 정의되지 않은 모든 항목에 대해 기본값이 사용됩니다.
{: note}

### 내 토큰에 청구를 추가하는 이유가 무엇입니까?
{: #why-custom-claims}

추가적인 네트워크 호출을 작성하지 않더라도 앱에서 사용자 또는 해당 사용자가 수행할 수 있는 작업에 대해 알고 있어야 하는 모든 항목이 이미 토큰에 포함되어 있습니다! 대량의 데이터가 존재하지 않을 경우 이를 통해 더욱 효율적으로 작업할 수 있습니다. 또한 이러한 맵핑된 속성은 서명된 토큰에 저장되기 때문에 네트워크를 통해 전송될 때 해당 속성의 무결성을 보증할 수 있습니다.


### 어떤 유형의 청구를 정의할 수 있습니까?
{: #custom-claim-types}

{{site.data.keyword.appid_short_notm}}에서 제공되는 청구는 사용자 정의 레벨에 따라 구분되는 몇 가지 카테고리로 분류됩니다.

*등록된 청구*: {{site.data.keyword.appid_short_notm}}에서 정의되고 사용자 정의 맵핑으로 대체할 수 없는 액세스 및 ID 토큰에 몇 가지 청구가 존재합니다. 청구가 제한된 경우 서비스에서 해당 청구를 무시합니다. 이 청구는 `iss`, `aud`, `sub`, `iat`, `exp`, `amr` 및 `tenant`입니다.

*제한된 청구*: 청구가 맵핑되는 토큰에 따라 일부 청구의 사용자 정의 가능성이 제한됩니다. 액세스 토큰의 경우 `scope`가 제한된 유일한 청구입니다. 이 청구는 사용자 정의 맵핑으로 대체할 수는 없지만 고유 범위로 확장할 수 있습니다. 범위 청구가 액세스 토큰에 맵핑되는 경우 값이 문자열이어야 하며 `appid_` 접두부를 사용할 수 없습니다. 그렇지 않을 경우 무시됩니다. ID 토큰의 경우 `identities` 및 `oauth_clients` 청구를 수정하거나 대체할 수 없습니다.

*정규화된 청구*: 모든 ID 토큰에는 {{site.data.keyword.appid_short_notm}}에서 정규화된 청구로 인식되는 청구 세트가 포함되어 있습니다. 이러한 청구 세트가 사용 가능한 경우 ID 제공자에서 토큰으로 직접 맵핑됩니다. 이러한 청구는 명시적으로 생략할 수는 없지만 사용자 정의 청구 맵핑으로 대체할 수 있습니다. 청구에는 `name`, `email`, `picture`, `local` 및 `gender`가 있습니다.


### 청구를 토큰에 맵핑하는 방법은 무엇입니까?
{: #custom-claims-mapping}

각각의 맵핑은 청구를 검색하기 위해 사용되는 키 및 데이터 소스 오브젝트를 통해 정의됩니다. 각각의 사용자 정의 청구는 각각의 토큰에 대해 개별적으로 설정되며 순차적으로 적용됩니다. 각각의 토큰에 대해 최대 100개의 청구를 최대 100KB의 페이로드까지 등록할 수 있습니다.

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="아이디어 아이콘"/> 청구 맵핑 오브젝트에 대한 정보</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>필수</td>
        <td>청구의 소스를 정의합니다. ID 제공자의 사용자 정보 또는 사용자의 {{site.data.keyword.appid_short_notm}} 사용자 정의 속성을 참조할 수 있습니다. </br> 옵션에는 `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid` 및 `attributes` 등이 있습니다.</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>필수</td>
        <td>소스 데이터의 청구를 정의합니다. </td>
      </tr>
    </tbody>
  </table>

점 구문을 사용하여 맵핑에서 중첩된 청구를 참조할 수 있습니다. 예: `nested.attribute`
{:tip}

</br>

## {{site.data.keyword.appid_short_notm}} 토큰 구성
{: #configuring-tokens}

GUI 또는 관리 API를 사용하여 {{site.data.keyword.appid_short_notm}} 토큰을 구성할 수 있습니다.
{: shortdesc}


### GUI를 사용하여 토큰 수명 구성
{: #configuring-tokens-ui}

1. 서비스 대시보드로 이동하십시오.
2. 탐색의 **ID 제공자** 섹션에서 **관리** 페이지를 선택하십시오.
3. **설정** 탭에서 토큰을 구성하십시오.
  1. 사용자 상호작용 없이 사인인할 수 있도록 허용하려면 **새로 고치기 토큰**을 **켜짐**으로 설정하십시오.
  2. 새로 고치기 토큰의 수명을 설정하십시오. 만기는 일 단위로 설정되며 1 - 90 사이의 값이 될 수 있습니다. 숫자가 작을수록 사용자가 더 빈번하게 사인인해야 합니다.
  3. 액세스 토큰 수명을 설정하십시오. 만기는 분 단위로 설정되며 5 - 1440 사이의 값이 될 수 있습니다. 값이 작을수록 토큰 절도에 대비한 더 많은 보호가 제공됩니다.
  4. 익명 토큰 수명을 설정하십시오. [익명 토큰](/docs/services/appid?topic=appid-anonymous#anonymous)은 사용자가 앱과 상호작용하기 시작하는 시점에 해당 사용자에게 지정됩니다. 사용자가 사인인하면 익명 토큰의 정보가 해당 사용자와 연관된 토큰으로 전송됩니다. 만기는 일 단위로 설정되며 1 - 90 사이의 값이 될 수 있습니다.

</br>

### 관리 API를 사용하여 토큰 구성
{: #configuring-tokens-api}

**시작하기 전에**

다음과 같은 전제조건이 준비되어 있어야 합니다.

* {{site.data.keyword.appid_short_notm}} 인스턴스의 테넌트 ID. 이 ID는 GUI의 **서비스 인증 정보** 섹션에서 찾을 수 있습니다.
* IAM(Identity and Access Management) 토큰. IAM 토큰을 얻는 방법에 대한 도움말은 [IAM 문서](/docs/iam?topic=iam-iamtoken_from_apikey)를 참조하십시오.

**청구 맵핑**

1. 토큰 구성이 포함된 `/config/tokens` 엔드포인트에 대한 PUT 요청을 작성하십시오.

  헤더:
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  본문:
  ```
   {
       "access": {
           "expires_in": 3600,
       },
       "refresh": {
           "expires_in": 2592000,
           "enabled": true
       },
       "anonymous": {
           "expires_in": 2592000,
           "enabled": true
       },
       "accessTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "name_id"
           }
       ],
       "idTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "attributes.uid"
           }
       ]
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="아이디어 아이콘"/> 토큰 구성에 대한 정보</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>선택사항</td>
        <td>액세스 토큰 및 ID 토큰에 대한 분 단위의 만기 시간(`expires_in`)이 포함된 오브젝트입니다. </br> </br> 기본 만기는 60분입니다. </td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>선택사항</td>
          <td>새로 고치기 토큰에 대한 일 단위의 만기 시간(`expires_in`)이 포함된 오브젝트입니다. </br> </br> 기본 만기는 30일입니다. </td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>선택사항</td>
          <td>익명 액세스 및 ID 토큰에 대한 일 단위의 만기 시간(`expires_in`)이 포함된 오브젝트입니다. </br> </br> 기본 만기는 30일입니다.
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>선택사항</td>
          <td>액세스 토큰과 관련된 청구가 맵핑될 때 작성되는 오브젝트가 포함된 배열입니다.</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>선택사항</td>
          <td>ID 토큰과 관련된 청구가 맵핑될 때 작성되는 오브젝트가 포함된 배열입니다.</td>
      </tr>
    </tbody>
  </table>

  요청 예제:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
            }
          ],
          "idTokenClaims": [
            {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
  }' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
