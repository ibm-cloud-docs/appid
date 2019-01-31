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

# Integrations
{: #integrations}

With {{site.data.keyword.security-advisor_long}}, you can integrate other built-in insights, partner solutions, or create your own custom integrations.
{: shortdesc}


## Pre-integrated findings
{: #integrate-built-in}

With {{site.data.keyword.security-advisor_long}}, you can gain insight into potential issues through built-in service capabilities.
{: shortdesc}


Out of the box {{site.data.keyword.security-advisor_short}} integrates with:

* Certificate Manager for notifications that are related to certificate expiry and lifecycle.
* Vulnerability Advisor for details on image vulnerabilities and configuration issues.

To learn more, check out [Taking advantage of pre-integrated services](setup.html)!

</br>

## Partner solutions
{: #integrate-partner}

Partner solutions are a way to enhance security for your IBM Cloud deployments by by creating a link between {{site.data.keyword.security-advisor_short}} and other security tools outside of IBM Cloud.
{: shortdesc}

Current {{site.data.keyword.security-advisor_short}} partners include Neuvector.

Are you a partner and interested in integrating your solution with {{site.data.keyword.security-advisor_short}}? Reach out to our team by contacting Matt Ward at wardm@us.ibm.com!
{: tip}

### NeuVector
{: #integrate-neuvector}

[NeuVector](https://neuvector.com/) provides a highly integrated, automated security platform for Kubernetes and Red Hat OpenShift that allows you to monitor and protect container network traffic. Specifically, East-West network traffic.

With NeuVector, you can detect network threats and violations to prevent attacks of your container based applications. Through monitoring, you can prevent exploits and breakouts by detecting root privilege escalations, port scans, reverse shells, and suspicious file system activity in your containers and hosts.

For help setting up your NeuVector instance, see [Partner solutions](partners.html#neuvector).



## Custom integrations
{: #integrate-custom}

You might already have a security tool that you depend on. You can integrate that tool with the {{site.data.keyword.security-advisor_short}} dashboard so that all of your security information is centralized in one place!
{: shortdesc}

**Integrating your own tools with the GUI**

By using the {{site.data.keyword.security-advisor_short}} GUI, you can bookmark your internal and external security tools so that you have one point of access to everything from the {{site.data.keyword.security-advisor_short}} dashboard. For example, you could bookmark PagerDuty.

**Integrating your own tools with the API**

With the Findings API, you can integrate findings from your custom security tools into the {{site.data.keyword.security-advisor_short}} dashboard. This could be any custom or partner tool that generates a security alert or finding that also supports API based interaction.

**Get started**

To learn the recommended practice on how to leverage the APIs and create bookmarks through the GUI, see [Custom security tools](/docs/services/security-advisor/custom.html).

</br>





## Network Analytics (preview)
{: #integrate-network-analytics}

With the network analytics preview, you can detect threats by monitoring your {{site.data.keyword.containerlong_notm}} cluster communication.
{: shortdesc}

By monitoring cluster communication for suspicious communication to and from your clusters, you can take advantage of threat intelligence that is offered by IBM X-Force to flag any potential issues. When a suspicious communication is identified, a finding is issued that you can review and evaluate.

For more detailed information about network analytics, see [Network analytics](network-analytics.html).
{: tip}



</br>
</br>
