---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-04"

keywords: Authentication, authorization, identity, app security, secure, rates, cloud directory, rate limit, attempts

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


# {{site.data.keyword.appid_short_notm}} limits
{: #limits}

Rate limiting is used to control the amount of traffic that is coming and going through your instance of {{site.data.keyword.appid_full}}. By limiting requests or resources, you can protect your applications.
{: shortdesc}

## {{site.data.keyword.appid_short_notm}} lite plan 
{: #lite-limits}

Review the following table to see the limits that are in place for lite instances of {{site.data.keyword.appid_short_notm}}. 

<table>
    <tr>
        <th>Resource</th>
        <th>Maximum</th>
    </tr>
    <tr>
        <td>Users</td>
        <td>1000</td>
    </tr>
    <tr>
        <td>Authentications</td>
        <td>1000 per month</td>
    </tr>
</table>

## General
{: #general-limits}

The following table lists the maximum per user limits for {{site.data.keyword.appid_short_notm}} resources and the blocking period when the limits are exceeded. These limits apply to any user who can create {{site.data.keyword.appid_short_notm}} resources.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Limit</th>
        <th>When Exceeded</th>
    </tr>
    <tr>
        <td>Sign in attempts by one user</td>
        <td>11 per minute</td>
        <td>User unable to sign in for 1 minute.</td>
    </tr>
    <tr>
        <td>Update user profile attributes</td>
        <td>5 per minute</td>
        <td>User unable to update profile for 1 minute.</td>
    </tr>
        <td>Delete user profile attributes</td>
        <td>5 per minute</td>
        <td>User unable to update profile for 1 minute.</td>
    </tr>
</table>



## Cloud Directory
{: #limits-cd}

Review the following table to see limits that are associated with Cloud Directory.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Configurable</th>
        <th>Limit</th>
        <th>When Exceeded</th>
    </tr>
    <tr>
        <td>Sign in attempts per account</td>
        <td>Yes</td>
        <td>Unlimited</td>
        <td>All sign-in attempts for the instance are blocked for one minute.</td>
    </tr>
    <tr>
        <td>Sign up attempts per account</td>
        <td>Yes</td>
        <td>Unlimited</td>
        <td>All sign-up attempts for the instance are blocked for one minute.</td>
    </tr>
    <tr>
        <td>Email sending request</td>
        <td>No</td>
        <td>10 emails in 5 minutes per user</td>
        <td>Email requests for the user are blocked for 30 minutes.</td>
    </tr>
    <tr>
        <td>SMS sending request</td>
        <td>No</td>
        <td>10 SMS in 5 minutes per user</td>
        <td>SMS requests for the user are blocked for 30 minutes.</td>
    </tr>
</table>

For more information, see the [rate limit management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig){: external}.