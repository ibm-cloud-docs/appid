---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-22"

keywords: help, support, error, multiple users, attribute, ticket, identity provider, redirect uri, custom url, virtual user, idp, identity settings, user profile

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



# Troubleshooting: General
{: #troubleshooting}

If you have problems while you're working with {{site.data.keyword.appid_full}}, consider these techniques for troubleshooting and getting help.
{: shortdesc}

## Getting help and support
{: #ts-gettinghelp}

You can get help with {{site.data.keyword.appid_short}} by [opening a support ticket](https://{DomainName}/unifiedsupport/cases/form). For more information about getting support, see [How do I get the support that I need](/docs/get-support?topic=get-support-using-avatar). To join the community and interact with other developers who use {{site.data.keyword.appid_short}}, you can find us on [Slack](https://www.ibm.com/cloud/blog/announcements/get-help-with-ibm-cloud-app-id-related-questions-on-slack){: external} or [Stack Overflow](https://stackoverflow.com/){: external} with the `ibm-appid` tag.


## A user is not redirected to the app after sign-in
{: #ts-signin-fail}
{: troubleshoot} 
{: support}

{: tsSymptoms}
A user signs in to your application through an identity provider's sign in page, and either nothing happens or the sign-in fails.

{: tsCauses}
Sign-in might fail for the following reasons:

* Your redirect URL was not properly added to [the allow list](/docs/appid?topic=appid-faq#faq-redirect).
* The user is not authorized.
* The user tried to sign in with the wrong credentials.

{: tsResolve}
For a redirect to occur:

* Verify that your redirect URL is correct. It must be exact for the redirect to work.
* Be sure that your user is signing in with the correct credentials
* Check that they're configured in your identity provider user settings.



## A custom URI is rejected
{: #ts-custom-uri}

{: tsSymptoms}
When you enter a web redirect URL that uses a custom URL Scheme, it is rejected by the {{site.data.keyword.appid_short_notm}} console.

{: tsCauses}
Your URL might be rejected for the following reasons:

* The URL does not follow an `http` or `https` scheme
* The URL ends with `://`
* There is a typographical error in your URL

The limitations are in place for security purposes.

{: tsResolve}
To resolve the issue, verify that the URL is correct. If your URL does not meet the requirements, you can create an HTTPS endpoint in your app to redirect the received grant code to your custom URL. Specify the created endpoint as your redirect URL in the {{site.data.keyword.appid_short_notm}} console. For more information about redirect URIs, see [Adding redirect URIs](/docs/appid?topic=appid-managing-idp#add-redirect-uri)


## A user is not redirected to the identity provider
{: #ts-redirect}

{: tsSymptoms}
A user tries to sign in to your application, but the sign-in page doesn't display when prompted.

{: tsCauses}
The identity provider can fail for several reasons:

* The redirect URI that is listed in {{site.data.keyword.appid_short_notm}} is written incorrectly.
* The identity provider doesn't recognize the authentication request.
* The identity provider expects HTTP-POST binding.
* The identity provider expects a signed AuthnRequest.

{: tsResolve}
You can try some of these solutions:

* Update your sign-in URL. This URL is sent as part of the `AuthnRequest` and must be exact.
* Be sure that your {{site.data.keyword.appid_short_notm}} metadata is set correctly in your identity provider settings.
* Configure your identity provider to accept the `AuthnRequest` in the HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} does not support signing `AuthnRequests`.

If none of the solutions work, it is possible that you might have a connection issue.
{: tip}


## An attribute is showing the wrong value
{: #ts-saml-attribute}

{: tsSymptoms}
An attribute value exists in a user profile, but it's not associated with the correct attribute.

{: tsCauses}
The user profile attribute is not mapped correctly.

{: tsResolve}
Map the attribute in your identity provider settings. {{site.data.keyword.appid_short_notm}} expects the following attributes:
* `name`
* `email`
* `locale`
* `picture`



## Error: Too many requests
{: #ts-requests}
{: troubleshoot} 
{: support}

{: tsSymptoms}
You attempt to view the home page of your app but receive the following error:

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
You might receive a `too many requests` error if you are performing automated testing with only one virtual user. Each user is limited to five sign-in attempts in a 1-minute time span. Sign-in attempts are limited in order to prevent brute force DDoS and other types of similar attacks.

{: tsResolve}
To resolve the issue, you might want to use multiple virtual users when you perform testing.



## Why didn't my user get an email?
{: #ts-verification}

{: tsSymptoms}
Your users don't receive an email when the sign-up, forgot their password, change their password or to verify their account.

{: tsCauses}
A user might not receive their requested email because it is sent to spam, there is a misconfiguration, or an internal error.

{: tsResolve}
To resolve this issue, you can try the following solutions:

* Verify with the user that the email was not sent to their spam folder. If it was, have them mark the sender as `not spam`. To avoid this, consider [bringing your own email sender](/docs/appid?topic=appid-cd-types#cd-custom-email).
* Verify your [messaging configuration](/docs/appid?topic=appid-cd-types). 
* Ensure that a resend option is present on your sign-in screen so that your user can request that an email is resent if an internal error occurs.

If you add a user through the {{site.data.keyword.appid_short_notm}} dashboard, the user is verified automatically and does not receive an email.
{: note}


