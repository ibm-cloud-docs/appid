---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 클라우드 디렉토리 구성
{: #cd}

사용자는 이메일 또는 사용자 이름과 비밀번호를 사용하여 모바일 및 웹 앱에 등록하고 사인인할 수 있습니다. 클라우드 디렉토리는 클라우드에서 유지보수되는 사용자 레지스트리입니다. 사용자가 앱에 등록할 때 해당 사용자가 사용자의 디렉토리에 추가됩니다. 이 기능을 사용하여 사용자는 앱 내에서 자신의 계정을 자유롭게 관리할 수 있습니다.
{: shortdesc}

</br>

## 디렉토리 설정 관리
{: #cd-settings}

앱에 대한 알림 및 사용자 제어의 레벨을 관리할 수 있습니다. 다음 이미지에 표시된 대로 클라우드 디렉토리는 신속하게 설정할 수 있습니다. 이러한 설정은 서비스 대시보드에서 언제든 업데이트할 수 있습니다.
{: shortdesc}


![클라우드 디렉토리 구성](/images/cloud-directory.png)
그림. 클라우드 디렉토리 구성 과정


1. 클라우드 디렉토리가 ID 제공자로 설정되어 있는지 확인하고 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. **끄기**로 설정된 경우에도 여전히 개발 용도로 콘솔을 통해 사용자를 추가할 수 있습니다.
2. 사용자가 지정된 사용자 이름 또는 이메일로 인증되는지 선택하십시오. 이 필드는 등록, 사인인 및 비밀번호 찾기 플로우에 사용됩니다. 사용자가 사용자 이름 및 비밀번호로 사인인할 수 있도록 허용하는 경우 사용자 이름은 8자 이상이어야 하며 공백, 쉼표 또는 슬래시를 포함할 수 없습니다. **참고:** 클라우드 디렉토리에 사용자가 없는 경우에만 옵션을 전환할 수 있습니다. 
3. 발신인 세부사항을 구성하십시오. 메시지가 표시될 이메일 주소, 발신인 및 사용자가 회신할 대상을 지정하십시오.
  조치 URL을 구성하는 경우에는 사용자가 링크를 클릭할 수 있도록 충분한 시간을 제공하십시오. 사용자는 이메일에 비밀번호 재설정을 요청하는 기능과 같은 특정 옵션이 있는지 확인해야 합니다.
  {: tip}
4. 사용자가 수신하는 이메일의 유형 및 발신인 정보의 유형을 결정하십시오.
5. 제공된 템플리트를 사용하여 브랜드가 있는 메시지나 개인화된 메시지를 사용자 정의하십시오. 자세한 정보는 [메시지 관리](/docs/services/appid/cloud-directory.html#cd-messages)를 참조하십시오.
6. GUI의 **사용자** 탭에서 앱에 등록한 사용자를 확인하십시오.

단일 사용자가 1분에 최대 다섯 번 사인인할 수 있습니다. 여섯 번째 시도하면 오류가 표시됩니다.
{: tip}

</br>

## 메시지 관리
{: #cd-messages}

템플리트는 사용자에게 전송할 수 있는 이메일 메시지의 예입니다. 메시지의 컨텐츠 및 레이아웃을 업데이트하여 템플리트를 사용자 정의할 수 있습니다.
{: shortdesc}

1. 대시보드의 **ID 제공자 > 클라우드 디렉토리 > 설정** 탭에서 전송할 메시지를 **설정**으로 지정하십시오.

2. 선택사항: <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">언어 관리 API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 메시지 템플리트에서 사용할 다른 언어를 설정하십시오. 지원되는 언어 코드 목록은 [지원되는 언어](#languages)를 참조하십시오.

3. **메시지 유형**을 선택하십시오.

4. 메시지의 컨텐츠 및 디자인을 변경하여 메시지를 사용자 정의하십시오. 매개변수를 사용하여 메시지를 개인화할 수 있습니다. 변경사항을 저장하십시오!

### 메시지 유형

다양한 유형의 메시지를 사용자에게 발송할 수 있습니다. UI로 프로그래밍된 예제 메시지를 보내도록 선택하거나 더 개인적인 앱 환경을 위해 컨텐츠를 사용자 정의할 수 있습니다.

<dl>
  <dt>환영</dt>
    <dd><p>사용자가 등록을 마치면 애플리케이션을 이용하는 사용자를 이메일을 통해 환영할 수 있습니다. 사용자를 환영하거나 보류하려면 최대한 메시지를 관련시키십시오.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 모든 메시지 매개변수 </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> 로그인 위젯에 대해 구성한 이미지를 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{user.displayName}</code></td>
          <td> 사용자가 앱과 상호작용할 때 사용하도록 선택한 화면 이름을 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{user.email}</code></td>
          <td> 사용자의 등록된 이메일 주소를 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{user.username}</code></td>
          <td> 인증 방법이 사용자 이름 및 비밀번호로 설정된 경우 사용자의 지정된 사용자 이름을 표시합니다.</td>
        </tr>
        <tr>
          <td><code>%{user.firstName}</code></td>
          <td> 사용자의 지정된 이름을 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{user.formattedName}</code></td>
          <td> 사용자의 전체 이름을 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{user.lastName}</code></td>
          <td> 사용자의 지정된 성을 표시합니다. </td>
        </tr>
      </tbody>
    </table>
    <p>**참고**: 사용자가 매개변수로 수집된 정보를 제공하지 않는 경우 공백으로 표시됩니다.</p></dd>
  <dt>비밀번호 찾기</dt>
    <dd><p>비밀번호를 잊었거나 어떤 이유로든 이의 업데이트가 필요한 경우, 사용자는 비밀번호 재설정을 요청할 수 있습니다. 요청에 대한 이메일 응답을 사용자 정의할 수 있습니다. 사용자가 변경을 요청한 경우 이메일의 링크를 클릭할 때까지 비밀번호는 변경되지 않습니다.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 비밀번호 변경 매개변수 </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> 링크가 유효한 기간(시)을 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> 링크가 유효한 기간(분)을 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.code}</code></td>
          <td> URL의 일부로 일회성 패스코드를 표시합니다. 이는 각 개인이 서로 다른 코드를 보유함을 의미합니다. 예를 들면, <code>https://appid-wfm.bluemix.net/verify/6574839563478</code>입니다. </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.link}</code></td>
          <td> 비밀번호를 재설정하기 위해 사용자가 클릭하는 링크를 표시합니다. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>검증</dt>
    <dd><p>사용자가 이메일을 통해 검증하도록 요청할 수 있습니다. 검증을 요청하여 앱에 등록할 수 있는 허위 계정의 수를 제한할 수 있습니다. 사용자가 이메일을 검증할 때까지 앱에 대한 액세스를 제한하거나 프로파일을 작성하는 사용자를 관리하는 방법으로 이를 사용할 수 있습니다.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 메시지 매개변수 검증 </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> 링크가 유효한 기간(시)을 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> 링크가 유효한 기간(분)을 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{verify.code}</code></td>
          <td> 일회성 확인 URL을 표시합니다. </td>
        </tr>
        <tr>
          <td><code>%{verify.link}</code></td>
          <td> 설정에 지정한 조치 URL을 표시합니다. </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>비밀번호 변경</dt>
    <dd><p>비밀번호가 업데이트될 때 사용자에게 알릴 수 있습니다. 이는 사용자가 비밀번호 변경을 요청하지 않은 경우에 유용합니다. 사용자는 적절한 단계를 수행하여 계정을 재차 보호할 수 있습니다. </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 비밀번호 변경 매개변수 </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
          <td> 새 비밀번호가 적용된 시간을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> 비밀번호 변경이 요청된 IP 주소를 표시합니다. </td>
        </tr>
      </tbody>
    </table>
    </dd>
</dl>
</br>
**참고**: {{site.data.keyword.appid_short_notm}}에서는 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 메일 전달 서비스로 사용합니다. 모든 이메일은 단일 SendGrid 계정으로 발송됩니다.


</br>

## 비밀번호 보안 등급 관리
{: #strength}

클라우드 디렉토리에 사용할 수 있는 비밀번호에 대한 요구사항을 설정할 수 있습니다.
{: shortdesc}

보안 등급이 높은 비밀번호를 사용하면 누군가 수동 또는 자동화된 방식으로 비밀번호를 추측하는 것이 어렵거나 불가능할 수 있습니다. 비밀번호 보안 등급은 정규식 문자열로 설정됩니다.

몇 가지 공통 비밀번호 보안 등급 예는 다음과 같습니다.

- 8자 이상이어야 합니다. 정규식 예: `^.{8,}$`
- 하나의 숫자, 하나의 소문자 및 하나의 대문자를 포함해야 합니다. 정규식 예: `^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- 영문자 및 숫자만 포함해야 합니다. 정규식 예: `^[A-Za-z0-9]*$`
- 하나 이상의 고유 문자여야 합니다. 정규식 예: `^(\w)\w*?(?!\1)\w+$`

요구사항을 설정하려면
<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">관리
API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용해야 합니다.

</br>



</br>

## 지원되는 언어
{: #languages}

<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">언어 관리 API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 사용자 통신이 작성될 수 있는 언어를 설정할 수 있습니다. 그러나 영어만 즉시 사용할 수 있습니다. 사용자는 메시지를 번역할 책임이 있습니다. API를 사용하여 구성을 설정한 후 템플리트 텍스트를 변경할 수 있도록 GUI가 업데이트됩니다.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>코드</th>
    <th>언어</th>
    <th>지역</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>아프리칸스어</td>
    <td>남아프리카</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>알바니아어</td>
    <td>알바니아</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>암하라어</td>
    <td>에티오피아</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>아랍어</td>
    <td>알제리</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>아랍어</td>
    <td>바레인</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>아랍어</td>
    <td>이집트</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>아랍어</td>
    <td>이라크</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>아랍어</td>
    <td>요르단</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>아랍어</td>
    <td>쿠웨이트</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>아랍어</td>
    <td>레바논</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>아랍어</td>
    <td>리비아</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>아랍어</td>
    <td>모리타니아</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>아랍어</td>
    <td>모로코</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>아랍어</td>
    <td>오만</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>아랍어</td>
    <td>카타르</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>아랍어</td>
    <td>사우디아라비아</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>아랍어</td>
    <td>시리아</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>아랍어</td>
    <td>튀니지</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>아랍어</td>
    <td>아랍에미리트</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>아랍어</td>
    <td>예멘</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>아르메니아어</td>
    <td>아르메니아</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>아삼어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>아제르바이잔어</td>
    <td>아제르바이잔</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>바스크어</td>
    <td>스페인</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>벨라루스어</td>
    <td>벨라루스</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>벵골어</td>
    <td>방글라데시</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>벨라루스어</td>
    <td>벨라루스</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>벵골어</td>
    <td>방글라데시</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>벵골어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>보스니아어</td>
    <td>보스니아</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>불가리아어</td>
    <td>불가리아</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>버마어</td>
    <td>미얀마</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>카탈로니아어</td>
    <td>스페인</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>중국어</td>
    <td>중국</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>중국어</td>
    <td>싱가포르</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>대만어</td>
    <td>홍콩 특별 행정구</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>대만어</td>
    <td>마카오</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>대만어</td>
    <td>대만</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>크로아티아어</td>
    <td>크로아티아</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>체코어</td>
    <td>체코 공화국</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>덴마크어</td>
    <td>덴마크</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>네덜란드어</td>
    <td>벨기에</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>네덜란드어</td>
    <td>네덜란드</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>영어</td>
    <td>오스트레일리아</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>영어</td>
    <td>벨기에</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>영어</td>
    <td>카메룬</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>영어</td>
    <td>캐나다</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>영어</td>
    <td>가나</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>영어</td>
    <td>홍콩 특별 행정구</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>영어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>영어</td>
    <td>아일랜드</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>영어</td>
    <td>케냐</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>영어</td>
    <td>모리셔스</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>영어</td>
    <td>뉴질랜드</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>영어</td>
    <td>나이지리아</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>영어</td>
    <td>필리핀</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>영어</td>
    <td>싱가포르</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>영어</td>
    <td>남아프리카</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>영어</td>
    <td>탄자니아</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>영어</td>
    <td>영국</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>영어</td>
    <td>미국</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>영어</td>
    <td>잠비아</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>영어</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>에스토니아어</td>
    <td>에스토니아</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>필리핀어</td>
    <td>필리핀</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>핀란드어</td>
    <td>핀란드</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>프랑스어</td>
    <td>알제리</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>프랑스어</td>
    <td>카메룬</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>프랑스어</td>
    <td>콩고민주공화국</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>프랑스어</td>
    <td>벨기에</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>프랑스어</td>
    <td>캐나다</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>프랑스어</td>
    <td>프랑스</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>프랑스어</td>
    <td>코트디부아르</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>프랑스어</td>
    <td>룩셈부르크</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>프랑스어</td>
    <td>모리타니아</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>프랑스어</td>
    <td>모리셔스</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>프랑스어</td>
    <td>모로코</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>프랑스어</td>
    <td>세네갈</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>프랑스어</td>
    <td>스위스</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>프랑스어</td>
    <td>튀니지</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>갈리시아어</td>
    <td>스페인</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>간다어</td>
    <td>우간다</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>그루지야어</td>
    <td>조지아</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>독일어</td>
    <td>오스트리아</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>독일어</td>
    <td>독일</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>독일어</td>
    <td>룩셈부르크</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>독일어</td>
    <td>스위스</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>그리스어</td>
    <td>그리스</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>구자라트어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>하우사어</td>
    <td>나이지리아</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>히브리어</td>
    <td>이스라엘</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>힌디어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>헝가리어</td>
    <td>헝가리</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>아이슬란드어</td>
    <td>아이슬란드</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>이그보어</td>
    <td>나이지리아</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>인도네시아어</td>
    <td>인도네시아</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>이탈리아어</td>
    <td>이탈리아</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>이탈리아어</td>
    <td>스위스</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>일본어</td>
    <td>일본</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>칸나다어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>카자흐어</td>
    <td>카자흐스탄</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>크메르어</td>
    <td>캄보디아</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>킨야르완다어</td>
    <td>르완다</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>콩카니어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>한국어</td>
    <td>대한민국</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>리투아니아어</td>
    <td>리투아니아</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>라트비아어</td>
    <td>라트비아</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>크메르어</td>
    <td>캄보디아</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>마케도니아어</td>
    <td>마케도니아</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>말레이어(라틴)</td>
    <td>말레이시아</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>말라얄람어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>몰타어</td>
    <td>몰타</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>마라티어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>몽골어(키릴)</td>
    <td>몽고</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>네팔어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>네팔어</td>
    <td>네팔</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>노르웨이어(복말)</td>
    <td>노르웨이</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>노르웨이어(니노르스크)</td>
    <td>노르웨이</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>오리야어(오디아어)</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>오로모어</td>
    <td>에티오피아</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>폴란드어</td>
    <td>폴란드</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>포르투갈어</td>
    <td>앙골라</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>포르투갈어</td>
    <td>브라질</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>포르투갈어</td>
    <td>마카오</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>포르투갈어</td>
    <td>모잠비크</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>포르투갈어</td>
    <td>포르투갈</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>펀잡어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>루마니아어</td>
    <td>루마니아</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>러시아어</td>
    <td>러시아</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>세르비아어(키릴)</td>
    <td>세르비아</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>세르비아어(라틴)</td>
    <td>몬테네그로</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>세르비아어(라틴)</td>
    <td>세르비아</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>싱헐리즈어</td>
    <td>스리랑카</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>슬로바키아어</td>
    <td>슬로바키아</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>슬로베니아어</td>
    <td>슬로베니아</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>스페인어</td>
    <td>아르헨티나</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>스페인어</td>
    <td>볼리비아</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>스페인어</td>
    <td>칠레</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>스페인어</td>
    <td>콜롬비아</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>스페인어</td>
    <td>코스타리카</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>스페인어</td>
    <td>도미니카 공화국</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>스페인어</td>
    <td>에콰도르</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>스페인어</td>
    <td>엘살바도르</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>스페인어</td>
    <td>과테말라</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>스페인어</td>
    <td>온두라스</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>스페인어</td>
    <td>멕시코</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>스페인어</td>
    <td>니카라과</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>스페인어</td>
    <td>파나마</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>스페인어</td>
    <td>파라과이</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>스페인어</td>
    <td>페루</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>스페인어</td>
    <td>푸에토리코</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>스페인어</td>
    <td>스페인</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>스페인어</td>
    <td>미국</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>스페인어</td>
    <td>우루과이</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>스페인어</td>
    <td>베네수엘라</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>스와힐리어</td>
    <td>케냐</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>스와힐리어</td>
    <td>탄자니아</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>스웨덴어</td>
    <td>스웨덴</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>타밀어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>텔루구어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>태국어</td>
    <td>태국</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>터키어</td>
    <td>터키</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>우크라이나어</td>
    <td>우크라이나</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>우르두어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>우르두어</td>
    <td>파키스탄</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>우즈베크어(키릴)</td>
    <td>우즈베키스탄</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>우즈베크어(라틴)</td>
    <td>우즈베키스탄</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>베트남어</td>
    <td>베트남</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>웨일즈어</td>
    <td>영국</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>요루바어</td>
    <td>나이지리아</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>줄루어</td>
    <td>남아프리카</td>
  </tr>
</table>
