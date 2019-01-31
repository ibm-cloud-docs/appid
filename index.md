---

copyright:
  years: 2019
lastupdated: "2019-01-31"

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

# Getting started tutorial
{: #index}

With {{site.data.keyword.security-advisor_long}}, you can instantly view the security posture of your {{site.data.keyword.Bluemix_notm}} through a single, centralized dashboard.
{:shortdesc}

{{site.data.keyword.security-advisor_short}} is a cloud service that is enabled by default for all {{site.data.keyword.Bluemix_notm}} accounts. As such, you do not need to provision any instance of the service.
{: tip}

The service receives security information from various sources and displays any security alerts or vulnerabilities that require your attention in the service dashboard. Out of the box, there are several pre-populated cards in your dashboard. These findings are from security services in IBM Cloud, but you can also add cards or custom partner solutions so that all of your security tools can be accessed from the same location.

Through pre-integrated findings, you can monitor:

- Certificates that you manage with {{site.data.keyword.cloudcerts_long_notm}}
- Vulnerabilities in container images that are stored in {{site.data.keyword.registrylong_notm}}

You can also gain insight into suspicious clients and potentially compromised containers that run on your {{site.data.keyword.containerlong_notm}} clusters. With the feature enabled and configured, cluster network communication, both incoming and outgoing, is collected and continuously monitored and analyzed based on threat intelligence. You can learn more by reading [Network analytics](network-analytics.html)

</br>

## Getting to the service dashboard
{: #start-dashboard}

Ready to get started? You can get to the service dashboard in one of the following ways:

<ul>
  <li>By using the tile:
    <ol>
      <li>Log in to <a href="https://console.cloud.ibm.com/catalog/" target="_blank">{{site.data.keyword.Bluemix_notm}}<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</li>
      <li>Navigate to the **Catalog** and click **Security and Identity**.</li>
      <li>Select the {{site.data.keyword.security-advisor_short}} tile. A dashboard opens where you can view security information for the preconfigured integrated tools such as vulnerability advisor and certificate manager.</li>
    </ol>
  </li>
  <li>By using the menu:
    <ol>
      <li>Log in to <a href="https://console.cloud.ibm.com" target="_blank">{{site.data.keyword.Bluemix_notm}}<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</li>
      <li>From your dashboard, click the hamburger menu to expand your options.</li>
      <li>Click **Security**. An overview of the security dashboard opens.</li>
      <li>Click **Getting Started** in the navigation to see general overview information about the service, or click **Dashboard** if you prefer to learn by seeing the service in action.</li>
    </ol>
  </li>
</ul>

Are your pre-integrated findings not displaying any information? You might not have any certificates or images for {{site.data.keyword.security-advisor_short}} to monitor. Learn more about what {{site.data.keyword.security-advisor_short}} needs to populate the dashboard cards in [Leveraging pre-integrated services](setup.html).

</br>

## Next steps
{: #start-next}

Now that you've seen the dashboard in action, [learn more](about.html) about how {{site.data.keyword.security-advisor_short}} can help you. You can also send user feedback by using [developerWorks](ts_index.html) to contribute ideas for the service as it develops.

</br>

## Availability
{: #start-availability}

Currently, you can take advantage of {{site.data.keyword.security-advisor_short}} in the Dallas, and London regions.
