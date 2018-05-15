---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# About
{: #about}

You can use {{site.data.keyword.appid_full}} to add authentication to your apps and protect your back-end resources.
{:shortdesc}

## Reasons to use the service
{: #reasons}

Why would you want to use {{site.data.keyword.appid_short_notm}}? Check out the following scenarios to see whether any of them apply to you.
{: shortdesc}

<table>
  <tr>
    <th> Scenario </th>
    <th> Reason </th>
  </tr>
  <tr>
    <td> You need to add [authorization and authentication](/docs/services/appid/authorization.html) to your mobile and web apps but don't have a background in security. </td>
    <td> {{site.data.keyword.appid_short_notm}} makes it easy to add an authentication step to your apps. You can use the service to communicate with [identity providers](/docs/services/appid/identity-providers.html) to manage access to your apps. </td>
  </tr>
  <tr>
    <td> You want to limit access to your apps and back-end resources. </td>
    <td> The service gives you the ability to [protect your resources](/docs/services/appid/protecting-resources.html) for both authenticated and anonymous users. </td>
  </tr>
  <tr>
    <td> You want to build personalized app experiences for your users. </td>
    <td> With {{site.data.keyword.appid_short_notm}}, you can [store user data](/docs/services/appid/user-profile.html) such as app preferences or information from their public social profiles, and then use that data to customize each experience of your app. </td>
  </tr>
  <tr>
    <td> You want to give users the ability to gain access to your app with their email and a password. </td>
    <td> {{site.data.keyword.appid_short_notm}} allows you to create a [cloud directory](/docs/services/appid/cloud-directory.html), which makes it possible for you to add user sign-up and sign-in to your apps. Cloud directory provides you with the framework to maintain a user registry that can scale with your user base. With the pre-built functionality for self service, such as email verification and password resets, you can be sure that your app is authenticating users securely. </td>
  </tr>
</table>


## Integrations
{: #integrations}

You can use {{site.data.keyword.appid_short_notm}} with other {{site.data.keyword.Bluemix_notm}} offerings.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>By configuring ingress in a standard cluster, you can secure your apps at the cluster level. Check out the {{site.data.keyword.appid_short_notm}} authentication ingress annotation to get started.</dd>
  <dt>{{site.data.keyword.openwhisk}} and API Connect</dt>
    <dd>When you create your APIs with [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) and [API Connect](/docs/apis/management/manage_apis.html), you can secure your applications at the gateway rather than in your app code. To see the integration in action, watch <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Try out one of our sample Cloud Foundry apps to see how you can integrate app id into your apps.</dd>
  <dt>iOS Programming Guide</dt>
    <dd>Do you develop apps for Apple? Try out the <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS Programming Guide <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> to learn, experiment, and enhance your existing iOS apps with {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

## Cross regional disaster recovery
{: #recovery}

Issues can arise when working with technology. With that in mind, {{site.data.keyword.appid_short_notm}} is built to support disaster recovery. You can build your apps with recovery in mind as well.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} is a highly resilient service that is run on  {{site.data.keyword.containerlong_notm}} which provides the ability to replicate clusters, worker nodes, and pods across regions. With multiple regions that support several availability zones, we are able to provide regional high availability.

You can implement cross-regional disaster recovery for your services by using the {{site.data.keyword.appid_short_notm}} management API. With the API, you can perform administrative tasks like copying service configurations across instances of the service in different regions or synchronizing Cloud Directory and user profiles. With the API, you can ensure that the changes that you apply to an {{site.data.keyword.appid_short_notm}} instance in your primary region are applied across the board.

To ensure updates and failover across {{site.data.keyword.appid_short_notm}} instances in different regions, you might want to consider the following:

* Synchronize your service instance configuration. This might include your identity provider, login widget customization, or email templates.
* Synchronize Cloud Directory users and user profiles by using the management API.
* Synchronize app failover from a primary instance to a secondary instance by adding both instance configurations. This might include URLs, client_ids, secrets, and more.
* Synchronize any other areas that you want to replicate.
