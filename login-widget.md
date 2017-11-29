---

copyright:
  years: 2017
lastupdated: "2017-11-29"

---
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# The login widget

## Customizing the login widget
{: #login-widget}

You can configure your login widget to display the logo and colors of your choice.
{:shortdesc}

When the {{site.data.keyword.appid_short}} service is configured with two or more identity providers, the user can select an identity provider in the login widget. You can customize your login widget by completing the following steps:

1. Open the {{site.data.keyword.appid_short_notm}} service dashboard.
2. Select the **Login Customization** section, where you can modify the appearance of the login widget to align with your company's brand.
3. Upload your company's logo by selecting a PNG or JPG file from your local system. The recommended image size is 320 x 320 pixels. The maximum file size is 100 Kb.
4. Select a header color for the widget from the color picker, or enter the hex code for another color.
5. Inspect the preview pane, and click **Save Changes** when you are happy with your customizations. A confirmation message is displayed.

**Note**: You are not required to rebuild your application. The image is stored in the {{site.data.keyword.appid_short}} database and is displayed at the next login.

## Running the login widget with the Android SDK
{: #authenticate-android}

When you configure more than one identity provider, users are shown a login widget upon visiting your app. As a default, if you configure only one, the user is redirected to the configured identity providers authentication screen.


After the {{site.data.keyword.appid_short_notm}} client SDK is initialized, you can authenticate your users by running the login widget.

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
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //User authenticated
        }
      });
  ```
  {: codeblock}

## Running the login widget with the iOS SDK
{: #authenticate-ios}

When you configure more than one identity provider, users are shown a login widget upon visiting your app. As a default, if you configure only one, the user is redirected to the configured identity providers authentication screen.


1. Add the following import to the file in which you want to use the SDK.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Run the following command to launch the widget.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
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
