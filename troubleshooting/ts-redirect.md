---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-11"

keywords: help, support, error, multiple users, attribute, ticket, identity provider, redirect uri, custom url, virtual user, idp, identity settings, user profile

subcollection: appid

content-type: troubleshoot

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

# Why is my user not redirected to my app? 
{: #ts-redirect}
{: troubleshoot}

When a user signs into your app by using {{site.data.keyword.appid_full}}, they are redirected back to your application, but occasionally a redirect might fail.
{: shortdesc}


If your redirect URL is rejected by the service when you enter it in the UI, be sure that it is a valid URL that is formatted correctly. [Learn more](/docs/appid?topic=appid-managing-idp#add-redirect-uri).
{: tip}


## Why isn't a user redirected to my application after they sign-in by using an identity provider?
{: #ts-signin-fail}
{: support}

A user signs in to your application through an identity provider's sign in page, and either nothing happens or the sign-in fails.
{: tsSymptoms}

Sign-in might fail for the following reasons:
{: tsCauses}

* Your redirect URL was not properly added to [the allow list](/docs/appid?topic=appid-faq#faq-redirect).
* The user is not authorized.
* The user tried to sign in with the wrong credentials.

For a redirect to occur:
{: tsResolve}

* Verify that your redirect URL is correct. It must be exact for the redirect to work.
* Be sure that your user is signing in with the correct credentials
* Check that they're configured in your identity provider user settings.


## Why isn't a user redirected to an identity provider when they try to sign-in?
{: #ts-redirect-idp}

A user tries to sign in to your application, but the sign-in page doesn't display when prompted.
{: tsSymptoms}

The identity provider can fail for several reasons:
{: tsCauses}

* The redirect URI that is listed in {{site.data.keyword.appid_short_notm}} is written incorrectly.
* The identity provider doesn't recognize the authentication request.
* The identity provider expects HTTP-POST binding.
* The identity provider expects a signed AuthnRequest.

You can try some of these solutions:
{: tsResolve}

* Update your sign-in URL. This URL is sent as part of the `AuthnRequest` and must be exact.
* Be sure that your {{site.data.keyword.appid_short_notm}} metadata is set correctly in your identity provider settings.
* Configure your identity provider to accept the `AuthnRequest` in the HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} does not support signing `AuthnRequests`.

If none of these solutions work, it is possible that they might have a connection issue.
{: tip}

