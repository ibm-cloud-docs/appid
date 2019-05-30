---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-30"

keywords: authentication, authorization, identity, app security, secure, rates, cloud directory, rate limit, attempts

subcollection: appid

---

{:new_window: target="_blank"}
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


# App ID limits
{: #limits}

Rate limiting is used to control the amount of traffic that is coming and going through your instance of App ID. By limiting requests or resources, you can protect your applications. There are also general limits in place for the App ID service.
{: shortdesc}

## App ID lite plan 
{: #lite-limits}

Review the following table to see the limits that are in place for lite instances of App ID. 

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

The following table lists the maximum limits for IBM Cloud App ID resources. These limits apply to any user who can create IBM Cloud App ID resources.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Maximum amount</th>
        <th>Maximum users</th>
    </tr>
    <tr>
        <td>Sign in attempts by one user</td>
        <td>5 per minute</td>
        <td>per user</td>
    </tr>
    <tr>
        <td>Update user profile attributes</td>
        <td>5 per minute</td>
        <td>per user</td>
    </tr>
        <tr>
        <td>Delete user profile attributes</td>
        <td>5 per minute</td>
        <td>per user</td>
    </tr>
</table>



## Cloud Directory 

Review the following table to see limits that are associated with Cloud Directory.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Maximum</th>
        <th>Configurable</th>
    </tr>
    <tr>
        <td>Sign in attempts per account</td>
        <td>Unlimited</td>
        <td>True</td>
    </tr>
    <tr>
        <td>Sign up attempts per account</td>
        <td>Unlimited</td>
        <td>True</td>
    </tr>
    <tr>
        <td>Email sending request</td>
        <td>10 in 10 minutes</br> If exceeded, email requests are blocked for 30 minutes.</td>
        <td>False</td>
    </tr>
</table>

For more information, see the <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">rate limit management API.</a>
