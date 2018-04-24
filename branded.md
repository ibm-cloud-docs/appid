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

# Branding the sign-in experience
{: #branding}

You can display your own customized screens and take advantage of the authentication and authorization capabilities of {{site.data.keyword.appid_full}}. With cloud directory as your identity provider, your users are able to interact with your app with less help from you. They're able to sign inwithout asking for help.
{: shortdesc}

When you use your own screens, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) is used to provide access and identity tokens.


## Displaying customized screens with the Android SDK
{: #branded-ui-android}

With cloud directory enabled, you can call customized screens with the Android SDK.  <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Check out this blog! <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
{: shortdesc}

</br>
**Sign in**

1. Set **Cloud Directory** to **On** as an identity provider.
2. Place the following command in your code.
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
  {: pre}

</br>
</br>

## Displaying customized screens with the iOS Swift SDK
{: #branded-ui-ios-swift}

With cloud directory enabled, you can call customized screens with the iOS Swift SDK. 
{: shortdesc}

</br>
**Sign in**

1. In the identity provider tab on the GUI, set cloud directory to **On**.
2. Log in by using the resource owner password. Access and identity tokens are obtained when a user attempts to log in by using their username and password.
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
  {: pre}


</br>
</br>

## Displaying customized screens with the Node.js SDK
{: #branded-ui-nodejs}

With cloud directory enabled, you can call customized screens with the Node.js SDK. 
{: shortdesc}

**Sign in**
1. Set cloud directory to **On** in your identity provider settings and specify a callback endpoint.
2. Add a post route to your app that can be called with the username and password parameters and log in by using the resource owner password.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // allow flash messages
    }));
    ```
    {: pre}
    `WebAppStrategy` allows users to sign in to your web apps with a username and password. After a successful login, a user's access token is stored in the HTTP session and is available during the session. Once the HTTP session is destroyed or expired, the token is invalid.
    {: tip}

