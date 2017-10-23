---

copyright:
  years: 2017
lastupdated: "2017-10-23"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Configuring identity providers
{: #setting-up-idp}

You can configure Facebook, Google, or a combination of the two to set up a single sign-on experience for your users. By using an identity provider, users are able to sign in with credentials they are already familiar with.

{:shortdesc}



## Configuring Facebook authentication
{: #facebook}

Configure the {{site.data.keyword.appid_short}} service to use Facebook as an identity provider.


### Getting an app ID and secret from Facebook
{: #getting-facebook-appid}

To use Facebook as an identity provider, you must add and configure the website platform on your Facebook application.

1. Log in to your account on the <a href="https://developers.facebook.com/docs/apps/register" target="blank">Facebook for Developers site <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Make note of the Facebook app ID and secret. These values are needed to configure your web project for authentication in your service dashboard.
3. Add the web platform and enter the site URL.
4. From the products list, select **Facebook Login**.
5. In the Valid OAuth redirect URLs field, enter the authorization server callback endpoint URL. After configuring your service instance, you can add this value.
6. Click **Save Changes**.

### Configuring {{site.data.keyword.appid_short_notm}} for Facebook authentication
{: #configuring-facebook-appid}

When you have your Facebook app ID and secret, and your Facebook for Developers app is configured to serve web clients, you can edit the Facebook authentication in your service dashboard.

1. From the **Manage** tab of your service dashboard, select **Facebook** and click **Edit**.
2. Enter the Facebook app ID and secret that you obtained from the Facebook for Developers website.
3. Copy the URI that is in the **Redirect URI for Facebook for Developers** field. Paste the URI into the **Valid OAuth redirect URIs** field in the **Facebook Login** section of the Facebook Developers Portal.
4. Click **Save**.
5. Optional: For web apps, enter the redirect URL in the **Web Application Redirect URLs** field. This value is determined by the developer and used to access the redirect URL after the authorization process is completed.


