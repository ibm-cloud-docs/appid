---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:faq: data-hd-content-type='faq'}


# FAQ
{: #faq}

This FAQ provides answers to common questions about the {{site.data.keyword.appid_full}} service.
{: shortdesc}


## How does {{site.data.keyword.appid_short_notm}} calculate pricing?
{: #pricing}
{: faq}

With {{site.data.keyword.appid_short_notm}}, you pay less as you use more resources.
{: shortdesc}

The graduated tier plan consists of three parts: the number of authentication events, both regular and advanced security, and the number of authorized users. You are charged each month, based on the summary of the two parts. The total price is the cumulative charge for each level of usage, consisting of your quantity multiplied by the unit price at that tier.

Your first 1000 authentication events and first 1000 authorized users are free each month, with the exception of any advanced security events. Any advanced security events incurs an extra charge.

### Authentication events

An authentication event occurs when a new access token, regular or anonymous, is issued. Tokens can be issued as a response to a sign-in request that is initiated by a user, or on behalf of the user by an app. By default, access tokens are valid for one hour and anonymous tokens are valid for 30 days. After the token expires, you must create a new token to access protected resources. You can update the expiration time of your {{site.data.keyword.appid_short_notm}} tokens on the **Sign-in Expiration** page of the service dashboard.

#### Advanced security features

Advanced security features give you the ability to strengthen the security of your application.
{: shortdesc}

<table>
  <tr>
    <th>Feature</th>
    <th>Benefit</th>
  </tr>
  <tr>
    <td>Multi-Factor Authentication</td>
    <td>MFA for Cloud Directory confirms a user’s identity by requiring a user to enter a one time passcode that is sent to their email in addition to their email and password.</td>
  </tr>
  <tr>
    <td>Password policy management</td>
    <td>As an account owner, you can enforce more secure passwords for Cloud Directory by configuring a set of rules that user passwords must conform to. Examples include, the number of attempted sign-ins before lockout, expiration times, minimum time span between password updates, or the number of times that a password can't be repeated. For a complete list of the options and set up information, see [Advanced password management](cloud-directory.html#advanced-password).</td>
  </tr>
</table>

By default, advanced security features are disabled. If you turn on Multi-Factor Authentication or password policy management you incur an extra charge. If you disable all of the advanced features, your account will revert to the lower-cost policy. For example, if you obtained 10,000 access tokens. Then turned on MFA and password policy management, and obtained 10,000 more. You would pay for 20,000 authentication events and 10,000 advanced security events.

These features are available only to those instances that are on the graduated tier pricing plan and that were created after March 15th, 2018.
{: note}

### Authorized users

An authorized user is a unique user that signs in with your service whether directly or indirectly, including anonymous users. You are charged for one authorized user each time a new user signs in to your application, including anonymous users. For example, if a user signs in with Facebook and later signs in by using Google, they are considered two separate authorized users.

For the most up to date pricing information for {{site.data.keyword.appid_short_notm}}, see the [pricing calculator](https://console.cloud.ibm.com/pricing/configure/service/AdvancedMobileAccess-d6aece47-d840-45b0-8ab9-ad15354deeea).
{: important}

</br>


## Why do I need to whitelist my redirect URL?
{: #redirect}
{: faq}

A redirect URL is the callback endpoint of your app. To prevent phishing attacks, {{site.data.keyword.appid_short_notm}} validates the URL against the whitelist of redirect URLs. When phishing occurs, the possibility that an attacker can gain access to your users tokens exists.

To add your URL to the whitelist:

1. Navigate to **Identity Providers > Manage**.
2. In the **Add web redirect URL** field, type the URL and click **+**.

Do not include any query parameters in your URL. They are ignored in the validation process. Example URL: `http://host:[port]/path`
{: tip}

</br>

## How does encryption work in {{site.data.keyword.appid_short_notm}}?
{: #encryption}
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
      <td>The service uses <code>javax.crypto</code> Java libraries, but never exposes an encryption functions.</td>
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

</br>

## What does {{site.data.keyword.appid_short_notm}} expect a SAML assertion to look like?
{: #saml-example}
{: faq}

The service expects a SAML assertion to look like the following example.

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}

</br>

## What type of algorithms are supported for SAML signatures
{: #saml-signatures}
{: faq}

You can use any of the following algorithms to process XML digital signatures.

<table>
  <tr>
    <th> Type of algorithm </th>
    <th> Algorithm options </th>
  </tr>
  <tr>
    <td>Canonicalization and transformation algorithms with and without comments</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">Canonicalization <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">Exclusive Canonicalization with and without comments <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">Enveloped Signature transform <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li></ul></td>
  </tr>
  <tr>
    <td>Hashing algorithms</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">SHA1 digests <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">SHA256 digests <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">SHA512 digests <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li></ul></td>
  </tr>
  <tr>
    <td>Signature algorithms</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li></ul></td>
  </tr>
</table>

For more information about using a SAML identity provider, see [Configuring enterprise identity providers](enterprise.html).
