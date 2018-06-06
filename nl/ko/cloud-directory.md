---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 클라우드 디렉토리 구성
{: #cd}

{{site.data.keyword.appid_short_notm}}를 구성하여 ID 제공자로 클라우드 디렉토리를 사용할 수 있습니다. 이메일과 비밀번호를 사용하여 모바일과 엡 앱에 등록 및 사인인할 수 있습니다. 클라우드 디렉토리는 클라우드에서 유지보수되는 사용자 레지스트리입니다. 사용자가 이메일과 비밀번호를 사용하여 앱에 등록하면 사용자 디렉토리에 추가됩니다. 이 기능을 사용하면 일반 사용자가 앱에서 고유 계정을 자유롭게 관리할 수 있습니다.
{: shortdesc}

</br>

## 디렉토리 설정 관리
{: #cd-settings}

앱에 대한 알림 및 사용자 제어의 레벨을 관리할 수 있습니다. 다음 이미지에 표시된 대로 클라우드 디렉토리는 신속하게 설정할 수 있습니다. 이러한 설정은 서비스 대시보드에서 언제든 업데이트할 수 있습니다.
{: shortdesc}

![클라우드 디렉토리 구성](/images/cloud-directory.png)

1. 클라우드 디렉토리가 ID 제공자로 설정되어 있는지 확인하고 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. **끄기**로 설정된 경우 콘솔을 통해 계속해서 사용자를 추가할 수 있으나, 이는 개발 목적으로만 가능합니다.
2. 발신인 세부사항을 구성하십시오. 메시지가 표시될 이메일 주소, 발신인 및 사용자가 회신할 대상을 지정하십시오.
  **참고**: 사용자가 링크를 클릭하는 데 충분한 시간을 지정하도록 조치 URL을 구성하는 시기를 확인하십시오. 사용자는 이메일에 비밀번호 재설정을 요청하는 기능과 같은 특정 옵션이 있는지 확인해야 합니다.
3. 사용자가 수신하는 이메일의 유형 및 발신인 정보의 유형을 결정하십시오.
4. 제공된 템플리트를 사용하여 사용자의 브랜드 또는 개인화된 메시지로 메시지를 사용자 정의하십시오. 자세한 정보는 [메시지 관리](/docs/services/appid/cloud-directory.html#cd-messages)를 참조하십시오.
5. GUI의 **사용자** 탭에서 앱에 등록한 사용자를 확인하십시오.

</br>

## 메시지 관리
{: #cd-messages}

템플리트는 사용자에게 전송할 수 있는 이메일 메시지의 예제입니다. 메시지의 컨텐츠 및 레이아웃을 업데이트하여 템플리트를 사용자 정의할 수 있습니다. 디렉토리 설정 탭에서 이 메시지를 **설정** 또는 **해제**로 설정할 수 있습니다.
{: shortdesc}

1. **메시지 유형**을 선택하십시오.
2. 메시지의 컨텐츠 및 디자인을 변경하여 메시지를 사용자 정의하십시오. 매개변수를 사용하여 메시지를 개인화할 수 있습니다. 변경사항을 저장하십시오!

### 메시지 유형

사용자에게 보낼 수 있는 메시지 유형은 여러 가지가 있습니다. UI로 프로그래밍된 예제 메시지를 보내도록 선택하거나 더 개인적인 앱 환경을 위해 컨텐츠를 사용자 정의할 수 있습니다.

<dl>
  <dt>환영</dt>
    <dd><p>사용자가 애플리케이션에 등록한 후 이메일을 통해 사용자를 환영할 수 있습니다. 사용자를 환영하거나 보류하려면 최대한 메시지를 관련시키십시오.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 모든 유형의 메시지에 사용할 수 있는 매개변수 </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> 로그인 위젯에 대해 구성한 이미지를 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> 사용자가 앱과 상호작용할 때 사용하도록 선택한 화면 이름을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> 사용자의 등록된 이메일 주소를 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> 사용자의 지정된 이름을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> 사용자의 전체 이름을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> 사용자의 지정된 성을 표시합니다. </td>
        </tr>
      </tbody>
    </table>
    <p>**참고**: 사용자가 매개변수로 수집된 정보를 제공하지 않는 경우 공백으로 표시됩니다.</p></dd>
  <dt>비밀번호 찾기</dt>
    <dd><p>어떠한 이유로든 잊어버린 비밀번호를 재설정해야 하는지 또는 업데이트해야 하는지를 물어볼 수 있습니다. 요청에 대한 이메일 응답을 사용자 정의할 수 있습니다. 사용자가 변경을 요청한 경우 이메일의 링크를 클릭할 때까지 비밀번호는 변경되지 않습니다.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 비밀번호 변경 매개변수 </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 링크가 유효한 기간(시)을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 링크가 유효한 기간(분)을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> URL의 일부로 일회성 패스코드를 표시합니다. 이는 각 개인이 서로 다른 코드를 보유함을 의미합니다. 예를 들면, <code>https://appid-wfm.bluemix.net/verify/6574839563478</code>입니다. </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> 비밀번호를 재설정하기 위해 사용자가 클릭하는 링크를 표시합니다. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>검증</dt>
    <dd><p>사용자가 이메일을 통해 검증하도록 요청할 수 있습니다. 검증을 요청하여 앱에 등록할 수 있는 허위 계정의 수를 제한할 수 있습니다. 사용자가 이메일을 검증할 때까지 앱에 대한 액세스를 제한하거나 프로파일을 작성하는 사용자를 관리하는 방법으로 이를 사용할 수 있습니다.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 메시지 매개변수 검증 </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 링크가 유효한 기간(시)을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 링크가 유효한 기간(분)을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> 일회성 확인 URL을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> 설정에 지정한 조치 URL을 표시합니다. </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>비밀번호 변경</dt>
    <dd><p>비밀번호가 업데이트될 때 사용자에게 알릴 수 있습니다. 비밀번호 변경을 요청하지 않은 경우 유용합니다. 계정의 보안을 재설정하기 위한 적절한 단계를 수행할 수 있습니다.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 비밀번호 변경 매개변수 </th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
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
**참고**: {{site.data.keyword.appid_short_notm}}에서는 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 메일 전달 서비스로 사용합니다. 모든 이메일은 하나의 SendGrid 계정을 사용하여 보냅니다.

</br>
## 다음 단계
이제 클라우드 디렉토리를 구성했으므로 loginwidget의 코드를 앱 코드에 추가할 준비가 되었습니다. 다음 이미지에서 SDK 언어 아이콘을 클릭하여 수행해야 하는 작업을 확인하십시오.
{: shortdesc}

<img usemap="#options-map" border="0" class="image" id="options" src="images/options.png" width="750" alt="SDK 언어 아이콘을 클릭하여 앱에서 클라우드 디렉토리를 시작하십시오." style="width:750px;" />
<map name="options-map" id="options-map">
<area href="branded.html#branded-ui-android" alt="Android SDK로 사인인 환경 관리" shape="rect" coords="187, 6, 305, 120" />
<area href="branded.html#branded-ui-ios-swift" alt="iOS Swift SDK로 사인인 환경 관리" shape="rect" coords="333, 6, 448, 125" />
<area href="branded.html#branded-ui-nodejs" alt="Node.js SDK로 사인인 환경 관리" shape="rect" coords="472, 7, 590, 121" />
</map>
