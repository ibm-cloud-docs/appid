---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Configuring enterprise identity providers
{: #enterprise}

If you already have an existing user repository and a certified way to authenticate users to your internal systems you can configure the {{site.data.keyword.appid_full}} service to use an enterprise identity provider.
{: shortdesc}

## Understanding SAML
{: #saml}

SAML is an open standard for exchanging authentication and authorization data between an identity provider who asserts the user identity and a service provider who consumes the user identity information.
{: shortdesc}

How does it work?

{{site.data.keyword.appid_short_notm}} functions as a service provider and initiates a single sign on (SSO) login to a third-party provider such as Active Directory Federation Services. The <a href="http://saml.xml.org/saml-specifications" target="_blank">SAML <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> protocol supports different profiles and bind options. {{site.data.keyword.appid_short_notm}} supports the web browser SSO profile, with HTTP Post binding.

### SAML assertions and identity token claims

A SAML assertion is a package of information that contains one or more statements. The assertion contains the authorization decision, and it might contain identity information about the user.

When a user signs in with an identity provider, that provider sends an assertion to {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} propagates user identity information that is returned in the SAML assertion to your app as OIDC token claims. The SAML attribute must correspond to 1 of the following OIDC claims to be added to the identity token.

The following claims can be added:
* `name`
* `email`
* `locale`
* `picture`

The remaining SAML attribute elements that do not correspond to any of the standard names are ignored. Note that if one or more of those values change on the provider's side, the new values are available only after the user logs in again.

## Configuring your app to work with an external SAML identity provider
{: #configuring-saml}

You can configure the {{site.data.keyword.appid_short_notm}} service to use a Security Assertion Markup Language (SAML) identity provider.
{: shortdesc}

### Providing metadata to your identity provider

To configure your app, you need to provide information to a SAML compatible identity provider. The information is exchanged through a metadata XML file that also contains configuration data that is used to establish trust.

1. In the **Manage** tab of the {{site.data.keyword.appid_short_notm}} dashboard, set **SAML 2.0** to **On**. Then, click **Edit** to configure your SAML settings.
2. Click **Download SAML Metadata file**. Your identity provider expects the following information from the file.
  <table>
    <tr>
      <th> Variable </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>The identifier that lets the identity provider know that {{site.data.keyword.appid_short_notm}} has issued the SAML request.</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>The location that the identity provider sends the SAML assertions after successfully authenticating a user.</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>The instructions on how the identity provider should send the SAML response.</td>
    </tr>
    <tr>
      <td><code>NameID Format<code></td>
      <td>The way in which the identity provider knows which identifier format it needs to send in the subject of an assertion. The way in which {{site.data.keyword.appid_short_notm}} identifies users.</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned<code></td>
      <td>The way that an identity provider checks to see if it needs to sign the assertion. The service expects that the assertion is signed, but does not support encrypted assertions.</td>
    </tr>
  </table>

3. Provide the data to your identity provider. If your identity provider supports uploading the metadata file, you can do so. If it doesn't, configure the properties manually. Not every identity provider will use the same properties, so if you don't use all of them, it's okay.

The property names may differ between identity providers.
{: tip}

### Providing metadata to {{site.data.keyword.appid_short_notm}}

You'll need to obtain data from the identity provider and provide it to {{site.data.keyword.appid_short_notm}}.

1. Navigate to the **SAML 2.0** tab of the {{site.data.keyword.appid_short_notm}} dashboard. Input the following metadata that you obtained from the identity provider in the **Provide Metadata from SAML IdP** section.
  <table>
    <tr>
      <th> Variable </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>The URL that the user is redirected to for authentication. It is hosted by your SAML identity provider.</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>The globally unique name for a SAML identity provider.</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>The certificate issued by your SAML identity provider. It is used for signing and validating SAML assertions. All providers are different, but you might be able to download the signing certificate from your identity provider. The certificate must be in <code>.pem</code> format.</td>
    </tr>
  </table>

2. Optional: Provide a **Secondary certificate** that is used if signature validation fails on the primary certificate. If the signing key remains the same, {{site.data.keyword.appid_short_notm}} does not block authentication for expired certificates.

3. Update the **Provider Name**, and click **Save**. The default name is SAML.


### Testing your configuration

You can test the configuration between your SAML Identity Provider and {{site.data.keyword.appid_short_notm}}.

1. Be sure that you've saved your configuration.
2. Navigate to the **SAML 2.0** tab of the {{site.data.keyword.appid_short_notm}} dashboard and click **Test**. A new tab opens.
3. Login in with a user that your identity provider has already authenticated.
4. After you complete the form, you are redirected to another page.
  * Successful authentication: The connection between {{site.data.keyword.appid_short_notm}} and the Identity Provider is working correctly. The page displays valid [access and identity tokens](/docs/services/appid/authorization.html#key-concepts).
  * Failed authentication: The connection is broken. The page displays the errors and the SAML response XML file.
