---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# 문제점 해결: SAML
{: #troubleshooting-idp}

{{site.data.keyword.appid_full}}에서 작동하도록 SAML을 구성할 때 문제점이 발생하는 경우 문제점을 해결하고 도움을 받기 위해 다음과 같은 기술을 고려하십시오.
{: shortdesc}


## 일반 구성 문제
{: #ts-common-saml}

SAML 프레임워크는 여러 프로파일, 플로우 및 구성을 지원하는데, 이는 ID 제공자 구성이 올바르게 구성되어야 한다는 것을 의미합니다. SAML 관련 작업을 수행할 때 발생할 수 있는 일반적인 문제를 해결하는 데 도움을 얻으려면 다음 주제를 확인하십시오.
{: shortdesc}


이 페이지에 표시되지 않는 ID 제공자의 특정 오류 코드 및 메시지에 대한 자세한 설명을 보려면 [SAML 스펙](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html)을 검색하십시오. 원하는 내용을 찾지 못할 경우 ID 제공자 관리자에게 문의하면 자세한 정보를 얻을 수 있습니다.
{: note}



### `RelayState` 매개변수 누락
{: #ts-saml-relaystate}

**증상**

`RelayState` 매개변수가 인증 응답에서 누락되었습니다. 


**원인**

{{site.data.keyword.appid_short_notm}}에서 `RelayState`라는 오파크 매개변수를 인증 요청의 일부로 전송합니다. 응답에 이 매개변수가 표시되지 않는다면 ID 제공자가 이 매개변수를 올바르게 리턴하도록 구성되지 않았을 수 있습니다. `RelayState`의 형식은 다음과 같습니다. 

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

**해결 방법**

`RelayState` 매개변수를 어떠한 방식으로도 수정하지 않고 {{site.data.keyword.appid_short_notm}}에 리턴하도록 SAML 제공자가 구성되었는지 확인하십시오. 


### NameID 필드가 누락되었거나 잘못됨
{: #ts-saml-nameid}

**증상**

인증 요청을 전송할 때 `NameID` 관련 오류가 수신됩니다. 

**원인**

{{site.data.keyword.appid_short_notm}}는 서비스 제공자로서 사용자를 서비스 및 ID 제공자로 식별하는 방법을 정의합니다. {{site.data.keyword.appid_short_notm}}를 사용할 경우 다음 예에 표시된 것과 같이 `NameID` 필드의 `NameID` 인증 요청에서 사용자가 식별됩니다. 

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**해결 방법**

이 문제를 해결하려면 ID 제공자 `NameID`가 이메일 주소로 형식화되었는지 확인하십시오. ID 제공자 레지스트리의 모든 사용자가 올바른 이메일 주소 형식을 사용하는지 확인하십시오. 그런 다음 레지스트리에 있는 사용자의 이메일이 여러 개 있는 경우에도 항상 올바른 이메일이 리턴되도록 `NameID` 필드가 적절하게 정의되었는지 확인하십시오. 



### 응답 서명 실패
{: #ts-saml-response-sign-fail}

**증상**

인증 요청을 전송할 때 다음과 같은 오류 메시지가 수신됩니다. 

```
SAML 어설션 서명을 확인할 수 없습니다. {{site.data.keyword.appid_short_notm}}가 SAML 제공자의 서명 인증서로 구성되었는지 확인하십시오.
```
{: screen}

**원인**

{{site.data.keyword.appid_short_notm}}에서는 응답의 모든 SAML 어설션에 서명할 것으로 예상합니다. 서비스가 응답에서 서명을 찾지 못하거나 서명을 확인할 수 없는 경우 오류가 리턴됩니다. 

**해결 방법**

이 문제를 해결하려면 다음을 수행해야 합니다. 

* ID 제공자의 메타데이터 XML 파일에서 서명 인증서를 추출하십시오. `<KeyDescriptor use="signing">`이 포함된 키를 사용해야 합니다. 
* 응답 서명 알고리즘을 XXX로 설정하십시오.  





### 응답 복호화 실패
{: #ts-saml-decrypt-fail}

**증상**

인증 요청에 대한 응답으로 다음 오류 메시지 중 하나가 수신됩니다. 

오류 메시지 1: 

```
예상치 않게 암호화된 어설션이 수신되었습니다. {{site.data.keyword.appid_short_notm}} SAML 구성에서 응답 암호화를 사용으로 설정하십시오.
```
{: screen}

오류 메시지 2:  

```
SAML 어설션을 복호화할 수 없습니다. SAML 제공자가 {{site.data.keyword.appid_short_notm}} 암호화를 사용하여 구성되었는지 확인하십시오.
```
{: screen}


**원인**

ID 제공자가 암호화를 사용하도록 구성된 경우 SAML 인증 요청(AuthnRequest)에 서명하도록 {{site.data.keyword.appid_short_notm}}를 구성해야 합니다. 그런 다음 해당 구성을 예상하도록 ID 제공자를 구성해야 합니다. 이러한 오류는 다음 이유 중 하나로 발생할 수 있습니다. 

- ID 제공자 SAML 응답을 암호화하도록 {{site.data.keyword.appid_short_notm}}가 구성되어 있지 않습니다. 
- {{site.data.keyword.appid_short_notm}}가 어설션을 올바르게 복호화할 수 없습니다. 


**해결 방법**

오류 메시지 1을 수신할 경우, SAML 구성이 암호화된 응답을 예상하도록 설정되어 있는지 확인하십시오. 기본적으로 {{site.data.keyword.appid_short_notm}}는 응답이 암호화될 것으로 예상하지 않습니다. 암호화를 구성하려면 [API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)를 사용하여 `encryptResponse` 매개변수를 **true**로 설정하십시오. 

오류 메시지 2를 수신할 경우, 인증서가 올바른지 확인하십시오. 서명 인증서는 {{site.data.keyword.appid_short_notm}} 메타데이터 XML 파일에서 얻을 수 있습니다. `<KeyDescriptor use="signing">`이 포함된 키를 사용해야 합니다. ``를 서명 알고리즘으로 사용하도록 ID 제공자가 구성되었는지 확인하십시오.  


### Responder 오류 코드
{: #ts-saml-responder}

**증상**

인증 요청을 전송할 때 다음과 같은 일반 오류 메시지가 수신됩니다. 

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**원인**

{{site.data.keyword.appid_short_notm}}에서 초기 인증 요청을 전송하지만, ID 제공자가 사용자 인증을 수행하고 응답을 리턴해야 합니다. 여러 가지 이유로 인해 ID 제공자가 이 오류 메시지를 처리해야 할 수도 있습니다. 

ID 제공자가 다음과 같은 상황일 경우 메시지가 표시될 수 있습니다.  

* 사용자 이름을 찾지 못하거나 확인할 수 없습니다. 
* 인증 요청(`AuthnRequest`)에 정의된 `NameID` 형식을 지원하지 않습니다. 
* 인증 컨텍스트를 지원하지 않습니다. 
* 인증 요청에 서명해야 하거나 서명에 특정 알고리즘을 사용합니다. 

**해결 방법**

이 문제를 해결하려면 구성 및 사용자 이름을 확인하십시오. 올바른 인증 컨텍스트 및 변수가 정의되어 있는지 확인하십시오. 특정 방법으로 요청에 서명해야 하는지 확인하십시오. 




### 지원되지 않는 인증 요청
{: #ts-saml-unsupported-request}

**증상**

지원되지 않는 인증 요청에 대한 메시지가 수신됩니다. 

**원인**

{{site.data.keyword.appid_short_notm}}에서 인증 요청을 생성할 때 인증 컨텍스트를 사용하여 인증 및 SAML 어설션의 품질을 요청할 수 있습니다. 

**해결 방법**

이 문제를 해결하기 위해 인증 컨텍스트를 업데이트할 수 있습니다. 기본적으로 {{site.data.keyword.appid_short_notm}}에서는 인증 클래스 `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` 및 `exact` 비교를 사용합니다. 사용자는 API를 사용하여 유스 케이스에 맞도록 컨텍스트 매개변수를 업데이트할 수 있습니다. 




### SAML 요청 서명 실패
{: #ts-saml-request-sign-fail}

**증상**

인증 요청을 확인할 수 없다는 오류가 수신됩니다. 

**원인**

SAML 인증 요청(`AuthNRequest`)에 서명하도록 {{site.data.keyword.appid_short_notm}}를 구성할 수 있지만, 해당 구성을 예상하도록 ID 제공자를 구성해야 합니다. 

**해결 방법**

이 문제를 해결하려면 다음을 수행하십시오. 

* [set SAML IdP API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)를 통해 `signRequest` 매개변수를 `true`로 설정하여 인증 요청에 서명하도록 {{site.data.keyword.cloud_notm}}가 구성되어 있는지 확인하십시오. 요청 URL을 검토하여 인증 요청에 서명되었는지 확인할 수 있습니다. 서명은 조회 매개변수로 포함됩니다. 예: `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* ID 제공자가 올바른 인증서를 사용하여 구성되었는지 확인하십시오. 서명 인증서를 얻으려면 {{site.data.keyword.cloud_notm}} 대시보드에서 다운로드한 {{site.data.keyword.cloud_notm}} 메타데이터 XML 파일을 확인하십시오. `<KeyDescriptor use="signing">`이 포함된 키를 사용해야 합니다. 

* ``를 서명 알고리즘으로 사용하도록 ID 제공자가 구성되었는지 확인하십시오. 



## 연결 디버깅
{: #ts-saml-debug-connection}

구성이 올바르지만 여전히 버그가 있습니까? SAML 연결을 디버깅하는 데 도움이 되는 다음 몇 가지 팁을 확인하십시오.
{: shortdesc}


### SAML 인증 요청과 응답을 어떻게 캡처합니까? 
{: #ts-saml-capture}

SAML 요청과 응답을 캡처하는 데 사용할 수 있는 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) 및 [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) 등의 브라우저 플러그인에 대한 여러 옵션이 있습니다. 플러그인을 사용하고 싶지 않으십니까? 문제 없습니다. Atlassian은 추가 [수동 추출 방식](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html)에 대한 지시사항을 제공합니다. 


### 메시지를 이해할 수 없습니다! 어떻게 메시지를 디코딩할 수 있습니까? 
{: #ts-saml-decode-messages}

SAML 디버그 도구를 사용한 후에도 여전히 문제가 있는 경우에는 메시지를 디버깅하는 데 유용한 [SAML 개발자 도구](https://www.samltool.com/online_tools.php)를 사용해 보십시오. 잊지 마십시오! SAML 메시지를 가로챈 위치에 따라 요청은 [URL 인코딩](https://www.samltool.com/online_tools.php), [Base 64 인코딩 및 deflated](https://www.samltool.com/decode.php) 또는 [암호화](https://www.samltool.com/decrypt.php) 상태일 수 있습니다. 

SAML 응답과 같은 SAML 메시지를 복호화할 경우에는 온라인 도구를 사용하지 마십시오. 정보를 복호화하려면 이 도구에 암호화 개인 키에 대한 액세스 권한이 필요합니다. 키는 개인용 및 액세스 제어 상태로 유지해야 합니다. 이 절에서 설명한 복호화 도구는 디버깅 용도로만 사용해야 합니다.
{: important}

