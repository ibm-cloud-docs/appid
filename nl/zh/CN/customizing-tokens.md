---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-25"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# 定制令牌
{: #customizing-tokens}

您可以配置 {{site.data.keyword.appid_short_notm}} 令牌以满足应用程序的特定需求。
{: shortdesc}

**有哪些类型的令牌？**

{{site.data.keyword.appid_short_notm}} 通过不同类型的令牌来保护应用程序。

* 访问令牌：支持与通过授权过滤器保护的后端资源进行通信。如果访问令牌未与特定用户相关联，那么令牌的功能受到限制。
* 身份令牌：包含个人信息，用于认证用户。根据应用程序配置，可以在认证用户之前颁发身份令牌。这允许您在用户登录到应用程序之前，开始将属性与这些用户相关联。
* 刷新令牌：可用于延长用户在不重新认证的情况下保持登录的时间。

想了解有关令牌的更多信息？请阅读[了解令牌](authorization.html#tokens)中的更多信息。
{: tip}

</br>

**什么是定制选项？**

您可以通过设置有效期或向令牌添加定制声明来定制令牌。请查看下表以了解如何配置生命周期，或继续阅读以了解映射定制属性。

<table>
  <tr>
    <th>令牌类型</th>
    <th>值类型</th>
    <th>缺省值</th>
    <th>选项</th>
  </tr>
  <tr>
    <td>访问令牌</td>
    <td>分钟</td>
    <td>60</td>
    <td>5 到 1440 之间的任何值</td>
  </tr>
  <tr>
    <td>身份令牌</td>
    <td>分钟</td>
    <td>60</td>
    <td>5 到 1440 之间的任何值</td>
  </tr>
  <tr>
    <td>刷新令牌</td>
    <td>天</td>
    <td>30</td>
    <td>1 到 9 之间的任何值</td>
  </tr>
  <tr>
    <td>匿名令牌</td>
    <td>天</td>
    <td>30</td>
    <td>1 到 9 之间的任何值</td>
  </tr>
</table>

</br>

**为什么要将声明添加到令牌中？**

您可能会因为多种原因而希望跟踪额外属性。与应用程序开发者合作时，您可以映射角色和许可权。或者，在最终用户上构建概要文件时，您可以跟踪额外的信息来帮助创建个性化体验。

</br>

**有任何安全注意事项吗？**

有。由于令牌用于识别用户并保护资源，因此令牌的生命周期会影响多个不同方面。通过定制令牌配置，可以确保满足安全性和用户体验需求。但是，如果某个令牌遭到泄露，那么恶意用户会有更多时间来影响应用程序。

想了解有关应该考虑的安全注意事项的更多信息？请查看[定制属性](custom-attributes.html)。
{: tip}

</br>
</br>

## 了解定制属性和声明
{: #custom-claims}

您可以将用户概要文件属性映射到访问令牌和身份令牌声明。这意味着日后您不必再转至 [/userinfo 端点](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/userInfo)，也无需拉取定制属性，因为这些属性已存储在令牌中！
{: shortdesc}


**为什么要将属性添加到声明中？**

不必进行额外的网络调用，应用程序可能需要了解的有关用户或用户可执行操作的一切信息都已包含在令牌中！如果您没有海量数据，这将使您更加高效。此外，在网络中发送这些映射的属性时，可以确保这些属性的完整性，因为它们都存储在签名令牌中。

</br>

**可以定义哪些类型的声明？**

{{site.data.keyword.appid_short_notm}} 提供的声明分为多个类别，根据其定制级别进行区分。

*注册的声明*：访问令牌和身份令牌中有一些声明是由 {{site.data.keyword.appid_short_notm}} 定义的，无法被定制映射覆盖。如果声明受限，那么服务会将其忽略。声明包括 `iss`、`aud`、`sub`、`iat`、`exp`、`amr` 和 `tenant`。

*受限声明*：根据声明映射到的令牌，某些声明的定制能力受到限制。对于访问令牌，`scope` 是唯一的受限声明。此声明不能被定制映射覆盖，但可使用您自己的作用域进行扩展。scope 声明映射到访问令牌时，其值必须是字符串且不能以 `appid_` 为前缀，否则会将其忽略。在身份令牌中，无法修改或覆盖 `identities` 和 `oauth_clients` 声明。

*规范化声明*：每个身份令牌都包含一组声明，这些声明由 {{site.data.keyword.appid_short_notm}} 识别为规范化声明。这些声明可用时，会直接将其从身份提供者映射到令牌。这些声明不能显式省略，但可被定制声明映射覆盖。声明包括 `name`、`email`、`picture`、`local` 和 `gender`。

</br>

**如何定义声明？**

每个映射都由一个数据源对象和一个用于检索声明的键来定义。每个定制声明分别针对每个令牌进行设置，并按顺序应用。对于最大有效内容为 100 KB 的每个令牌，最多可以注册 100 个声明。

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="“构想”图标"/> 了解声明映射对象</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>必需</td>
        <td>定义声明的源。此项可以引用身份提供者的用户信息或用户的 {{site.data.keyword.appid_short_notm}} 定制属性。</br> </br> 选项包括：`saml`, `cloud_directory`、`facebook`、`google`、`appid_custom`、`ibmid` 和 `attributes`。</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>必需</td>
        <td>定义源数据的声明。</td>
      </tr>
    </tbody>
  </table>

可以使用点语法在映射中引用嵌套的声明。示例：`nested.attribute`
{:tip}

</br>

## 配置 {{site.data.keyword.appid_short_notm}} 令牌
{: #configuring-tokens}

您可以使用 GUI 或管理 API 来配置 {{site.data.keyword.appid_short_notm}} 令牌。
{: shortdesc}

### 使用 GUI 配置令牌生命周期
{: #configuring-tokens-ui}

1. 浏览到服务仪表板。
2. 在导航的**身份提供者**部分中，选择**管理**页面。
3. 在**设置**选项卡中，配置令牌。
  1. 要允许登录而无需用户交互，请将**刷新令牌**设置为**开启**。
  2. 设置刷新令牌生存期。到期时间以天为单位进行设置，可以是范围在 1 到 90 之间的任何值。该数字越小，用户必须重新登录的频率越高。
  3. 设置访问令牌生存期。到期时间以分钟为单位进行设置，可以是范围在 5 到 1440 之间的值。该值越小，防止令牌被盗的保护力度越大。
  4. 设置匿名令牌生存期。在用户开始与应用程序进行交互时，会为用户分配[匿名令牌](/docs/services/appid/progressive.html#anonymous)。用户登录后，匿名令牌中的信息随即会传输到与该用户关联的令牌。到期时间以天为单位进行设置，可以是 1 到 90 之间的任何值。

</br>

### 使用管理 API 配置令牌
{: #configuring-tokens-api}

**开始之前**

确保您已满足以下先决条件：

* {{site.data.keyword.appid_short_notm}} 实例的租户标识。这可以在 GUI 的**服务凭证**部分中找到。
* Identity and Access Management (IAM) 令牌。有关获取 IAM 令牌的帮助，请查看 [IAM 文档](/docs/iam/apikey_iamtoken.html)。

**映射声明**

1. 使用令牌配置对 `/config/tokens` 端点发出 PUT 请求。

  头：
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  主体：
  ```
   {
       "access": {
           "expires_in": 3600,
       },
       "refresh": {
           "expires_in": 2592000,
           "enabled": true
       },
       "anonymous": {
           "expires_in": 2592000,
           "enabled": true
       },
       "accessTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "name_id"
           }
       ],
       "idTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "attributes.uid"
           }
       ]
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="“构想”图标"/> 了解令牌配置</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>可选</td>
        <td>包含访问令牌和身份令牌到期时间 `expires_in`（以分钟为单位）的对象。</br> </br> 缺省到期时间为 60 分钟。</td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>可选</td>
          <td>包含刷新令牌到期时间 `expires_in`（以天为单位）的对象。</br> </br> 缺省到期时间为 30 天。</td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>可选</td>
          <td>包含匿名访问令牌和身份令牌到期时间 `expires_in`（以天为单位）的对象。</br> </br> 缺省到期时间为 30 天。
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>可选</td>
          <td>一个数组，包含在映射与访问令牌相关的声明时创建的对象。</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>可选</td>
          <td>一个数组，包含在映射与身份令牌相关的声明时创建的对象。</td>
      </tr>
    </tbody>
  </table>

  示例请求：
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
            }
          ],
          "idTokenClaims": [
            {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
  }' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
