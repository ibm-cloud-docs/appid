---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-29"

keywords: Authentication, authorization, identity, app security, secure

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
{:faq: data-hd-content-type='faq'}


# FAQ
{: #faq}

This FAQ provides answers to common questions about the {{site.data.keyword.appid_full}} service.
{: shortdesc}


## How does {{site.data.keyword.appid_short_notm}} calculate pricing?
{: #faq-pricing}
{: faq}

With {{site.data.keyword.appid_short_notm}}, you pay less as you use more resources.
{: shortdesc}

The graduated tier plan consists of three parts: the number of authentication events, both regular and advanced security, and the number of authorized users. You are charged each month, based on the summary of the two parts. The total price is the cumulative charge for each level of usage, consisting of your quantity multiplied by the unit price at that tier.

Your first 1000 authentication events and first 1000 authorized users are free each month, except for any advanced security events. Any advanced security events incur an extra charge.

### Authentication events
{: #faq-authentication}

An authentication event occurs when a new access token, regular or anonymous, is issued. Tokens can be issued as a response to a sign-in request that is initiated by a user, or on behalf of the user by an app. By default, access tokens are valid for one hour and anonymous tokens are valid for 30 days. After the token expires, you must create a new token to access protected resources. You can update the expiration time of your {{site.data.keyword.appid_short_notm}} tokens on the **Manage > Authentication > Authentication Settings** page of the service dashboard.

#### Advanced security features

Advanced security features give you the ability to strengthen the security of your application.
{: shortdesc}

By default, advanced security features are disabled. If you turn on MFA,runtime activity tracking, or password policy management you incur an extra charge. For example, if you obtained 10,000 access tokens. Then, you turned on password policy management and obtained 10,000 more. You would pay for 20,000 authentication events and 10,000 advanced security events. If you disable all of the advanced features, your account reverts to the lower-cost policy.

<table>
  <caption>Description of the benefits that are gained with advanced authentication events</caption>
  <tr>
    <th>Feature</th>
    <th>Benefit</th>
  </tr>
  <tr>
    <td>Multi-factor authentication</td>
    <td>[MFA for Cloud Directory](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) confirms a user’s identity by requiring a user to enter a one time passcode that is sent to their email in addition to their entering their email and password.</td>
  </tr>
  <tr>
    <td>Runtime authentication activity tracking</td>
    <td>By integrating {{site.data.keyword.at_short}} with {{site.data.keyword.appid_short_notm}} you can track two different types of authentication events at runtime. For example: A password reset request, authentication failures, or a user log out.</td>
  </tr>
  <tr>
    <td>Password policy management</td>
    <td>As an account owner, you can enforce more secure passwords for Cloud Directory by configuring a set of rules that user passwords must conform to. Examples include, the number of attempted sign-ins before lockout, expiration times, minimum time span between password updates, or the number of times that a password can't be repeated. For a complete list of the options and set-up information, see [Advanced password management](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password).</td>
  </tr>
</table>



These features are available only to those instances that are on the graduated tier pricing plan and that were created after 15 March 2018.
{: note}

### Authorized users
{: #faq-authorized}

An authorized user is a unique user that signs in with your service whether directly or indirectly, including anonymous users. You are charged for one authorized user each time a new user signs in to your application, including anonymous users. For example, if a user signs in with Facebook and later signs in by using Google, they are considered two separate authorized users.

For the most up-to-date pricing information, you can create a cost estimate by clicking **Add to estimate** in the {{site.data.keyword.appid_short_notm}} section of the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog/services/app-id).
{: tip}



## Why do I need to whitelist my redirect URI?
{: #faq-redirect}
{: faq}

A redirect URI is the callback endpoint of your app. To prevent phishing attacks, {{site.data.keyword.appid_short_notm}} validates the URI against the whitelist of redirect URIs. When phishing occurs, the possibility that an attacker can gain access to your user's tokens exists. For more information about redirect URIs, see [Adding redirect URIs](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).

Do not include any query parameters in your URL. They are ignored in the validation process. Example URL: `http://host:[port]/path`
{: tip}



## How does encryption work in {{site.data.keyword.appid_short_notm}}?
{: #faq-encryption}
{: faq}

Check out the following table for answers to commonly asked questions about encryption.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="More information icon"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Why do you use encryption?</td>
      <td>One way that we protect our users information is by encrypting customer data at rest The service encrypts customer data at rest with per-tenant keys.</td>
    </tr>
    <tr>
      <td>Did you build your own algorithms? Which ones do you use in your code?</td>
      <td>We did not build our own, the service uses <code>AES</code> and <code>SHA-256</code> with salting.</td>
    </tr>
    <tr>
      <td>Do you use public or open source encryption modules or providers? Do you ever expose encryption functions? </td>
      <td>The service uses <code>javax.crypto</code> Java libraries, but never exposes an encryption function.</td>
    </tr>
    <tr>
      <td>How do you store keys?</td>
      <td>Keys are generated, encrypted with a master key that is specific to each region, and then stored locally. The master keys are stored in {{site.data.keyword.keymanagementserviceshort}}. At the storage and middleware levels, there is service level encryption which means that there is one key for all customers. At the app level, each customer has their own encryption key.</td>
    </tr>
    <tr>
      <td>What is the key strength that you use?</td>
      <td>The service uses 16 bytes.</td>
    </tr>
    <tr>
      <td>Do you invoke any remote APIs that expose encryption capabilities?</td>
      <td>No, we do not.</td>
    </tr>
  </tbody>
</table>



## What is the difference between {{site.data.keyword.appid_short_notm}} and Keycloak?
{:# faq-keycloak}

Both {{site.data.keyword.appid_short_notm}} and Keycloak can be used to add authentication to applications and secure services. The main difference between the two offerings is the way in which they're packaged.
{: shortdesc}

Keycloak is packaged as software which means that you, as the developer, are responsible for maintaining functionality of the product after you download it. You're responsible for hosting, high-availability, compliance, backups, DDoS protection, load balancing, web firewalls, databases, and more.

{{site.data.keyword.appid_short_notm}} is a fully managed offering that is provided "as-a-service". This means that IBM takes care of the operation of the service, handles compliancy, availability in multiple zones, SLA, and more. {{site.data.keyword.appid_short_notm}} also has an out-of-the-box integrated experience with the {{site.data.keyword.cloud_notm}} Platform that includes native runtimes and services such as the {{site.data.keyword.containershort_notm}}, {{site.data.keyword.openwhisk_short}}, and {{site.data.keyword.cloudaccesstrailshort}}.
