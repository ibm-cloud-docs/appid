---

copyright:
  years: 2017, 2018
lastupdated: "2017-01-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Configuring social identity providers
{: #setting-up-idp}

Identity providers provide an extra level of authentication for your mobile and web apps. With {{site.data.keyword.appid_full}} you can configure one or several identity providers to set up a single sign-on experience for your app.
{: shortdesc}

## Default configuration
{: #default}

{{site.data.keyword.appid_short_notm}} provides a default configuration to help with the initial set up of your identity providers.
{: shortdesc}

The default credentials are set up for Facebook and Google. You are limited to 100 uses of the credentials per instance, per day. Because they are IBM credentials, they should be used in your apps only in development mode. Prior to publishing your app, [update the configuration to your own credentials](/docs/services/appid/identity-providers.html).


## Configuring Facebook
{: #facebook}

You can configure the {{site.data.keyword.appid_short}} service to use Facebook as an identity provider.
{: shortdesc}

### Getting an app ID and secret from Facebook

To use Facebook as an identity provider, you must add and configure the website platform on your Facebook application.

1. Log in to your account on the <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for developers site <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Make note of the Facebook app ID and secret. These values are needed to configure your web project for authentication in your service dashboard.
3. Add the web platform and enter the site URL.
4. From the products list, select **Facebook Login**.
5. In the Valid OAuth redirect URLs field, enter the authorization server callback endpoint URL. After configuring your service instance, you can add this value.
6. Click **Save Changes**.


### Configuring {{site.data.keyword.appid_short_notm}} for Facebook authentication

When you have your Facebook app ID and secret, and your Facebook for Developers app is configured to serve web clients, you can edit the Facebook authentication in your service dashboard.

1. From the **Manage** tab of your service dashboard, select **Facebook** and click **Edit**.
2. Enter the Facebook app ID and secret that you obtained from the Facebook for Developers website.
3. Copy the URI that is in the **Redirect URI for Facebook for Developers** field. Paste the URI into the **Valid OAuth redirect URIs** field in the **Facebook Login** section of the Facebook Developers Portal.
4. Click **Save**.
5. Optional: For web apps, enter the redirect URL in the **Web Application Redirect URLs** field. This value is determined by the developer and used to access the redirect URL after the authorization process is completed.


## Configuring Google
{: #google}

You can configure the {{site.data.keyword.appid_short}} service to use Google as an identity provider.
{: shortdesc}

### Getting a client ID and secret from Google

Create a project in the <a href="https://developers.google.com/" target="_blank">Google Developers Console <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, configure the project to serve web clients, and obtain a client ID and secret.

1. Create a project.
2. Add the Google+ API to your Google project.
3. Add credentials to the Google+ API.
    1. Select Google+ API as the type of API.
    2. Select **Web Browser** as where you'll be calling the API.
    3. Choose **User data**.
    4. Fill out the required fields to create a client ID. A secret is created at the same time.
4. Make note of the Google client ID and secret. In the credentials tab, select the ID that you created to obtain your secret and client ID.

### Configuring {{site.data.keyword.appid_short}} for Google authentication

After you've configured your Google project and have your client ID and secret, you can edit your service dashboard for Google authentication.

1. From the **Manage** tab of your service dashboard, select **Google** and click **Edit**.
2. Enter the client ID and secret that you obtained from the Google Developers Console.
3. Authorize the {{site.data.keyword.appid_short}} URL.
    1. Copy the **Redirect URL for Google Developer Console** from the Google identity provider details.
    2. In the credentials tab of your Google project, select the client ID that you created for this integration.
    3. Paste the URL from {{site.data.keyword.appid_short}} into the **Authorized redirect URIs** field and click **Save**.
4. Click **Save** to update your Google configuration in {{site.data.keyword.appid_short}}.
5. Optional: For web apps, enter a redirect URL in the **Mangage** tab. After the authorization process completes, a user is sent to this URL.
