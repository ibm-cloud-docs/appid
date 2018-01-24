---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Managing cloud directory
{: #cd}

You can configure {{site.data.keyword.appid_short_notm}} to use cloud directory as an identity provider. Users can sign-up and sign-in to your mobile and web apps by using an email and a password. A cloud directory is a user registry that is maintained in the cloud. When a user signs up for your app with their email and a password, they are added to your directory of users. With this feature, end users have the freedom to manage their own account within your app.
{: shortdesc}

</br>
</br>

## Managing directory settings
{: #cd-settings}

You can configure the notifications and level of user control for your app. Setting up your cloud directory can be done quickly, as shown in the following image.

![Configuring cloud directory](/images/cloud-directory.png)

1. Be sure that cloud directory is turned on as an identity provider and set **Allow users to sign up and reset their password** to **On**. You can still add users through the console when it's set to **Off**, but only for development purposes.
2. Configure your sender details. Specify the email address from which your messages appear to be from, the sender, and to whom your users can reply.
  **Note**: Be sure when configuring your action URL that you give enough time for a user to click the link. A user must verify their email to have certain options, such as the ability to request a reset of their password.
3. Determine the types of emails a user receives and the sender information.
4. Using the templates provided, customize your messages with your brand, or personalized messages. For more information see [Managing messages](/docs/services/appid/cloud-directory.html#cd-messages).
5. Review cloud directory activity in the **Users** tab of the GUI.

</br>
</br>

## Managing messages
{: #cd-messages}

A template is an example of an email message that you may send to your users. You can customize the template by updating the content and layout of the message. You can set these messages to **On** or **Off** in the directory settings tab.

1. Select a **Message type**.
2. Customize your message by changing the content and design of the message. You can use parameters to personalize your messages. Don't forget to save your changes!

### Types of messages

There are several types of messages that you can send to your users. You can choose to send the example message that it programmed into the UI or you can customize the content for a more personal app experience.

<dl>
  <dt> Welcome </dt>
    <dd>You can welcome a user to your application via email, after they've registered. To welcome and retain your users, make your message as engaging as possible.
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parameters that can be used in any type of message </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Displays the image that you configured for your login widget. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> Displays the screen name a user has chosen to use when interacting with the app. </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> Displays the user's registered email address. </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> Displays the user's specified first name. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Displays a user's full name. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Displays the user's specified last name. </td>
        </tr>
      </tbody>
    </table>

    **Note**: If a user does not supply the information pulled by the parameter, it appears blank.</dd>
  <dt> Forgot password </dt>
    <dd> A user can ask to have their password reset should they forget or need to update it for any reason. You can customize the email response to their request. When a user requests a change, their password remains unchanged until they click the link in this email.

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Password change parameters </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Displays the number of hours the link is valid. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Displays the number of minutes the link is valid. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> Displays a one-time passcode as part of the URL. This would mean that each person would have a different code. Example: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Displays the link that a user clicks to reset their password. </td>
        </tr>
       </tbody>
    </table></dd>
  <dt> Verification </dt>
    <dd> You can request that a user verifies their account via email. By requesting a verification, you limit the number of fake accounts that can sign up for your app. You can restrict access to your app until a user has verified their email, or use it as a way to manage which users you create profiles for.
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Verification message parameters </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Displays the number of hours the link is valid. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Displays the number of minutes the link is valid. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> Displays a one-time verification URL. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> Displays the action URL that you specified in settings. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt> Password change </dt>
    <dd> You can let a user know when their password has been updated. This is helpful if a they did not request their password be changed. They can take the proper steps to re-secure their account.

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Password change parameters </th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> Displays the time at which a new password went into effect. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Displays the IP address from which the password change was requested. </td>
        </tr>
      </tbody>
    </table></dd>
</dl>

</br>
</br>




## Managing cloud directory with the Android SDK
{: #managing-android}

You can use the Android SDK to manage cloud directory as an identity provider.
{: shortdesc}

### Sign in customization

You can configure the sign in screen with your branding to create a more cohesive app experience for your users. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="_blank">Check out our blog! <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>

1. Set **Cloud Directory** to **On** as an identity provider.
2. Log in by using the <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html" target="_blank">resource owner password <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. You can obtain the access and identity token by supplying the end user's information.
   ```java
   AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
           new TokenResponseListener() {
           @Override
            public void onAuthorizationFailure (AuthorizationException exception) {
               //Exception occurred
            }

            @Override
            public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
              //User authenticated
            }
           });
   ```
   {: codeblock}
   <table>
     <thead>
       <th colspan=2><img src="images/idea.png"/> Understanding this commands response </th>
     </thead>
     <tbody>
       <tr>
         <td><code>onAuthorizationFailure</code> </td>
         <td> Something went wrong. Try again in a few minutes. If this response persists, contact our team for support. </td>
       </tr>
       <tr>
         <td><code>onAuthorizationSuccess</code></td>
         <td> The user was authenticated. You receive access and identity tokens for the user. </td>
       </tr>
     </tbody>
   </table>

### Sign Up

Allow users to sign up for your app with their email and a password.

1. Set **Allow users to sign up and reset their password** to **ON** in the settings for cloud directory.
2. Call the LoginWidget to start the sign up flow.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchSignUp(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  			 }

  			 @Override
  			 public void onAuthorizationCanceled () {
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  				 if (accessToken != null && identityToken != null) {
  				 } else {
  				 }

  			 }
  		 });
   ```
   {: codeblock}
   <table>
     <thead>
       <th colspan=2><img src="images/idea.png"/> Understanding this commands response </th>
     </thead>
     <tbody>
       <tr>
         <td><code>onAuthorizationFailure</code> </td>
         <td> Something went wrong with the command. Try running the command again in a few minutes. If this response persists, contact our team for support. </td>
       </tr>
       <tr>
         <td><code>onAuthorizationCanceled</code></td>
         <td> The user chose to cancel the request. </td>
       </tr>
       <tr>
         <td><code>onAuthorizationSuccess</code></td>
         <td> If a user's access and identity tokens are valid then they are authenticated. Email verification is required if their tokens are null. </td>
       </tr>
     </tbody>
   </table>


### Forgot Password

Allow users to request a temporary password should they forget theirs or need to update it for any reason.

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **ON** in the settings for cloud directory.
2. Call the LoginWidget to start the forgot password flow.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
   			 public void onAuthorizationCanceled () {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   			 }
   		 });
    ```
    {: codeblock}
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Understanding this commands response </th>
      </thead>
      <tbody>
        <tr>
          <td><code>onAuthorizationFailure</code> </td>
          <td> Something went wrong with the command. Try running the command again in a few minutes. If this response persists, contact our team for support. </td>
        </tr>
        <tr>
          <td><code>onAuthorizationCanceled</code></td>
          <td> The user chose to cancel the request. </td>
        </tr>
        <tr>
          <td><code>onAuthorizationSuccess</code></td>
          <td> The access and identity tokens are no longer valid and the user will need to use their new password to gain access to the app. </td>
        </tr>
      </tbody>
    </table>


### Change Details

Allow users to edit their account details such as their name and email.

1. Set **Allow users to sign up and reset their password** to **ON** in the settings for cloud directory.
2. Call the LoginWidget to start the change details flow.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  			 }

  			 @Override
  			 public void onAuthorizationCanceled () {
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  			 }
  		 });
   ```
   {: codeblock}
   <table>
     <thead>
       <th colspan=2><img src="images/idea.png"/> Understanding this command's response </th>
     </thead>
     <tbody>
       <tr>
         <td><code>onAuthorizationFailure</code> </td>
         <td> Something went wrong. Try again in a few minutes. If this response persists, contact our team for support. </td>
       </tr>
       <tr>
         <td><code>onAuthorizationCanceled</code></td>
         <td> The user chose to cancel the request. </td>
       </tr>
       <tr>
         <td><code>onAuthorizationSuccess</code></td>
         <td> The user was authenticated. You receive new access and identity tokens for the user. </td>
       </tr>
     </tbody>
   </table>

### Change Password

Let your users know when their password is updated.

1. Set **Allow users to sign up and reset their password** to **ON**, in the settings for cloud directory.
2. Call the LoginWidget to start the change password flow.
   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
   			 public void onAuthorizationCanceled () {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   			 }
   		 });
   ```
   {: codeblock}
   <table>
     <thead>
       <th colspan=2><img src="images/idea.png"/> Understanding this command's response </th>
     </thead>
     <tbody>
       <tr>
         <td><code>onAuthorizationFailure</code> </td>
         <td> Something went wrong. Try again in a few minutes. If this response persists, contact our team for support. </td>
       </tr>
       <tr>
         <td><code>onAuthorizationCanceled</code></td>
         <td> The user chose to cancel the request. </td>
       </tr>
       <tr>
         <td><code>onAuthorizationSuccess</code></td>
         <td> The user was authenticated. You receive new access and identity tokens for the user. </td>
       </tr>
     </tbody>
   </table>

