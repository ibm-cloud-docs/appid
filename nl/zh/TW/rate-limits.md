---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, rates, cloud directory, rate limit, attempts

subcollection: appid

---

{:external: target="_blank" .external}
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


# App ID 限制
{: #limits}

速率限制用來控制透過您的 App ID 實例送入和送出的資料流量。藉由限制要求或資源，您可以保護應用程式。
{: shortdesc}

## App ID 精簡方案 
{: #lite-limits}

請檢閱下表，以查看針對 App ID 精簡實例的現有限制。 

<table>
    <tr>
        <th>資源</th>
        <th>上限</th>
    </tr>
    <tr>
        <td>使用者</td>
        <td>1000</td>
    </tr>
    <tr>
        <td>鑑別</td>
        <td>每月 1000 次</td>
    </tr>
</table>

## 一般
{: #general-limits}

下表列出 IBM Cloud App ID 資源的每個使用者上限限制，以及超出限制時的封鎖期間。這些限制適用於可以建立 IBM Cloud App ID 資源的任何使用者。
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>限制</th>
        <th>超出時</th>
    </tr>
    <tr>
        <td>一位使用者的登入嘗試數</td>
        <td>每分鐘 5 次</td>
        <td>使用者無法登入，持續 1 分鐘。</td>
    </tr>
    <tr>
        <td>更新使用者設定檔屬性</td>
        <td>每分鐘 5 次</td>
        <td>使用者無法更新設定檔，持續 1 分鐘。</td>
    </tr>
        <td>刪除使用者設定檔屬性</td>
        <td>每分鐘 5 次</td>
        <td>使用者無法更新設定檔，持續 1 分鐘。</td>
    </tr>
</table>



## Cloud Directory
{: #limits-cd}

請檢閱下表，以查看與 Cloud Directory 相關聯的限制。
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>可配置</th>
        <th>限制</th>
        <th>超出時</th>
    </tr>
    <tr>
        <td>每個帳戶的登入嘗試數</td>
        <td>是</td>
        <td>無限制</td>
        <td>實例的所有登入嘗試都遭到封鎖，持續一分鐘。</td>
    </tr>
    <tr>
        <td>每個帳戶的註冊嘗試數</td>
        <td>是</td>
        <td>無限制</td>
        <td>實例的所有註冊嘗試都遭到封鎖，持續一分鐘。</td>
    </tr>
    <tr>
        <td>電子郵件傳送要求</td>
        <td>否</td>
        <td>每位使用者 10 分鐘內 10 封電子郵件</td>
        <td>使用者的電子郵件要求遭到封鎖，持續 30 分鐘。</td>
    </tr>
</table>

如需相關資訊，請參閱<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">速率限制管理 API</a>。
