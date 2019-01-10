---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# 多因子认证
{: #mfa}

多因子认证 (MFA) 是一种确认用户身份的方法，该方法要求用户使用其所知内容以外的某些内容来验证其身份是否与其声明的一致。例如，通过 {{site.data.keyword.appid_full}}，可以让用户输入在输入电子邮件和密码后发送到其电子邮件的一次性代码。
{: shortdesc}

MFA 仅可用于 Cloud Directory 用户。如果要使用采用 SAML 2.0 的企业登录或使用社交登录，那么可以在使用的身份提供者中启用 MFA。
{: note}

如果启用了 MFA，那么每次新用户尝试登录时，登录窗口小部件都要求进行 MFA。用户成功输入其凭证后，会将一次性密码发送到他们创建其帐户时注册的电子邮件地址。每个代码为 6 个字符，到期时间为 5 分钟。如果用户未收到其代码，那么他们可以请求发送其他代码，但不会重置到期时间。代码到期后，将强制用户重复整个登录过程。

如果用户电子邮件尚未通过管理 API 或通过注册时的电子邮件验证进行确认，那么在 MFA 代码验证成功时将确认该电子邮件。如果需要更改用户的电子邮件地址，管理员可以使用[管理 API](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser)。

MFA 可用于[累进层价格套餐](faq.html#pricing)上的 {{site.data.keyword.appid_short_notm}} 实例。
{: note}

## 了解流程
{: #understanding}



1. 向应用程序用户显示 {{site.data.keyword.appid_short_notm}} 的缺省登录 UI。

2. 用户输入自己的 Cloud Directory 用户凭证，例如其电子邮件或用户名及其密码。

3. 验证凭证并返回 MFA 表单。该表单要求用户粘贴通过电子邮件发送的代码。

4. 用户收到发送至其电子邮件地址的一次性密码，并将其输入到缺省的 MFA UI 中。

5. 系统会验证 MFA 代码，然后使用授权代码重定向到客户端应用程序，以继续执行 OAuth 2 流程。


</br>

## 配置 MFA
{: #configuration}

{{site.data.keyword.appid_short_notm}} 通过登录窗口小部件，支持 MFA 作为 Cloud Directory 用户的 OAuth 2.0 授权代码流程的一部分。
{: shortdesc}

要通过 GUI 配置 MFA，请查看 [Cloud Directory](cloud-directory.html)。
{: note}

### 使用 API 进行配置

您可以使用管理 API 来配置 MFA。
{: shortdesc}

**开始之前**

确保您已满足以下先决条件：

* {{site.data.keyword.appid_short_notm}} 实例的租户标识。这可以在仪表板的**服务凭证**部分中找到。
* Identity and Access Management (IAM) 令牌。有关获取 IAM 令牌的帮助，请查看 [IAM 文档](/docs/iam/apikey_iamtoken.html)。


1. 通过使用 MFA 配置向 `/config/mfa` 端点发出 PUT 请求以将 `isActive` 设置为 `true`，从而启用 MFA。

  头：
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  主体：
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  示例请求：
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. 通过使用 MFA 配置向 `/mfa/channels/{channelType}` 端点发出 PUT 请求来启用 MFA 通道。`isActive` 设置为 `true` 时，说明 MFA 通道已启用。

  头：
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channelType}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3>支持的通道类型</th>
    </thead>
    <tbody>
      <tr>
        <td>`email`</td>
      </tr>
    </tbody>
  </table>

  主体：
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  示例请求：
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/mfa/channels/{channelType}'
  ```
  {: screen}

</br>