</br>
</br>
</br>

## Managing cloud directory with the iOS Swift SDK
{: #managing-ios-swift}

You can use the iOS Swift SDK to manage cloud directory as an identity provider.

### Sign in customization

You can configure the sign in screen with your branding to create a more cohesive app experience for your users.
1. In the identity provider tab on the GUI, set cloud directory to **On**.
2. Log in by using the resource owner password. You can obtain an access and ID token by supplying the end user's username and password.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Understanding this command's response </th>
    </thead>
    <tbody>
      <tr>
        <td><code>onAuthorizationFailure</code> </td>
        <td> Something went wrong. Try again in a few minutes. If this response persists, contact our team for support. </td>
      </tr>
      <tr>
        <td><code>onAuthorizationSuccess</code></td>
        <td> The user was authenticated. You receive access and identity tokens for the user. </td>
      </tr>
    </tbody>
  </table>

### Sign Up

Allow users to sign up for your app with their email and a password.

1. Set **Allow users to sign up and reset their password** to **On**, in the settings for cloud directory.
2. Call the LoginWidget to start the sign up flow.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Understanding this command's response </th>
    </thead>
    <tbody>
      <tr>
        <td><code>onAuthorizationFailure</code> </td>
        <td> Something went wrong. Try again in a few minutes. If this response persists, contact our team for support. </td>
      </tr>
      <tr>
        <td><code>onAuthorizationCanceled</code></td>
        <td> The user chose to cancel the request. </td>
      </tr>
      <tr>
        <td><code>onAuthorizationSuccess</code></td>
        <td> If a user's access and identity tokens are valid then they are authenticated. Email verification is required if their tokens are null. </td>
      </tr>
    </tbody>
  </table>

### Forgot Password

Allow users to request a temporary password should they forget theirs or need to update it for any reason.

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the forgot password flow.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Understanding this command's response </th>
    </thead>
    <tbody>
      <tr>
        <td><code>onAuthorizationFailure</code> </td>
        <td> Something went wrong. Try again in a few minutes. If this response persists, contact our team for support. </td>
      </tr>
      <tr>
        <td><code>onAuthorizationCanceled</code></td>
        <td> The user chose to cancel the request. </td>
      </tr>
      <tr>
        <td><code>onAuthorizationSuccess</code></td>
        <td> The access and identity tokens are no longer valid and the user will need to use their new password to gain access to the app. </td>
      </tr>
    </tbody>
  </table>

### Change Details

Allow users to edit their account details such as their name and email.

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the change details flow.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
       }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Understanding this command's response </th>
    </thead>
    <tbody>
      <tr>
        <td><code>onAuthorizationFailure</code> </td>
        <td> Something went wrong. Try again in a few minutes. If this response persists, contact our team for support. </td>
      </tr>
      <tr>
        <td><code>onAuthorizationCanceled</code></td>
        <td> The user chose to cancel the request. </td>
      </tr>
      <tr>
        <td><code>onAuthorizationSuccess</code></td>
        <td> The user was authenticated. You receive new access and identity tokens for the user. </td>
      </tr>
    </tbody>
  </table>

