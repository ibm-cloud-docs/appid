---

copyright:
  years: 2017, 2025
lastupdated: "2025-05-01"

keywords: authentication, authorization, app id cost, identity, app security, cloud directory, app id pricing

subcollection: appid

---

{{site.data.keyword.attribute-definition-list}}

# How does  {{site.data.keyword.appid_short_notm}} calculate pricing?
{: #pricing}

When you work with  {{site.data.keyword.appid_short_notm}}, you are charged based on the number of authentication events, the number of authorized users, and the number of advanced security events.
{: shortdesc}

For the most up-to-date pricing information, you can create a cost estimate by clicking **Add to estimate** in the  {{site.data.keyword.appid_short_notm}} section of the [{{site.data.keyword.cloud_notm}} catalog](/catalog/services/app-id).
{: tip}

## Pricing plans 
{: #pricing-plans}

The service offers two pricing plans.

Lite
:   Each month, your first 1000 authentication events and 1000 authorized users per service instance are free, except for any advanced security events. You incur an extra charge for any advanced security events. In this plan, you can issue access and anonymous tokens when a user or an app initiates a sign-in request.

Graduated tier
:   In the graduated tier plan, you are charged each month after you reach the limits of the lite plan. The cost is based on the summary of three parts: the number of authentication events, the number of authorized users, and the number of advanced security events.

    For example, if these quantities are in the 1 - 10,000 tier, the charge for each authentication event, authorized user, and advanced security event is assessed by multiplying each quantity by the unit price that is set for that tier. Then, the total price is calculated by combining the charges for authentication events, authorized users, and advanced security events.

## What are authorized users?
{: #authorized-users-pricing}

An authorized user is a unique user that signs in with your service whether directly or indirectly, including anonymous users. You are charged for one authorized user each time a new user signs in to your application, including anonymous users. For example, if a user signs in with Facebook and later signs in by using Google, they are considered two separate authorized users. The total number of your authorized users includes future users that you preregistered to your app because you already know who they are going to be. You are charged for each future user at the time of registration. For example, you work at a company and recently hired a team lead. When you preregister them to your application, they become an authorized user and count toward your total. As an authorized user, they can sign in for the first time without needing to interact with you. [Learn more](/docs/appid?topic=appid-preregister).

## What are authentication events?
{: #authentication-events-pricing}

An authentication event happens when you issue a new regular or anonymous access token. Tokens can be issued in response to a sign-in request that is initiated by the user, or by an app on behalf of the user. By default, your users' access tokens are valid for 1 hour and anonymous tokens are valid for 30 days. After the tokens expire, your users must create a new token to access protected resources. You can manage the expiration time of your  {{site.data.keyword.appid_short_notm}} tokens on the **Manage Authentication > Authentication Settings** page of the service dashboard.


## What are advanced security features?
{: #security-features-pricing}

You can strengthen the security of your application with advanced security features such as Multi-Factor authentication (MFA), runtime activity tracking, and password policy management. An advanced authentication event happens when you issue tokens for advanced security features.

By default, advanced features are disabled. You incur an extra charge when you enable them. For example, if you obtain 10,000 access tokens, then you turn on password policy management and obtain 10,000 more. You would pay for 20,000 authentication events and 10,000 advanced security events. If you disable all the advanced features, your account reverts to the original-cost policy.

| Feature | Benefit |
|-----|----|
| Multi-factor authentication | With [MFA for Cloud Directory](/docs/appid?topic=appid-cd-mfa#cd-mfa), you can confirm a user’s identity by requiring them to enter a one time passcode that is sent to their email or SMS after they enter their email and password. |
| Runtime authentication activity tracking | By integrating {{site.data.keyword.at_short}} with {{site.data.keyword.appid_short_notm}}, you can track different types of authentication events at run time. For example, a password reset request, authentication failures, or a user logout. |
| Password policy management | As an account owner, you can enforce more secure passwords for Cloud Directory by configuring a set of rules that user passwords must conform to. Examples include, the number of attempted sign-ins before lockout, expiration times, minimum time span between password updates, or the number of times that a password can't be repeated. For a complete list of the options and setup information, see [Advanced password management](/docs/appid?topic=appid-cd-strength#cd-advanced-password). |
{: caption="Description of the benefits that are gained with advanced authentication events" caption-side="top"}

These features are available only to those instances that are on the graduated tier pricing plan and that were created after 15 March 2018.
{: note}

## When am I charged?
{: #when-charge}

Your first 1000 authentication events and 1000 authorized users per service instance are free of charge. You are charged monthly for any additional authentication events and authorized users, as well as any advanced security features that are enabled for each service instance.

## How do I stop getting charged for  {{site.data.keyword.appid_short_notm}}?
{: #stop-charge}

If you no longer want to be charged for authentication events and authorized users, you need to ensure that no user can authenticate by using  {{site.data.keyword.appid_short_notm}}. You must remove the  {{site.data.keyword.appid_short_notm}} configuration from your app code or confirm that your users are not able to use the configuration to log in to your app. To stop getting charged for advance security features, you must disable them on the **Manage Authentication > Authentication Settings** page of the service dashboard.
