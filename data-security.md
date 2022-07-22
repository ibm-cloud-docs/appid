---

copyright:
  years: 2017, 2022
lastupdated: "2022-07-22"

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


# Securing your data in {{site.data.keyword.appid_short_notm}}
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.appid_full}}, it is important to know exactly what data is stored and encrypted and how you can delete any stored personal data.
{: shortdesc}


## How your data is stored and encrypted in {{site.data.keyword.appid_short_notm}}
{: #data-storage} 

{{site.data.keyword.appid_short_notm}} stores and encrypts user profile attributes. As a multi-tenant service, every tenant has a designated encryption key and user data in each tenant is encrypted with only that tenant's key. {{site.data.keyword.appid_short_notm}} ensures that private information is encrypted before it is stored.

You can add a higher level of encryption control to your data at rest (when it is stored) by enabling integration with a `_Key Management Service_` (KMS). The data that you store in {{site.data.keyword.cloud_notm}} is encrypted at rest by using `_envelope encryption_`. If you need to control the encryption keys, you can integrate {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.hscrypto}}. This process is commonly referred to as Bring Your Own Key (BYOK). With {{site.data.keyword.keymanagementserviceshort}} and {{site.data.keyword.hscrypto}}, you can create, import, and manage encryption keys. You can assign access policies to the keys, assign users or service IDs to the keys, or give the key access only to a specific service.

