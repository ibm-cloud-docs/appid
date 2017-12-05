---

copyright:
  years: 2017
lastupdated: "2017-12-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Managing Cloud Directory
{: #cd}

You can configure {{site.data.keyword.appid_short_notm}} to use Cloud Directory as an identity provider. When users sign in with their email and a password, they are added to your directory and you can manage your users from the service GUI.
{: shortdesc}

<!--- What is a cloud directory? --->

## Managing directory settings

You can configure the notifications and level of user control for your app. In the **Directory Settings** tab of the GUI, you can decide how much self service your users will be able to do.

1. To allow users to use an email to sign up, you must set **Allow users to sign up and reset their password** to **On**. You can still add users through the console when it's set to **Off**, but only for development purposes.
2. Configure your sender details. Specify the email that will send the messages, who will appear as the sender, and to whom your users can reply.
  **Note**: Be sure when configuring your action URL that you give enough time for a user to click the link. A user must verify their email to have certain options, such as the ability to request a reset of their password.
3. Determine the types of emails a user receives and the sender information.



## Managing messages

A template is an example of an email message that you may send to your users. You can customize the template by updating the content and layout of the message. You can set these messages to **On** or **Off** in the directory settings tab.

1. Select a **Message type**.
2. Customize your message by changing the content and design of the message. You can use parameters to personalize your messages. Don't forget to save your changes!

### Types of messages

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



## Managing Cloud Directory with the Android SDK
{: #managing-android}

Be sure to set **Cloud Directory identity provider** to **ON** when using the following APIs.

### Login using Resource Owner Password
You can obtain an access and ID token by supplying the end user's username and password.

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

### Sign Up

Make sure to set **Allow users to sign up and reset their password** to **ON** in the settings for Cloud Directory.

 Use the LoginWidget class to start the sign up flow.
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
			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
				 if (accessToken != null && identityToken != null) {
				     //User authenticated
				 } else {
				     //email verification is required
				 }

			 }
		 });
 ```
 {: codeblock}

### Forgot Password
Be sure to set **Allow users to sign up and reset their password** and **Forgot password email** to **ON** in the settings for Cloud Directory.

Use the LoginWidget class to start the forgot password flow.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
 			 public void onAuthorizationFailure (AuthorizationException exception) {
 				 //Exception occurred
 			 }

 			 @Override
 			 public void onAuthorizationCanceled () {
 				 //forogt password canceled by the user
 			 }

 			 @Override
 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
 				 //forgot password finished, in this case accessToken and identityToken will be null.

 			 }
 		 });
  ```
  {: codeblock}

### Change Details
Be sure to set **Allow users to sign up and reset their password** to **ON** in the settings for Cloud Directory. Use the LoginWidget class to start the change details flow. This API can be used only when the user logs in by using Cloud Directory as their identity provider.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  				 //Exception occurred
  			 }

  			 @Override
  			 public void onAuthorizationCanceled () {
  				 //changed details canceled by the user
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  				 //User authenticated, and fresh tokens received
  			 }
  		 });
   ```
   {: codeblock}

### Change Password
Make sure to set **Allow users to sign up and reset their password** to **ON**, in the settings for Cloud Directory.

Use the LoginWidget class to start the change password flow. This API can be used only when the user logged in by using Cloud Directory as their identity provider.

   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   				 //Exception occurred
   			 }

   			 @Override
   			 public void onAuthorizationCanceled () {
   				 //change password canceled by the user
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   				   //User authenticated, and fresh tokens received
   			 }
   		 });
   ```
   {: codeblock}

## Managing Cloud Directory with the iOS Swift SDK


### Login using Resource Owner Password

You can obtain an access and ID token by supplying the end user's username and password.
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

### Sign Up

Make sure to set **Allow users to sign up and reset their password** to **ON**, in the settings for Cloud Directory.

Use the LoginWidget class to start the sign up flow.
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

### Forgot Password
Make sure to set **Allow users to sign up and reset their password** and **Forgot password email** to **ON** in the settings for Cloud Directory.

Use the LoginWidget class to start the forgot password flow.
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

### Change Details

Make sure to set **Allow users to sign up and reset their password** to **ON** in the settings for Cloud Directory.

Use the LoginWidget class to start the change details flow. This API can be used only when the user logs in by using Cloud Directory as their identity provider.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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

### Change Password

Make sure to set **Allow users to sign up and reset their password** to **ON** in the settings for Cloud Directory.

Use the LoginWidget class to start the change password flow. This API can be used only when the user logs in by using Cloud Directory as an identity provider.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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


## Managing Cloud Directory with the Node.js SDK
Make sure that the Cloud Directory identity provider is set to **ON** and include the callback endpoint.

### Login using resource owner password flow
WebAppStrategy allows users to login to your web application by using a username and password.
After a successful login, the user's access token is persisted in the HTTP session, and is available as long as the HTTP session is kept alive. Once the HTTP session is destroyed or expired, the token is destroyed as well.

To allow user's to login using a username and password, add to your app a post route that will be called with the username and password parameters.

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
  * If you submit the request using an HTML form, use [body-parser](https://www.npmjs.com/package/body-parser) middleware.
  * Use [connect-flash](https://www.npmjs.com/package/connect-flash) for getting the returned error message. See the `web-app-sample-server.js`.

### Sign up
To launch the {{site.data.keyword.appid_short_notm}} sign up form, pass the WebAppStrategy "show" property and set it to `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

    **Note**:
    * If in your Cloud directory settings, **Allow users to sign-in without email verification** is set to **No**, the process ends without retrieving {{site.data.keyword.appid_short_notm}} access and ID tokens.
    * Be sure to set **Allow users to sign up and reset their password** to **ON** in the Cloud directory settings.


### Forgot Password
To launch the {{site.data.keyword.appid_short_notm}} forgot password form, pass the WebAppStrategy `show` property and set it to `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

**Note**:
* If in your Cloud directory settings, **Allow users to sign-in without email verification** is set to **No**, the process ends without retrieving {{site.data.keyword.appid_short_notm}} access and ID tokens.
* Be sure to set **Allow users to sign up and reset their password** and **Forgot password email** to **ON** in the Cloud directory settings.

### Change Details
To launch the {{site.data.keyword.appid_short_notm}} change details form, pass the WebAppStrategy `show` property and set it to `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

**Note**:
* A user must be authenticated by using Cloud Directory as the identity provider.
* Be sure to set **Allow users to sign up and reset their password** to **ON** in the Cloud directory settings.


### Change Password
To launch the {{site.data.keyword.appid_short_notm}} change password form, pass the WebAppStrategy `show` property and set it to `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

**Note**:
* A user must be authenticated by using Cloud Directory as the identity provider.
* Be sure to set **Allow users to sign up and reset their password** to **ON** in the Cloud directory settings.
