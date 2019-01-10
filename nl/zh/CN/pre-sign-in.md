---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}
{:codeblock: .codeblock}

# 在用户登录之前添加属性
{: #sign-in}

通过 {{site.data.keyword.appid_full}}，对于已知需要访问应用程序的用户，您可以在这些用户初始登录之前，开始为其构建概要文件。
{: shortdesc}

要了解有关属性类型的更多信息，请查看[了解用户概要文件](user-profile.html)。要了解有关定制属性及其安全注意事项的更多信息，请查看[定制属性](custom-attributes.html)。
{: tip}

**为什么需要在用户首次登录之前，先将用户的信息添加到应用程序？**

假设使用 {{site.data.keyword.appid_short_notm}} 的应用程序要联合来自 SAML 身份提供者的现有用户。您可能希望某些用户在首次登录到应用程序时立即具有 `admin` 访问权。为了实现这一点，您可以使用预注册端点为这些用户设置定制 `admin` 属性，并向其授予对管理控制台的访问权，而无需您执行任何进一步操作。请确保考虑更改缺省设置可能引发的[安全问题](custom-attributes.html)。

**如何标识用户？**

可以使用以下其中一项来标识用户：

* 身份提供者中用户的唯一标识（称为 **GUID**）。虽然此标识始终存在且保证是唯一的，但不一定现成可用或易于理解。例如，Cloud Directory 使用 16 字节随机 GUID。
* 用户的**电子邮件**（如果可用）。

**如何确定哪个身份提供者提供了哪些信息？**

查看下表以了解可以使用的身份信息的类型。

<table>
  <thead>
    <tr>
      <th>身份提供者</th>
      <th>GUID</th>
      <th>电子邮件</th>
      <th>Sub</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cloud Directory</td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td></td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>定制</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="可用功能" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

**Cloud Directory 的处理方式是否不同？**

为了确保预注册用户属性的完整性，Cloud Directory 会对其用户设置其他需求。仅当启用并验证了电子邮件验证时，才能执行预注册。如果使用特定属性预注册 Cloud Directory 用户，那么这些属性适用于特定人员。如果未先验证电子邮件，那么其他用户有可能声明该电子邮件地址以及为其分配的任何属性。

该如何操作？

1. 将 Cloud Directory 设置为电子邮件和密码方式。您可以通过 UI 在 **Cloud Directory** 选项卡上的“常规设置”中执行此操作。还可以通过[管理 API](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/createCloudDirectoryUser) 设置此方式。

2. 通过以下其中一种方式验证用户的电子邮件地址以确认其身份：

  * 要通过电子邮件验证用户身份，请在服务仪表板的 **Cloud Directory** 选项卡中将**电子邮件验证**设置为**开启**。如果您添加了用户，但该用户在未先验证其电子邮件的情况下就登录到应用程序，那么登录会成功完成，但会删除其预定义的属性。
  * 要手动验证用户，您必须是管理员，并使用 Cloud Directory [管理 API](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/createCloudDirectoryUser)。创建或更新用户时，应该在用户数据有效内容中显式将 `status` 字段设置为 `CONFIRMED`。

**使用定制身份提供者时，需要执行任何特殊操作吗？**

预先将用户信息添加到应用程序时，可以使用认证流程提供的任何唯一标识。该标识必须与在授权请求期间发送的已签名 JSON Web 令牌的 `sub` _完全_匹配。如果标识不匹配，那么要添加的概要文件不会成功链接。



## 向应用程序添加用户信息
{: #add}

既然您已经了解了流程并考虑了安全影响，请尝试添加用户。

**开始之前：**

要使用 [/users](https://appid-management.ng.bluemix.net/swagger-ui/#!/Users/users_search_user_profile) 管理 API 端点为特定用户添加定制属性，您必须知道以下信息：

* 用户将用于登录的身份提供者。
* 身份提供者提供的用户唯一标识。

用户首次登录应用程序时，{{site.data.keyword.appid_short_notm}} 会搜索该用户。如果找到该用户，那么该用户会继承所分配的身份。如果找不到该用户，那么将根据身份提供者所提供的信息来创建新用户。

**要添加用户，请执行以下操作：**

1. 登录到 IBM Cloud。
  ```
  ibmcloud login
  ```
  {: pre}

2. 通过运行以下命令来查找 IAM 令牌。
  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. 对 `/users` 端点发出 POST 请求，该请求包含用户的描述以及要设置为 JSON 对象的属性。

  头：
  ```
  POST {management-url}/management/v4/{tenantId}/users
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  主体：
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes": {
             "mealPreference":"vegeterian"
           }
       }
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解组成部分</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>idp</em></code></td>
        <td>用户将向其进行认证的身份提供者。选项包含：`saml`、`cloud_directory`、`facebook`、`google`、`appid_custom` 和 `ibmid`。</td>
      </tr>
      <tr>
        <td><code><em>idp-identity</em></code></td>
        <td>身份提供者提供的唯一标识。</td>
      </tr>
      <tr>
        <td><code><em>profile</em></code></td>
        <td>包含定制属性 JSON 映射的用户概要文件。</td>
      </tr>
    </tbody>
  </table>

  示例请求：
  ```
  $ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
  ```
  {: screen}

3. 通过以下其中一种方式验证注册是否成功：
  * 在响应中检查用户标识。
    ```
    {
        "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
    }
    ```
    {: screen}
  * 检查用户概要文件是否已创建。

请记住，用户的预定义属性在其第一次认证之前为空，但用户是完全认证的用户，适合用于所有意向和用途。您可以使用用户的唯一标识，就像您使用已登录的用户那样。例如，您可以修改、搜索或删除概要文件。

既然您已将用户与特定属性相关联，请尝试[访问属性](/docs/services/appid/custom-attributes.html)！


</br>
