---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-29"

keywords: facebook, google, social, identity providers, single sign on, default configuration, authentication, authorization, identity, app security, idp, default credentials

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

# Social
{: #social}

With {{site.data.keyword.appid_full}}, you can configure social identity providers to set up a single sign-on experience for your app. By allowing a user to sign in with their social profiles, they no longer have to remember several different passwords for different applications.
{: shortdesc}


## Default configuration
{: #social-default}

{{site.data.keyword.appid_short_notm}} provides a default configuration to help you get up and running quickly with the service.
{: shortdesc}

Data is used when you engage in the Permitted Uses of the Service. By using the Service, you agree to adopting the policy for the collection and use of information in accordance with the outlined [privacy policy](/docs/appid?topic=appid-privacy-policy).
{: important}


When you configure {{site.data.keyword.appid_short_notm}}, Facebook, Google, and Cloud Directory are automatically enabled as identity providers. You can change the configuration at anytime. There are default credentials in place for Facebook and Google, but they are IBM credentials and should be used for testing whether to use the service only. Before you publish your app, update the configuration to your own credentials.

You are limited to 20 authentications with the default credentials per instance, per day.
{: note}


## Configuring Facebook
{: #facebook}

You can configure the {{site.data.keyword.appid_short_notm}} service to use Facebook as an identity provider.
{: shortdesc}

### Getting an app ID and secret from Facebook
{: #facebook-appid-secret}

To use Facebook as an identity provider, you must add and configure the website platform on your Facebook application.

1. Log in to your account on the [Facebook for Developers site](https://developers.facebook.com/docs/development){: external}.
2. Make note of the Facebook app ID and secret. These values are needed to configure your web project for authentication in your service dashboard.
3. Add the web platform and enter the site URL.
4. From the products list, select **Facebook Login**.
5. In the **Valid OAuth redirect URLs** field, enter the authorization server callback endpoint URL.
6. Click **Save Changes**.


### Configuring {{site.data.keyword.appid_short_notm}} for Facebook authentication
{: #facebook-configure}

When you have your Facebook app ID and secret, and your Facebook for Developers app is configured to serve web clients, you can edit the Facebook authentication in your service dashboard.

1. From the **Manage** tab of your service dashboard, select **Facebook** and click **Edit**.
2. Enter the Facebook app ID and secret that you obtained from the Facebook for Developers website.
3. Copy the URI that is in the **Redirect URI for Facebook for Developers** field. Paste the URI into the **Valid OAuth redirect URIs** field in the **Facebook Login** section of the Facebook Developers Portal.
4. Click **Save**.
5. Optional: For web apps, enter the redirect URL in the **Web Application Redirect URLs** field. This value is determined by the developer and used to access the redirect URL after the authorization process is completed. The URL must follow an `http` or `https` scheme. For a higher level of security, use an `https` scheme.


## Configuring Google
{: #google}

You can configure the {{site.data.keyword.appid_short_notm}} service to use Google as an identity provider.
{: shortdesc}

### Getting a client ID and secret
{: #google-clientid-secret}

Google documentation [link](https://developers.google.com/identity/gsi/web/guides/get-google-api-clientid){: external}

Create a project in the [Google Developers Console](https://console.cloud.google.com/home/dashboard?project=app-id-login&folder=&organizationId=){: external}, configure the project to serve web clients, and obtain a client ID and secret.

1. Create a project.
2. Open [credentials page](https://console.developers.google.com/apis){: external} of the Google APIs console.
3. If your project doesn't have a Web application-type client ID, click **Create credentials > OAuth client ID**.
4. Configure your level of consent.
5. In the **Authorized JavaScript Origins** field, input your site's domain.
6. Click **Create**.
7. Copy **Your Client ID** and **Your Client Secret**

### Configuring {{site.data.keyword.appid_short_notm}} for Google authentication
{: #google-configure}

After you configure your Google project and have your client ID and secret, you can edit your service dashboard for Google authentication.

1. From the **Manage** page of your service dashboard, select **Google** and click **Edit**.
2. Enter the client ID and secret that you obtained from the Google Developers Console.
3. Authorize the {{site.data.keyword.appid_short_notm}} URL.
   1. Copy the **Redirect URL for Google Developer Console** from the Google identity provider details.
   2. On the credentials page of your Google project, select the client ID that you created for this integration.
   3. Paste the URL from {{site.data.keyword.appid_short}} into the **Authorized redirect URIs** field and click **Save**.
4. Click **Save** to update your Google configuration in {{site.data.keyword.appid_short_notm}}.
5. For web apps, enter a redirect URL in the **Manage** tab. After the authorization process completes, a user is sent to this URL. The URL must follow an `http` or `https` scheme. For a higher level of security, use an `https` scheme.





