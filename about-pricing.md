---

copyright:
  years: 2022, 2023
lastupdated: "2023-10-02"

keywords: authentication, authorization, app id cost, identity, app security, cloud directory, app id pricing

subcollection: appid

---

{{site.data.keyword.attribute-definition-list}}

# How does {{site.data.keyword.appid_short_notm}} calculate pricing?
{: #pricing}

When you work with {{site.data.keyword.appid_short_notm}}, you are charged based on the number of monthly active users (MAU) and advanced security events triggered by MAU.
{: shortdesc}

For the most up-to-date pricing information, you can create a cost estimate by clicking **Add to estimate** in the {{site.data.keyword.appid_short_notm}} section of the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog/services/app-id).
{: tip}

## Pricing plans
{: #pricing-plans}

The service offers one Standard pricing plan that allows a number of monthly active users (MAU). With the Standard pricing plan, your first 50,000 business-to-consumer (B2C) MAU, 100 business-to-employee (B2E) MAU, and 100 Advanced MAU are free each month.

   * A B2C MAU is any unique Cloud Directory user, Google user, Facebook user, or anonymous user that has signed in by using your service. For example, if a user signs in with Facebook and later signs in by using Google, they are considered two separate active users. Additionally, Cloud Directory users are considered active by using the change password, forget password flow, or by logging out.
   * A B2E MAU is any unique SAML or custom IDP user that has signed in by using your service.
   * Machine to machine (M2M) is when backend services interact with your app and require authorization to perform specific actions. App ID verifies that the entity that makes the request is authorized and returns access and identity tokens to your app. All M2M token generation requests are free.
   * An Advanced MAU is when two-factor authentication, runtime activity, or advanced password policy is enabled when a B2C user is active or when runtime activity is enabled when a B2E user is active.

The following table shows the pricing tiers for a Standard plan.


| Tiers                  | Pricing |
|------------------------|----------------------|
| 1 - 50,000             | Free                 |
| 50,001 - 100,000       | $0.0055 USD          |
| 100,001 - 1,000,000    | $0.0046 USD          |
| 1,000,001 - 10,000,000 | $0.0032 USD          |
| 10,000,001+            | $0.0025 USD          |
{: class="simple-tab-table"}
{: caption="Table 1. Standard pricing plan for business-to-consumer monthly active user (B2C MAU)" caption-side="bottom"}
{: #B2C}
{: tab-title="B2C MAU"}
{: tab-group="standard-pricing-plan"}

| Tiers   | Pricing  |
|---------|----------------------|
| 1 - 100 | Free                 |
| 101+    | $0.0012 USD          |
{: class="simple-tab-table"}
{: caption="Table 1. Standard pricing plan for business to employee monthly active user (B2E MAU)" caption-side="bottom"}
{: #B2E}
{: tab-title="B2E MAU"}
{: tab-group="standard-pricing-plan"}

| Tiers               | Pricing  |
|---------------------|----------------------|
| 1 - 100             | Free                 |
| 101 - 50,000        | $0.035 USD           |
| 50,001 - 100,000    | $0.015 USD           |
| 100,001 - 1,000,000 | $0.012 USD           |
| 1,000,001+          | $0.01 USD            |
{: class="simple-tab-table"}
{: caption="Table 1. Standard pricing plan for advanced monthly active user (MAU)" caption-side="bottom"}
{: #advanced-MAU}
{: tab-title="Advanced MAU"}
{: tab-group="standard-pricing-plan"}

## What are monthly active users (MAU)?
{: #authorized-users-pricing}

A MAU is a unique user that signs in with your service whether directly or indirectly, including anonymous users. You are charged for one MAU each time a user signs in to your application triggering an authentication or security event. For example, if a user signs in with Facebook and later signs in by using Google, they are considered two separate MAU. An authentication event happens when you issue a new regular or anonymous access token. Tokens can be issued in response to a sign in request that is initiated by the user, or by an app on behalf of the user. By default, your users' access tokens are valid for one hour and anonymous tokens are valid for 30 days. After the tokens expire, your users must create a new token to access protected resources. You can manage the expiration time of your {{site.data.keyword.appid_short_notm}} tokens on the **Manage Authentication > Authentication Settings** page of the service dashboard.


## What are advanced security features?
{: #security-features-pricing}

You can strengthen the security of your application with advanced security features such as Multi-Factor authentication (MFA), runtime activity tracking, and password policy management. An advanced authentication event happens when you issue tokens for advanced security features.

By default, advanced features are disabled. You incur an extra charge when you enable them. For example, if you obtain 10,000 access tokens, then you turn on password policy management and obtain 10,000 more. You would pay for 20,000 authentication events and 10,000 advanced security events. If you disable all the advanced features, your account reverts to the original-cost policy.

| Feature | Benefit |
|-----|----|
|Multi-factor authentication | With [MFA for Cloud Directory](/docs/appid?topic=appid-cd-mfa#cd-mfa), you can confirm a user’s identity by requiring them to enter a one time passcode that is sent to their email or SMS after they enter their email and password. |
| Runtime authentication activity tracking | By integrating {{site.data.keyword.at_short}} with {{site.data.keyword.appid_short_notm}}, you can track different types of authentication events at run time. For example, a password reset request, authentication failures, or a user logout. For more information, see [Viewing runtime events](/docs/appid?topic=appid-at-events#at-monitor-runtime). |
| Password policy management | As an account owner, you can enforce more secure passwords for Cloud Directory by configuring a set of rules that user passwords must conform to. Examples include, the number of attempted sign-ins before lockout, expiration times, minimum time span between password updates, or the number of times that a password can't be repeated. For a complete list of the options and setup information, see [Advanced password management](/docs/appid?topic=appid-cd-strength#cd-advanced-password). |
{: caption="Table 1. Description of the benefits that are gained with advanced authentication events" caption-side="top"}

## How do I stop getting charged for {{site.data.keyword.appid_short_notm}}?
{: #stop-charge}

If you no longer want to be charged for security events and MAU, you need to ensure that no user can authenticate by using {{site.data.keyword.appid_short_notm}}. You must remove the {{site.data.keyword.appid_short_notm}} configuration from your app code or confirm that your users are not able to use the configuration to log in to your app. To stop getting charged for advance security features, you must disable them on the **Manage Authentication > Authentication Settings** page of the service dashboard.
