---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-23"

keywords: authentication, authorization, identity, app security, secure, tokens, jwt, development

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


# 토큰 유효성 검증
{: #token-validation}

토큰 유효성 검증은 최근의 앱 개발에서 매우 중요한 부분입니다. 토큰을 유효성 검증하여 권한 없는 사용자로부터 앱 또는 API를 보호할 수 있습니다. {{site.data.keyword.appid_full}}의 경우 액세스 및 ID 토큰을 사용하여 액세스 권한이 부여되기 전에 사용자 또는 앱이 인증되었는지 확인합니다. {{site.data.keyword.appid_short_notm}}에서 제공되는 SDK 중 하나를 사용하는 경우 토큰의 획득 및 유효성 검증이 둘 다 수행됩니다!
{: shortdesc}

{{site.data.keyword.appid_short_notm}}에서 토큰을 사용하는 방법에 대한 자세한 정보는 [토큰에 대한 정보](/docs/services/appid?topic=appid-tokens#tokens)를 참조하십시오.
{: tip}

토큰은 사용자가 자신이 누구라고 주장하는지 확인하기 위해 사용됩니다. 사용자는 해당 사용자가 지정된 기간 동안 보유할 수 있는 액세스 권한을 확인합니다. 사용자가 애플리케이션에 사인인하여 토큰이 발행되면 액세스 권한이 지정되기 전에 앱에서 해당 사용자를 유효성 검증해야 합니다.

</br>

**{{site.data.keyword.appid_short_notm}}에 해당하는 SDK가 없는 언어로 작업하는 경우 어떻게 됩니까?**

걱정하지 마십시오! 다음과 같은 세 가지 옵션이 제공됩니다.

* {{site.data.keyword.appid_short_notm}} API를 사용하여 작업
* 고유한 유효성 검증 로직 구현
* 임의의 OIDC 준수 오픈 소스 SDK 사용

피드백에 따르면 옵션 1이 일반적으로 가장 간단한 방법입니다.
{: tip}

</br>
</br>

## {{site.data.keyword.appid_short_notm}} API 사용
{: #remote-validation}

자체 검사를 사용하는 경우 {{site.data.keyword.appid_short_notm}}를 통해 토큰을 유효성 검증할 수 있습니다.
{: shortdesc}

1. [/introspect](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token) API 엔드포인트에 대한 POST 요청을 전송하여 토큰을 유효성 검증하십시오. 이 요청에서는 클라이언트 ID 및 시크릿이 포함된 기본 권한 헤더 및 토큰을 제공해야 합니다.

  요청 예제:

    ```
    POST /oauth/v4/{tenant_id}/introspect HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. 서버는 토큰의 만기 및 서명을 확인한 후 토큰이 활성인지 비활성인지 여부를 나타내는 JSON 오브젝트를 리턴합니다.

  응답 예제:

    ```
    {
      "active": true
    }
    ```
    {: screen}


## 수동 토큰 유효성 검증
{: #local-validation}

토큰을 구문 분석하고, 토큰 서명을 확인하고, 토큰에 저장된 청구를 유효성 검증하여 로컬에서 토큰을 유효성 검증할 수 있습니다.
{: shortdesc}


1. 토큰을 구문 분석하십시오. [JWT(JSON Web Token)](https://tools.ietf.org/html/rfc7519)는 안전하게 정보를 전달하기 위한 표준 방법입니다. 이 항목은 세 개의 기본 파트로 구성되어 있습니다(헤더, 페이로드 및 서명). 이러한 파트는 base64URL로 인코딩되고 점(.)으로 구분됩니다. 토큰을 구문 분석할 수 있는 모든 base64URL 디코더를 사용할 수 있습니다. 또는 [나열된 라이브러리](https://jwt.io/#libraries-io) 중 하나를 사용하여 토큰을 구문 분석할 수 있습니다.

  인코딩된 토큰 예제:

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  디코딩된 헤더 예제:

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  디코딩된 페이로드:

    ```
    {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. [/publickeys 엔드포인트](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys)에 대한 호출을 작성하여 공개 키를 검색하십시오. 리턴되는 공개 키는 [JWK(JSON Web Key)](https://tools.ietf.org/html/rfc7517)로 형식화됩니다.

  요청 예제:

    ```
    GET /oauth/v4/{tenant_id}/publickeys HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Cache-Control: no-cache
    ```
    {: screen}

3. 나중에 사용하기 위해 키를 앱 캐시에 저장하십시오. 키를 저장하는 경우 프로세스를 가속화하고 다른 호출이 작성될 때 네트워크 지연을 방지할 수 있습니다.

4. 공개 키 매개변수를 가져오십시오.

  응답 예제:

    ```
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 공개 키 매개변수 </th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>사용되는 알고리즘을 정의합니다.</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>키의 용도를 정의합니다.</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>키의 고유 ID를 정의합니다.</td>
      </tr>
      <tr>
        <td>기타</td>
        <td>함께 가져와야 하는 알고리즘에 특정한 다른 기타 매개변수가 존재할 수 있습니다.</td>
      </tr>
    </tbody>
  </table>

5. 토큰의 서명을 확인하십시오. 토큰 헤더에는 토큰 및 키 ID에 서명하기 위해 사용된 알고리즘 또는 일치하는 공개 키의 `kid` 청구가 포함되어 있습니다. 공개 키는 자주 변경되지 않기 때문에 앱에서 공개 키를 캐싱한 후 가끔씩 새로 고치면 됩니다. 캐싱된 키에서 `kid` 청구가 누락된 경우 로컬로 토큰을 유효성 검증할 수 있습니다.

  1. 애플리케이션에서 수신되는 토큰 헤더가 공개 키의 매개변수와 일치하는지 확인하도록 하십시오.
  2. 특히 동일한 알고리즘이 사용되었으며 공개 키 캐시에 관련 키 ID가 있는 키가 포함되어 있는지 확인하십시오.
  3. 해시 값이 공개 키에 대한 PEM 양식의 서명과 동일한지 확인하십시오. 해시 값은 토큰의 페이로드 헤더를 결합하고 해싱하여 얻을 수 있습니다. 이 프로세스의 경우 수동으로 구현하기에 너무 복잡할 수 있기 때문에 [나열된 라이브러리](https://jwt.io/) 중 하나를 사용하여 서명을 유효성 검증하는 작업이 유용할 수 있습니다.

6. 토큰에 저장된 청구를 유효성 검증하십시오. 나중에 검사를 확인하기 위해 [이 목록](https://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation)을 사용할 수 있습니다.
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 유효성 검증해야 하는 청구 </th>
    </thead>
    <tbody>
      <tr>
        <td><code> iss </code></td>
        <td>발행자는 {{site.data.keyword.appid_short_notm}} OAuth 서버와 동일해야 합니다.</td>
      </tr>
      <tr>
        <td><code> exp </code></td>
        <td>현재 시간은 만기 시간 이전이어야 합니다.</td>
      </tr>
      <tr>
        <td><code> aud </code></td>
        <td>대상에는 앱의 클라이언트 ID가 포함되어 있어야 합니다.</td>
      </tr>
      <tr>
        <td><code> tenant </code></td>
        <td>테넌트에는 앱의 테넌트 ID가 포함되어 있어야 합니다.</td>
      </tr>
      <tr>
        <td><code> scope </code></td>
        <td>사용자에게 부여되는 권한의 범위입니다. 이 권한은 액세스 토큰에 특정합니다.</td>
      </tr>
    </tbody>
  </table>
