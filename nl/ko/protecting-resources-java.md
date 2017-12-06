---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Liberty for Java 리소스 보호
{: #protecting-liberty}

{{site.data.keyword.appid_short_notm}}를 사용하여 IBM Liberty for Java 앱에서 엔드포인트를 보호할 수 있습니다. Liberty for Java에는 OIDC(Open ID Connect) 요청을 처리하기 위한 내장 기능이 있습니다. 

## 시작하기 전에
{: #begin}

* 기존의 바인드 해제된 [IBM Liberty for Java 애플리케이션](https://console.bluemix.net/catalog/starters/liberty-for-java)이 필요합니다. 
Liberty for Java 앱 개발에 친숙해지려면 [앱](/docs/runtimes/liberty/index.html)을 참조하십시오. 
* [Apache Maven](https://maven.apache.org/download.cgi)이 설치되어 있는지 확인하십시오. 
* Liberty for Java에서 OIDC가 작동하는 방법을 학습하십시오. 

## Liberty for Java의 리소스 보호
{: #protecting-liberty}

1. UI에서 Liberty for Java 샘플을 다운로드하십시오. 샘플에는 표준 Liberty 파일의 Zip 파일이 포함되어 있습니다. 

2. 샘플의 압축이 풀린 디렉토리에서 터미널을 여십시오. 

3. Cloud Foundry 명령행을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. 프롬프트가 나타나면 신임 정보를 입력하십시오. 

  ```
  cf login
  ```
  {: codeblock}

4. 애플리케이션을 배치하십시오. 다음 명령을 실행하면 tenantid와 관련된 이름의 Liberty for Java 인스턴스가 작성됩니다. 

  ```
  cf push
  ```
  {: codeblock}

5. 서비스 인스턴스를 새 Liberty for Java 인스턴스에 바인드하고 애플리케이션을 재배치하십시오. 

6. 브라우저에서 애플리케이션을 열고 신임 정보를 사용하여 로그인하여 인증 활동을 검토하십시오. 


## Liberty for Java 샘플 업데이트
{: #updating-liberty}

샘플 앱에서 업데이트를 수행하려면 다음 지시사항을 사용하십시오. 

1. 서블릿, jsp 및 html을 작성하십시오. 
2. 보호된 리소스를 정의하고 이를 `web.xml` 및 `server.xml` 권한 필터에 추가하십시오. 
3. WAR 파일을 작성하고 이를 Liberty for Java에 배치하십시오. 

앱 업데이트에 대한 자세한 정보는 [기존 애플리케이션에 {{site.data.keyword.appid_short_notm}} 추가](/docs/services/appid/existing.html#existing-liberty)를 참조하십시오. 
