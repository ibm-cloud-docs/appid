---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

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

通过 Cloud Directory，您可以使用用于增强安全性的预构建功能以及自助服务来管理可缩放注册表中的用户。
{: shortdesc}

Cloud Directory 用户与 {{site.data.keyword.appid_short_notm}} 用户不同。用户可以使用您配置的不同身份提供者选项来注册应用程序，或者您可以将用户添加到目录。本主题中提到的用户是指与作为身份提供者的 Cloud Directory 关联的用户。
{: note}

## 查看用户信息
{: #cd-user-info}

可以使用 API 或使用仪表板，将有关所有 Cloud Directory 用户的所有已知信息作为一个 JSON 对象进行查看。
{: shortdesc}


### 使用 GUI

可以使用 {{site.data.keyword.appid_short_notm}} 仪表板来查看有关应用程序用户的详细信息。 

1. 导航至 {{site.data.keyword.appid_short_notm}} 实例的 **Cloud Directory > 用户**选项卡。

2. 浏览表或使用电子邮件地址进行搜索，以查找要查看其信息的用户。

3. 在用户所在行的溢出菜单中，单击**查看用户详细信息**。这将打开一个页面，其中包含该用户的信息。请查看下表以了解可以查看的信息。

<table>
  <tr>
    <th colspan="2">用户详细信息</th>
  </tr>
  <tr>
    <td>用户标识</td>
    <td>用户标识取决于配置的用户注册类型。如果已配置电子邮件和密码流程，那么标识为用户的电子邮件。如果使用的是用户名和密码流程，那么标识为在注册时提供的用户名。</td>
  </tr>
  <tr>
    <td>电子邮件</td>
    <td>连接到用户的主要电子邮件地址。</td>
  </tr>
    <tr>
    <td>姓氏和名字</td>
    <td>用户在注册过程中提供的姓氏和名字。</td>
  </tr>
  <tr>
    <td>上次登录时间</td>
    <td>用户上次登录到应用程序的时间戳记。注：如果是通过仪表板添加的用户，那么登录时间为空，直到用户自己登录到应用程序。执行登录后，用户会同时成为 App ID 用户。</td>
  </tr>
  <tr>
    <td>标识</td>
    <td>{{site.data.keyword.appid_short_notm}} 分配给用户的标识。在 UI 中，不会显示该值，但可以将其复制并粘贴到文本编辑器中以查看该值。</td>
  </tr>
  <tr>
    <td>预定义属性</td>
    <td>预定义属性是基于 SCIM 的有关用户的已知信息。</td>
  </tr>
  <tr>
    <td>定制属性</td>
    <td>定制属性是添加到用户概要文件的其他信息，或者在用户与应用程序交互时了解到的用户相关信息。</td>
  </tr>
  <tr>
    <td>摘要</td>
    <td>所有属性汇集起来构成一个概要文件，以提供 Cloud Directory 用户的完整概述。有关更多信息，请参阅[用户概要文件](/docs/services/appid?topic=appid-profiles)。</td>
  </tr>
</table>

</br>

### 使用 API

可以使用 {{site.data.keyword.appid_short_notm}} API 来查看有关应用程序用户的详细信息。 

1. 从服务实例获取租户标识。

2. 使用标识性查询（例如，电子邮件地址）来搜索 App ID 用户，以查找用户标识。

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users?query={identifying-search-query}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

      示例：

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@email.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. 通过使用在上一步中获取的标识，对 `cloud_directory/users` 端点发出 GET 请求以查看其完整用户概要文件。

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-ID}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  示例响应：

  ```
  {
    sub: "c155c0ff-337a-46d3-a22a-a8f2cca08995",
    name: "Test User",
    email: "testuser@test.com",
    identities: [
      {
        provider: "cloud_directory",
        id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
        idpUserInfo: {
          displayName: "Test User",
          active: true,
          mfaContext: {},
          emails: [
            {
              value: "testuser@test.com",
              primary: true
            }
          ],
          meta: {
            lastLogin: "2019-05-20T16:33:20.699Z",
            created: "2019-05-20T16:25:13.019Z",
            location: "/v1/6b8ab644-1d4a-4b3e-bcd9-777ba8430a51/Users/f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            lastModified: "2019-05-20T16:33:20.707Z",
            resourceType: "User"
          },
          scemas: [
            "urn:ietf:params:scim:schemas:core:2.0:User"
          ],
          name: {
            givenName: "Test",
            familyName: "User",
            formatted: "Test User"
            },
          id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
          status: "CONFIRMED",
          idpType: "cloud_directory"
        }
      }
    ]
  }
  ```
  {: screen}

  要查看 {{site.data.keyword.appid_short_notm}} 支持的完整用户数据集，请查看 [SCIM 核心模式](https://tools.ietf.org/html/rfc7643#section-8.2)。{: tip}


## 添加和删除用户
{: #add-delete-users}

可以通过 {{site.data.keyword.appid_short_notm}} 仪表板或使用 API 来管理 Cloud Directory 用户。
{: shortdesc}

用户向应用程序注册时，可通过自动触发欢迎或验证请求等电子邮件的自助服务工作流程来进行注册。您以管理员身份向应用程序添加用户时，不会启动自助服务工作流程，这意味着用户不会从应用程序收到任何电子邮件。如果您希望用户仍能在被添加时收到相关通知，那么可以通过 [App ID 管理 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher) 来触发消息传递流程。


### 添加用户
{: #add-users}

用户向应用程序注册时，会将其添加为用户。出于测试目的，您可以通过 {{site.data.keyword.appid_short_notm}} 仪表板或使用 API 来添加用户。

如果禁用自助服务注册或代表用户来添加该用户，那么用户在被添加时不会收到欢迎或验证电子邮件。
{: tip}



**要使用 GUI 添加新用户，请执行以下操作：**

1. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的 **Cloud Directory > 用户**选项卡。

2. 单击**添加用户**。这将显示一个表单。

3. 输入**名字**、**姓氏**、**电子邮件**和**密码**。请确保您尝试注册的电子邮件尚未被其他用户使用。要确保正确输入了密码，请通过在**重新输入密码**字段中输入密码来进行确认。

4. 单击**保存**。这将创建 Cloud Directory 用户。

</br>


**要使用 API 添加新用户，请执行以下操作：**

以下流程说明如何使用电子邮件和密码添加用户。您还可以选择使用用户名和密码流程。

1. 从应用程序或服务凭证中获取 `tenantID`。

2. 获取 {{site.data.keyword.cloud_notm}} IAM 令牌。

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. 使用步骤 2 中获取的令牌，向 `cloud-directory/users` 端点发出 POST 请求。请注意，此示例使用的是电子邮件/密码流程。您还可以使用用户名/密码流程。

  ```
  curl --X POST "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users"
  -H "accept: application/json"
  -H "content-type: application/json"
  -H "authorization: Bearer {token}"
  -d {
    "displayName": "Test User",
    "password": "{App-ID-Cloud-Directory-User-Password}",
    "active": true,
    "emails": [
      {
        "value": "{App-ID-Cloud-Directory-User-Email}",
        "primary": true
      }
    ]
  }
  ```
  {: codeblock}

</br>


### 删除用户
{: #delete-users}

如果要从目录中除去用户，可以通过 GUI 或使用 API 删除该用户。
{: shortdesc}

**要通过 GUI 删除用户，请执行以下操作：**

1. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的 **Cloud Directory > 用户**选项卡。

2. 单击要删除的用户旁边的复选框。这将显示一个框。

3. 在该框中，单击**删除**。这将显示一个屏幕。

4. 确认您了解通过单击**删除**来删除用户是无法撤销的操作。如果这是误操作，您可以将用户重新添加到目录，但有关该用户的任何信息都不再可用。

</br>

**要使用 API 删除用户，请执行以下操作：**

1. 获取租户标识。

2. 使用连接到用户的电子邮件来搜索目录，以查找用户标识。

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users?email={user-email}" -H "accept: application/json"
  ```
  {: codeblock}

3. 删除用户。

  ```
  curl --X DELETE "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-GUID}"
  -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}



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
    <td>在获取 IAM 令牌之前，请确保您具有<code>管理者</code>许可权。有关获取 IAM 令牌的帮助，请查看<a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。</td>
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
