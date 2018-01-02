---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 소셜 ID 제공자 구성
{: #setting-up-idp}

ID 제공자는 모바일 및 웹 앱에 대한 추가 인증 레벨을 제공합니다. {{site.data.keyword.appid_full}}를 사용하면 앱에 대한 싱글 사인온 환경을 설정할 수 있도록 하나 이상의 ID 제공자를 구성할 수 있습니다.
{: shortdesc}

## 기본 구성
{: #default}

{{site.data.keyword.appid_short_notm}}는 ID 제공자의 초기 설정에 도움이 되도록 기본 구성을 제공합니다.
{: shortdesc}

기본 신임 정보가 Facebook 및 Google에 맞게 설정되어 있습니다. 매일 인스턴스당 최대 100개까지만 신임 정보를 사용할 수 있습니다. IBM 신임 정보이므로, 이는 개발 모드에서만 앱에서 사용되어야 합니다. 앱을 공개하기 전에 [자체 신임 정보로 구성을 업데이트](/docs/services/appid/identity-providers.html)하십시오. 


## Facebook 구성
{: #facebook}

Facebook을 ID 제공자로 사용하도록 {{site.data.keyword.appid_short}} 서비스를 구성할 수 있습니다.
{: shortdesc}

### Facebook에서 앱 ID 및 본인확인정보 가져오기

Facebook을 ID 제공자로 사용하려면 Facebook 애플리케이션에서 웹 사이트 플랫폼을 추가하고 구성해야 합니다. 

1. <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for developers 사이트 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에서 사용자 계정에 로그인하십시오. 
2. Facebook 앱 ID 및 본인확인정보를 기록해 두십시오. 이러한 값은 서비스 대시보드에서 인증을 위해 웹 프로젝트를 구성하는 데 필요합니다. 
3. 웹 플랫폼을 추가하고 사이트 URL을 입력하십시오.
4. 제품 목록에서 **Facebook 로그인**을 선택하십시오.
5. 올바른 OAuth 경로 재지정 URL 필드에서 권한 서버 콜백 엔드포인트 URL을 입력하십시오. 서비스 인스턴스 구성 후에 이 값을 추가할 수 있습니다.
6. **변경사항 저장**을 클릭하십시오.


### Facebook 인증용 {{site.data.keyword.appid_short_notm}} 구성

Facebook 앱 ID와 본인확인정보가 있으며 개발자용 Facebook 앱이 웹 클라이언트를 제공하도록 구성되어 있으면 서비스 대시보드에서 Facebook 인증을 편집할 수 있습니다. 

1. 서비스 대시보드의 **관리** 탭에서 **Facebook**을 선택하고 **편집**을 클릭하십시오. 
2. 개발자용 Facebook 웹 사이트에서 확보한 Facebook 앱 ID 및 본인확인정보를 입력하십시오. 
3. **개발자용 Facebook의 경로 재지정 URI** 필드에 있는 URI를 복사하십시오. Facebook 개발자 포털의 **Facebook 로그인** 섹션에서 **올바른 OAuth 경로 재지정 URI** 필드에 URI를 붙여넣기하십시오. 
4. **저장**을 클릭하십시오.
5. 선택사항: 웹 앱의 경우 **웹 애플리케이션 경로 재지정 URL** 필드에 경로 재지정 URL을 입력하십시오. 이 값은 개발자가 판별하며 권한 부여 프로세스가 완료된 후에 경로 재지정 URL에 액세스하는 데 사용됩니다. 


## Google 구성
{: #google}

Google을 ID 제공자로 사용하도록 {{site.data.keyword.appid_short}} 서비스를 구성할 수 있습니다.
{: shortdesc}

### Google에서 클라이언트 ID 및 본인확인정보 가져오기

<a href="https://developers.google.com/" target="_blank">Google 개발자 콘솔 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에서 프로젝트를 작성하고 웹 클라이언트를 서비스하는 프로젝트를 구성한 후에 클라이언트 ID 및 본인확인정보를 가져오십시오. 

1. 프로젝트를 작성하십시오. 
2. Google+ API를 Google 프로젝트에 추가하십시오. 
3. 신임 정보를 Google+ API에 추가하십시오.
    1. API 유형으로 Google+ API를 선택하십시오. 
    2. API를 호출할 위치로서 **웹 브라우저**를 선택하십시오. 
    3. **사용자 데이터**를 선택하십시오. 
    4. 클라이언트 ID를 작성하기 위한 필수 필드를 모두 채우십시오. 본인확인정보가 동시에 작성됩니다. 
4. Google 클라이언트 ID 및 본인확인정보를 기록해 두십시오. 신임 정보 탭에서 본인확인정보와 클라이언트 ID를 가져오기 위해 작성한 ID를 선택하십시오. 

### Google 인증용 {{site.data.keyword.appid_short}} 구성

Google 프로젝트를 구성하고 클라이언트 ID 및 본인확인정보를 보유한 후에는 Google 인증을 위한 서비스 대시보드의 편집이 가능합니다. 

1. 서비스 대시보드의 **관리** 탭에서 **Google**을 선택하고 **편집**을 클릭하십시오. 
2. Google 개발자 콘솔에서 가져온 클라이언트 ID 및 본인확인정보를 입력하십시오. 
3. {{site.data.keyword.appid_short}} URL의 권한을 부여하십시오. 
    1. Google ID 제공자 세부사항에서 **Google 개발자 콘솔의 경로 재지정 URL**을 복사하십시오. 
    2. Google 프로젝트의 신임 정보 탭에서 이 통합을 위해 작성된 클라이언트 ID를 선택하십시오. 
    3. {{site.data.keyword.appid_short}}의 URL을 **권한 부여된 경로 재지정 URI** 필드에 붙여넣고 **저장**을 클릭하십시오. 
4. **저장**을 클릭하여 {{site.data.keyword.appid_short}}의 Google 구성을 업데이트하십시오. 
5. 선택사항: 웹 앱에 대해 **관리** 탭에서 경로 재지정 URL을 입력하십시오. 권한 부여 프로세스가 완료되면 사용자가 이 URL로 보내집니다. 
