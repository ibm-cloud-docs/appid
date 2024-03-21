---

copyright:
  years: 2017, 2023
lastupdated: "2023-01-18"

keywords: rate limits, traffic control, limit request, lite instances, per minute, per instance, per user, limits

subcollection: appid

---

{{site.data.keyword.attribute-definition-list}}

# Known issues and limitations
{: #known-issues-limits}

{{site.data.keyword.compliance_full}} includes the following known issues and limits that might impact your experience.
{: shortdesc}


## Limits
{: #limits}

{{site.data.keyword.appid_full}} is deprecated. As of 01 May 2024, you can't create new instances, and access to free instances will be removed. Existing instances are supported until 01 October 2025. Any instances that still exist on that date will be deleted. {: deprecated}

Rate limiting is used to control the amount of traffic that is coming and going through your instance of {{site.data.keyword.appid_full}}. By limiting requests or resources, you can protect your applications.



### General
{: #general-limits}

The following table lists the maximum per user limits for {{site.data.keyword.appid_short_notm}} resources and the blocking period when the limits are exceeded. These limits apply to any user who can create {{site.data.keyword.appid_short_notm}} resources.
{: shortdesc}

| Action | Limit | When exceeded |
|:-------|:------|:--------------|
| Sign in attempts by one user | 11 per minute | User unable to sign in for 1 minute. |
| Update user profile attributes | 5 per minute | User unable to update profile for 1 minute. |
| Delete user profile attributes | 5 per minute | User unable to update profile for 1 minute. |
| Roles per {{site.data.keyword.appid_short_notm}} instance | 50 |   |
| Scopes per application | 50 |   |
| Applications per {{site.data.keyword.appid_short_notm}} instance | 200 |   |
| Changes to instance by users within 24 hours | 10,000 | |
| Users per instance | 100,000 | |
| Management APIs requests per second | 50 per second | Requests are blocked for 30 seconds |
| All other APIs requests per second | 200 per second | Requests are blocked for 30 seconds |
{: caption="Table 2. General rate limits" caption-side="top"}



### Cloud Directory
{: #limits-cd}

Review the following table to see limits that are associated with Cloud Directory.
{: shortdesc}

| API | Configurable | Limit | When exceeded |
|:----|:-------------|:------|:------------- |
| Sign in attempts per account | Yes | 200 per second | All sign-in attempts for the instance are blocked for 1 minute. |
| Sign up attempts per account | Yes | 200 per second | All sign-up attempts for the instance are blocked for 1 minute. |
| Email sending request | No | 10 emails in 5 minutes per user | Email requests for the user are blocked for 30 minutes. |
| SMS sending request | No | 10 SMS in 5 minutes per user | SMS requests for the user are blocked for 30 minutes. |
| MFA code characters | No | 6 numeric characters | The code automatically has 6 characters that must be input by the user. |
| MFA code expiration | No | 15 minutes | If a user does not validate their code within 15 minutes, they can request that another code is sent as long as the authentication session is not expired. Within the authentication session, the code can be sent multiple times. Once the authentication session expires, the user must repeat the login process from the beginning. |
{: caption="Table 3. Cloud Directory limits" caption-side="top"}

For more information, see the [rate limit management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig){: external}.


### Ingress annotation
{: #annotation-limits}

Be sure to review the following limitations before you configure your annotation.

* Refresh tokens are not currently supported.
* {{site.data.keyword.containerlong}} supports one Ingress per namespace. If you already have one, you can update the existing Ingress configuration or use a different namespace.
* The annotation does not work behind a proxy.


### Extensions
{: #limits-extensions}

* The response from your pre-mfa extension point must not exceed 10 KB. If it does, the request is canceled and the user is required to complete MFA.
* If it takes {{site.data.keyword.appid_short_notm}} longer than 5 seconds to establish a connection to your pre-mfa extension point, or if the request takes longer than 7 seconds to complete, the request is canceled and the user is required to complete MFA.
