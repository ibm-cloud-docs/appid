
---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}

# IBMid
{: #ibmid}

You can integrate IBMid into {{site.data.keyword.appid_short_notm}} as your identity provider. IBMid is an OAuth2, OIDC identity provider that can help you to manage user identities for your enterprise applications by authenticating your users.
{: shortdesc}


At the moment, this feature is available in the IBM Cloud staging environment. If you have a need to use this feature in a production environment, please contact the {{site.data.keyword.appid_short_notm}} development team in the #appid-adopters channel on Slack.
{: note}


## Understanding the default settings
{: #default}

Out-of-the-box {{site.data.keyword.appid_short_notm}} is configured with default settings to help you get up and running quickly. The default should be used for testing purposes **only**.
{: shortdesc}

Because the default configuration is provided by IBM, there are strict usage limitations that can be used:

## Registering with {{site.data.keyword.appid_short_notm}}

**Before you begin**

Be sure you have the following prerequisites:

* An instance of {{site.data.keyword.appid_short_notm}}
* The redirect URL that is listed in the IBMid configuration tab of the {{site.data.keyword.appid_short_notm}} dashboard.


**To register with IBMid:**

1. Navigate to the [SSO Self-Service Provisioner](https://w3.innovate.ibm.com/tools/sso/home.html).
2. Click the **Register a IBMid application** tab. Be sure that you understand IBM's privacy statement and then click **Accept**.
3. Enter your information into the required fields and click **Next**.
4. On the IBMid Protocol Selection page, leave the default **Use IBMid OpenID Connect OpenID Connect 1.0** selected. Click **Next**.
5. Select the provider that matches your stage of development. Click **Next**.
6. Enter your **IBMid OIDC Client Details**.
  1. Specify a unique **Client Name**.
    This cannot be edited later.
    {: tip}
  2. Copy the **Client ID** and **Client Secret** that are generated for you and save them for a later step.
  3. Enter the **Redirect URIs** that you obtained before you got started.
  4. Specify the **Grant Types** that you want to use by checking one or more boxes.
  5. Make a note the provided **Endpoints**.
  5. Click **Next**.

7. Review your configuration and check **I agree Terms of Use for IBMid**.
8. Click **Finish**.


**Configuring {{site.data.keyword.appid_short_notm}}:**

1. Sign in to your IBM Cloud account and navigate to your instance of {{site.data.keyword.appid_short_notm}}.
2. From the list of **Identity Providers**, select **IBMid**.
3. Enter the Client ID and secret that you saved in step 6 of registering with IBMid.
4. Select the provider that matches your phase of development.
5. Click **Save**.


## Next steps
{: #steps}

Now that your IBMid configuration is complete, you can integrate {{site.data.keyword.appid_short_notm}} into your [web](web-apps.html) or [mobile](mobile-apps.html) application, learn about [tokens](tokens.html), or start building [user profiles](user-profile.html).
