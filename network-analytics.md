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

# Network Analytics (beta)
{: #network-analytics}


With {{site.data.keyword.security-advisor_long}}, you can gain insight into potentially hazardous network communication that is related to your {{site.data.keyword.containerlong_notm}} clusters. To preview this capability, click the arrow on the Network Analytics card in the **{{site.data.keyword.security-advisor_short}} Tools** section of the [**Capabilities** page](https://console.bluemix.net/security/advisor/#!/overview).
{: shortdesc}

The Network Analytics preview is available in the US-South region only.
{: note}

The Network Analytics preview feature consists of three modules:

1. **Net-flow collecting agent**: Installed on your cluster, the agent collects network information and sends it to the analytics backend. Read more about [data collection](#data-collection).

2. **Analytics backend**: The analytics backend identifies suspicious communication to and from the cluster. It uses threat intelligence that is offered by [IBM X-Force![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/security/xforce) to interpret the network information. When a suspicious communication is identified, the analytics backend monitors such communications and sends out security findings to the {{site.data.keyword.security-advisor_short}} dashboard.

3. **{{site.data.keyword.security-advisor_short}} dashboard**: Findings and KPIs from the analytics backend are presented in two cards:

   - **Suspicious Clients (incoming traffic)**: This card shows KPIs and Findings regarding suspicious external clients that are accessing the cluster, such as when a member of a botnet approaches one of the cluster IPs. Learn more about [suspicious clients](#suspicious-clients).
   - **Suspicious server IPs (outgoing traffic)**: This card shows KPIs and Findings that have [suspicious server IPs](#suspicious-server-ips) that run as part of the cluster. Example: When the cluster approaches a server that is suspected to distribute malware.


## Data collection
{: #analytics-data-collection}

{{site.data.keyword.security-advisor_short}} can help protect your cluster by adding network monitoring. Deployed as part of your cluster, network monitoring is used to provide information about cluster communications. To enable Network Analytics, network flow information is collected about the communication that takes place between the cluster and external entities.
{: shortdesc}

The following information is collected:

* The IP address of the peers that are communicating
* The ports that they use
* The set of protocols that are being used
* The amount of data that is transferred
* A set of protocol-specific parameters
* Various time stamps.

**The actual data that is exchanged is not collected**.

Network monitoring works as part of the cluster with other services such as {{site.data.keyword.loganalysisshort_notm}} so that you can focus on the business logic. You can review the network monitoring insights in your {{site.data.keyword.security-advisor_short}} dashboard.


## Suspicious clients (incoming traffic)
{: #analytics-suspicious-clients}

The {{site.data.keyword.security-advisor_short}} dashboard includes a suspicious client card that summarizes various information about communications in which the cluster acts as a server that is approached by an external client.
{: shortdesc}

Analyzed communication might produce a finding such as:

- An external client with poor reputation, such as a client that is known to distribute malware or is associated with anonymous services, approaches one of the cluster associated URLs or IPs. For example, a scanner approaches one of the cluster open ports. Such communication might suggest inadequate protection of cluster associated URLs and IPs, and also pending or actual hazards.


## Suspicious server IPs (outgoing traffic)
{: #analytics-suspicious-server-ips}

The {{site.data.keyword.security-advisor_short}} dashboard includes a suspicious server IP card that summarizes various information about communications in which the cluster acts as a client that approaches an external server.
{: shortdesc}

Analyzed communication might produce a finding such as:

- A client from within the cluster, such as workload deployment, approaches an external node with poor reputation, such as a botnet. Such communication might suggest that the workload is compromised and requires attention by your security team. The finding varies based on the reputation of the approached external node, the communication patterns, and the level of certainty offered by the intelligence.

- The cluster URL or one of its IPs has poor reputation. Review a poor reputation to check that the cluster is not compromised or otherwise engaged in unacceptable activity.
