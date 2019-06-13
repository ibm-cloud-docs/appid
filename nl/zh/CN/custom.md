---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-13"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, private key, public key, jwt

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

# 定制
{: #custom-identity}

您可以在进行认证时使用自己的定制身份提供者。您的身份提供者可遵循 {{site.data.keyword.appid_full}} 没有明确支持的任何认证机制，包括专有认证机制。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 未提供对特定身份提供者的直接支持时，您可以使用定制身份流程将认证协议桥接到 {{site.data.keyword.appid_short_notm}} 的现有认证流程。例如，您希望使用 GitHub 或 LinkedIn 来允许用户登录。可以使用身份提供者的现有 SDK 来方便地提供用户认证信息，然后打包这些信息，并将其与 {{site.data.keyword.appid_short_notm}} 进行交换。在许多企业场景中，原有身份提供者可能使用其自己的定制认证协议，但您仍然希望利用 {{site.data.keyword.appid_short_notm}} 的功能。对于此类型的场景，定制身份流程提供了分离的方法，以在不公开用户凭证的情况下安全地认证用户。

## 配置定制身份
{: #custom-configure}

您可以使用以下步骤将定制身份提供者配置为使用 {{site.data.keyword.appid_short_notm}}。
{: shortdesc}

### 开始之前
{: #custom-identity-before}

要在 {{site.data.keyword.appid_short_notm}} 和定制身份提供者之间建立信任，您必须具有最小长度为 2048 的 RSA PEM 密钥对。确保安全备份用于生产的任何密钥。

如何使用这些密钥？

- 专用密钥在应用程序或身份提供者中用于对 JWT 签名。
- {{site.data.keyword.appid_short_notm}} 使用公用密钥来验证包含用户信息的 JWT。

要使用 Open SSL 来生成 RSA PEM 密钥对，请运行以下命令：

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}

</br>

### 使用 GUI 进行配置
{: #custom-identity-configure-gui}

1. 登录到您的 {{site.data.keyword.cloud_notm}} 帐户，并导航至 {{site.data.keyword.appid_short_notm}} 实例。

2. 在**管理**选项卡中，将**定制身份提供者**设置为**开启**。

3. 向 {{site.data.keyword.appid_short_notm}} 注册公用密钥。
  1. 导航至**定制身份提供者**选项卡。
  2. 在**公用密钥**框中粘贴公用密钥，然后单击**保存**。



### 使用 API 进行配置
{: #custom-identity-configure-api}

通过向[管理 API 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_custom_idp)发出 PUT 请求来注册密钥。

```
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## 测试您的配置
{: #custom-identity-testing}

使用有效的公用密钥配置 {{site.data.keyword.appid_short_notm}} 实例后，可以使用服务所提供的测试应用程序来验证是否正确设置了配置。在示例应用程序中，可以查看在执行标准登录流程期间返回的 {{site.data.keyword.appid_short_notm}} 访问令牌和身份令牌有效内容。

1. 在**定制身份提供者**选项卡中，单击**测试**以打开测试应用程序。

2. 创建遵循定制身份[协议](/docs/services/appid?topic=appid-custom-auth#generating-jwts)的[示例 JWT](https://jwt.io/)。

3. 将 JWT 粘贴到标注为 **JSON Web 令牌**的框中，然后单击**测试**以执行样本认证。

如果成功，现在可以在标准登录流程中看到可用于应用程序的已解码 {{site.data.keyword.appid_short_notm}} 身份令牌和访问令牌。

## 后续步骤
{: #custom-identity-next}

既然已配置了定制身份提供者，请[将其添加到应用程序](/docs/services/appid?topic=appid-custom-auth#custom-auth)！
