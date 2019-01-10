---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# 관리
{: #managing}

ID 제공자(IdP)는 인증을 통해 모바일 및 웹 앱에 대한 보안 레벨을 추가합니다. {{site.data.keyword.appid_full}}를 사용하는 경우 사용자를 위한 사용자 정의 사인인 경험을 작성하기 위해 하나 이상의 ID 제공자를 구성할 수 있습니다.
{: shortdesc}


**ID 제공자가 무엇입니까?**

ID 제공자는 사용자, 기능 ID 또는 애플리케이션 등의 엔티티에 대한 정보를 작성하고 관리합니다. 제공자는 비밀번호 등의 인증 정보를 사용하여 엔티티의 ID를 확인합니다. 그런 다음 IdP에서 다른 서비스 제공자에게 ID 정보를 전송합니다. ID 제공자가 엔티티를 인증하기 때문에 {{site.data.keyword.appid_short_notm}}는 해당 엔티티에 권한을 부여하고 앱에 대한 액세스를 부여할 수 있습니다.

</br>

**{{site.data.keyword.appid_short_notm}}에서 통합을 제공하는 ID 제공자에는 무엇이 있습니까?**

서비스에서 사용하도록 사전 구성되어 있는 몇 가지 제공자가 존재합니다.

<table>
  <tr>
    <th>제공자</th>
    <th>유형</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>[클라우드 디렉토리](/docs/services/appid/cloud-directory.html)</td>
    <td>관리 레지스트리</td>
    <td>클라우드에서 고유한 사용자 레지스트리를 유지보수할 수 있습니다. 사용자가 앱에 등록하면 해당 사용자가 사용자 디렉토리에 추가됩니다. 이 옵션은 사용자가 앱 내에서 자신의 계정을 더 자유롭게 관리할 수 있도록 해줍니다.</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid/enterprise.html)</td>
    <td>엔터프라이즈</td>
    <td>일반 사용자의 경험에 싱글 사인온을 작성할 수 있습니다.</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid/identity-providers.html#facebook)</td>
    <td>소셜</td>
    <td>일반 사용자가 해당 Facebook 인증 정보를 사용하여 앱에 로그인할 수 있습니다.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid/identity-providers.html#google)</td>
    <td>소셜</td>
    <td>일반 사용자가 해당 Google+ 인증 정보를 사용하여 앱에 로그인할 수 있습니다.</td>
  </tr>
  <tr>
    <td>[사용자 정의](/docs/services/appid/custom.html)</td>
    <td> </td>
    <td>제공된 옵션 중 사용자의 특정 요구사항을 충족하는 옵션이 없는 경우 {{site.data.keyword.appid_short_notm}}에서 작동하도록 고유한 ID 플로우를 구성할 수 있습니다.</td>
  </tr>
  
</table>

</br>

**{{site.data.keyword.appid_short_notm}}는 어떻게 ID 제공자와 상호작용합니까?**

{{site.data.keyword.appid_short_notm}}는 OpenID Connect, SAML 등의 여러 프로토콜을 사용하여 ID 제공자와 상호작용합니다. 예를 들어 OpenID Connect는 Facebook, Google 등의 여러 소셜 제공자에서 사용되는 프로토콜입니다. <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 또는 <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 등의 엔터프라이즈 제공자는 일반적으로 SAML을 ID 프로토콜로 사용합니다. [클라우드 디렉토리](cloud-directory.html)의 경우 서비스에서 SCIM을 사용하여 ID 정보를 확인합니다.

애플리케이션 ID에서 작동합니까? [애플리케이션 ID](app-to-app.html)를 참조하십시오.
{: tip}

</br>
</br>

