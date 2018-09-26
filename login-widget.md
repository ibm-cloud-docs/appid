---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-26"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Displaying the login widget
{: #default}

{{site.data.keyword.appid_full}} provides a login widget that lets you give your users secure sign-in options.
{: shortdesc}

When your app is configured to use an identity provider, visitors to your app are directed to a sign in screen by the login widget. With the login widget you can display a default sign in screen. And, as an added bonus, you can update your sign in flow at any time, without changing your source code in any way!

Want to create an experience that's unique to your app? You can [bring your own screens](/docs/services/appid/branded.html)!
{: tip}

**What is the default?**

You can take advantage of {{site.data.keyword.appid_short_notm}}, even without your own UI screens, by displaying the login widget. By default, when only one provider is set to **On**, visitors are redirected to that identity providers authentication screen. But, when more than one identity provider is configured, the user is redirected to the login widget. There, the user can choose the identity provider that they want to sign in to your app with.

**How much information does {{site.data.keyword.appid_short_notm}} obtain from an identity provider?**

When you use social or enterprise identity providers, {{site.data.keyword.appid_short_notm}} never has access to a users account information. The service uses a token that is issued by the identity provider to verify that a user is who they say that they are. Because the service never has access to user information, users must go through their chosen identity provider to do any other actions such as resetting their password. For example, if a user signs into your app with Facebook, and then wanted to change their password, they must go to www.facebook.com to do so.

When you use [Cloud Directory](/docs/services/appid/cloud-directory.html), {{site.data.keyword.appid_short_notm}} is the identity provider. The service uses your registry to verify your users identity. Because {{site.data.keyword.appid_short_notm}} is the provider, users can take advantage of advanced functionality, such as resetting their password, directly in your app.

</br>
</br>

## Customizing the default sign in screen
{: #login-widget}

{{site.data.keyword.appid_short_notm}} provides a default login screen that you can call if you don't have your own UI screens to display. You can customize the screen to display the logo and colors of your choice.
{: shortdesc}

To customize the screen:

1. Open the {{site.data.keyword.appid_short_notm}} service dashboard.
2. Select the **Login Customization** section. You can modify the appearance of the login widget to align with your company's brand.
3. Upload your company's logo by selecting a PNG or JPG file from your local system. The recommended image size is 320 x 320 pixels. The maximum file size is 100 Kb.
4. Select a header color for the widget from the color picker, or enter the hex code for another color.
5. Inspect the preview pane, and click **Save Changes** when you are happy with your customizations. A confirmation message is displayed.
6. In your browser, refresh your login page to verify your changes.

Don't forget! You can take advantage of {{site.data.keyword.appid_short_notm}} with other languages too. If you don't see an SDK for the language you're working in, you can alway use the APIs. Check out check out <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">our blogs<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{: tip}

</br>

## Displaying the login widget with the Android SDK
{: #android}

You can call the preconfigured sign in screen with the Android SDK.
{: shortdesc}


Place the following command in your code.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        @Override
        public void onAuthorizationCanceled () {
          //Authentication canceled by the user
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
          //User authenticated
        }
      });
  ```
{: codeblock}

</br>
</br>

## Displaying the login widget with the iOS Swift SDK
{: #ios-swift}

You can call a preconfigured sign in screen with the iOS Swift SDK.
{: shortdesc}

Place the following command in your code.

  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

</br>
</br>

## Displaying the login widget with the Node.js SDK
{: #nodejs}

You can call a preconfigured sign in screen with the Node.js SDK.
{: shortdesc}

Add a post route to your app that can be called with the username and password parameters and log in by using the resource owner password.

    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // allow flash messages
    }));
    ```
    {: codeblock}

`WebAppStrategy` allows users to sign in to your web apps with a username and password. After a successful login, a user's access token is stored in the HTTP session and is available during the session. After the HTTP session is destroyed or expired, the token is invalid.
{: tip}



