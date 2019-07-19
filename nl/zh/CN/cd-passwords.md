---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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

# 定义密码策略
{: #cd-strength}

您可以为要用于 Cloud Directory 的密码设置需求。
通过定义用户必须遵循的特定需求，可以确保更安全的应用程序。
{: shortdesc}

## 策略：密码强度
{: #cd-password-strength}

如果密码强度高，就难以甚至不可能通过手动或自动方式来猜到密码。要设置用户密码强度需求，可以使用以下步骤。
{: shortdesc}

1. 转至 {{site.data.keyword.appid_short_notm}} 仪表板的**密码策略**选项卡。

2. 在**定义密码强度**框中，单击**编辑**。这将打开一个屏幕。

3. 在**密码强度**框中输入有效的正则表达式字符串。

  示例：
    - 必须至少为 8 个字符。(`^.{8,}$`)
    - 必须包含一个数字、一个小写字母和一个大写字母。(`^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`)
    - 必须仅包含英语字母和数字。(`^[A-Za-z0-9]*$`)
    - 必须至少包含一个唯一字符。(`^(\w)\w*?(?!\1)\w+$`)

4. 单击**保存**。

可以在 {{site.data.keyword.appid_short_notm}} 控制台的“Cloud Directory 设置”页面中或者使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来设置密码强度。
{: note}


## 高级密码策略
{: #cd-advanced-password}


您可以通过强制实施密码约束来增强应用程序的安全性。
{: shortdesc}


可以创建包含以下五个功能的任意组合的高级密码策略：

 - 重复提供错误的凭证后锁定
 - 避免密码复用
 - 密码到期时间
 - 密码更改最短间隔时间
 - 确保密码不包含用户名


 启用此功能时，将激活对高级安全功能的额外计费。有关更多信息，请参阅 [{{site.data.keyword.appid_short_notm}} 如何计算定价](/docs/services/appid?topic=appid-faq#faq-pricing)。
 {: important}


### 策略：避免密码复用
{: #cd-avoid-reuse}

用户更改其密码时，您可能希望阻止他们选择最近使用过的密码。
{: shortdesc}

通过使用 GUI 或 API，可以选择用户必须使用了多少个新密码之后才能重复使用先前用过的密码。设置选项包括范围在 1 到 10 之间的任何整数值。

如果开启此选项，那么用户无法使用自己最近使用过的密码。如果用户尝试将其密码设置为自己最近使用过的密码，那么会在缺省登录窗口小部件 GUI 中显示错误，并提示该用户输入其他选项。

先前的密码会以用户当前密码的存储方式安全地存储。
{: note}


### 策略：重复提供错误的凭证后锁定
{: #cd-lockout}

您可能希望在检测到可疑行为（例如，多次连续尝试使用不正确的密码登录）时暂时阻止登录能力，从而保护用户的帐户。此度量可以帮助阻止恶意方通过猜测用户密码来获得对用户帐户的访问权。
{: shortdesc}

通过使用 GUI 或 API，可以设置用户在最多尝试登录失败多少次后，其帐户会暂时锁定。您还可以定义帐户锁定的时间长度。可以选择以下选项：

* 尝试次数：1 到 10 之间的任何整数值。
* 锁定期：在 1 分钟到 1440 分钟（24 小时）范围内指定的任何整数值（以分钟为单位）。

如果帐户已锁定，那么用户无法登录，也无法完成其他任何自助服务操作（例如，更改其密码），直到指定的锁定期过后才行。锁定期结束后，将对用户自动解锁。

您可以在锁定期结束之前对用户解锁。要确定用户是否被锁定，请查看 `active` 字段是否设置为 `false`。还可以检查服务仪表板的**用户**选项卡上用户的状态是否设置为`已禁用`。要对用户解锁，您必须使用 [API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) 将 `active` 字段设置为 `true`。


### 策略：密码更改最短间隔时间
{: #cd-minimum-time}

您可能希望通过设置用户在前后两次更改密码之间必须等待的最短时间，以阻止用户快速切换密码。
{: shortdesc}

此功能与“避免密码复用”策略一起使用时特别有用。如果没有此限制，用户就可以直接快速连续地多次更改其密码，从而绕过对复用最近用过的密码的限制。可以选择范围在 1 到 720 小时（30 天）内的任何值。此字段以小时为单位进行指定。


### 策略：密码到期时间
{: #cd-expiration}

出于安全原因，您可能希望强制实施密码轮换策略，以便用户在指定的时间量后必须更改其密码。
{: shortdesc}

通过使用 GUI 或 API，可以设置用户密码保持有效的时间段。用户密码到期后，将强制用户在下一次登录时重置其密码。可以选择范围在 1 到 90 天内的任意整数。

可以使用提供的缺省 GUI 快速开始使用登录窗口小部件。系统会指示用户提供新密码，然后才能完成登录。

如果使用的是定制登录体验，那么用户尝试使用到期的密码登录时会触发错误。配置应用程序以提供必要的用户体验是您的责任。您可以调用更改密码 API 来设置新密码。

令牌端点响应类似于以下内容：

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

此选项第一次设置为“开启”时，任何现有用户密码都没有到期日期。到期时间段从用户更改其密码之日开始计算。您可能希望通过将此功能设置为“开启”，鼓励用户更新其密码。
{: note}


### 策略：确保密码不包含用户名
{: #cd-no-username}

为了获得更高强度的密码，您可能希望阻止用户在密码中包含其用户名或其电子邮件地址的第一部分。
{: shortdesc}

此约束不区分大小写。用户无法通过变更其中部分或全部字符的大小写来使用个人信息。要配置此选项，请将开关切换为**开启**。
{: note}

