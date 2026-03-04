---

copyright:
  years: 2017, 2026
lastupdated: "2026-03-04"

keywords: help, support, error, multiple users, attribute, ticket, identity provider, redirect uri, custom url, virtual user, idp, identity settings, user profile

subcollection: appid

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my user not redirected to my app? 
{: #ts-redirect}
{: troubleshoot}

When a user signs into your app by using {{site.data.keyword.appid_full}}, they are redirected back to your application, but occasionally a redirect might fail.
{: shortdesc}


If your redirect URL is rejected by the service when you enter it in the console, be sure that it is a valid URL that is formatted correctly. [Learn more](/docs/appid?topic=appid-managing-idp#add-redirect-uri).
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
