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


# App ID の制限
{: #limits}

App ID のインスタンスが送受信するトラフィック量を制御するために、レート制限が使用されます。 要求またはリソースを制限することで、アプリケーションを保護できます。
{: shortdesc}

## App ID ライト・プラン 
{: #lite-limits}

以下の表を参照して、App ID のライト・インスタンスに適用される制限を確認してください。 

<table>
    <tr>
        <th>リソース</th>
        <th>最大</th>
    </tr>
    <tr>
        <td>ユーザー</td>
        <td>1000</td>
    </tr>
    <tr>
        <td>認証</td>
        <td>1 カ月あたり 1000</td>
    </tr>
</table>

## 一般
{: #general-limits}

IBM Cloud App ID リソースに対するユーザーごとの上限と、その制限を超えた場合のブロック時間を以下の表にリストします。 これらの制限は、IBM Cloud App ID リソースを作成できるすべてのユーザーに適用されます。
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>制限</th>
        <th>超過時</th>
    </tr>
    <tr>
        <td>1 ユーザーによるサインイン試行回数</td>
        <td>1 分あたり 5 回</td>
        <td>ユーザーは 1 分間サインインできない。</td>
    </tr>
    <tr>
        <td>ユーザー・プロファイル属性の更新</td>
        <td>1 分あたり 5 回</td>
        <td>ユーザーは 1 分間プロファイルを更新できない。</td>
    </tr>
        <td>ユーザー・プロファイル属性の削除</td>
        <td>1 分あたり 5 回</td>
        <td>ユーザーは 1 分間プロファイルを更新できない。</td>
    </tr>
</table>



## クラウド・ディレクトリー
{: #limits-cd}

以下の表を参照して、クラウド・ディレクトリーに関する制限を確認してください。
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>構成可能かどうか</th>
        <th>制限</th>
        <th>超過時</th>
    </tr>
    <tr>
        <td>1 アカウントあたりのサインイン試行回数</td>
        <td>はい</td>
        <td>無制限</td>
        <td>インスタンスに対するすべてのサインイン試行が 1 分間ブロックされる。</td>
    </tr>
    <tr>
        <td>1 アカウントあたりの登録試行回数</td>
        <td>はい</td>
        <td>無制限</td>
        <td>インスタンスに対するすべての登録試行が 1 分間ブロックされる。</td>
    </tr>
    <tr>
        <td>E メール送信要求</td>
        <td>いいえ</td>
        <td>1 ユーザーあたり 10 分でメール 10 通</td>
        <td>ユーザーの E メール要求が 30 分間ブロックされる。</td>
    </tr>
</table>

詳しくは、<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">レート制限管理 API</a> を参照してください。
