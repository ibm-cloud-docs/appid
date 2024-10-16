---

copyright:
  years: 2017, 2024
lastupdated: "2024-10-09"

keywords: app log in, login widget, sign in, default screen, forgot password, mfa, multi-factor authentication, sign up, reset password, facebook, google, identity provider, social log in, saml, authentication, authorization, cloud directory

subcollection: appid

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}
{:terraform: .ph data-hd-interface='terraform'}
{:release-note: data-hd-content-type='release-note'}


# Using the Login Widget
{: #login-widget}

With {{site.data.keyword.appid_full}} you can use a default UI, called a Login Widget, to allow application users the ability to choose the identity provider that they want to sign in with. If you're using Cloud Directory, the Login Widget also provides additional UI's for extra functionalities such as sign-up, forgot password, multi-factor authentication, and more.
{: shortdesc}

## Understanding the Login Widget
{: #widget-understanding}

One of the best parts of the Login Widget is that you can start using {{site.data.keyword.appid_short_notm}} before you implement any of your own authentication UIs - which makes the developer onboarding experience that much easier.

### What is the default Login Widget behavior?
{: #widget-default}

By default, the Login Widget is enabled to use Facebook, Google, and Cloud Directory. You can change the behavior at any time by choosing which identity providers that you want to configure as an option. When more than one identity provider is enabled, the Login Widget presents a screen where the user can make their identity provider selection. But, if you have a single provider that is enabled, users do not see the previously mentioned selection screen. They are taken directly to the identity provider to begin the sign-in process.

For example, if you're using the default - Facebook, Google, and Cloud Directory - users see the screen. If you enable Facebook only, user's are taken directly to Facebook for authentication.



### Which screens can be displayed for each provider?
{: #widget-options}

When you use Cloud Directory, {{site.data.keyword.appid_short_notm}} is able to provide you with the extended functionality of user management. The extended functionality also applies to the Login Widget's capabilities. User's that are stored in Cloud Directory can take advantage of the functionality such as signing up or resetting their password directly in the Login Widget. Check out the following table to see which screens you can display for each type of identity provider.

| Login Widget screen | Social identity provider | Enterprise identity provider | Cloud Directory |
|-----|----| -----| ------ |
| Sign in | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Sign up | | | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Forgot password | | | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Change password | | | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Account details | | | ![Checkmark icon](../../icons/checkmark-icon.svg) |
{: caption="The Login Widget screens that each identity provider can display" caption-side="top"}


### Customizing an SSO login flow
{: #widget-custom-sso}

After a successful authentication, App ID creates a session cookie with encrypted access and identity tokens that your apps can use for authentication. Another way to customize the flow is to send an access token to your browser so that any browser app can use the token in its Ajax request.


## Customizing the Login Widget
{: #widget-customize}

The Login Widget is dynamic. You can customize the look and feel or identity provider configuration, and the changes are applied immediately. You do not need to update your application code or redeploy your app in any way!
{: shortdesc}

Do you need more customization than the Login Widget provides? You can implement your own, fully customized UI for user sign in, sign up, reset password, and other flows to create an experience that's unique to your app. To get started, check out [branding your app](/docs/appid?topic=appid-branded).
{: tip}

To customize the screen:

1. Open the {{site.data.keyword.appid_short_notm}} service dashboard.
2. Select the **Login Customization** section. You can modify the appearance of the Login Widget to align with your company's brand.
3. Upload your company's logo by selecting a PNG or JPG file from your local system. The recommended image size is 320 x 320 pixels. The maximum file size is 100 Kb.
4. Select a header color for the widget from the color picker, or enter the hex code for another color.
5. Inspect the preview pane, and click **Save Changes** when you are happy with your customizations. A confirmation message is displayed.
6. In your browser, refresh your login page to verify your changes.


## Displaying the Login Widget with the Android SDK
{: #widget-display-android}

You can call preconfigured screens with the [Android client SDK](https://github.com/ibm-cloud-security/appid-clientsdk-android){: external}.
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

### Sign up
{: #widget-android-signup}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Add the following code to your app. When a user signs up for your app from your custom screen, the sign-up flow is started. The following call not only registers the user, but can also send a verification email to complete the registration, depending on your Cloud Directory configurations.

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
   {: codeblock}

</br>

### Forgot password
{: #widget-android-forgot-password}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
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

### Change details
{: #widget-android-change-details}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
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

### Change password
{: #widget-android-change-password}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
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



## Displaying the Login Widget with the iOS Swift SDK
{: #widget-display-ios-swift}

You can call preconfigured screens with the [iOS Swift client SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift){: external}.
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

### Sign up
{: #widget-ios-signup}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Place the following code in your application. When a user attempts to sign up for your application, the login widget is called and displays your custom sign-up page.

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

### Forgot password
{: #widget-ios-forgot-password}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
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

### Change details
{: #widget-ios-change-details}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
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

### Change password
{: #widget-ios-change-password}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
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


## Displaying the Login Widget with the Node.js SDK
{: #widget-display-nodejs}

You can call preconfigured screens with the [Node.js server SDK](https://github.com/ibm-cloud-security/appid-serversdk-nodejs){: external}.
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

### Sign up
{: #widget-nodejs-signup}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. Place the following code in your application. When a user attempts to sign up for your application, the login widget is called and displays your custom sign-up page.

   ```javascript
   app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
   successRedirect: LANDING_PAGE_URL,
   show: WebAppStrategy.SIGN_UP
   }));
   ```
   {: codeblock}

</br>

### Forgot password
{: #widget-nodejs-forgot-password}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. **Allow users to manage their account from your app** must be set to **On**.
2. In the **Reset Password** tab of the service dashboard, be sure that **Forgot password email** is set to **On**.
3. Place the following code in your application to pass the *show* property to `WebAppStrategy.FORGOT_PASSWORD`. When a user requests that their password to your app be updated, the login widget is called and the process starts.

   ```javascript
   app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
   successRedirect: LANDING_PAGE_URL,
   show: WebAppStrategy.FORGOT_PASSWORD
   }));
   ```
   {: codeblock}

</br>

### Change details
{: #widget-nodejs-change-details}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
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

### Change password
{: #widget-nodejs-change-password}

1. Configure your Cloud Directory [settings](/docs/appid?topic=appid-cloud-directory#cd-settings) in the GUI. Both **Allow users to sign up to your app** and **Allow users to manage their account from your app** must be set to **On**.
2. In the **Password changed** tab of the service dashboard, set **Password changed email** to
3. Place the following code in your application to pass the *show* property to `WebAppStrategy.FORGOT_PASSWORD` to launch the change details form.

   ```javascript
   app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
   successRedirect: LANDING_PAGE_URL,
   show: WebAppStrategy.CHANGE_PASSWORD
   }));
   ```
   {: codeblock}
