---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 保护 Liberty for Java 资源
{: #protecting-liberty}

可以使用 {{site.data.keyword.appid_short_notm}} 来保护 IBM Liberty for Java 应用程序中的端点。Liberty for Java 中内置了处理 OpenID Connect (OIDC) 请求的能力。

## 开始之前
{: #begin}

* 您需要一个未绑定的现有 [IBM Liberty for Java 应用程序](https://console.bluemix.net/catalog/starters/liberty-for-java)。要熟悉如何开发 Liberty for Java 应用程序，请参阅相关[文档](/docs/runtimes/liberty/index.html)。
* 确保已安装 [Apache Maven](https://maven.apache.org/download.cgi)。
* 了解 OIDC 如何与 Liberty for Java 一起运作。

## 保护 Liberty for Java 中的资源
{: #protecting-liberty}

1. 从 UI 下载 Liberty for Java 样本。该样本包含一个 zip 文件，其中含有标准 Liberty 文件。

2. 在解压缩样本的目录中打开终端。

3. 使用 Cloud Foundry 命令行，登录到 {{site.data.keyword.Bluemix_notm}}。根据提示，输入您的凭证。

  ```
  cf login
  ```
  {: codeblock}

4. 部署应用程序。运行以下命令会创建一个名称与租户标识相关的 Liberty for Java 实例。

  ```
  cf push
  ```
  {: codeblock}

5. 将您的服务实例绑定到新的 Liberty for Java 实例，然后重新部署应用程序。

6. 在浏览器中打开您的应用程序，然后使用您的凭证进行登录，以查看认证活动。


## 更新 Liberty for Java 样本
{: #updating-liberty}

要在样本应用程序中进行更新，请使用以下指示信息：

1. 创建 servlet、jsp 和 html。
2. 定义受保护资源，然后将它们添加到 `web.xml` 和 `server.xml` 授权过滤器中。
3. 创建一个 WAR 文件，然后将其部署到 Liberty for Java。

有关更新应用程序的更多信息，请参阅[向现有应用程序添加 {{site.data.keyword.appid_short_notm}}](/docs/services/appid/existing.html#existing-liberty)。
