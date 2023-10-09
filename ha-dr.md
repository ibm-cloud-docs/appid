---

copyright:
  years: 2017, 2023
lastupdated: "2023-10-09"

keywords: HA for {{site.data.keyword.appid_short_notm}}, DR for {{site.data.keyword.appid_short_notm}}, high availability for {{site.data.keyword.appid_short_notm}}, disaster recovery for {{site.data.keyword.appid_short_notm}}, failover for {{site.data.keyword.appid_short_notm}}

subcollection: appid

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
{:beta: .beta}
{:term: .term}
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
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}
{:release-note: data-hd-content-type='release-note'}

# Understanding high availability and disaster recovery for {{site.data.keyword.appid_short_notm}}
{: #ha-dr}

{{site.data.keyword.appid_full}} is a highly available, regional service that runs in the following regions:

* Dallas (`us-south`)
* Frankfurt (`eu-de`)
* London (`eu-gb`)
* Osaka (`jp-osa`)
* Sao Paulo (`br-sao`)
* Sydney (`au-syd`)
* Tokyo (`jp-tok`)
* Toronto (`ca-tor`)
* Washington (`us-east`)

In each supported region, {{site.data.keyword.appid_short_notm}} exists in multiple availability zones with no single point of failure. In addition to the zones, you can set up policies for cross-regional failover or cross-regional disaster recovery. However, this process is not automatic. 

To establish cross-region high availability and implement a recovery plan, you must create and maintain backup instances in multiple regions. To synchronize a service instance in one region with an instance in another region, you can use only the [management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external} or a combination of the [management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/) and the [{{site.data.keyword.cloud_notm}} Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external} provider. 

Backing up and restoring your {{site.data.keyword.appid_short_notm}} instance to ensure cross-regional availability requires a few basic steps. You must:

1. Define the policies for configuring the storage of the backup of your {{site.data.keyword.appid_short_notm}} instance. This configuration includes planning how the data, such as the user profiles and Cloud Directory users, is to be stored in your instance's backup. 

  Create the backup system before an outage incident occurs in your primary location. To maintain continuous protection, as recommended, automate the process to generate the backup and run it periodically.
  {: tip} 

2. Create and configure an instance of {{site.data.keyword.appid_short_notm}} in another region (for example, a secondary location).
3. Set up a process to store the backup and restore it in the {{site.data.keyword.appid_short_notm}} instance that is in the secondary location.

To learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}, see [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime) or [Service Level Agreements](/docs/overview?topic=overview-slas).