---

copyright:
  years: 2017, 2026
lastupdated: "2026-03-04"

keywords: user registry, sign up, sign in, username, email, password, account settings, reset password, email sender, email verification, app security

subcollection: appid

---

{{site.data.keyword.attribute-definition-list}}


# Configuring Cloud Directory
{: #cloud-directory}

With {{site.data.keyword.appid_full}}, you can create a scalable user registry for your apps so that users can sign up and sign in with either a username or email and a password. You can decide the level of self-service that you want your users to have. For example, users can sign up for your app independently or you can allow them to manage their account settings, such as a password reset, from your app. 
{: shortdesc}


## Managing directory settings
{: #cd-settings}

You can configure the level of self-service that is allowed in your application by using the service dashboard. The settings can be updated at any time and are reflected in your app without any required change to your code or redeploy of your application.
{: shortdesc}

1. Go to **Manage authentication** in the {{site.data.keyword.appid_short_notm}} dashboard and toggle **Cloud Directory** to **Enabled**. You can also enable other providers but to offer Cloud Directory as an option in the Login Widget, it must be enabled.

2. Go to **Authentication Settings** and configure your redirect URIs and sign in expiration settings. For more information about the settings, see [Managing authentication](/docs/appid?topic=appid-managing-idp)

3. Go to **Cloud Directory > Settings**.

4. Select the way that your want to **Allow users to sign-up and sign-in** to your app. Options include **Email and password** or **Username and password**. User's can sign in with either an email that they already possess or they can create a username to use when they interact with your app.

   You can toggle between the options before users are added to your directory. After the first user is added, future users must also use the same configuration. To add future users to your application, you must use the **Email and password** configuration.
   {: note}

5. Set **Allow users to sign up to your app** to **Yes**. If you choose not to allow users to sign up, you can add users through the dashboard or the management API for development purposes.

6. To provide the highest level of self-service, set **Allow users to manage their account from your app** to **Yes**. When set to yes, users are able to reset or change their password, or reset their details. If you want to limit your user's self-service ability, set the value to **No**.
