---

copyright:
  years: 2017, 2021
lastupdated: "2021-06-23"

keywords: anonymous authentication, progressive authentication, profile, user profile, authorization, sign in, secure app, identity provider, authorization

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

# Anonymous authentication
{: #anonymous}

With {{site.data.keyword.appid_full}}, you can allow users to anonymously browse your application under an anonymous user profile. If the user chooses to sign in, you can allow them to still access their anonymous attributes by attaching their anonymous profile to their user identity with {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

## Understanding the progressive authentication flow
{: #progressive}

When a user chooses not to sign in immediately, they are considered an anonymous user. In an example of you as an online retailer, an anonymous user can have limited interactions with your app such as adding objects to a shopping cart. However, you might require users to sign in to check out the items in the shopping cart. If a user chooses to sign in, you can allow them to access the same objects that are placed in their shopping carts before they sign in. 

You can use {{site.data.keyword.appid_short_notm}} to create an anonymous user profile and issue anonymous tokens for users who browse your app anonymously. Using these anonymous tokens, you can customize the user's experience of your app by managing the attributes that are stored in the anonymous user profile. If the user signs in and the anonymous tokens did not expire, you can link their anonymous profile with their existing identified user profile. For more information about configuring token lifetime, check out [Managing authentication](/docs/appid?topic=appid-managing-idp#idp-token-lifetime).

If an existing identified user profile does not exist, you can create a new identified user profile. After a user is identified, their anonymous token becomes invalid. However, an identified user can still access the attributes of their anonymous profile because they are accessible with the new access and identity tokens. 

You can assign only one anonymous profile to an identified user profile. If the existing identified user profile is already associated with an existing anonymous user, the access and identity tokens provide access only to that existing anonymous profile's attributes. The access and identity tokens do not provide access to a new anonymous profile created in a different session. However, until the new anonymous token expires, the user can still access information available through the new anonymous token. While you develop your app, you can choose how to merge new anonymous attributes to existing identified user profiles.

### What does the progressive authentication flow look like? 

In the following image, you can see the direction of communication that defines the progressive authentication flow between the user, your application, {{site.data.keyword.appid_short_notm}}, and the identity provider.

![The path to becoming an identified user when they start as anonymous](images/auth-anon-user.svg){: caption="Figure 1. Progressive authentication flow of anonymous user" caption-side="bottom"}

1. The user interacts with areas of your app that do not require authentication. 
2. Your application notifies {{site.data.keyword.appid_short_notm}} that the user wants to interact with your app as an anonymous user. 
3. {{site.data.keyword.appid_short_notm}} creates an ad hoc user profile and calls the OAuth login that issues anonymous tokens for the anonymous user. 
4. Using the anonymous tokens from {{site.data.keyword.appid_short_notm}}, you can create, read, update, and delete the attributes that are stored in the anonymous user profile. 
5. The user might choose to sign in to access more features of your app.
6. Your application notifies {{site.data.keyword.appid_short_notm}} that the user wants to interact with your app as an identified user. 
7. {{site.data.keyword.appid_short_notm}} returns the login widget to your app. 
8. The user selects their preferred identity provider and provides their credentials. 
9. Your application informs {{site.data.keyword.appid_short_notm}} that the user selected an identity provider.
10. {{site.data.keyword.appid_short_notm}} authenticates the call with the identity provider. 
11. The identity provider confirms whether the login was successful. 
12. {{site.data.keyword.appid_short_notm}} uses the anonymous token to find the anonymous profile and attaches the user's identity to it.
13. After {{site.data.keyword.appid_short_notm}} creates the new tokens, the service invalidates the user's anonymous token. 
14. {{site.data.keyword.appid_short_notm}} returns the new access and identity tokens. The new tokens contain the public information that is shared by the identity provider and the attributes of the user's formerly anonymous profile. 
15. The user is granted access to your app.
