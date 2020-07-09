---

copyright:
  years: 2017, 2020
lastupdated: "2020-07-09"

keywords: data encryption in app id, data storage for app id, personal data in app id, data deletion for app id, data in app id, data security in app id

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



# Securing your data in {{site.data.keyword.appid_short_notm}}
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.appid_full}}, it is important to know exactly what data is stored and encrypted and how you can delete any stored personal data.
{: shortdesc}


## How your data is stored and encrypted in {{site.data.keyword.appid_short_notm}}
{: #data-storage} 

{{site.data.keyword.appid_short_notm}} stores and encrypts user profile attributes. As a multi-tenant service, every tenant has a designated encryption key and user data in each tenant is encrypted with only that tenant's key. {{site.data.keyword.appid_short_notm}} ensures that private information is encrypted before it is stored.




## Deleting your data in {{site.data.keyword.appid_short_notm}}
{: #data-delete}

When you delete an instance of {{site.data.keyword.appid_short_notm}}, all of the user associated data is also deleted. When the service instance is deleted, a 7 day reclamation period begins. During that time, you are able to restore the instance and all of the associated user data. However, if the instance and data are permanently deleted, it cannot be restored. {{site.data.keyword.appid_short_notm}} does not store any data from permanently deleted instances.

The {{site.data.keyword.appid_short_notm}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.appid_short_notm}} service description, which you can find in the [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).


### Deleting an instance
{: #service-delete}

If you no longer need an instance of {{site.data.keyword.appid_short_notm}}, you can delete the service instance and any data that is stored. You can also choose to delete your service instance by using the console.

1. Delete the service and place it in a reclamation period of 7 days.

  ```
  ibmcloud resource service-instance-delete <service_name>
  ```
  {: codeblock}

2. Optional: To permanently delete your instance get the reclamation ID.

  ```
  ibmcloud resource reclamations --resource-instance-id <tenantId>
  ```
  {: codeblock}

  If you choose not to permanently delete the instance, the instance and data are still deleted at the end of the 7 day reclamation period.
  {: tip}

3. Optional: Permanently delete the reclamation instance.

  ```
  ibmcloud resource reclamation-delete <reclamationId>
  ```
  {: codeblock}

  If you permanently delete the instance, you cannot restore your data. 
  {: important}



### Restoring a deleted instance
{: #data-restore}

If you haven't permanently deleted your instance, you can restore it during the reclamation period.

1. Get the reclamation ID.

  ```
  ibmcloud resource reclamations --resource-instance-id <tenantId>
  ```
  {: codeblock}

2. Restore the reclamation.

  ```
  ibmcloud resource reclamation-restore <reclamationId>
  ```
  {: codeblock}

