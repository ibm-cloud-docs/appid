---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-08"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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


# 教程：设置用户角色
{: #tutorial-roles}

在对应用程序进行编码时，很难确保适当的人员在适当的时候具有适当的访问权。为了帮助处理该过程，可以使用 {{site.data.keyword.appid_full}} 来定义定制属性，例如 `role`，此属性允许您分配不同类型的用户。然后，可以使用应用程序对每种类型的用户强制执行不同级别的许可权。通过使用本分步指南，您可以了解如何设置用户属性，更新用户属性，然后使用 {{site.data.keyword.appid_short_notm}} API 将其注入到令牌中。
{: shortdesc}

不熟悉这些 API 吗？请使用 [Postman 集合](https://github.com/ibm-cloud-security/appid-postman)来试用 API。
{: tip}

## 场景 
{: #roles-scenario}

假设您是一个虚构的主题公园的开发者。您的任务是管理 [Web 应用程序](/docs/services/appid?topic=appid-web-apps)的访问权，并且您认为这样做的最简单方法是针对每种类型的用户设置角色。您有多种不同类型的角色，例如公园员工和游客，所有角色都需要不同级别的许可权。您希望能够简化流程，并确保用户在首次登录到应用程序时就分配有正确的角色。  
{: shortdesc}

没问题！您可以使用 {{site.data.keyword.appid_short_notm}} 的[定制属性功能](/docs/services/appid?topic=appid-custom-attributes)来存储任何类型的用户相关信息。由于您使用的是基于角色的访问控制，因此可以创建名为 `role` 的属性，并分配不同的值来指定角色类型。例如，主题公园可能有 `visitor` 或 `staff`，可作为 `role` 属性的不同值。然后，可以确保应用程序代码强制实施您分配的访问策略和特权。

虽然本教程是专门针对 Web 应用程序和 Cloud Directory 编写的，但属性的适用范围要大得多。定制属性可以是您希望使用的任何内容。只要属性数不超过 100,000 个，且格式设置为纯 JSON 对象，就可以存储所有类型的信息！
{: note}


## 开始之前
{: #roles-before}

准备好了吗？让我们开始吧！

开始之前，确保您已满足以下先决条件：
- {{site.data.keyword.appid_short_notm}} 服务的实例
- 一组服务凭证
- 可以访问和验证的电子邮件地址


## 步骤 1：配置 {{site.data.keyword.appid_short_notm}} 实例
{: #roles-configure-app}

您需要先配置 {{site.data.keyword.appid_short_notm}} 的实例，然后才能开始为 Cloud Land 用户添加属性。
{: shortdesc}

1. 在服务仪表板的**身份提供者**选项卡中，启用 **Cloud Directory**。虽然本教程使用的是 [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)，但您还可以选择使用其他任何 IdP，例如 [SAML](/docs/services/appid?topic=appid-enterprise)、[Facebook](/docs/services/appid?topic=appid-social#facebook)、[Google](/docs/services/appid?topic=appid-social#google) 或[定制提供者](/docs/services/appid?topic=appid-custom-identity)。

2. 在 **Cloud Directory > 电子邮件验证**选项卡中，启用验证并将**允许用户在未先验证其电子邮件地址的情况下登录到应用程序**设置为**否**。使用定制属性设置与许可权相关的角色时，请确保用户必须验证其身份后，才可采用您设置的属性。

3. 在**概要文件**选项卡中，将**更改应用程序中的定制属性**设置为**已禁用**。

  缺省情况下，任何具有访问令牌的用户都可以更改定制属性。要确保应用程序安全性，必须配置 {{site.data.keyword.appid_short_notm}}，以便只能由应用程序的管理员或所有者来更改定制属性。这样可防止用户更改自己的定制属性，并防止用户向自己授予不应该拥有的许可权。
  {: important}

太棒了！您的仪表板已配置完毕，您已准备就绪，可以开始设置角色。


## 步骤 2：在其他用户登录前代表该用户设置角色
{: #roles-set-before}

Cloud Land 有新进工作人员！您了解了他们的所有信息，但他们要过几天才能开始使用系统。您可以通过创建 {{site.data.keyword.appid_short_notm}} 用户以及包含属性（如 `staff` 角色）的概要文件来[预注册员工](/docs/services/appid?topic=appid-preregister)。
{: shortdesc}

此过程不会完成 Cloud Directory 注册。用户仍必须注册应用程序，才能继承您创建的概要文件中的属性。
{: tip}

1. 使用 CLI 登录到 {{site.data.keyword.cloud_notm}}。

  ```
  ibmcloud login
  ```
  {: pre}

2. 获取 IAM 访问令牌。

  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. 发出 POST 请求，以针对新用户创建包含 `staff` 属性的用户概要文件。请确保您可以访问并验证所使用的电子邮件。

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": “user@email.com“,
    "profile": {
      "attributes": {
             “role”: “staff”
      }
    }
  }'
  ```
  {: pre}

  成功响应输出：

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. 验证是否使用 `staff` 角色创建了概要文件。

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

  成功响应主体：

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

太棒了！您已向应用程序预注册了用户。现在，用户使用您用于预注册的标识登录到应用程序时，会创建 Cloud Directory 用户，并且该用户会继承 {{site.data.keyword.appid_short_notm}} 用户概要文件。接下来，学习如何更新属性。


## 步骤 3：更新用户属性
{: #roles-update-attributes}

Cloud Land 在不断增长！为了跟上增长情况，您的公司将雇佣新员工。步骤 2 中的 `staff` 用户现在已是经理。您可以通过[分配新角色](/docs/services/appid?topic=appid-custom-attributes)来更新其概要文件。
{: shortdesc}

1. 更新概要文件。

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
             “role”: “manager”
      }
    }
  }'
  ```
  {: pre}

3. 查看概要文件以验证它是否已正确更新。

  ```
  curl --request POST \
  GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

  成功响应输出：

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

非常好！


## 步骤 4：将属性注入到令牌中
{: #roles-map-claims}

主题公园越来越受欢迎，因而不断增长！面对如此多的新游客和员工，您希望限制发出的请求数。为了提高性能，您可以将用户概要文件属性映射到访问权和身份令牌声明。通过映射定制声明，可以在令牌本身中存储定制属性。
{: shortdesc}

[令牌配置](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)是全局的，这意味着此配置会应用于每个具有 `role` 属性的用户，而不考虑向其分配的实际角色。
{: tip}


1. 对令牌配置端点发出请求。

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
           "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: pre}

  <table>
    <tr>
      <th>变量 </th>
      <th>描述</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td> <td>租户标识用于在请求中识别 {{site.data.keyword.appid_short_notm}} 的实例。您可以在仪表板的<em>服务凭证</em>选项卡中找到您的标识。如果没有凭证集，那么可以遵循 GUI 中的步骤来创建凭证。</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>对于 <code>accessTokenClaim</code> 和 <code>idTokenClaims</code>，将 source 设置为 <code>attribute</code>。</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>对于 <code>accessTokenClaim</code> 和 <code>idTokenClaims</code>，将 sourceClaim 设置为 <code>role</code>。</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>此值将应用于每种令牌类型，并且必须在每个请求中进行设置。如果先前在 GUI 中设置了此值，然后运行此请求，那么请求中的值将覆盖先前设置的值。请确保将到期时间设置为适合您配置的正确值。</td>
    </tr>
  </table>

  成功响应输出：

  ```
  {
      "access": {
           "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## 步骤 5：查看访问令牌
{: #roles-view-token}

（可选）可以通过查看访问令牌来验证步骤 4 是否成功。
{: shortdesc}

1. 出于测试目的，请使用 {{site.data.keyword.appid_short_notm}} GUI 来创建 Cloud Directory 用户。

  1. 在**用户**选项卡中，单击**添加用户**。这将显示一个表单。
  2. 输入名字和姓氏、电子邮件和密码。
  3. 单击**保存**。

2. 对您的客户端标识和私钥进行编码。

  1. 在 {{site.data.keyword.appid_short_notm}} GUI 的**服务凭证**选项卡中，复制您的客户端标识和私钥。
  2. 使用 Base64 编码器对这些授权信息进行编码。
  3. 复制输出以用于以下命令。

4. 使用 API 登录以获取访问令牌信息。返回的令牌已编码。

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: pre}

5. 对访问令牌进行解码。
  1. 复制先前命令的响应输出中的令牌。
  2. 在浏览器中，导航至 https://jwt.io/。
  3. 将令牌粘贴到标注为**已编码**的框中。

6. 在**已解码**部分中，验证是否可以看到该角色。

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "role": "manager"
  }
  ```
  {: screen}



## 后续步骤
{: #roles-next}

非常棒！您已完成本教程。接下来，可以尝试配置[多因子认证](/docs/services/appid?topic=appid-cd-mfa)或设置[您自己的品牌 GUI](/docs/services/appid?topic=appid-branded)。
