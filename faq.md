---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# FAQ
{: #faq}

This FAQ provides answers to common questions about the {{site.data.keyword.appid_full}} service.
{: shortdesc}


## How does {{site.data.keyword.appid_short_notm}} calculate pricing?
{: #pricing}

With {{site.data.keyword.appid_short_notm}}, you pay less as you use more resources.
{: shortdesc}

The graduated tier plan consists of two parts: the number of authentication events and the number of authorized users. You are charged each month, based on the summary of the two parts. The total price is the cumulative charge for each level of usage, consisting of your quantity multiplied by the unit price at that tier.

### Authentication events

An authentication event occurs when a new access token, regular or anonymous, is issued. For identified users, each new access token is valid by default for 1 hour (be it through real user authentication or via refresh tokens). Anonymous tokens are valid by default for 1 month. After the token expires, you must create a new token to access protected resources. You can update the expiration time of {{site.data.keyword.appid_short_notm}} tokens on the **Sign-in Expiration** page in the {{site.data.keyword.appid_short_notm}} dashboard.

When you use {{site.data.keyword.appid_short_notm}} in mobile applications, tokens are stored in key-store or key-chain and are added to every future request. The tokens are accessible by using the App ID Android or iOS SDK. When you use {{site.data.keyword.appid_short_notm}} in web applications, it is recommended to store the tokens in application session cookies.


### Authorized users

An authorized user is a unique user that logs in with your service whether directly or indirectly. You are charged for one authorized user every time a new user logs in from each identity provider, including anonymous users. For example, if a user logs in with Facebook, and later logs in by using Google, they are considered two separate authorized users.

For more information on graduated tier pricing, see the [{{site.data.keyword.Bluemix_notm}} pricing docs](/docs/billing-usage/how_charged.html#services).

</br>

## Why do I need to whitelist my redirect URL?
{: #redirect}

A redirect URL is the callback endpoint of your app. To prevent phishing attacks, App ID validates the URL against the whitelist of redirect URLs. When phishing occurs, there is a chance that an attacker may gain access to your users tokens.

To add your URL to the whitelist:

1. Navigate to **Identity Providers > Manage**.
2. In the **Add web redirect URL** field, type the URL and click **+**.

Do not include any query parameters in your URL. They are ignored in the validation process. Example URL: `http://host:[port]/path`
{: tip}

</br>

## How does encryption work in {{site.data.keyword.appid_short_notm}}?
{: #encryption}

Check out the following table for answers to commonly asked questions about encryption.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="More information icon"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Why do you use encryption?</td>
      <td>The service encrypts customer data at rest with per-tenant keys. This is one way of protecting our users information.</td>
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
      <td>Keys are generated and then stored locally after being encrypted by using a master key that is specific to each region. The master keys are stored in {{site.data.keyword.keymanagementserviceshort}}. Storage and middleware levels have service level encryption which means that there is one key for all customers. The application level and customer by customer encryption which means that each customer has their own encryption key.</td>
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
