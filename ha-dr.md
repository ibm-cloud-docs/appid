---

copyright:
  years: 2017, 2025
lastupdated: "2025-06-25"

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
{:terraform: .ph data-hd-interface='terraform'}
{:release-note: data-hd-content-type='release-note'}

# Understanding high availability and disaster recovery for {{site.data.keyword.appid_short_notm}}
{: #ha-dr}

[High availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible in the presence of unexpected failures. [Disaster recovery](#x2113280){: term} is the process of recovering the service instance to a working state.
{: shortdesc}

{{site.data.keyword.appid_full}} is a regional service that fulfills the defined [Service Level Objectives (SLO)](/docs/resiliency?topic=resiliency-slo) with the Standard plan. For more information about the available {{site.data.keyword.cloud_notm}} regions and data centers for {{site.data.keyword.appid_short_notm}}, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

## High availability architecture
{: #id-ha-architecture}

An {{site.data.keyword.appid_short_notm}} service instance is provisioned across multiple zones in a multi-zone region with no single point of failure. In the event of an instance node or availability zone failure, the service continues to run with API requests being routed through a global load balancer to the surviving highly available instance nodes. There may be a short period of time (seconds) between the outage and the global load balancer recognizing the failure, during which time, requests may be sent to the failed instance. Workloads that programmatically access the service instance should follow the [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha) to maintain availability. There is no noticeable degradation of service during a zonal failure.



## Disaster recovery architecture
{: #id-disaster-recovery-intro}


To recover from a service instance outage, a recovery service instance should be craeted in a recovery region. In general, the recovery service instance should be configured with the same data as the source service instance. Be sure that you create backup instances in a recovery region prior to a potential disaster and that you regularly maintain them to ensure that they are in sync with the source instance. 

### Disaster recovery features
{: #id-dr-features}

Plan for the recovery into a recovery region. The recovery instance should align with the workload [disaster recovery approaches within IBM Cloud.](/docs/resiliency?topic=resiliency-dr-approaches) The recovery instance should track data changes to primary service instance for data including password policies, users, and SAML configurations.


## Backing up and restoring your instances
{: #backup-restore}

Backing up and restoring your {{site.data.keyword.appid_short_notm}} instance to ensure cross-regional availability requires a few basic steps. You must:

1. Define the policies for configuring the storage of the backup of your {{site.data.keyword.appid_short_notm}} instance. This configuration includes planning how the data, such as the user profiles and Cloud Directory users, is to be stored in your instance's backup. 

   Create the backup system before an outage incident occurs in your primary location. To maintain continuous protection, as recommended, automate the process to generate the backup and run it periodically.
   {: tip} 

2. Create and configure an instance of {{site.data.keyword.appid_short_notm}} in another region.
3. Set up a process to store the backup and restore it in the {{site.data.keyword.appid_short_notm}} instance that is in the secondary location.


### Backing up your instance by using the API
{: #backup-api}
{: api}

To backup your {{site.data.keyword.appid_short_notm}} instance by using the [management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}, write a script to send a request to the {{site.data.keyword.appid_short_notm}} API to generate files that contain the setup information for your {{site.data.keyword.appid_short_notm}} instance. Store these files in a secure location because they are required to restore the {{site.data.keyword.appid_short_notm}} instance in a secondary region.

Define the settings of your backup based on the setup in your {{site.data.keyword.appid_short_notm}} instance, such as what is needed for your use case. For example, in the following scenario, you configure your {{site.data.keyword.appid_short_notm}} instance with the following settings:

-	password policies, such as locking the user profile for 60 minutes if the user inputs a wrong password for three times in a row
-	SAML configuration

To retrieve these user settings with the management API, send:
- a GET request to the [`/management/v4/<tenantId>/config/cloud_directory/advanced_password_management`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.get_cloud_directory_advanced_password_management){: external} endpoint to get the configuration of the advanced password management.

```sh
curl -X 'GET' \
  'https://<region>.appid.cloud.ibm.com/management/v4/<tenantId>/config/cloud_directory/advanced_password_management' \
  --header 'accept: application/json' \
  --header 'Authorization: Bearer <IAM_Token>'
```
{: codeblock}


- a GET request to the [`/management/v4/<tenantId>/config/idps/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp){: external} endpoint to get the SAML identity provider configuration, which includes the status and credentials.

```sh
curl -X 'GET' \
  'https://<region>.appid.cloud.ibm.com/management/v4/<tenantId>/config/idps/saml' \
  --header 'accept: application/json' \
  --header 'Authorization: Bearer <IAM_Token>'
```
{: codeblock}


In addition to keeping a backup of the configuration settings of your {{site.data.keyword.appid_short_notm}} instance, you must generate a backup of your Cloud Directory users and user profiles. To achieve this task, it is recommended that you use the management API.

-	To export Cloud Directory users, use the [cloud_directory/export/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExportAll){: external} API endpoint. To download the export, use the [cloud_directory/export/download](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryDownloadExport){: external} API. For more details about how to export Cloud Directory users with the Management API, read the [Exporting all users](/docs/appid?topic=appid-cd-users&interface=api#cd-export-all) documentation.
-	To export users profiles, use the [users/export](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesExport) endpoint.
-	These two export APIs generate two backup files, which you must store securely to use later in the restore process.

### Backing up your instance by using Terraform and the API
{: #backup-terraform-management-api}
{: terraform}

To backup your {{site.data.keyword.appid_short_notm}} settings with Terraform, you can write Terraform scripts to generate files that contain the setup information for your {{site.data.keyword.appid_short_notm}} instance. Store these files in a secure location because you must use them to restore the {{site.data.keyword.appid_short_notm}} instance in a secondary region.

Define the settings of your backup based on the setup in your {{site.data.keyword.appid_short_notm}} instance, such as what is needed for your use case. For example, in the following scenario, you configure your {{site.data.keyword.appid_short_notm}} instance with the following settings:

-	password policies, such as locking the user profile for 60 minutes if the user inputs a wrong password for three times in a row
-	SAML configuration

With the following terraform script, you can retrieve your current configuration and store it into files.

```terraform
terraform {
  required_providers {
    ibm = {
      source = "IBM-Cloud/ibm"
      version = ">= 1.12.0"
    }
  }
}

variable "tenant_id" {
  type = string
  default = "<<YOUR TENANT ID>>"
}

variable "region" {
  type = string
  default = "<<THE REGION YOUR TENANT IS LOCATED>>"
}

provider "ibm" {
  region = var.region
  ibmcloud_api_key = "<<API KEY TO ACCESS APP ID INSTANCE>>"
}

##### ---------- Getting the configuration from your App ID instance ---------- #####

# Get Settigs about Password's rules
data "ibm_appid_apm" "app" {
    tenant_id = var.tenant_id   
}

# Get SAML config
data "ibm_appid_idp_saml" "saml" {
    tenant_id = var.tenant_id
}

##### ---------- Saving the App ID configuration to files ---------- #####

resource "local_file" "app_config" {
    content  = jsonencode(data.ibm_appid_apm.app)
    filename = "${path.module}/backup_configurations/app_config.json"
}

resource "local_file" "saml_config" {
    content  = jsonencode(data.ibm_appid_idp_saml.saml)
    filename = "${path.module}/backup_configurations/saml_config.json"
}
```
{: codeblock}

In the previous scenario, the files that contain the backups are stored locally. But, you can store them in any other storage location that you prefer, such as [IBM Cloud Object Storage](https://www.ibm.com/products/cloud-object-storage).

To generate a backup of Cloud Directory users and user profiles, it is recommended that you use the management API.

-	To export Cloud Directory users, use the [cloud_directory/export/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExportAll){: external} API endpoint. To download the export, use the [cloud_directory/export/download](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryDownloadExport){: external} API. For more details about how to export Cloud Directory users with the Management API see [Exporting all users](/docs/appid?topic=appid-cd-users&interface=api#cd-export-all).
-	To export users profiles, use the [users/export](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesExport){: external} endpoint.
-	These two export APIs generate two backup files, which you must store to use later in the restore process.


### Restoring your {{site.data.keyword.appid_short_notm}} instance by using the API
{: #restore-api}
{: api}

First, you must manually provision a new instance of {{site.data.keyword.appid_short_notm}} in the secondary region. Then, you can restore your {{site.data.keyword.appid_short_notm}} settings by reading the backup files and by using the management API request to setup the {{site.data.keyword.appid_short_notm}} instance in the secondary region.

Continuing with the scenario that is included in the backup section, you can restore the SAML configuration and the password policies by sending the following to the management API:

- a PUT request to the [`/management/v4/<tenantId>/config/cloud_directory/advanced_password_management`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_advanced_password_management){: external} endpoint to update the advanced password management configuration. Pass the data that is stored in the backup as the HTTP request body.

```sh
curl -X 'PUT' \
  'https://<region>.appid.cloud.ibm.com/management/v4/<tenantId>/config/cloud_directory/advanced_password_management' \
  --header 'accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'Authorization: Bearer <IAM_Token>' \
  -d '<Data_from_your_backup_file>'
```
{: codeblock}

- a PUT request to the [`/management/v4/<tenantId>/config/idps/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp){: external} endpoint to update the SAML IdP configuration. Pass the data that is stored in the backup as the HTTP request body.

```sh
curl -X 'PUT' \
  'https://<region>.appid.cloud.ibm.com/management/v4/<tenantId>/config/idps/saml' \
  --header 'accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'Authorization: Bearer <IAM_Token>' \
  -d '<Data_from_your_backup_file>'
```
{: codeblock}

To restore the backups of your Cloud Directory users and their profiles, if available, it is recommended that you use the management API:

-	To import Cloud Directory users, use the [cloud_directory/import/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImportAll){: external} API endpoint. For more details about how to import Cloud Directory users with the Management API read the [Importing all users](/docs/appid?topic=appid-cd-users&interface=api#cd-import-all) documentation.
-	To import the users profiles, use the [users/import](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesImport){: external} endpoint.



### Restoring your {{site.data.keyword.appid_short_notm}} instance by using Terraform and the API
{: #backup-restore-terraform-api}
{: terraform}

When you are using a combination of the Terraform and the management API to restore your {{site.data.keyword.appid_short_notm}} instance, the first step is to write your Terraform script to provision a new instance of {{site.data.keyword.appid_short_notm}} in the secondary region. Then, you can restore your {{site.data.keyword.appid_short_notm}} settings by reading the backup files and by using the terraform commands to setup the {{site.data.keyword.appid_short_notm}} instance in the secondary region.

Continuing with the scenario that is included in the [backup](/docs/appid?topic=appid-ha-dr&interface=terraform#backup-terraform-management-api) section, you can restore the SAML configuration and the password policies with the following script:

```terraform
terraform {
  required_providers {
    ibm = {
      source = "IBM-Cloud/ibm"
      version = ">= 1.12.0"
    }
  }
}

variable "backup_region" {
  type = string
  default = "<<REGION WHERE TO CREATE THE NEW APPID INSTANCE>>"
}

variable "backup_appid_instance_name" {
  type = string
  default = "<<THE NAME OF THE NEW APPID INSTANCE>>"
}

provider "ibm" {
  region = var.backup_region
  ibmcloud_api_key = "<<API KEY TO ACCESS APP ID INSTANCE>>"
}

##### ---------- Creating an AppID instance in a secondary location ---------- #####

data "ibm_resource_group" "group" {
  name = "Default"
}

resource "ibm_resource_instance" "backup_appid_instance" {
  name              = var.backup_appid_instance_name
  service           = "appid"
  plan              = "graduated-tier"
  location          = var.backup_region
  resource_group_id = data.ibm_resource_group.group.id
  tags              = ["backup_instance", "backup_of_appid_from_primary_region"]
}

##### ---------- Getting the configuration from the local backups ---------- #####

locals {
	app_config = jsondecode(file("${path.module}/backup_configurations/app_config.json"))
	saml_config = jsondecode(file("${path.module}/backup_configurations/saml_config.json"))
}


##### ---------- Restoring the App ID configuration into the new App ID instance ---------- #####


# Setting SAML config in the new App ID Instance
resource "ibm_appid_idp_saml" "saml" {
  tenant_id = resource.ibm_resource_instance.backup_appid_instance.guid
  is_active = local.saml_config.is_active
  config {
    entity_id = local.saml_config.config[0].entity_id
    sign_in_url = local.saml_config.config[0].sign_in_url
    display_name = local.saml_config.config[0].display_name
    encrypt_response = local.saml_config.config[0].encrypt_response
    sign_request = local.saml_config.config[0].sign_request
    certificates = [local.saml_config.config[0].certificates[0]]
  }
}

# Setting password policies config in the new App ID Instance
resource "ibm_appid_apm" "apm" {
  tenant_id = resource.ibm_resource_instance.backup_appid_instance.guid
  enabled = local.app_config.enabled
  prevent_password_with_username = local.app_config.prevent_password_with_username

  password_reuse {
    enabled = local.app_config.password_reuse[0].enabled
    max_password_reuse = local.app_config.password_reuse[0].max_password_reuse
  }

  password_expiration {
    enabled = local.app_config.password_expiration[0].enabled
    days_to_expire = local.app_config.password_expiration[0].days_to_expire
  }

  lockout_policy {
    enabled = local.app_config.lockout_policy[0].enabled
    lockout_time_sec = local.app_config.lockout_policy[0].lockout_time_sec
    num_of_attempts = local.app_config.lockout_policy[0].num_of_attempts
  }

  min_password_change_interval {
    enabled = local.app_config.min_password_change_interval[0].enabled
    min_hours_to_change_password = local.app_config.min_password_change_interval[0].min_hours_to_change_password
  }
}

```
{: codeblock}


To restore Cloud Directory users and user profiles, it is recommended that you use the management API:
-	To import Cloud Directory users, use the [cloud_directory/import/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImportAll){: external} API endpoint. For more details about how to import Cloud Directory users with the management API, see [Importing all users](/docs/appid?topic=appid-cd-users&interface=api#cd-import-all).
-	To import the users profiles, use the [users/import](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesImport){: external} endpoint.


## Your responsibilities for HA and DR
{: #id-hadr-responsibilities}

The following information can help you create and continuously practice your plan for HA and DR. Disaster recovery steps must be practiced on a regular basis. When building your plan consider the following failure scenarios and resolution.

### Customer recovery from BYOK loss
{: #id-byok-loss-recovery}

If your service instance was provisioned by using the root key from either {{site.data.keyword.keymanagementservicefull}} or {{site.data.keyword.hscrypto}} and you accidentally deleted the root key, open a support case for the respective service, and include the following information:
- Your service instance's CRN
- Your backup Key Protect or HPCS instance's CRN
- The new Key Protect or HPCS root key ID
- The original Key Protect or HPCS instance's CRN and key ID, if available

See Recovering from an accidental key loss for authorization in the [Key Protect](/docs/key-protect?topic=key-protect-restore-keys) and [HPCS docs](/docs/hs-crypto?topic=hs-crypto-restore-keys).


## Change management
{: #id-change-management}

Change management includes tasks such as upgrades, configuration changes, and deletion.

It is recommended that you grant users and processes the IAM roles and actions with the least privilage required for their work. For example, limit the ability to delete production resources.


## How {{site.data.keyword.IBM}} helps ensure disaster recovery
{: #id-ibm-disaster-recovery}

{{site.data.keyword.IBM}} takes specific recovery actions in the case of a disaster.

### How {{site.data.keyword.IBM}} recovers from zone failures
{: #id-ibm-zone-failure}

In the event of a zone failure IBM Cloud will resolve the zone outage and when the zone comes back on-line, the global load balancer will resume sending API requests to the restored instance node without need for customer action.

### How {{site.data.keyword.IBM}} recovers from regional failures
{: #id-ibm-regional-failure}

When a region is restored after a failure, IBM will attempt to restore the service instance from the regional state resulting in no loss of data and the service instance restored with the same connection strings.

If regional state is corrupted the service will be restored to the state of the last internal backup.  All data associated with the service is backed up twice daily by the service in a cross-region Cloud Object Storage bucket managed by the service. There is a potential for 24-hour’s worth of data loss. **These backups are not available for customer managed disaster recovery.** When a service is recovered from backups the instance ID will be restored as well so clients using the endpoint will not need to be updated with new connection strings.

- RTO = 4 hours
- RPO = 12 hours maximum

In the event that IBM can not restore the service instance, the customer must restore as described in the disaster recovery section.

## How {{site.data.keyword.IBM}} maintains services
{: #id-ibm-service-maintenance}

All upgrades follow the {{site.data.keyword.IBM}} service best practices and have a recovery plan and rollback process in-place. Regular upgrades for new features and maintenance occur as part of normal operations. Such maintenance can occasionally cause short interruption intervals that are handled by [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha). Changes are rolled out sequentially, region by region and zone by zone within a region. Updates are backed out at the first sign of a defect.

Complex changes are enabled and disabled with feature flags to control exposure.

Changes that impact customer workloads are detailed in notifications. For more information, see [monitoring notifications and status](/docs/account?topic=account-viewing-cloud-status) for planned maintenance, announcements, and release notes that impact this service.
