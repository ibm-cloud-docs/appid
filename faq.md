---

copyright:
  years: 2017, 2023
lastupdated: "2025-05-01"

keywords: pricing, advanced security, authentication events, activity tracking, runtime activity, password policies, keycloak, allow list redirect url, redirect uri

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


# FAQ for {{site.data.keyword.appid_short_notm}}
{: #faq}

This FAQ provides answers to common questions about the {{site.data.keyword.appid_full}} service.
{: shortdesc}


## Why do I need to allowlist my redirect URI?
{: #faq-redirect}
{: faq}
{: support}

A redirect URI is the callback endpoint of your application. When you allowlist your URI, you're giving {{site.data.keyword.appid_short_notm}} the OK to send your users to that location. At runtime, {{site.data.keyword.appid_short_notm}} validates the URI against your allowlist before it redirects the user. This process can help prevent phishing attacks and lessens the possibility that an attacker is able to gain access to your user's tokens. For more information about redirect URIs, see [Adding redirect URIs](/docs/appid?topic=appid-managing-idp#add-redirect-uri).

Do not include any query parameters in your URL. They are ignored in the validation process. Example URL: `http://host:[port]/path`
{: tip}



## How does encryption work in {{site.data.keyword.appid_short_notm}}?
{: #faq-encryption}
{: faq}

Check out the following table for answers to commonly asked questions about encryption.

| Question | Answer |
|-----|----|
| Why do you use encryption? | One way that we protect our users' information is by encrypting customer data at rest and in transit. The service encrypts customer data at rest with per-tenant keys and enforces TLS 1.2+ in all network segments. |
| Which algorithms are used in {{site.data.keyword.appid_short_notm}}? | The service uses `AES` and `SHA-256` with salting. |
| Do you use public or open source encryption modules or providers? Do you ever expose encryption functions?  | The service uses `avax.crypto` Java libraries, but never exposes an encryption function. |
| How are keys stored? | Keys are generated, encrypted with a master key that is specific to each region, and then stored locally. The master keys are stored in [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-getting-started-tutorial). Each region has its own root-of-trust key that is stored in [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-getting-started-tutorial), which is backed up by HSM. Each service instance (tenant) has its own data encryption and token signature keys, which are encrypted by using the region's root-of-key trust. |
| What is the key strength that you use? | The service uses 16 bytes. |
| Do you invoke any remote APIs that expose encryption capabilities | No, we do not. |
{: caption="Frequently asked questions about how {{site.data.keyword.appid_short_notm}} handles encryption" caption-side="top"}


## What clock synchronization does {{site.data.keyword.appid_short_notm}} use?
{: #faq-ntp}
{: faq}

{{site.data.keyword.appid_short_notm}} runs in {{site.data.keyword.cloud_notm}}, which uses an internal NTP server: `servertime.service.softlayer.com`.

Synchronizing your application with {{site.data.keyword.appid_short_notm}}'s time source depends on which environment that you're using to run your application.

* If your application is running in IBM Cloud Classic Infrastructure, set your NTP servers to `servertime.service.softlayer.com`.
* If your application is running in IBM Cloud VPC Infrastructure, set your NTP servers to `time.adn.networklayer.com`.
* If your application is not running in IBM Cloud, you do not have access to these time servers. In this case, set your NTP servers to `time-a.nist.gov` or `time-b.nist.gov`.



## What is the difference between {{site.data.keyword.appid_short_notm}} and Keycloak?
{: #faq-keycloak}
{: faq}

Both {{site.data.keyword.appid_short_notm}} and Keycloak can be used to add authentication to applications and secure services. The main difference between the two offerings is how they're packaged.
{: shortdesc}

Keycloak is packaged as software, which means that you, as the developer, are responsible for maintaining functionality of the product after you download it. You're responsible for hosting, high-availability, compliance, backups, DDoS protection, load balancing, web firewalls, databases, and more.

{{site.data.keyword.appid_short_notm}} is a fully managed offering that is provided "as-a-service". This means that IBM takes care of the operation of the service, handles compliancy, availability in multiple zones, SLA, and more. {{site.data.keyword.appid_short_notm}} also has an integrated experience with the {{site.data.keyword.cloud_notm}} Platform that includes native runtimes and services such as the {{site.data.keyword.containershort_notm}}, {{site.data.keyword.openwhisk_short}}, and {{site.data.keyword.cloudaccesstrailshort}}.



## Can I use the same client ID in more than one application?
{: #faq-multiple-apps}
{: faq}
{: support}

While you technically `_can_` use the same credentials in more than one application, it is highly recommended that you do not for several reasons. Foremost, because when you're sharing your ID across applications any type of attack or compromise then affects your entire environment rather than one application. For example, if you're using your ID across three applications and one of them becomes compromised, all three are then compromised.  An attacker is able to impersonate any of your apps. The second reason is that when you're using the same client ID in multiple apps, there is no way to differentiate between applications. For example, you're unable to tell which app was used to generate a token.

## How can I update my application to use a new service instance without losing any data
{: #migrate-service}

You can migrate the information in one instance of {{site.data.keyword.appid_short_notm}} to another.
{: shortdesc}

1. Create an instance of the service.
2. Duplicate your identity provider configuration by using the GUI.
3. [Migrate your user profiles](/docs/appid?topic=appid-user-admin). Known users are exported as a JSON object. Anonymous user's cannot be migrated. You can choose to import the entire object into the new instance or break it up and divide the users as you see fit if you have more than one instance. For Cloud Directory, see [Migrating users](/docs/appid?topic=appid-cd-users#user-migration). For federated identity providers, use the following steps.
4. Create application credentials to invoke the new service instance.
   1. In the service dashboard, navigate to the **Applications** tab.
   2. Click **Add Application** and give your application a name. Then, click **Save**.
   3. Click **View credentials** in the table and copy the output.
   4. Paste your new credentials into your application.
5. Update your application to use the new credentials including any URLs.
6. Depending on your configuration, you might need to redeploy or unbind and rebind your application.


## Can {{site.data.keyword.appid_short_notm}} help configure logout?
{: #faq-logout}

Depending on how you configure your application, {{site.data.keyword.appid_short_notm}} can help to facilitate a log out functionality for your users. Check out the following table to see where functionality for logout is available.

|  | Description |
|---------|-------------|
| {{site.data.keyword.appid_short_notm}} SDKs | The {{site.data.keyword.appid_short_notm}} SDKs have a built-in logout functionality.  |
| Cloud Directory SSO[^sso] | {{site.data.keyword.appid_short_notm}} provides built in logout functionality for the Cloud Directory SSO feature. |
| Ingress | Ingress provides a built in logout functionality. |
| Istio | The Istio adapter is configured to provide log out functionality through OIDC. |
{: caption="Log out functionality options" caption-side="top"}
{: row-headers}

[^sso]: All redirect URLs that are used with the Cloud Directory SSO feature must be added to the log out URL allowlist in the {{site.data.keyword.appid_short_notm}} UI.

### Configuring logout
{: #faq-logout-how}

To configure logout, you must configure your application to send a request to your identity provider. Then, to redirect the user to an area of your application that does not require authentication. In most use-cases, an application server session might be set by the {{site.data.keyword.appid_short_notm}} SDKs, Ingress, or Istio that works in partnership with a federated identity provider such as SAML or Cloud Directory to enable authentication and authorization.

In the following HTML example, an {{site.data.keyword.appid_short_notm}} SDK is used to configure log out. But, if you are working with another option, you can use this snippet as a guide and update it to fit your needs.

```html
<script>
  var ticker = setInterval(tick, 1000);
  var counter = 5;
  function tick() {
    var timerDiv = document.getElementById("timer");
    if (counter > 0) {
      timerDiv.innerText = "Logged out. Redirecting back in " + (counter--) + " seconds.";
    } else {
      document.location = "./appid_logout";
    }
  } </script>
<iframe height="0" width="0" src="https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0"></iframe>
```
{: screen}
