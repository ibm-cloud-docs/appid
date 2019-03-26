---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-26"

keywords: authentication, authorization, identity, app security, secure, development, identity provider, tokens, customization, lifetime

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


# Managing
{: #managing-idp}

Identity providers (IdP's) add a level of security for your mobile and web apps, through authentication. With {{site.data.keyword.appid_full}}, you can configure one or several identity providers to create a custom sign-in experience for your users.
{: shortdesc}


## Configuring providers
{: #configuring-provider}

An identity provider creates and manages information about an entity such as a user, a functional ID, or an application. The provider verifies the identity of the entity by using credentials, such as a password. Then, the IdP sends the identity information to another service provider. Because the identity provider authenticates the entity, {{site.data.keyword.appid_short_notm}} is able to authorize it and grant access to your apps.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} interacts with identity providers by using multiple protocols such as OpenID Connect, SAML, and more. For example, OpenID Connect is the protocol that is used with many social providers such as Facebook, Google. Enterprise providers such as <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, or <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, generally use SAML as their identity protocol. For [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), the service uses SCIM to verify identity information.

Working with application identity? Check out [Application identity](/docs/services/appid?topic=appid-app).
{: tip}

There are several providers that the service can be configured to use. Check out the following table to learn about your options.

<table>
  <tr>
    <th>Provider</th>
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
    <td>You can create a single sign-on experience for your end users.</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid?topic=appid-social#facebook)</td>
    <td>Social</td>
    <td>End users can sign in to your app by using their Facebook credentials.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid?topic=appid-social#google)</td>
    <td>Social</td>
    <td>End users can sign in to your app by using their Google credentials.</td>
  </tr>
  <tr>
    <td>[Custom](/docs/services/appid?topic=appid-custom-identity#custom-identity)</td>
    <td> </td>
    <td>If none of the provided options fit your specific need, you can configure your own identity flow to work with {{site.data.keyword.appid_short_notm}}.</td>  
  </tr>
</table>

To manage your identity providers:

1. Navigate to your service dashboard.
2. In the **Identity Providers** section of the navigation, select the **Manage** page.
3. On the **Identity Providers** tab, set the providers that you want to use, to **On**.
4. Optional: Decide whether to turn off **Anonymous users**, or leave the default, which is **On**. When set to **On**, user attributes are associated with the user from the moment they begin interacting with your app. For more information about the path to becoming an identified user, see [Progressive authentication](/docs/services/appid?topic=appid-anonymous#progressive)

{{site.data.keyword.appid_short_notm}} provides default credentials to help with your initial set-up of Facebook and Google+. You are limited to 100 uses of the credentials per instance, per day. Because they are IBM credentials, they are meant to be used only for development. Before you publish your app, update the configuration to your own credentials.
{: tip}


## Configuring your settings
{: #configuring-settings}

You can decide configure your redirect URIs and token information for your app by using the GUI. The settings apply across all of the identity providers configured for this instance of the service. For example, when you set a token expiration it applies to all providers that you have configured whether their social or enterprise.


### Adding redirect URIs
{: #add-redirect-uri}

A redirect URI is the callback endpoint of your app. During the sign in flow, {{site.data.keyword.appid_short_notm}} validates the URIs before allowing clients to participate in the authorization workflow which helps to prevent phishing attacks and grant code leakage. By registering your URI, you're telling {{site.data.keyword.appid_short_notm}} that the URI is trusted and it's okay to redirect your users.

Be sure to only register URIs of applications that you trust.
{: note}


1. Click **Authentication Settings** to see your URI and token configuration options.

2. In the **Add web redirect URI** field, type the URI. Each URI should begin with `http://` or `https://` and must include the full path, including any query parameters for the redirect to be successful. Need help formatting? Check out the following table for some examples.

  <table>
    <tr>
      <th>Type</th>
      <th>Example URI</th>
    </tr>
    <tr>
      <td>Custom domain</td>
      <td><code>http://mydomain.net/myapp2path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Ingress subdomain</td>
      <td><code>https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Logout</td>
      <td><code>http://mydomain.net/myapp2path/appid_logout</code></td>
    </tr>  
  </table>

3. Click the **+** symbol in the **Add web redirect URIs** box.

4. Repeat steps one through three until all possible URIs are added to your list.



### Configuring token lifetime
{: #idp-token-lifetime}

Token lifetime begins again at each user sign in. For example, you set your refresh token lifetime to 10 days. An access token and a refresh token are created when the user signs in for the first time. If the user returns to your app a few days later, 3 days to be specific, they would not need to sign in again. But, if the user waited 12 days after their initial sign in, and then returned to your app, then they would need to sign in again and a set of tokens is associated with the user.

1. To allow sign in without the need for user interaction, set **refresh tokens** to **On**.

2. Set your refresh token lifetime. Expiration is set in days and can be any value in range 1 to 90. The smaller the number, the more frequently a user must sign themselves in.

3. Set your access token lifetime. The expiration is set in minutes and can be in range 5 to 1440. The smaller the value, the more protection that you have in cases of token theft.

4. Set your anonymous token lifetime. An [anonymous token](/docs/services/appid?topic=appid-anonymous#progressive) is assigned to users the moment they begin interacting with your app. When a user signs in, the information in the anonymous token is then transferred to the token associated with the user. Expiration is set in days and can be any value between 1 and 90.

For more information about tokens, check out [Understanding tokens](/docs/services/appid?topic=appid-key-concepts#tokens).
