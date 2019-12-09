---

copyright:
  years: 2017, 2019
lastupdated: "2019-12-09"

keywords: identity provider, idp, app security, mobile app, web app, authentication, authorization, oidc, saml, protocols, facebook, google, w3id, cloud directory, redirect url, redirect uri, token configuration, token lifetime, log in configuration

subcollection: appid

---

{:external: target="_blank" .external}
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

# Managing authentication
{: #managing-idp}

Identity providers (IdP's) add a level of security for your mobile and web apps, through authentication. With {{site.data.keyword.appid_full}}, you can configure one or several identity providers to create a custom sign-in experience for your users.
{: shortdesc}


{{site.data.keyword.appid_short_notm}} interacts with identity providers by using various protocols such as OpenID Connect, SAML, and more. For example, OpenID Connect is the protocol that is used with many social providers such as Facebook, Google. Enterprise providers such as [Azure Active Directory](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory){: external}, or [Active Directory Federation Service](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service){: external}, generally use SAML as their identity protocol. For [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), the service uses SCIM to verify identity information.

When you use social or enterprise identity providers, {{site.data.keyword.appid_short_notm}} reads user account information. Because the service never has write access to the information, users must go through their chosen identity provider to do actions, such as resetting their password. For example, if a user signs in to your app with Facebook, and then wanted to change their password, they must go to `www.facebook.com` to do so.
{: note}

When you use [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), {{site.data.keyword.appid_short_notm}} is the identity provider. The service uses your registry to verify your users identity. Because {{site.data.keyword.appid_short_notm}} is the identity provider, users can take advantage of advanced functionality, such as resetting their password, directly in your app.

Working with application identity? Check out [Application identity](/docs/services/appid?topic=appid-app).
{: tip}

There are several identity providers that the service can be configured to use. Check out the following table to learn about your options.

<table>
  <caption>Table 1. Identity provider options</caption>
  <tr>
    <th>Identity provider</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)</td>
    <td>Managed registry</td>
    <td>You can maintain your own user registry in the cloud. When a user signs up for your app, they are added to your directory of users. This option gives your users more freedom to manage their own account within your app.</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid?topic=appid-enterprise#enterprise)</td>
    <td>Enterprise</td>
    <td>You can create a single sign-on experience for your users.</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid?topic=appid-social#facebook)</td>
    <td>Social</td>
    <td>Users can sign in to your app by using their Facebook credentials.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid?topic=appid-social#google)</td>
    <td>Social</td>
    <td>Users can sign in to your app by using their Google credentials.</td>
  </tr>
  <tr>
    <td>[Custom](/docs/services/appid?topic=appid-custom-identity#custom-identity)</td>
    <td> </td>
    <td>If none of the provided options fit your specific need, you can configure your own identity flow to work with {{site.data.keyword.appid_short_notm}}.</td> 
  </tr>
</table>

## Managing providers
{: #managing-providers}

An identity provider creates and manages information about an entity such as a user, a functional ID, or an application. The provider verifies the identity of the entity by using credentials, such as a password. Then, the IdP sends the identity information back to {{site.data.keyword.appid_short_notm}}, which authorizes the user and then grants access to your app.
{: shortdesc}

1. Navigate to your service dashboard.
2. In the **Identity Providers** section of the navigation, select the **Manage** page.
3. On the **Identity Providers** tab, set the providers that you want to use, to **On**.
4. Optional: Decide whether to turn off **Anonymous users**, or leave the default, which is **On**. When set to **On**, user attributes are associated with the user from the moment they begin interacting with your app. For more information about the path to becoming an identified user, see [Progressive authentication](/docs/services/appid?topic=appid-anonymous#progressive)

{{site.data.keyword.appid_short_notm}} provides default credentials to help with your initial setup of Facebook and Google+. You are limited to 20 uses of the credentials per instance, per day. Because they are IBM credentials, they are meant to be used only for development. Before you publish your app, update the configuration to your own credentials.
{: tip}


## Adding redirect URIs
{: #add-redirect-uri}

Your application redirects users to {{site.data.keyword.appid_short_notm}} for authentication. After authentication completes, {{site.data.keyword.appid_short_notm}} redirects users back to your application. In order for App ID to be able to redirect users back to your app, you need to register the redirect URI. During the sign-in flow, {{site.data.keyword.appid_short_notm}} validates the URIs before it allows clients to participate in the authorization workflow, which helps to prevent phishing attacks and grant code leakage. By registering your URI, you're telling {{site.data.keyword.appid_short_notm}} that the URI is trusted and it's OK to redirect your users.

1. Click **Authentication Settings** to see your URI and token configuration options.

2. In the **Add web redirect URI** field, type the URI. Each URI should begin with `http://` or `https://` and must include the full path, including any query parameters for the redirect to be successful. Need help formatting your URI? Check out the following table for some examples.

  <table>
    <caption>Table 2. Example web redirect URIs</caption>
    <tr>
      <th>Type</th>
      <th>Example URI</th>
    </tr>
    <tr>
      <td>Custom domain</td>
      <td><code>https://mydomain.net/myapp2path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Ingress subdomain</td>
      <td><code>https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Logout</td>
      <td><code>https://mydomain.net/myapp2path/appid_logout</code></td>
    </tr>
    <tr>
      <td>Wildcard</td>
      <td><code>https://mydomain.net/*</code> <br> Wildcards are not recommended for use in production apps.</td>
    </tr>  
  </table>

  It is recommended that you always use encryption and avoid HTTP.
  {: note}

3. Click the **+** symbol in the **Add web redirect URI's** box.

    Be sure to register only URIs of applications that you trust.
    {: important}

4. Repeat steps one through three until all possible URIs are added to your list.


Not sure where your redirect URI comes from? Watch the following short video to see where to get it and how to add it to your list.

<iframe class="embed-responsive-item" id="redirecturi" title="{{site.data.keyword.appid_short_notm}}: How to fix invalid redirect URI" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6hxqbvpc054?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>



## Configuring token lifetime
{: #idp-token-lifetime}

App ID uses tokens to identify users and secure your resources. You can adjust your configuration to fit your applications needs by setting the lifespan of the tokens. Token lifetime begins again each time a user signs in. For example, you set your refresh token lifetime to 10 days. An access token and a refresh token are created when the user signs in for the first time. If the user returns to your app 3 days later, they wouldn't need to sign in again. But, if the user waited 12 days after their initial sign-in, and then returned to your app, they would need to sign in again. For more information about tokens, check out [Understanding tokens](/docs/services/appid?topic=appid-tokens#tokens).

When you set token expiration, the values apply to all of the providers that you make available. If you want to customize your tokens further, try calling the API to [map custom claims](/docs/services/appid?topic=appid-customizing-tokens) so that the user information is available at run time. Note that when you work with the API the customization times are configured differently.
{: tip}

1. Go to the **Manage Authentication > Authentication settings** tab of the service dashboard.
2. In the **Sign-in Expiration** tab, toggle refresh token to **Enabled**.
3. For each token type, add a value for each token type as described in the following table.

  <table>
    <caption>Table 3. Token types and customization options</caption>
    <tr>
      <th>Token type</th>
      <th>Description</th>
      <th>Default</th>
      <th>Options</th>
    </tr>
    <tr>
      <td>[Access](/docs/services/appid?topic=appid-tokens#access)</td>
      <td>The length of time for which access tokens are valid. The smaller the value, the more protection that you have in cases of token theft.</td>
      <td>60 minutes</td>
      <td>Any value in the range 5 - 1440</td>
    </tr>
    <tr>
      <td>[Refresh](/docs/services/appid?topic=appid-tokens#refresh)</td>
      <td>The length of time for which refresh tokens are valid. The smaller the number, the more frequently a user must sign themselves in.</td>
      <td>30 days</td>
      <td>Any value in the range 1 - 90</td>
    </tr>
    <tr>
      <td>[Anonymous](/docs/services/appid?topic=appid-anonymous)</td>
      <td>The length of time for which anonymous tokens are valid. Anonymous tokens are assigned to users the moment they begin interacting with your app. When a user signs in, the information in the anonymous token is then transferred to the token associated with the user.</td>
      <td>30 days</td>
      <td>Any value in the range 1 - 90</td>
    </tr>
  </table>

  [Identity tokens](/docs/services/appid?topic=appid-tokens#identity) are automatically configured to match the length of time that you set for access tokens. The values cannot be different.
  {: tip}

3. Click **Save**. 




