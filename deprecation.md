---

copyright:
  years: 2024
lastupdated: "2024-03-18"

keywords:

subcollection: appid

---

{{site.data.keyword.attribute-definition-list}}

# Deprecation of App ID 
{: #appid-deprecation}

Starting on 28 March 2024, App ID is deprecated and no new instances can be created or purchased starting on 01 May 2023. The service will no longer be supported by {{site.data.keyword.cloud}} as of 31 March 2025. At the end-of-life date, any instances of App ID that are still running will be permanently disabled and deprovisioned.
{: shortdesc}

If you are an existing customer, you can continue to use your App ID instance until 31 March 2025. However, it's strongly recommended that you immediately assess your workloads and plan your migration to {{site.data.keyword.IBM_notm}} Security Verify. For more information about IBM Security Verify, see [{{site.data.keyword.IBM_notm}} Security Verify: IAM solutions ](https://www.ibm.com/verify){: external}.


## Important dates
{: #deprecation-timeline}

| Stage | Date | Description |
| ---------------- | ----------------- | ------------------------------------------------------------ |
| Deprecation announcement | 28 March 2024  | Announcement of the App ID deprecation. Existing instances will continue to run. |
| End of marketing | 01 May 2024 | No new instances of App ID can be created or purchased. Existing instances will continue to run. |
| End of support   | 31 March 2025 | You can continue to use any existing instances of App ID, but support is no longer available.  |
| End of life | 01 October 2025   | Running instances of App ID are permanently disabled and deprovisioned. |
{: caption="Table 1. Deprecation timeline" caption-side="bottom"}

## Deprecation details
{: #deprecation-details}

Review the following details about the App ID deprecation:

* The service will be removed from the {{site.data.keyword.cloud_notm}} catalog on 01 May 2024, and no new instances can be created after that date. Your existing instances created before this date will continue to run until 01 October 2025.
* This deprecation means that support including updates, bug fixes, and technical support for the product is no longer available effective 01 October 2025.
* Any remaining instances will be permanently disabled and deleted as of 01 October 2025, including any user data.
* No support cases can be opened after 31 March 2025.
* An equivalent product is available for you to start migrating to today. For more information, see [Overview and use cases for {{site.data.keyword.IBM_notm}} Security Verify](https://docs.verify.ibm.com/verify/docs/use-cases){: external}.

## Next steps for current users
{: #deprecation-next-steps}

Current users can continue using existing instances of App ID even though App ID is deprecated. However, it is not recommended as {{site.data.keyword.IBM_notm}} will no longer be providing support, including bug fixes or security updates. You can discontinue use and migrate to {{site.data.keyword.IBM_notm}} Security Verify starting today. As of 31 May 2025, all running instances will be deleted, including any user data.

If you have any further questions about this deprecation, you can contact {{site.data.keyword.cloud_notm}} Support until the end of support date on 31 March 2025.
{: note}

### Migrating to {{site.data.keyword.IBM_notm}} Security Verify
{: #migrate-security-verify}

{{site.data.keyword.IBM_notm}} Security Verify is the recommended solution for authentication to your workloads, including SAML Federation and App ID identities managed with App IDs Cloud Directory. Fpr more information about see [IBM Security Verify](https://www.ibm.com/verify) and register for a 90-day free trial. To learn more about onboarding to IBM Security Verify, see [Security Verify Summary](https://docs.verify.ibm.com/verify/docs/use-cases#summary){: external}.

{{site.data.keyword.IBM_notm}} recommends using IBMid Federation if you require Federated access to {{site.data.keyword.cloud_notm}}. For more information see the section on Enabling authentication from an external identity provider. You can also learn more about IBMid Federation with the {{site.data.keyword.cloud_notm}} SAML Federation Guide.

If you are an existing customer, you can continue to use your App ID instance until 31 March 2025. However, {{site.data.keyword.IBM_notm}} strongly recommends that you immediately assess your workloads and plan your migration to {{site.data.keyword.IBM_notm}} Security Verify. 

### Deleting App ID instances and data
{: #service-delete}

Existing instances of App ID can continue to be used until 01 October 2025. You can start deleting your service instances and the associated data by using the following steps when you're ready. Following this process ensures that all instances and user information stored in the service is permanently deleted.

If you don't manually delete your instances and data before 01 October 2025, it will be done for you on this date.
{: note}

When you delete an instance of {{site.data.keyword.appid_short_notm}}, all the user-associated data is also deleted. When the service instance is deleted, a 7-day reclamation period begins. During that time, you are able to restore the instance and all the user-associated data. However, if the instance and data are permanently deleted, it cannot be restored. {{site.data.keyword.appid_short_notm}} does not store any data from permanently deleted instances.

The {{site.data.keyword.appid_short_notm}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.appid_short_notm}} service description, which you can find in the [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).

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

For more details about data deletion policies, see [Deleting your data in App ID](/docs/appid?topic=appid-mng-data#service-delete).






