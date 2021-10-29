---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-12"

keywords: Migrating users, multiple service instances, manage service, access, configuration, duplicate, export, app security, identity

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


# Managing service instances
{: #service-instance-management}

There are times when you might need to have more than one instance of {{site.data.keyword.appid_short_notm}} or migrate to a new instance. You might need to have an instance of {{site.data.keyword.appid_short_notm}}in multiple regions or different versions for different types of users. No problem! You can easily export your identity provider configuration. 
{: shortdesc}


## Migrating to another instance
{: #migrate-service}

You can migrate the information in one instance of {{site.data.keyword.appid_short_notm}} to another.
{: shortdesc}

1. Create a new instance of the service.

2. Duplicate your identity provider configuration by using the GUI.

3. [Migrate your user profiles](/docs/appid?topic=appid-user-admin). Known users are exported as a JSON object. Anonymous user's cannot be migrated. You can choose to import the entire object into the new instance or break it up and divide the users as you see fit if you have more than one instance.

   For Cloud Directory, see [Migrating users](/docs/appid?topic=appid-cd-users#user-migration). For federated identity providers, use the following steps.
   {: note}

4. Create application credentials to invoke the new service instance.

   1. In the service dashboard navigate to the **Applications** tab.

   2. Click **Add Application** and give your application a name. Then, click **Save**.

   3. Click **View credentials** in the table and copy the output.

   4. Paste your new credentials into your application.

5. Update your application to use the new credentials including any URLs. 

6. Depending on your configuration, you might need to redeploy or unbind and rebind your application.

