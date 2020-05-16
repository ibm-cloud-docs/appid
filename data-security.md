---

copyright:
  years: 2017, 2020
lastupdated: "2020-05-16"

keywords: data encryption in app id, data storage for app id, personal data in app id, data deletion for app id, data in app id, data security in app id

subcollection: appid

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:new_window: target="_blank"}
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