### Change Password

Let your users know when their password is updated.

1. Set **Allow users to sign up and reset their password** to **On** in the settings for cloud directory.
2. Call the LoginWidget to start the change password flow.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
       }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Understanding this command's response </th>
    </thead>
    <tbody>
      <tr>
        <td><code>onAuthorizationFailure</code> </td>
        <td> Something went wrong. Try again in a few minutes. If this response persists, contact our team for support. </td>
      </tr>
      <tr>
        <td><code>onAuthorizationCanceled</code></td>
        <td> The user chose to cancel the request. </td>
      </tr>
      <tr>
        <td><code>onAuthorizationSuccess</code></td>
        <td> The user was authenticated. You receive new access and identity tokens for the user. </td>
      </tr>
    </tbody>
  </table>

</br>
</br>
</br>

## Managing cloud directory with the Node.js SDK
{: #managing-nodejs}

You can use the Node.js SDK to manage cloud directory as an identity provider.

### Sign in customization

You can configure the sign in screen with your branding to create a more cohesive app experience for your users.

1. Be sure that cloud directory is set to **On** in your identity provider settings and that a callback endpoint is specified.
2. Add a post route to your app that can be called with the username and password parameters and log in by using the resource owner password.
    **Note**: WebAppStrategy allows users to log in to your web apps with a username and password. After a successful login, a user's access token is stored in the HTTP session and is available for the duration of the session. Once the HTTP session is destroyed or has expired, the token is no longer valid.
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
      <th colspan=2><img src="images/idea.png"/> Understanding this commands components </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> Set this value to the URL where you want to redirect a user after successful authentication. The default is the original request URL. Example: <code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td> Set this value to the URL where you want to redirect a user if their authentication fails. The default is the original request URL.</td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td> Set this value to <code>true</code> to receive an error message that is returned from Cloud Directory. The default value is false. </td>
      </tr>
     </tbody>
  </table>

    **Note**:
      * If you submit the request using an HTML form, use [body-parser](https://www.npmjs.com/package/body-parser) middleware
      * You can use [connect-flash](https://www.npmjs.com/package/connect-flash) for getting the returned error message. See the `web-app-sample-server.js`.

### Sign up

Allow users to sign up for your app with their email and a password.

1. Set **Allow users to sign up and reset their password** to **On** in the cloud directory settings. If this is set to no, the process ends without retreiving access and identity tokens.
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Understanding this commands components </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> Set this value to the URL where you want to redirect a user after successful authentication. The default is the original request URL. Example: <code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> show </code></td>
        <td> Set this value to your sign up page. </td>
      </tr>
     </tbody>
  </table>

### Forgot Password

Allow users to request a temporary password should they forget theirs or need to update it for any reason.

1. Set **Allow users to sign up and reset their password** and **Forgot password email** to **ON** in the cloud directory settings. If this is set to no, the process ends without retrieving access and identity tokens.
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Understanding this commands components </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> Set this value to the URL where you want to redirect a user after successful authentication. The default is the original request URL. Example: <code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> show </code></td>
        <td> Set this value to your forgotten password message. </td>
      </tr>
     </tbody>
  </table>


### Change Details

Allow users to edit their account details such as their name and email.

1. Set **Allow users to sign up and reset their password** to **On** in the cloud directory settings
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Understanding this commands components </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> Set this value to the URL where you want to redirect a user after successful authentication. The default is the original request URL. Example: <code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> show </code></td>
        <td> Set this value to your account details page. </td>
      </tr>
     </tbody>
  </table>

### Change Password

Let your users know when their password is updated.

1. Set **Allow users to sign up and reset their password** to **On** in the cloud directory settings.
2. Pass the WebAppStrategy `show` property and set it to `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Understanding this commands components </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> Set this value to the URL where you want to redirect a user after successful authentication. The default is the original request URL. Example: <code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> show </code></td>
        <td> Set this value to your change password message. </td>
      </tr>
     </tbody>
  </table>

