---

copyright:
  years: 2017, 2021
lastupdated: "2021-06-04"

keywords: custom identity provider, authorization, bring your own idp, proprietary idp, legacy idp, oauth, oidc, authentication, oatuh, app security, public key, jwt

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

# Custom
{: #custom-identity}

You can use your own custom identity provider when you authenticate. Your identity provider can conform to any authentication mechanism that is not specifically supported by {{site.data.keyword.appid_full}}, including proprietary.
{: shortdesc}

When {{site.data.keyword.appid_short_notm}} does not provide direct support for a particular identity provider, you can use the custom identity flow to bridge the authentication protocol to {{site.data.keyword.appid_short_notm}}'s existing authentication flow. For example, you want to use GitHub or LinkedIn to allow your users to sign in. You can use the identity provider's existing SDK to facilitate user authentication information before packaging and exchanging it with {{site.data.keyword.appid_short_notm}}. In many enterprise scenarios, a legacy identity provider might use its own custom authentication protocol, but you still want to leverage the capabilities of {{site.data.keyword.appid_short_notm}}. For this type of scenario, the custom identity flow provides a decoupled means of securely authenticating your users without exposing their credentials.

## Configuring custom identity
{: #custom-configure}

You can use the following steps to configure your custom identity provider to work with {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Before you begin
{: #custom-identity-before}

To establish trust between {{site.data.keyword.appid_short_notm}} and your custom identity provider, you must have an RSA PEM key pair with a minimum length of 2048. Be sure that you securely back up any keys that you use in production.

How are the keys used?

- Your private key is used in your app or identity provider to sign JWTs.
- Your public key is used by {{site.data.keyword.appid_short_notm}} to validate the JWT that contains user information.

To generate an RSA PEM key pair by using Open SSL, run the following command:

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}



### Configuring with the GUI
{: #custom-identity-configure-gui}

1. Sign in to your {{site.data.keyword.cloud_notm}} account and navigate to your instance of {{site.data.keyword.appid_short_notm}}.

2. In the **Manage** tab, set **Custom Identity Provider** to **On**.

3. Register your public key with {{site.data.keyword.appid_short_notm}}.
  1. Navigate to the **Custom Identity Provider** tab
  2. Paste your public key in the **Public Key** box and click **Save**.



### Configuring with the API
{: #custom-identity-configure-api}

Register your key by making a PUT request to the [Management API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_custom_idp).

```sh
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## Testing your configuration
{: #custom-identity-testing}

After you configure your {{site.data.keyword.appid_short_notm}} instance with a valid public key, you can use the test application that is provided by the service to verify that your configuration is correctly set up. In the example app, you can see {{site.data.keyword.appid_short_notm}} access and identity token payloads that are returned during a standard sign-in flow.

1. From the **Custom Identity Provider** tab, click **Test** to open the test application.

2. Create an [example JWT](https://jwt.io/) following the custom identity [protocol](/docs/appid?topic=appid-custom-auth#generating-jwts).

3. Paste your JWT into the box that is labeled **JSON Web Token** and click **Test** to execute a sample authentication.

If successful, you can now see the decoded {{site.data.keyword.appid_short_notm}} identity and access tokens that would be available to your application in a standard sign-in flow.

## Next steps
{: #custom-identity-next}

Now that your custom identity provider is configured, [add it to your application](/docs/appid?topic=appid-custom-auth#custom-auth)!
