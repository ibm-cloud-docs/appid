---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# 为应用程序添加品牌形象
{: #branding}

您可以显示自己的定制屏幕，使用自己的登录流程，并利用 {{site.data.keyword.appid_full}} 的认证和授权功能。通过将 Cloud Directory 用作身份提供者，用户不需要多少帮助就可以与应用程序进行交互。用户无需寻求帮助就可以完成登录、注册、更改密码等操作。
{: shortdesc}

**为什么要显示我自己的屏幕？**

复用现有 UI 时，您可为应用程序创建紧密结合的登录流程。通过使用相同的图像、颜色和品牌形象，用户更有可能识别到您的品牌，甚至在未直接与您的应用程序交互的情况下也是如此。

</br>

**显示我自己的屏幕需要哪种配置？**

要显示您自己的 UI，您必须将 [Cloud Directory(/docs/services/appid/cloud-directory.html)] 用作身份提供者。可通过多种不同的方式来[配置](cloud-directory.html) Cloud Directory。您可以决定要发送的消息类型，并定制相关内容和设计。不知道该怎么说？没问题。GUI 中有一些示例消息可供您使用。

要使用除英语之外的其他[语言](cloud-directory.html#languages)？您可以使用<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">语言管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来选择其他语言，以显示您自己的已翻译内容。
{: tip}

</br>



**这些流程在技术上有何不同？**

服务使用 OAuth2 授权流程来映射授权流程。配置社交身份提供者（例如 Facebook）时，<a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html" target="_blank">授权流程 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 用于调用登录窗口小部件。您使用自己的屏幕时，<a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html" target="_blank">资源所有者密码凭证流程 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 会用于提供访问令牌和身份令牌，以允许您调用登录屏幕。

</br>

**有任何示例应用程序可说明其工作方式吗？**

有！请查看以下任一示例以了解 Cloud Directory 的工作方式：

* <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="_blank">Use your own branded UI for user sign-in with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/use-ui-flows-user-sign-sign-app-id/" target="_blank">Use your own UI and Flows for User Sign-Up and Sign-in with with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/custom-login-page-app-id-integration/" target="_blank">Use a custom login page with  {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>

</br>
</br>

## 使用 Android SDK 来为应用程序添加品牌形象
{: #branded-ui-android}

在启用 Cloud Directory 的情况下，可以使用 Android SDK 来调用定制屏幕。您可以选择希望用户能够与其进行交互的屏幕组合。<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">查看此博客 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 以获取详细示例！
{: shortdesc}

</br>

**登录**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。
2. 将以下代码添加到应用程序中。用户单击定制屏幕上的登录时，将触发登录流程。通过提供最终用户的用户名和密码，可获取访问令牌、身份令牌和刷新令牌。

  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //User authenticated
        }
      });
  ```
  {: pre}

</br>
</br>

## 使用 iOS Swift SDK 来为应用程序添加品牌形象
{: #branded-ui-ios-swift}

在启用 Cloud Directory 的情况下，可以使用 [iOS Swift SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift) 来调用您自己的品牌屏幕。
{: shortdesc}

</br>

**登录**

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。
2. 将以下代码放入应用程序中。用户尝试登录时，会调用登录屏幕，并且授权和认证流程将从定制登录页面开始。

  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
        }

        }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}

</br>
</br>

## 使用 Node.js SDK 为应用程序添加品牌形象
{: #branded-ui-nodejs}

在启用 Cloud Directory 的情况下，可以使用 Node.js SDK 来调用定制屏幕。
{: shortdesc}

**登录**

通过使用 WebAppStrategy，用户可以使用其用户名和密码登录 Web 应用程序。用户成功登录到应用程序后，只要其访问令牌保持有效，就会在 HTTP 会话中持久存储其访问令牌。在 HTTP 会话关闭或到期后，访问令牌也将销毁。


1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。
2. 将以下代码放入应用程序中。用户尝试登录时，会调用登录屏幕，并且授权和认证流程将从定制登录页面开始。

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 命令参数</th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>要在成功认证后将用户重定向到的 URL。</td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>要在认证失败时将用户重定向到的 URL。</td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td>设置为 <code>true</code> 时，将从 Cloud Directory 服务返回一条错误消息。缺省情况下，此值设置为 <code>false</code>。</td>
      </tr>
    </tbody>
  </table>

**注**：如果以 HTML 形式提交请求，那么可以使用<a href="https://www.npmjs.com/package/body-parser" target="blank">主体解析器 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 中间件。要查看返回的错误消息，可以使用 <a href="https://www.npmjs.com/package/connect-flash" target="blank">connect-flash <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。要了解其工作方式，请查看 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js" target="blank">Web 应用程序样本 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

</br>
</br>

## 使用 API 为应用程序添加品牌形象
{: #branded-ui-api}

您可以显示自己的定制屏幕，并利用 {{site.data.keyword.appid_short_notm}} 的认证和授权功能。利用 Cloud Directory 作为身份提供者，用户不需要多少帮助就可以与应用程序进行交互。用户无需寻求帮助就可以完成登录、注册、重置密码等操作。
{: shortdesc}

为了实现此目标，{{site.data.keyword.appid_short_notm}} 公开了 REST API。您可使用这些 REST API 构建为 Web 应用程序提供服务的后端服务器，或使用自己的定制屏幕与移动应用程序进行交互。

管理 API 通过 IBM Cloud Identity and Access Management 生成的令牌进行保护。这意味着帐户所有者可以指定团队成员对每个服务实例的访问级别。有关 IAM 和 {{site.data.keyword.appid_short_notm}} 如何协作的更多信息，请参阅[服务访问管理](/docs/services/appid/iam.html)。

在配置[设置](/docs/services/appid/cloud-directory.html)后，您可以调用以下端点以显示每个屏幕。

**注册**

您可以使用 `/sign_up` 端点来允许用户向应用程序注册。在请求主体中提供以下数据：
  * 您的租户标识。
  * Cloud Directory 用户数据。请参阅 [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) 以获取更多详细信息。
    * `password` 属性。
    * 在 `primary` 属性设置为 `true` 的电子邮件数组中，必须包含至少 1 个电子邮件地址。

根据您的[电子邮件配置](/docs/services/appid/cloud-directory.html)，用户向应用程序注册时，可能会收到验证请求和/或收到欢迎他们的电子邮件。用户注册您的应用程序时，将触发这两种类型的电子邮件。验证电子邮件包含用户可单击以确认其身份的链接；这将显示一个屏幕，感谢他们验证或确认其验证已完成。  

要显示您自己的发布验证页面，请执行以下操作：

1. 在 {site.data.keyword.appid_short_notm}} 仪表板中浏览到 Cloud Directory 身份提供者。
2. 单击**电子邮件验证**选项卡。
3. 在**定制验证页面 URL** 中，输入登录页面的 URL。

当提供此值时，{{site.data.keyword.appid_short_notm}} 将调用 URL 和 `context` 查询。当您调用 `/sign_up/confirmation_result` 端点并传递接收到的 `context` 参数时，将显示结果，告知您用户是否已验证其帐户。如果已验证，那么您可以显示定制页面。

</br>
**忘记密码**
您可以使用 `/forgot_password` 端点允许用户在忘记密码时恢复其密码。

在请求主体中提供以下数据：
  * 您的租户标识。
  * Cloud Directory 用户的电子邮件。

调用端点时，系统会向用户发送重置密码的电子邮件。该电子邮件包含**重置**按钮。按下该按钮后，{{site.data.keyword.appid_short_notm}} 将显示一个允许用户重置其密码的屏幕。

您可以提供您自己的重置密码后的页面：

1. 在 GUI 中配置 Cloud Directory [设置](cloud-directory.html#cd-settings)。**允许用户通过应用程序管理自己的帐户**必须设置为**开启**。
2. 在服务仪表板的**重置密码**选项卡中，确保将**忘记密码电子邮件**设置为**开启**。
3. 在**定制重置密码页面的 URL** 中输入登录页面的 URL  

当提供此值时，{{site.data.keyword.appid_short_notm}} 将调用 URL 和 `context` 查询。`context` 参数用于在调用 `/forgot_password/confirmtion_result` 时接收结果。如果结果成功，那么可以显示定制页面。

向定制重置密码页面添加一个随机字符串，并在提交请求时将其传递到后端。让您的处理程序验证字符串，并仅在其有效时调用 `/change_password` 端点。这样做，您可以降低后端重置密码端点的漏洞。
{: tip}

</br>
**更改密码**

在两种情况下，可以使用 `/change_password` 端点。当用户提交重置请求时，或者用户登录到应用程序并想要更新其密码时。

在请求主体中提供以下数据以在重置请求后更新其密码：
  * 您的租户标识。
  * 用户新密码
  * Cloud Directory 用户 UUID。
  * 可选：执行密码重置的 IP 地址。如果您选择传递 IP 地址，那么占位符 `%{passwordChangeInfo.ipAddress}` 可用于更改密码电子邮件模板。

根据您的配置，当更改密码时，{{site.data.keyword.appid_short_notm}} 可能会向用户发送电子邮件，告知用户发生密码更改。

</br>
要允许用户登录应用程序更改其密码：

在请求主体中提供以下数据：
  * 您的租户标识。
  * 用户新密码
  * Cloud Directory 用户 UUID。

您的更改密码页面应提示用户输入其当前密码及其新密码。
{: tip}

您的后端使用 ROP API 验证用户的当前密码，如果有效，则使用新密码调用端点。根据您的配置，当更改密码时，{{site.data.keyword.appid_short_notm}} 可能会向用户发送电子邮件，告知用户发生密码更改。

</br>
**重新发送**

您可以使用 `/resend/{templateName}` 在用户由于某种原因而未接收到电子邮件时重新发送电子邮件。

在请求主体中提供以下数据：
  * 租户标识。
  * 模板名称
  * Cloud Directory 用户 UUID。

**更改详细信息**

当用户登录到应用程序时，他们可以更新其部分信息。您可以使用 `/Users/{userId}` 来获取和更新其信息。

更新用户详细信息后，端点会以 [SCIM 格式](https://tools.ietf.org/html/rfc7643#section-8.2) 获取请求主体中更新的用户数据。请确保仅更改相关详细信息。

无法更改其电子邮件地址。
{: tip}
