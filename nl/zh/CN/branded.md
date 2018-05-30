---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# 有品牌形象的登录体验
{: #branding}

您可以显示自己的定制屏幕，并利用 {{site.data.keyword.appid_full}} 的认证和授权功能。利用 Cloud Directory 作为身份提供者，用户不需要多少帮助就可以与应用程序进行交互。他们可以在不寻求帮助的情况下登录。
{: shortdesc}

当您使用自己的屏幕时，[资源所有者密码凭证流程](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)可用于提供访问令牌和身份令牌。


## 使用 Android SDK 显示定制屏幕
{: #branded-ui-android}

在启用 Cloud Directory 的情况下，可以使用 Android SDK 来调用定制屏幕。<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">查看此博客！<img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>
{: shortdesc}

</br>
**登录**

1. 将 **Cloud Directory** 作为身份提供者设置为**开启**。
2. 将以下命令放在代码中。
  ```java
 AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
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

## 使用 iOS Swift SDK 显示定制屏幕
{: #branded-ui-ios-swift}

在启用 Cloud Directory 的情况下，可以使用 iOS Swift SDK 来调用定制屏幕。
{: shortdesc}

</br>
**登录**

1. 在 GUI 上的身份提供者选项卡中，将 Cloud Directory 设置为**开启**。
2. 使用资源所有者密码登录。当用户尝试使用其用户名和密码登录时，会获取访问令牌和身份令牌。
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
        }

        }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: pre}


</br>
</br>

## 使用 Node.js SDK 显示定制屏幕
{: #branded-ui-nodejs}

在启用 Cloud Directory 的情况下，可以使用 Node.js SDK 来调用定制屏幕。
{: shortdesc}

**登录**
1. 在身份提供者设置中，将 Cloud Directory 设置为**开启**，然后指定回调端点。
2. 为应用程序添加发布路径（可以使用用户名和密码参数来调用该路径），然后使用资源所有者密码登录。

    ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
    {: pre}
    利用 `WebAppStrategy`，用户可以使用用户名和密码登录 Web 应用程序。成功登录后，用户的访问令牌会存储在 HTTP 会话中，并在整个会话过程中可用。当 HTTP 会话销毁或到期后，令牌也无效。
    {: tip}

