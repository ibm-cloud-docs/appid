---> or Active Directory Federation Services, generally use SAML as their identity protocol.


## Configuring settings

You can decide which providers that you want to use, your redirect URLs, and token information for your app. The information that you input on this page applies across all of your identity providers. For example: when you set token expiration, it applies to enterprise providers and to social providers.

**To configure your providers:**

1. Navigate to your service dashboard.
2. Click the **Identity Providers** twisty to view all of your options, and select the **Manage** page.
3. On the **Identity Providers** tab, and set the providers that you want to use, to **On**.
4. Optional: Decide whether to turn off **Anonymous users**, or leave the default, which is **On**. When set to **On**, you can begin associating custom user attributes with your users prior to their initial sign in.

{{site.data.keyword.appid_short_notm}} provides default credentials to help with your initial set-up of Facebook and Google+. You are limited to 100 uses of the credentials per instance, per day. Because they are IBM credentials, they are meant to be used only for development. Before you publish your app, update the configuration to your own credentials.
{: tip}

**To configure your settings:**


1. Add your redirect URLs. A redirect URL is the callback endpoint of your app. To prevent phishing attacks, {{site.data.keyword.appid_short_notm}} validates the URLs against the whitelist.
  1. In the **Add web redirect URL** field, type the URL and click the **+** icon.
  2. Repeat step one until all possible redirect URLs have been added.

  Do not include any query parameters in your URL. They are ignored in the validation process. Example URL: `http://host:[port]/path`
  {: tip}

2. Configure your tokens.
  1. To allow sign in without the need for user interaction, set **refresh tokens** to **On**.
  2. Set your refresh token lifetime. Expiration is set in days and can be any value between 1 and 90. The lower the number, the more frequently a user must sign in themselves.
  3. Set your access token lifetime. Before a user can gain access to your application, they must have a valid access token associated with them. The expiration is set in minutes and can be between 5 and 1440 minutes. The smaller the value, the better the security for cases of token theft.
  4. Set your anonymous token lifetime. An [anonymous token](/docs/services/appid/progressive.html#anonymous) is assigned to users that interact with your application prior to sign in. When a user signs in, the information in the anonymous token is then transferred to the token associated with the user. Expiration is set in days and can be any value between 1 and 90.

</staging>