## Managing your own keys
{: #customer-keys}

{{site.data.keyword.appid_short_notm}} uses envelope encryption to implement both provider-managed and customer-managed keys. Envelope encryption describes encrypting one encryption key with another encryption key. The key used to encrypt the actual data is known as a data encryption key (DEK). The DEK itself is never stored but is wrapped by a second key that is known as the key encryption key (KEK) to create a wrapped DEK. To decrypt data, the wrapped DEK is unwrapped to get the DEK. This process is possible only by accessing the KEK, which in this case is your root key that is stored in your KMS. {{site.data.keyword.keymanagementserviceshort}} keys are secured by FIPS 140-2 Level 3 certified cloud-based hardware security modules (HSMs), and {{site.data.keyword.hscrypto}} keys are secured by FIPS 140-2 Level 4 certified cloud-based HSMs.

### Enabling customer-managed keys for {{site.data.keyword.appid_short_notm}} by using {{site.data.keyword.keymanagementserviceshort}}
{: #enable-customer-keys-kp}

If you choose to work with a key that you manage, you must ensure that valid IAM authorization is assigned to the {{site.data.keyword.appid_short_notm}} service. 

1. [Create an instance of {{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-provision#provision-gui).
2. [Generate or import your own root key](/docs/key-protect?topic=key-protect-create-root-keys) to your instance of {{site.data.keyword.keymanagementserviceshort}}. When you use {{site.data.keyword.keymanagementserviceshort}} to create a root key, the service generates cryptographic key material that is rooted in cloud-based HSMs. Be sure that the name of your key does not contain any personal information such as your name or location.
3. Grant service access to {{site.data.keyword.keymanagementserviceshort}}. You must be the account owner or an administrator for the instance of {{site.data.keyword.keymanagementserviceshort}} that you're working with. You must also have at least Viewer access for the {{site.data.keyword.appid_short_notm}} service. 
   1. Go to **Manage > Access IAM > Authorizations**.
   2. Create an authorization to allow access to {{site.data.keyword.keymanagementserviceshort}}.
   3. Select the source account.
   4. Select {{site.data.keyword.appid_short_notm}} as your source service.
   5. Select {{site.data.keyword.keymanagementserviceshort}} as your target service.
   6. Specify the scope of the access. 
   7. Assign the Reader role.
   8. Click **Authorize**.
4. Create an instance of the {{site.data.keyword.appid_short_notm}} service.
   1. Select your {{site.data.keyword.keymanagementserviceshort}} instance.
   2. Select the root key that you previously authorized.
   3. Click **Create**.


{{site.data.keyword.appid_short_notm}} supports state changes to your key.
{: note}


#### Rotating your keys
{: #rotate-key-kp}

When you [rotate your KEK](/docs/key-protect?topic=key-protect-key-rotation), {{site.data.keyword.appid_short_notm}} rewraps the DEKs associated with the rotated key, ensuring that your user data is always protected with your up-to-date encryption key.

#### Deleting your keys
{: #delete-key-kp}

When you [delete your KEK](/docs/key-protect?topic=key-protect-delete-keys), user data becomes inaccessible within 4 hours of deletion. Although user data is not destroyed when a key is deleted, {{site.data.keyword.appid_short_notm}} is no longer able to decrypt the user data, making it inaccessible.

### Enabling customer-managed keys for {{site.data.keyword.appid_short_notm}} by using {{site.data.keyword.hscrypto}}
{: #enable-customer-keys-hpcs}

If you choose to work with a key that you manage, you must ensure that valid IAM authorization is assigned to the {{site.data.keyword.appid_short_notm}} service. 

1. [Create an instance of {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started#provision-service).
2. [Initialize your instance](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) by loading a master key from smart cards or from your workstation.
3. [Generate or import your own root key](/docs/hs-crypto?topic=hs-crypto-create-root-keys) to your instance of {{site.data.keyword.hscrypto}}. When you use {{site.data.keyword.hscrypto}} to create a root key, the service generates cryptographic key material that is rooted in cloud-based HSMs. Be sure that the name of your key does not contain any personal information such as your name or location.
4. Grant service access to {{site.data.keyword.hscrypto}}. You must be the account owner or an administrator for the instance of {{site.data.keyword.hscrypto}} that you're working with. You must also have at least Viewer access for the {{site.data.keyword.appid_short_notm}} service. 
   1. Go to **Manage > Access IAM > Authorizations**. 
   2. Create an authorization to allow access to {{site.data.keyword.keymanagementserviceshort}}.
   3. Select the source account.
   4. Select {{site.data.keyword.appid_short_notm}} as your source service.
   5. Select {{site.data.keyword.hscrypto}} as your target service.
   6. Specify the scope of the access. 
   7. Assign the Reader role.
   8. Click **Authorize**.
5. Create an instance of the {{site.data.keyword.appid_short_notm}} service.
   1. Select your {{site.data.keyword.hscrypto}} instance.
   2. Select the root key that you previously authorized.
   3. Click **Create**.

{{site.data.keyword.appid_short_notm}} supports state changes to your key.
{: note}

#### Rotating your keys
{: #rotate-key-hpcs}

When you [rotate your KEK](/docs/hs-crypto?topic=hs-crypto-rotate-keys), {{site.data.keyword.appid_short_notm}} rewraps the DEKs associated with the rotated key, ensuring your user data is always protected with your up-to-date encryption key.

#### Deleting your keys
{: #delete-key-hpcs}

When you [delete your KEK](/docs/hs-crypto?topic=hs-crypto-delete-keys), user data becomes inaccessible within 4 hours of deletion. Although user data is not destroyed when a key is deleted, {{site.data.keyword.appid_short_notm}} is no longer able to decrypt the user data, making it inaccessible.




## Deleting your data in {{site.data.keyword.appid_short_notm}}
{: #data-delete}

When you delete an instance of {{site.data.keyword.appid_short_notm}}, all the user-associated data is also deleted. When the service instance is deleted, a 7-day reclamation period begins. During that time, you are able to restore the instance and all the user-associated data. However, if the instance and data are permanently deleted, it cannot be restored. {{site.data.keyword.appid_short_notm}} does not store any data from permanently deleted instances.

The {{site.data.keyword.appid_short_notm}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.appid_short_notm}} service description, which you can find in the [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).


### Deleting an instance
{: #service-delete}

If you no longer need an instance of {{site.data.keyword.appid_short_notm}}, you can delete the service instance and any data that is stored. You can also choose to delete your service instance by using the console.

1. Delete the service and place it in a reclamation period of 7 days.

   ```sh
   ibmcloud resource service-instance-delete <serviceName>
   ```
   {: codeblock}

2. Optional: To permanently delete your instance, get the reclamation ID.

   ```sh
   ibmcloud resource reclamations --resource-instance-id <tenantID>
   ```
   {: codeblock}

   If you choose not to permanently delete the instance, the instance and data are still deleted at the end of the 7 day reclamation period.
   {: tip}

3. Optional: Permanently delete the reclamation instance.

   ```sh
   ibmcloud resource reclamation-delete <reclamationId>
   ```
   {: codeblock}

   If you permanently delete the instance, you cannot restore your data. 
   {: important}



### Restoring a deleted instance
{: #data-restore}

If you didn't permanently delete your instance, you can restore it during the reclamation period.

1. Get the reclamation ID.

   ```sh
   ibmcloud resource reclamations --resource-instance-id <tenantID>
   ```
   {: codeblock}

2. Restore the reclamation.

   ```sh
   ibmcloud resource reclamation-restore <reclamationID>
   ```
   {: codeblock}

