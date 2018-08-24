---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 配置 Cloud Directory
{: #cd}

用户可以使用电子邮件或用户名和密码注册并登录到移动应用程序和 Web 应用程序。Cloud Directory 是在云中维护的用户注册表。当用户注册应用程序时，会将其添加到您的用户目录中。利用此功能，用户可以在应用程序中自由管理自己的帐户。
{: shortdesc}

</br>

## 管理目录设置
{: #cd-settings}

您可以配置通知以及用户对应用程序的控制级别。按照下图所示，您可以快速完成 Cloud Directory 的设置。随时可以从服务仪表板更新这些设置。
{: shortdesc}


![配置 Cloud Directory](/images/cloud-directory.png)
图. Cloud Directory 的配置过程


1. 确保开启 Cloud Directory 作为身份提供者，并将**允许用户注册并重置密码**设置为**开启**。如果设置为**关闭**，那么仍可以通过控制台添加用户以用于开发目的。
2. 选择用户是否使用指定的用户名或电子邮件进行认证。此字段将用于注册、登录和忘记密码流程。如果允许用户使用用户名和密码登录，那么用户名必须至少为 8 个字符，并且不能包含空格、逗号或斜杠。 **注：**仅 Cloud Directory 中无用户时，才可以在选项之间进行切换。
3. 配置发件人详细信息。指定发件人的电子邮件地址，电子邮件消息将显示为从该地址发送，用户可以回复到该地址。
配置操作 URL 时，一定要为用户提供足够的时间来单击链接。用户必须验证其电子邮件中包含特定选项，例如，请求重置其密码的功能。
  {: tip}
4. 确定用户将接收的电子邮件类型以及发件人信息。
5. 借助提供的模板，使用您的品牌或个性化消息来定制消息。有关更多信息，请参阅[管理消息](/docs/services/appid/cloud-directory.html#cd-messages)。
6. 在 GUI 的**用户**选项卡中查看谁注册了您的应用程序。

1 分钟内单个用户最多可登录 5 次。如果进行了第六次尝试，那么将显示错误。
{: tip}

</br>

## 管理消息
{: #cd-messages}

模板是您可发送给用户的电子邮件示例。您可以通过更新消息的内容和布局来定制模板。
{: shortdesc}

1. 在仪表板的**身份提供者 > Cloud Directory > 设置**选项卡中，将想要发送的消息设置为**开启**。

2. 可选：使用<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">语言管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来设置想要在消息模板中使用的其他语言。有关支持的语言代码的列表，请参阅[支持的语言](#languages)。

3. 选择**消息类型**。

4. 通过更改消息的内容和设计，对消息进行定制。可以使用参数对消息进行个性化操作。切记保存更改！

### 消息的类型

您可以向用户发送多种类型的消息。您既可以选择发送已编程为 UI 的示例消息发送，也可以定制更为个性化的应用程序体验内容。

<dl>
  <dt>欢迎</dt>
    <dd><p>在用户注册后，您可以通过电子邮件欢迎用户使用您的应用程序。要欢迎用户加入并留住用户，尽可能让消息充满吸引力。
    </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 所有消息参数</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> 显示为登录窗口小部件配置的图像。</td>
        </tr>
        <tr>
          <td><code>%{user.displayName}</code></td>
          <td> 显示用户所选的在与应用程序交互时要使用的屏幕名称。</td>
        </tr>
        <tr>
          <td><code>%{user.email}</code></td>
          <td> 显示用户的注册电子邮件地址。</td>
        </tr>
        <tr>
          <td><code>%{user.username}</code></td>
          <td> 当认证方法设置为用户名和密码时，显示用户指定的用户名。</td>
        </tr>
        <tr>
          <td><code>%{user.firstName}</code></td>
          <td> 显示用户的指定名字。</td>
        </tr>
        <tr>
          <td><code>%{user.formattedName}</code></td>
          <td> 显示用户的全名。</td>
        </tr>
        <tr>
          <td><code>%{user.lastName}</code></td>
          <td> 显示用户的指定姓氏。</td>
        </tr>
      </tbody>
    </table>
    <p>**注**：如果用户未提供参数拉出的信息，将显示为空。</p></dd>
  <dt>忘记密码</dt>
    <dd><p>用户在忘记密码或出于任何原因需要更新密码时，可要求重置密码。您可以定制对这些请求的电子邮件响应。当用户请求更改时，在他们单击此电子邮件中的链接之前，其密码仍保持未更改状态。

    </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 密码更改参数</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> 显示链接保持有效的小时数。</td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> 显示链接保持有效的分钟数。</td>
        </tr>
        <tr>
          <td><code>%{resetPassword.code}</code></td>
          <td> 在 URL 中，显示一次性密码作为其中一部分。这意味着每个人都会收到不同的代码。示例：<code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.link}</code></td>
          <td> 显示用户单击以重置密码的链接。</td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>验证</dt>
    <dd><p>您可以请求用户通过电子邮件验证其帐户。通过请求验证，您可以限制可注册应用程序的伪帐户数。您可以限制为当用户已验证电子邮件后才可访问应用程序，或用于管理您将为哪些用户创建概要文件。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 验证消息参数</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> 显示链接保持有效的时数。</td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> 显示链接保持有效的分钟数。</td>
        </tr>
        <tr>
          <td><code>%{verify.code}</code></td>
          <td> 显示一次性验证 URL。</td>
        </tr>
        <tr>
          <td><code>%{verify.link}</code></td>
          <td> 显示在设置中指定的操作 URL。</td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>密码更改</dt>
    <dd><p>您可以在用户密码进行更新后告知用户。在用户并未请求更改密码时，该功能很有用。他们可以采取适当步骤来重新保护帐户的安全。

    </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="“更多信息”图标"/> 密码更改参数</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
          <td> 显示新密码生效的时间。</td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> 显示请求更改密码的 IP 地址。</td>
        </tr>
      </tbody>
    </table>
    </dd>
</dl>
</br>
**注**：{{site.data.keyword.appid_short_notm}} 使用 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 作为邮件传送服务。所有电子邮件都会使用单个 SendGrid 帐户发送。


</br>

## 管理密码强度
{: #strength}

您可以为要用于 Cloud Directory 的密码设置需求。
{: shortdesc}

如果密码强度高，就难以甚至不可能通过手动或自动方式来猜测密码。密码强度设置为正则表达式字符串。

一些常用的密码强度示例：

- 必须至少为 8 个字符。示例正则表达式：`^.{8,}$`
- 必须包含 1 个数字、1 个小写字母和 1 个大写字母。示例正则表达式：`^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- 必须仅包含英语字母和数字。示例正则表达式：`^[A-Za-z0-9]*$`
- 必须至少为 1 个唯一字符。示例正则表达式：`^(\w)\w*?(?!\1)\w+$`

您必须使用<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接"></a> 来设置需求。

</br>



</br>

## 支持的语言
{: #languages}

您可以使用<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">语言管理 API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>来设置可编写用户通信的语言。但是，仅英语开箱即用。您负责翻译消息。在使用 API 设置配置后，GUI 将更新，从而使您能够更改模板文本。
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>代码</th>
    <th>语言</th>
    <th>区域</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>南非荷兰语</td>
    <td>南非</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>阿尔巴尼亚语</td>
    <td>阿尔巴尼亚</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>阿姆哈拉语</td>
    <td>埃塞俄比亚</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>阿拉伯语</td>
    <td>阿尔及利亚</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>阿拉伯语</td>
    <td>巴林</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>阿拉伯语</td>
    <td>埃及</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>阿拉伯语</td>
    <td>伊拉克</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>阿拉伯语</td>
    <td>约旦</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>阿拉伯语</td>
    <td>科威特</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>阿拉伯语</td>
    <td>黎巴嫩</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>阿拉伯语</td>
    <td>利比亚</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>阿拉伯语</td>
    <td>毛里塔尼亚</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>阿拉伯语</td>
    <td>摩洛哥</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>阿拉伯语</td>
    <td>阿曼</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>阿拉伯语</td>
    <td>卡塔尔</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>阿拉伯语</td>
    <td>沙特阿拉伯</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>阿拉伯语</td>
    <td>叙利亚</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>阿拉伯语</td>
    <td>突尼斯</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>阿拉伯语</td>
    <td>阿拉伯联合酋长国</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>阿拉伯语</td>
    <td>也门</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>亚美尼亚语</td>
    <td>亚美尼亚</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>阿萨姆语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>阿塞拜疆语</td>
    <td>阿塞拜疆</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>巴斯克语</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>白俄罗斯语</td>
    <td>白俄罗斯</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>孟加拉语</td>
    <td>孟加拉国</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>白俄罗斯语</td>
    <td>白俄罗斯</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>孟加拉语</td>
    <td>孟加拉国</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>孟加拉语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>波斯尼亚语</td>
    <td>波斯尼亚</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>保加利亚语</td>
    <td>保加利亚</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>缅甸语</td>
    <td>缅甸</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>加泰隆尼亚语</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>简体中文</td>
    <td>中国</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>简体中文</td>
    <td>新加坡</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>繁体中文</td>
    <td>中国香港特别行政区</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>繁体中文</td>
    <td>中国澳门特别行政区</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>繁体中文</td>
    <td>台湾</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>克罗地亚语</td>
    <td>克罗地亚</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>捷克语</td>
    <td>捷克共和国</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>丹麦语</td>
    <td>丹麦</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>荷兰语</td>
    <td>比利时</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>荷兰语</td>
    <td>荷兰</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>英语</td>
    <td>澳大利亚</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>英语</td>
    <td>比利时</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>英语</td>
    <td>喀麦隆</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>英语</td>
    <td>加拿大</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>英语</td>
    <td>加纳</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>英语</td>
    <td>中国香港特别行政区</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>英语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>英语</td>
    <td>爱尔兰</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>英语</td>
    <td>肯尼亚</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>英语</td>
    <td>毛里求斯</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>英语</td>
    <td>新西兰</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>英语</td>
    <td>尼日利亚</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>英语</td>
    <td>菲律宾</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>英语</td>
    <td>新加坡</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>英语</td>
    <td>南非</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>英语</td>
    <td>坦桑尼亚</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>英语</td>
    <td>英国</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>英语</td>
    <td>美国</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>英语</td>
    <td>赞比亚</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>英语</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>爱沙尼亚语</td>
    <td>爱沙尼亚</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>菲律宾语</td>
    <td>菲律宾</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>芬兰语</td>
    <td>芬兰</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>法语</td>
    <td>阿尔及利亚</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>法语</td>
    <td>喀麦隆</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>法语</td>
    <td>刚果民主共和国</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>法语</td>
    <td>比利时</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>法语</td>
    <td>加拿大</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>法语</td>
    <td>法国</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>法语</td>
    <td>科特迪瓦</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>法语</td>
    <td>卢森堡</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>法语</td>
    <td>毛里塔尼亚</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>法语</td>
    <td>毛里求斯</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>法语</td>
    <td>摩洛哥</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>法语</td>
    <td>塞内加尔</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>法语</td>
    <td>瑞士</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>法语</td>
    <td>突尼斯</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>加利西亚语</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>干达语</td>
    <td>乌干达</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>格鲁吉亚语</td>
    <td>格鲁吉亚</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>德语</td>
    <td>奥地利</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>德语</td>
    <td>德国</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>德语</td>
    <td>卢森堡</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>德语</td>
    <td>瑞士</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>希腊语</td>
    <td>希腊</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>古吉拉特语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>蒙撒语</td>
    <td>尼日利亚</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>希伯莱语</td>
    <td>以色列</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>印度语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>匈牙利语</td>
    <td>匈牙利</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>冰岛语</td>
    <td>冰岛</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>伊博语</td>
    <td>尼日利亚</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>印度尼西亚语</td>
    <td>印度尼西亚</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>意大利语</td>
    <td>意大利</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>意大利语</td>
    <td>瑞士</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>日语</td>
    <td>日本</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>卡纳达语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>哈萨克语</td>
    <td>哈萨克斯坦</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>高棉语</td>
    <td>柬埔寨</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>卢旺达语</td>
    <td>卢旺达</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>孔卡尼语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>韩语</td>
    <td>韩国</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>立陶宛语</td>
    <td>立陶宛</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>拉脱维亚语</td>
    <td>拉脱维亚</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>高棉语</td>
    <td>柬埔寨</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>马其顿语</td>
    <td>马其顿</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>马来西亚拉丁语</td>
    <td>马来西亚</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>马拉雅拉姆语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>马耳他语</td>
    <td>马耳他</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>马拉地语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>蒙古斯拉夫语</td>
    <td>蒙古</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>尼泊尔语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>尼泊尔语</td>
    <td>尼泊尔</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>挪威语</td>
    <td>挪威</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>西挪威语</td>
    <td>挪威</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>奥里雅语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>奥罗莫语</td>
    <td>埃塞俄比亚</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>波兰语</td>
    <td>波兰</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>葡萄牙语 </td>
    <td>安哥拉</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>葡萄牙语 </td>
    <td>巴西</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>葡萄牙语 </td>
    <td>中国澳门特别行政区</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>葡萄牙语 </td>
    <td>莫桑比克</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>葡萄牙语 </td>
    <td>葡萄牙</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>旁遮普语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>罗马尼亚语</td>
    <td>罗马尼亚</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>俄语</td>
    <td>俄罗斯</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>塞尔维亚西里尔语</td>
    <td>塞尔维亚</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>塞尔维亚拉丁语</td>
    <td>黑山共和国</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>塞尔维亚拉丁语</td>
    <td>塞尔维亚</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>锡兰语</td>
    <td>斯里兰卡</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>斯洛伐克语</td>
    <td>斯洛伐克</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>斯诺文尼亚语</td>
    <td>斯洛文尼亚</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>西班牙语</td>
    <td>阿根廷</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>西班牙语</td>
    <td>玻利维亚</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>西班牙语</td>
    <td>智利</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>西班牙语</td>
    <td>哥伦比亚</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>西班牙语</td>
    <td>哥斯达黎加</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>西班牙语</td>
    <td>多米尼加共和国</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>西班牙语</td>
    <td>厄瓜多尔</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>西班牙语</td>
    <td>萨尔瓦多</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>西班牙语</td>
    <td>危地马拉</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>西班牙语</td>
    <td>洪都拉斯</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>西班牙语</td>
    <td>墨西哥</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>西班牙语</td>
    <td>尼加拉瓜</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>西班牙语</td>
    <td>巴拿马</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>西班牙语</td>
    <td>巴拉圭</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>西班牙语</td>
    <td>秘鲁</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>西班牙语</td>
    <td>波多黎各</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>西班牙语</td>
    <td>西班牙</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>西班牙语</td>
    <td>美国</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>西班牙语</td>
    <td>乌拉圭</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>西班牙语</td>
    <td>委内瑞拉</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>斯瓦希里语</td>
    <td>肯尼亚</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>斯瓦希里语</td>
    <td>坦桑尼亚</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>瑞典语</td>
    <td>瑞典</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>泰米尔语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>泰卢固语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>泰语</td>
    <td>泰国</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>土耳其语</td>
    <td>土耳其</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>乌克兰语</td>
    <td>乌克兰</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>乌尔都语</td>
    <td>印度</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>乌尔都语</td>
    <td>巴基斯坦</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>乌兹别克西里尔语</td>
    <td>乌兹别克斯坦</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>乌兹别克拉丁语</td>
    <td>乌兹别克斯坦</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>越南语</td>
    <td>越南</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>威尔士语</td>
    <td>英国</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>约鲁巴语</td>
    <td>尼日利亚</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>祖鲁语</td>
    <td>南非</td>
  </tr>
</table>
