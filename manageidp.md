---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-04"

keywords: identity provider, idp, app security, mobile app, web app, authentication, authorization, oidc, saml, protocols, facebook, google, w3id, cloud directory, redirect url, redirect uri, token configuration, token lifetime, log in configuration

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
{:terraform: .ph data-hd-interface='terraform'}
{:release-note: data-hd-content-type='release-note'}

# Managing authentication
{: #managing-idp}

Identity providers (IdP's) add a level of security for your mobile and web apps, through authentication. With {{site.data.keyword.appid_full}}, you can configure one or several identity providers to create a custom sign-in experience for your users.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} interacts with identity providers by using various protocols such as OpenID Connect, SAML, and more. For example, OpenID Connect is the protocol that is used with many social providers such as Facebook, Google. Enterprise providers such as [Azure Active Directory](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory){: external} or [Active Directory Federation Service](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service){: external}, generally use SAML as their identity protocol. For [Cloud Directory](/docs/appid?topic=appid-cloud-directory), the service uses SCIM to verify identity information.

When you use social or enterprise identity providers, {{site.data.keyword.appid_short_notm}} reads user account information. Because the service never has write access to the information, users must go through their chosen identity provider to do actions, such as resetting their password. For example, if a user signs in to your app with Facebook, and then wanted to change their password, they must go to `www.facebook.com` to do so.
{: note}

When you use [Cloud Directory](/docs/appid?topic=appid-cloud-directory), {{site.data.keyword.appid_short_notm}} is the identity provider. The service uses your registry to verify your users identity. Because {{site.data.keyword.appid_short_notm}} is the identity provider, users can take advantage of advanced functionality, such as resetting their password, directly in your app.

Working with application identity? Check out [Application identity](/docs/appid?topic=appid-app).
{: tip}

Several identity providers can be configured to be used by {{site.data.keyword.appid_short_notm}}. Check out the following table to learn about your options.

| Identity provider | Type | Description | 
|-----|----| -----| 
| [Cloud Directory](/docs/appid?topic=appid-cloud-directory) | Managed registry | You can maintain your own user registry in the cloud. When a user signs up for your app, they are added to your directory of users. This option gives your users more freedom to manage their own account within your app. | 
| [SAML](/docs/appid?topic=appid-enterprise#enterprise) | Enterprise | You can create a single sign-on experience for your users. |
| [Facebook](/docs/appid?topic=appid-social#facebook) | Social | Users can sign in to your app by using their Facebook credentials. |
| [Google+](/docs/appid?topic=appid-social#google) | Social | Users can sign in to your app by using their Google credentials. | 
| [Custom](/docs/appid?topic=appid-custom-identity#custom-identity) | Custom | If none of the provided options fit your specific need, you can configure your own identity flow to work with {{site.data.keyword.appid_short_notm}}. |
{: caption="Table 1. Identity provider options" caption-side="top"}

## Managing providers
{: #managing-providers}
{: help}
{: support}

An identity provider creates and manages information about an entity such as a user, a functional ID, or an application. The provider verifies the identity of the entity by using credentials, such as a password. Then, the IdP sends the identity information back to {{site.data.keyword.appid_short_notm}}, which authorizes the user and then grants access to your app.
{: shortdesc}

1. Navigate to your service dashboard.
2. In the **Identity Providers** section of the navigation, select the **Manage** page.
3. On the **Identity Providers** tab, set the providers that you want to use, to **On**.
4. Optional: Decide whether to turn off **Anonymous users**, or leave the default, which is **On**. When set to **On**, user attributes are associated with the user from the moment they begin interacting with your app. For more information about the path to becoming an identified user, see [Progressive authentication](/docs/appid?topic=appid-anonymous#progressive).

{{site.data.keyword.appid_short_notm}} provides default credentials to help with your initial setup of Facebook and Google+. You are limited to 20 uses of the credentials per instance, per day. Because they are IBM credentials, they are meant to be used only for development. Before you publish your app, update the configuration to your own credentials.
{: tip}


## Adding redirect URIs
{: #add-redirect-uri}

Your application redirects users to {{site.data.keyword.appid_short_notm}} for authentication. After authentication completes, {{site.data.keyword.appid_short_notm}} redirects users back to your application. In order for {{site.data.keyword.appid_short_notm}} to be able to redirect users back to your app, you need to register the redirect URI. During the sign-in flow, {{site.data.keyword.appid_short_notm}} validates the URIs before it allows clients to participate in the authorization workflow, which helps to prevent phishing attacks and grant code leakage. By registering your URI, you're telling {{site.data.keyword.appid_short_notm}} that the URI is trusted and it's OK to redirect your users.

1. Click **Authentication Settings** to see your URI and token configuration options.

2. In the **Add web redirect URI** field, type the URI. Each URI must begin with `http://` or `https://` and must include the full path, including any query parameters for the redirect to be successful. Need help formatting your URI? Check out the following table for some examples.

   | Type | Example URI |
   | ---- | ----------- |
   | Custom domain | `https://mydomain.net/myapp2path/appid_callback` |
   | Ingress subdomain | `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback` |
   | Wildcard | `https://mydomain.net/*`  \n ***Note: Wildcards are not recommended for use in production apps.*** | 
   {: caption="Table 2. Example web redirect URIs" caption-side="top"}

   It is recommended that you always use encryption and avoid HTTP.
   {: note}

3. Click the **+** symbol in the **Add web redirect URI's** box.

   Be sure to register only URIs of applications that you trust.
   {: important}

4. Repeat steps one through three until all possible URIs are added to your list.


## Configuring token lifetime
{: #idp-token-lifetime}
{: help}
{: support}

{{site.data.keyword.appid_short_notm}} uses tokens to identify users and secure your resources. You can adjust your configuration to fit your applications needs by setting the lifespan of the tokens. Token lifetime begins again each time a user signs in. For example, you set your refresh token lifetime to 10 days. An access token and a refresh token are created when the user signs in for the first time. If the user returns to your app 3 days later, they wouldn't need to sign in again. But, if the user waited 12 days after their initial sign-in, and then returned to your app, they would need to sign in again. For more information about tokens, check out [Understanding tokens](/docs/appid?topic=appid-tokens#tokens).

When you set token expiration, the values apply to all the providers that you make available. If you want to customize your tokens further, try calling the API to [map custom claims](/docs/appid?topic=appid-customizing-tokens) so that the user information is available at run time. When you work with the API, the customization times are configured differently.
{: tip}

1. Go to the **Manage Authentication > Authentication settings** tab of the service dashboard.
2. In the **Sign-in Expiration** tab, toggle refresh token to **Enabled**.
3. For each token type, add a value for each token type as described in the following table.

   | Token type | Description | Default | Options |
   | ---------- | ----------- | ------- | ------- |
   | [Access](/docs/appid?topic=appid-tokens#access) | The length of time for which access tokens are valid. The smaller the value, the more protection that you have in cases of token theft. | 60 minutes | Any value in the range 5 - 1440 |
   | [Refresh](/docs/appid?topic=appid-tokens#refresh) | The length of time for which refresh tokens are valid. The smaller the number, the more frequently a user must sign themselves in. | 30 days | Any value in the range 1 - 90 | 
   | [Anonymous](/docs/appid?topic=appid-anonymous) | The length of time for which anonymous tokens are valid. Anonymous tokens are assigned to users the moment that they begin interacting with your app. When a user signs in, the information in the anonymous token is then transferred to the token associated with the user. | 30 days | Any value in the range 1 - 90 | 
   {: caption="Table 3. Token types and customization options" caption-side="top"}

   [Identity tokens](/docs/appid?topic=appid-tokens#identity) are automatically configured to match the length of time that you set for access tokens. The values cannot be different.
   {: tip}

4. Click **Save**. 




