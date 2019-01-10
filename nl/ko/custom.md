---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}
{:codeblock: .codeblock}


# 사용자 정의
{: #custom-identity}

인증 시 고유한 사용자 정의 ID 제공자를 사용할 수 있습니다. ID 제공자는 소유권을 포함하여 {{site.data.keyword.appid_full}}에서 특정하게 지원되지 않는 인증 메커니즘을 준수할 수 있습니다.
{: shortdesc}

{{site.data.keyword.appid_short_notm}}에서 특정 ID 제공자에 대한 직접 지원을 제공하지 않을 경우 사용자 정의 ID 플로우를 사용하여 인증 프로토콜을 {{site.data.keyword.appid_short_notm}}의 기존 인증 플로우에 브릿징할 수 있습니다. 예를 들어 사용자가 사인인할 수 있도록 허용하기 위해 GitHub 또는 LinkedIn을 사용할 수 있습니다. {{site.data.keyword.appid_short_notm}}를 통해 사용자 인증 정보를 패키징 및 교환하기 전에 ID 제공자의 기존 SDK를 사용하여 해당 사용자 인증 정보를 활용할 수 있습니다. 많은 엔터프라이즈 시나리오에서 레거시 ID 제공자는 고유한 사용자 정의 인증 프로토콜을 사용하지만 여전히 {{site.data.keyword.appid_short_notm}}의 기능을 활용할 수 있습니다. 이러한 유형의 시나리오에서 사용자 정의 ID 플로우는 해당 인증 정보를 노출하지 않고 사용자를 안전하게 인증하기 위한 분리된 방법을 제공합니다.

## 사용자 정의 ID 구성
{: #custom-configure}

다음 단계를 사용하여 {{site.data.keyword.appid_short_notm}}에서 작동하도록 사용자 정의 ID 제공자를 구성할 수 있습니다.
{: shortdesc}

**시작하기 전에**

{{site.data.keyword.appid_short_notm}}와 사용자 정의 ID 제공자 사이에 신뢰를 설정하려면 최소 길이가 2048인 RSA PEM 키 쌍이 있어야 합니다. 프로덕션에서 사용하는 모든 키를 안전하게 백업해야 합니다.

키는 어떻게 사용됩니까?

- 개인 키는 JWT에 서명하기 위해 앱 또는 ID 제공자에서 사용됩니다.
- 공개 키는 사용자 정보가 포함된 JWT를 유효성 검증하기 위해 {{site.data.keyword.appid_short_notm}}에서 사용됩니다.

Open SSL을 사용하여 RSA PEM 키 쌍을 생성하려면 다음 명령을 실행하십시오.

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}

</br>

**GUI를 사용하여 구성**

1. {{site.data.keyword.Bluemix_notm}} 계정에 사인인한 후 {{site.data.keyword.appid_short_notm}}의 인스턴스로 이동하십시오.

2. **관리** 탭에서 **사용자 정의 ID 제공자**를 **켜기**로 설정하십시오.

3. 공개 키를 {{site.data.keyword.appid_short_notm}}에 등록하십시오.
  1. **사용자 정의 ID 제공자** 탭으로 이동하십시오.
  2. **공개 키** 상자에 공개 키를 붙여넣은 후 **저장**을 클릭하십시오.


</br>

**API를 사용하여 구성**

[관리 API 엔드포인트](https://appid-management.ng.bluemix.net/swagger-ui/#!/Identity_Providers/custom)에 대한 PUT 요청을 작성하여 키를 등록하십시오.

```
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## 구성 테스트
{: #testing}

올바른 공개 키를 사용하여 {{site.data.keyword.appid_short_notm}} 인스턴스를 구성한 후에는 해당 서비스에서 제공되는 테스트 애플리케이션을 사용하여 구성이 올바르게 설정되었는지 확인할 수 있습니다. 예제 앱에서는 표준 사인인 플로우 중에 리턴되는 {{site.data.keyword.appid_short_notm}} 액세스 및 ID 토큰 페이로드를 확인할 수 있습니다.

1. **사용자 정의 ID 제공자** 탭에서 **테스트**를 클릭하여 테스트 애플리케이션을 여십시오.

2. 사용자 정의 ID [프로토콜](/docs/services/appid/custom-auth.html#creating-jwts) 다음에 [JWT.io](https://jwt.io/)를 사용하여 예제 JWT를 작성하십시오.

3. **JSON 웹 토큰**으로 레이블 지정된 상자에 JWT를 붙여넣은 후 **테스트**를 클릭하여 샘플 인증을 실행하십시오.

정상적으로 완료되는 경우 이제 표준 사인인 플로우에서 애플리케이션이 사용할 수 있는 디코딩된 {{site.data.keyword.appid_short_notm}} ID 및 액세스 토큰이 표시됩니다.

## 다음 단계
{: #next}

사용자 정의 ID 제공자가 구성되었으면 [애플리케이션에 사용자 정의 ID 제공자를 추가](/docs/services/appid/custom-auth.html)하십시오!
