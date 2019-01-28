---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-28"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Displaying the Login Widget
{: #login-widget}

{{site.data.keyword.appid_full}} provides a Login Widget that lets you give your users secure sign in options.
{: shortdesc}

When your app is configured to use an identity provider, visitors to your app are directed to a sign-in screen by the Login Widget. With the Login Widget, you can display preconfigured screens for your sign-in flows. As a bonus, you can update your sign-in flow at any time without changing your source code in any way!

Want to create an experience that's unique to your app? You can [bring your own screens](/docs/services/appid/branded.html)!
{: tip}

## Understanding the Login Widget
{: #understanding}

You can take advantage of {{site.data.keyword.appid_short_notm}}, even without your own UI screens, by displaying the Login Widget.
{: shortdesc}

**What is the default?**

When more than one identity provider is configured, a user is redirected to the Login Widget when they try to sign in to your application. By using the Login Widget, users can choose the provider that they want to verify their identity with. But, when only one provider is set to **On**, visitors are redirected to that identity providers authentication screen.

**How much information does {{site.data.keyword.appid_short_notm}} obtain from an identity provider?**

When you use social or enterprise identity providers, {{site.data.keyword.appid_short_notm}} has read access to a users account information. The service uses a token and the assertions that are returned by the identity provider to verify that a user is who they say that they are. Because the service never has write access to the information, users must go through their chosen identity provider to do actions, such as resetting their password. For example, if a user signs in to your app with Facebook, and then wanted to change their password, they must go to www.facebook.com to do so.

When you use [Cloud Directory](/docs/services/appid/cloud-directory.html), {{site.data.keyword.appid_short_notm}} is the identity provider. The service uses your registry to verify your users identity. Because {{site.data.keyword.appid_short_notm}} is the provider, users can take advantage of advanced functionality, such as resetting their password, directly in your app.

**What kind of screens can be displayed for each type of provider?**

Check out the following table to see which screens you can display for each type of identity provider.

<table>
  <thead>
    <tr>
      <th>Login Widget screen</th>
      <th>Social identity provider</th>
      <th>Enterprise identity provider</th>
      <th>Cloud Directory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Sign in</td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Sign up</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Forgot password</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Change password</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Account details</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Feature available" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

</br>
</br>

## Customizing the Login Widget
{: #customize}

{{site.data.keyword.appid_short_notm}} provides a default login screen that you can call if you don't have your own UI screens to display. You can customize the screen to display the logo and colors of your choice.
{: shortdesc}

To customize the screen:

1. Open the {{site.data.keyword.appid_short_notm}} service dashboard.
2. Select the **Login Customization** section. You can modify the appearance of the Login Widget to align with your company's brand.
3. Upload your company's logo by selecting a PNG or JPG file from your local system. The recommended image size is 320 x 320 pixels. The maximum file size is 100 Kb.
4. Select a header color for the widget from the color picker, or enter the hex code for another color.
5. Inspect the preview pane, and click **Save Changes** when you are happy with your customizations. A confirmation message is displayed.
6. In your browser, refresh your login page to verify your changes.

Don't forget! You can take advantage of {{site.data.keyword.appid_short_notm}} with other languages too. If you don't see an SDK for the language you're working in, you can always use the APIs. Check out <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">our blogs<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{: tip}


## Displaying the Login Widget with the Android SDK
{: #android}

You can call preconfigured screens with the [Android client SDK](https://github.com/ibm-cloud-security/appid-clientsdk-android).
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

**Sign up**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Add the following code to your app. When a user signs up for your app from your custom screen, the sign up flow is started. The following call not only registers the user, but can also send a verification email to complete the registration, depending on your Cloud Directory configurations.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
      public void onAuthorizationCanceled () {
          //Sign up canceled by the user
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              //User authenticated
          } else {
              //email verification is required
          }
      }
  });
  ```
  {: pre}

</br>

**Forgot password**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
3. Add the following code to your app. When a user clicks "forgot password" in your application, the SDK calls the forgot_password API to send an email to the user that allows them to reset their password.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
   	public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
      public void onAuthorizationCanceled () {
          // Forogt password canceled by the user
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Forgot password finished, in this case accessToken and identityToken will be null.
      }
  });
  ```
  {: codeblock}

</br>

**Change details**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. In the **Password changed** tab of the service dashboard, set **Password changed email** to
3. Call the login widget to start the change details flow.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Exception occurred
      }

      @Override
      public void onAuthorizationCanceled () {
          // Changed details canceled by the user
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // User authenticated, and fresh tokens received
      }
  });
  ```
  {: codeblock}

</br>

**Change password**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Place the following code in your app to start the change password flow.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Exception occurred
      }

      @Override
      public void onAuthorizationCanceled () {
          // Change password canceled by the user
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // User authenticated, and fresh tokens received
      }
  });
  ```
  {: codeblock}


</br>
</br>

## Displaying the Login Widget with the iOS Swift SDK
{: #ios-swift}

You can call preconfigured screens with the [iOS Swift client SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

Place the following command in your code.

  ```swift
  import IBMCloudAppID
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

**Sign up**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Place the following code in your application. When a user attempts to sign up for your application, the login widget is called and displays your custom sign up page.

  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
       if accessToken == nil && identityToken == nil {
        //email verification is required
        return
       }
     //User authenticated
    }

    public func onAuthorizationCanceled() {
        //Sign up canceled by the user
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Exception occurred
    }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: codeblock}

</br>

**Forgot password**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
3. Place the following code in your application. When one of your app users requests that their password is updated, the login widget is called and the process starts.

  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
        //forgot password finished, in this case accessToken and identityToken will be null.
     }

     public func onAuthorizationCanceled() {
         //forgot password canceled by the user
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //Exception occurred
     }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: codeblock}

</br>

**Change details**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. In the **Password changed** tab of the service dashboard, set **Password changed email** to
3. Call the login widget to start the change details flow.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //changed details canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>

**Change password**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Place the following code in your app to start the change password flow.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //change password canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
           //Exception occurred
      }
   }

   AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}

</br>
</br>

## Displaying the Login Widget with the Node.js SDK
{: #nodejs}

You can call preconfigured screens with the [Node.js server SDK](https://github.com/ibm-cloud-security/appid-serversdk-nodejs).
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

</br>

**Sign up**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Place the following code in your application. When a user attempts to sign up for your application, the login widget is called and displays your custom sign up page.

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

**Forgot password**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
3. Place the following code in your application to pass the *show* property to `WebAppStrategy.FORGOT_PASSWORD`. When a user requests that their password to your app be updated, the login widget is called and the  process starts.

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

**Change details**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. In the **Password changed** tab of the service dashboard, set **Password changed email** to
3. Place the following code in your application to pass the *show* property to `WebAppStrategy.FORGOT_PASSWORD` to launch the change details form.

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

**Change password**

1. Configure your Cloud Directory [settings](/docs/services/appid/cloud-directory.html#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. In the **Password changed** tab of the service dashboard, set **Password changed email** to
3. Place the following code in your application to pass the *show* property to `WebAppStrategy.FORGOT_PASSWORD` to launch the change details form.

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

</br>
