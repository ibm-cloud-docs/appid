---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# 管理用户
{: #cd-users}

启用 Cloud Directory 后，用户可以使用电子邮件或用户名和密码来注册应用程序。
{: shortdesc}


Cloud Directory 用户与 {{site.data.keyword.appid_short_notm}} 用户不同。用户可以使用您配置的不同身份提供者选项来注册应用程序。本主题中提到的用户是指在注册应用程序时选择使用 Cloud Directory 选项的用户。
{: note}


## 添加和删除用户
{: #add-delete-users}

可以通过 {{site.data.keyword.appid_short_notm}} 仪表板或使用 API 来管理 Cloud Directory 用户。
{: shortdesc}

要查看特定用户的完整数据，可以使用 API 将 Cloud Directory 用户的信息作为 JSON 对象返回。要查看 {{site.data.keyword.appid_short_notm}} 支持的完整用户数据集，请查看 [SCIM 核心模式](https://tools.ietf.org/html/rfc7643#section-8.2)。

### 添加用户
{: #add-users}

可以使用以下步骤通过 {{site.data.keyword.appid_short_notm}} 仪表板来添加用户。

出于测试目的，您可以通过 {{site.data.keyword.appid_short_notm}} 仪表板来添加用户。

1. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的 **Cloud Directory > 用户**选项卡。

2. 单击**添加用户**。这将显示一个表单。

3. 输入**名字**、**姓氏**、**电子邮件**和**密码**。请确保您尝试注册的电子邮件尚未被其他用户使用。要确保正确输入了密码，请通过在**重新输入密码**字段中输入密码来进行确认。

4. 单击**保存**。这将创建 Cloud Directory 用户。


### 删除用户
{: #delete-users}

如果要从目录中除去用户，可以通过 GUI 删除该用户。

1. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的 **Cloud Directory > 用户**选项卡。

2. 单击要删除的用户旁边的复选框。这将显示一个框。

3. 在该框中，单击**删除**。这将显示一个屏幕。

4. 确认您了解通过单击**删除**来删除用户是无法撤销的操作。如果这是误操作，您可以将用户重新添加到目录，但有关该用户的任何信息都不再可用。


## 迁移用户
{: #user-migration}

有时，您可能需要设置 {{site.data.keyword.appid_short_notm}} 的新实例。如果您使用的是 Cloud Directory，那么这意味着您的用户必须迁移到新实例。您可以使用管理 API 来帮助进行迁移。
{: shortdesc}


您必须分配有对 {{site.data.keyword.appid_short_notm}} 的两个实例的`管理者` [IAM 角色](/docs/iam?topic=iam-getstarted#getstarted)。
{: note}


### 导出
{: cd-export}

您需要从当前实例中导出用户后，才能将这些用户添加到新实例。为此，您可以使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">导出管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

示例 cURL 命令：

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>变量 </th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>用于加密和解密用户散列密码的定制字符串。</td>
  </tr>
  <tr>
    <td><code>tenantID</code></td>
    <td>可以在服务凭证中找到的服务租户标识。您可以在 {{site.data.keyword.appid_short_notm}} 仪表板中找到服务凭证。</td>
  </tr>
</table>

仅会返回 Cloud Directory 用户及其概要文件。不会返回其他身份提供者的用户。
{: note}


### 导入
{: #cd-import}

既然您已准备好用户，现在可以将其信息导入到新实例中。为此，您可以使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">导入管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。


示例 cURL 命令：

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}



### 迁移脚本
{: cd-migration-script}

{{site.data.keyword.appid_short_notm}} 提供了可通过 CLI 使用的迁移脚本，可帮助加速迁移过程。

开始之前，请确保您具有以下参数信息：

<table>
  <tr>
    <th>参数</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>计划从中导出用户的 {{site.data.keyword.appid_short_notm}} 实例的租户标识。</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>计划将用户导入其中的 {{site.data.keyword.appid_short_notm}} 实例的租户标识。</td>
  </tr>
  <tr>
    <td>区域</td>
    <td>区域选项包括：<code>au-syd</code>、<code>eu-de</code>、<code>eu-gb</code>、<code>jp-tok</code> 和 <code>us-south</code>。</td>
  </tr>
  <tr>
    <td>IAM 令牌</td>
    <td>在获取 IAM 令牌之前，请确保您具有<code>管理者</code>许可权。有关获取 IAM 令牌的帮助，请查看<a href="https://cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。</td>
  </tr>
</table>

要运行脚本，请执行以下操作：

1. 克隆<a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">存储库 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
2. 打开终端，并导航至在其中克隆了存储库的文件夹。
3. 运行以下命令。

  ```
  npm install
  ```
  {: codeblock}

4. 使用您的参数运行以下命令：

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  示例命令：

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}