## 설정 구성
{: #configuring}

사용할 제공자, 경로 재지정 URL 및 앱의 토큰 정보를 결정할 수 있습니다. 구성된 설정은 이 서비스 인스턴스에 있는 모든 ID 제공자에 적용됩니다. 예를 들어 토큰 만기를 설정하는 경우 소셜인지 또는 엔터프라이즈인지 여부에 관계 없이 구성되어 있는 모든 제공자에 적용됩니다.

</br>

**제공자를 구성하려면 다음 작업을 수행하십시오.**

1. 서비스 대시보드로 이동하십시오.
2. 탐색의 **ID 제공자** 섹션에서 **관리** 페이지를 선택하십시오.
3. **ID 제공자** 탭에서 사용할 제공자를 **켜기**로 설정하십시오.
4. 선택사항: **익명 사용자**를 끌 것인지 또는 기본값인 **켜기**로 둘 것인지 여부를 결정하십시오. **켜기**로 설정된 경우 사용자 정의 사용자 속성이 앱과 상호작용을 시작하는 즉시 사용자와 연관됩니다. 식별된 사용자가 되는 경로에 대한 자세한 정보는 [점진적 인증](progressive.html#progressive)을 참조하십시오.

{{site.data.keyword.appid_short_notm}}는 Facebook 및 Google+의 초기 설정을 위한 기본 인증 정보를 제공합니다. 매일 인스턴스당 최대 100개까지만 인증 정보를 사용할 수 있습니다. 이 인증 정보는 IBM 인증 정보이므로 개발용으로만 사용되어야 합니다. 앱을 공개하기 전에 자체 인증 정보로 구성을 업데이트하십시오.
{: tip}

</br>

**설정을 구성하려면 다음 작업을 수행하십시오.**

1. 경로 재지정 URL을 추가하십시오. 경로 재지정 URL은 앱의 콜백 엔드포인트입니다. {{site.data.keyword.appid_short_notm}}는 피싱 공격을 차단하기 위해 화이트리스트에 대해 URL을 유효성 검증합니다.
  1. **웹 경로 재지정 URL 추가** 필드에 URL을 입력한 후 **+** 아이콘을 클릭하십시오.
  2. 가능한 모든 경로 재지정 URL이 목록에 추가될 때까지 1단계를 반복하십시오.

  URL에 조회 매개변수를 포함하지 마십시오. 이는 유효성 검증 프로세스에서 무시됩니다. 예: `http://host:[port]/path`
  {: tip}

2. 토큰을 구성하십시오. 토큰 수명은 각각의 사용자가 사인인하는 시점에 다시 시작됩니다. 예를 들어 새로 고치기 토큰 수명을 10일로 설정합니다. 사용자가 처음으로 사인인하면 액세스 토큰 및 새로 고치기 토큰이 작성됩니다. 사용자가 며칠 후에(구체적으로는 3일 후) 앱으로 돌아가는 경우 다시 사인인할 필요가 없습니다. 하지만 사용자가 초기 사인인 이후 12일 간 대기한 후 앱으로 돌아가는 경우 해당 사용자는 다시 사인인해야 하며 토큰 세트가 사용자와 연관됩니다.
  1. 사용자 상호작용 없이 사인인할 수 있도록 허용하려면 **새로 고치기 토큰**을 **켜짐**으로 설정하십시오.
  2. 새로 고치기 토큰의 수명을 설정하십시오. 만기는 일 단위로 설정되며 1 - 90 사이의 값이 될 수 있습니다. 숫자가 작을수록 사용자가 더 빈번하게 사인인해야 합니다.
  3. 액세스 토큰 수명을 설정하십시오. 만기는 분 단위로 설정되며 5 - 1440 사이의 값이 될 수 있습니다. 값이 작을수록 토큰 절도에 대비한 더 많은 보호가 제공됩니다.
  4. 익명 토큰 수명을 설정하십시오. [익명 토큰](/docs/services/appid/progressive.html#anonymous)은 사용자가 앱과 상호작용하기 시작하는 시점에 해당 사용자에게 지정됩니다. 사용자가 사인인하면 익명 토큰의 정보가 해당 사용자와 연관된 토큰으로 전송됩니다. 만기는 일 단위로 설정되며 1 - 90 사이의 값이 될 수 있습니다.

</br>
</br>
