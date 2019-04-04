---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}


# Configuring Cloud Directory
{: #cloud-directory}

With {{site.data.keyword.appid_full}}, users can sign up and sign in to your mobile and web apps by using an email or username and a password. A cloud directory is a user registry that is maintained in the cloud. When a user signs up for your app, they're added to your directory of users. With this feature, users have the freedom to manage their own account within your app.
{: shortdesc}


## Managing directory settings
{: #cd-settings}

You can configure the notifications and level of user control for your app. Setting up Cloud Directory can be done quickly, as shown in the following image. These settings can be updated at any time from the service dashboard and are reflected in your app without any code change required.
{: shortdesc}


![Configuring cloud directory](images/cloud-directory.png)
Figure. The configuration journey for Cloud Directory


1. Navigate to the **Manage authentications** tab of the {{site.data.keyword.appid_short_notm}} dashboard, be sure that Cloud Directory is set to **On**.

2. In the **Cloud Directory > Settings** tab, set **Allow users to sign up and sign in** to either **Email and password** or **User name and password**. User's can either sign in with an email that they already possess or create a user name to use when they interact with your app.

  You can toggle between the options before users are added to your directory. After the first user is added, future users must also use the same configuration.
  {: note}

2. Decide whether you want your users to create a username or use their email when they sign in. Both options require a password. After users are added to your directory, you can no longer toggle between the options.

3. Click **Edit** in the password criteria row to specify any requirements that you want to put in place. Password criteria is given as regex. For help determining strength or to see common examples see, [Managing password strength](/docs/services/appid?topic=appid-cd-passwords#cd-strength). Click **Save** to put your requirements into action.

4. Set **Allow users to sign up to your app** to **Yes**. You can still add users through the console if it's set to **No**. However, you it's most common to add users through the console for development purposes only.

5. Set **Allow users to manage their account from your app** to **Yes** if you want your users to be able to reset their password, change their password, or reset their details. If you want to limit your user's self-service ability, set the value to **No**.

6. Configure your email settings. Click **Edit** in the **Sender details** row to update your email settings. The email settings apply for all of the communication that is sent through {{site.data.keyword.appid_short_notm}}.

    1. Specify the email address that should send the email. If you choose to change the default, the email might be sent to a user's spam folder.

    2. Add a name for the Sender.

    3. Enter an email that can be used to send a response.

    4. Click **Save**.
