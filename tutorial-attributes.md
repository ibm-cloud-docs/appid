---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-21"

keywords: attributes, cloud directory, user registry, user management, personalization, customize app, user information, profiles, app security, user profile, app access, identity

subcollection: appid

content-type: tutorial
account-plan: lite
completion-time: 20m

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


# Customizing your user experience
{: #tutorial-attributes}
{: toc-content-type="tutorial"}
{: toc-completion-time="20m"}


In a world with everything at our finger tips, people expect their experiences to be tailored to them. Whether we're having an in-person conversation or shopping online, we want to see only the things that apply to us. By using this step-by-step guide, you can learn how to harness the power of user attributes and really capture your users attention with {{site.data.keyword.appid_short_notm}}.
{: shortdesc}


## Scenario
{: #attributes-scenario}

You're a developer for an online retailer, with a specialization in food. You're tasked with creating a personalized experience for your app users. You decide to focus your efforts on creating targeted advertising based on things that you know about your users. So, when a user signs up for your app, you ask them a few questions with answers that they can choose from. For example, you might ask the following question:

Do you have any dietary preferences?

  * I'm a vegetarian.
  * I'm a pescatarian.
  * I'm dairy-free.
  * I'm gluten-free.
  * I'm low carb.

You can then map their answers to [specific attributes](/docs/appid?topic=appid-profiles) that you can use to target the advertising that they're shown. 

Although this tutorial is written for web apps that use Cloud Directory, attributes can be used in a much broader sense. Custom attributes can be anything that you want them to be! As long as you stay under 100k attributes and you format them as a plain JSON object, you can store all types of information.
{: note}


## Before you begin
{: #attributes-before}

Ready? Let's get started!

Be sure that you have the following prerequisites before you begin:
- An instance of the {{site.data.keyword.appid_short_notm}} service
- A set of service credentials

New to the APIs? Try them out with this [Postman collection](https://github.com/ibm-cloud-security/appid-postman).
{: tip}


## Configuring your {{site.data.keyword.appid_short_notm}} instance
{: #attributes-configure-app}
{: step}

Before you can start adding attributes for your users, you need to configure your instance of {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

1. In the **Identity Providers** tab of the service dashboard, enable **Cloud Directory**. Although this tutorial focuses [Cloud Directory](/docs/appid?topic=appid-cloud-directory), you might also choose to use any of the other IdP's such as [SAML](/docs/appid?topic=appid-enterprise), [Facebook](/docs/appid?topic=appid-social#facebook), [Google](/docs/appid?topic=appid-social#google), or a [custom provider](/docs/appid?topic=appid-custom-identity).

2. In the **Cloud Directory > Email Verification** tab, enable verification and set **Allow users to sign-in to your app without first verifying their email address** to **Yes**.

3. Optionally, in the **Profiles** tab, set **Change custom attributes from the app** to **Enabled**. This allows users to update their attributes after they've answered your initial questionnaire.

Excellent! Your dashboard is configured and you're ready to start setting attributes.


## Creating user attributes
{: #attributes-set}
{: step}

When your users interact with your questionnaire, you can map their answers to specific attributes and then add those attributes to their file. 

Your application is responsible for mapping the answers to the specific attributes that you want to add to the profile.
{: note}


1. Update the profile with the attribute.

  ```
  curl --request PUT \
  https://<region>.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user_id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  -d '{
    "profile": {
      "attributes": {
        “food-preference”: “vegetarian, glutten-free”
      }
    }
  }'
  ```
  {: codeblock}

2. View the profile to verify that it was updated correctly.

  ```
  curl --request GET https://<region>.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user_id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Successful response output:

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
        "food-preference": "vegetarian, gluten-free"
      }
  }
  ```
  {: screen}

Great work!


## Injecting attributes into tokens
{: #attributes-tokens}
{: step}

Becoming more popular, you decide to implement a "deal-of-the-day". You want the first thing that the user sees when they sign in to your application to be a coupon for something that matches their dietary preferences. You can achieve this by injecting the attributes that are stored in their profiles into their tokens. By having the information available at runtime, you can have your application make a custom decision on the spot about which deal to show. 
{: shortdesc}

[Token configuration](/docs/appid?topic=appid-customizing-tokens#customizing-tokens) is global, which means that it applies to every user with the same attribute.
{: tip}


1. Make a request to the token configuration endpoint.

  ```
  curl --request PUT \
  https://<region>.appid.cloud.ibm.com/management/v4/<tenant-id>/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  -d '{
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
        {
        "source": "attributes",
        "sourceClaim": "food-preference"
        }
      ]
  }'
  ```
  {: codeblock}

  <table>
    <caption>Table 1. Token configuration variables</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td>
      <td>A tenant ID is how your instance of {{site.data.keyword.appid_short_notm}} is identified in the request. You can find your ID in the <em>Service credentials</em> tab of the dashboard. If you don't have a set, you can follow the steps in the GUI to create credentials.</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>For both <code>accessTokenClaim</code> and <code>idTokenClaims</code> set the source to <code>attribute</code>.</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>The specific attribute that you want to map to your token. In this case, <code>food-preference</code></td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>This value applies to each token type and must be set in each request. If you previously set the value in the GUI, and then run this request, then the values in the request override the previously set values. Be sure to set the expiration to the correct value for your configuration.</td>
    </tr>
  </table>

  Successful response output:

  ```
  {
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
        {
        "source": "attributes",
        "sourceClaim": "food-preference"
        }
      ]
  }
  ```
  {: screen}


## Viewing the access token
{: #attributes-view-token}
{: step}

Optionally, you can verify that step 4 was successful by viewing an access token.
{: shortdesc}

1. For testing purposes, create a Cloud Directory user by using the {{site.data.keyword.appid_short_notm}} GUI.

  1. In the **Users** tab, click **Add User**. A form displays.
  2. Enter a first and surname, an email, and password.
  3. Click **Save**.

2. Encode your client ID and secret.

  1. In the **Service Credentials** tab of the {{site.data.keyword.appid_short_notm}} GUI, copy your client ID and Secret.
  2. Use a base64 encoder to encode your authorization information.
  3. Copy the output to use in the following command.

  It is not recommended to use a browser-based encoder in production applications.
  {: tip}

4. Sign in by using the APIs to obtain your access token information. The token that is returned is encoded.

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded_client:secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  -d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: codeblock}

5. Decode your access token.
  1. Copy the token in the response output from the previous command.
  2. In a browser, navigate to https://jwt.io/.
  3. Paste the token into the box labeled **Encoded**.

  It is not recommended to use a browser-based decoder in production applications.
  {: tip}

6. In the **Decoded** section, verify that you can see the food preference.

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "food-preference": "vegetarian, gluten-free"
  }
  ```
  {: screen}



## Next steps
{: #attributes-next}

Nice work! You completed the tutorial. Next, you can try configuring [multi-factor authentication](/docs/appid?topic=appid-cd-mfa) or setting up [your own branded GUI](/docs/appid?topic=appid-branded).

