---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-06"

keywords: Authentication, authorization, identity, app security, secure, rates, cloud directory, rate limit, attempts

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


# App ID 한계
{: #limits}

비율 제한은 유입되어 App ID 인스턴스를 거치는 트래픽의 양을 제어합니다. 요청 또는 리소스를 제한하면 애플리케이션을 보호할 수 있습니다.
{: shortdesc}

## App ID Lite 플랜 
{: #lite-limits}

App ID의 Lite 인스턴스에 적합한 한계를 확인하려면 다음 표를 검토하십시오.  

<table>
    <tr>
        <th>리소스</th>
        <th>최대값</th>
    </tr>
    <tr>
        <td>사용자</td>
        <td>1000명</td>
    </tr>
    <tr>
        <td>인증</td>
        <td>매월 1000회</td>
    </tr>
</table>

## 일반사항
{: #general-limits}

다음 표는 IBM Cloud App ID 리소스에 대한 사용자당 최대값 한계 및 한계 초과 시 차단 기간을 보여줍니다. 이러한 한계는 IBM Cloud App ID 리소스를 작성할 수 있는 모든 사용자에게 적용됩니다.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>한계</th>
        <th>초과 시</th>
    </tr>
    <tr>
        <td>한 명씩 사인인 시도</td>
        <td>분당 5회</td>
        <td>사용자가 1분 동안 사인인할 수 없음</td>
    </tr>
    <tr>
        <td>사용자 프로파일 속성 업데이트</td>
        <td>분당 5회</td>
        <td>사용자가 1분 동안 프로파일을 업데이트할 수 없음</td>
    </tr>
        <td>사용자 프로파일 속성 삭제</td>
        <td>분당 5회</td>
        <td>사용자가 1분 동안 프로파일을 업데이트할 수 없음</td>
    </tr>
</table>



## Cloud Directory
{: #limits-cd}

Cloud Directory와 연관된 한계를 확인하려면 다음 표를 검토하십시오.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>구성 가능 여부</th>
        <th>한계</th>
        <th>초과 시</th>
    </tr>
    <tr>
        <td>계정별 사인인 시도</td>
        <td>예</td>
        <td>무제한</td>
        <td>인스턴스에 대한 모든 사인인 시도가 1분 동안 차단됩니다. </td>
    </tr>
    <tr>
        <td>계정별 등록 시도</td>
        <td>예</td>
        <td>무제한</td>
        <td>인스턴스에 대한 모든 등록 시도가 1분 동안 차단됩니다. </td>
    </tr>
    <tr>
        <td>이메일 전송 요청</td>
        <td>아니오</td>
        <td>사용자당 10분 동안 10개의 이메일</td>
        <td>사용자에 대한 이메일 요청이 30분 동안 차단됩니다. </td>
    </tr>
</table>

자세한 정보는 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">비율 제한 관리 API</a>를 참조하십시오. 
