---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-04"

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

## Backing up your {{site.data.keyword.appid_short_notm}} instance
{: #backup}

You can create backups of an {{site.data.keyword.appid_short_notm}} instance in a primary region. Then, you can restore these backups in another {{site.data.keyword.appid_short_notm}} instance that is configured in a secondary region. You can do so by using only the management API, or a combination of {{site.data.keyword.cloud_notm}} Terraform provider and the {{site.data.keyword.appid_short_notm}} management API. 

With the second method, you can use Terraform to backup and restore the {{site.data.keyword.appid_short_notm}} instance configurations. However, to backup and restore the Cloud Directory users and user profiles data, you must use the management API. Using both Terraform and the management API to backup and restore your {{site.data.keyword.appid_short_notm}} is a combined process because you can't use Terraform to export Cloud Directory users and their profiles.

### Backing up your instance by using the API
{: #backup-api}
{: api}

To backup your {{site.data.keyword.appid_short_notm}} instance by using only the [management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}, write a script to send a request to the {{site.data.keyword.appid_short_notm}} API to generate files that contain the setup information for your {{site.data.keyword.appid_short_notm}} instance. Store these files in a secure location because they are required to restore the {{site.data.keyword.appid_short_notm}} instance in a secondary region.

Define the settings of your backup based on the setup in your {{site.data.keyword.appid_short_notm}} instance, such as what is needed for your use case. For example, in the following scenario, you configure your {{site.data.keyword.appid_short_notm}} instance with the following settings:

-	password policies, such as locking the user profile for 60 minutes if the user inputs a wrong password for three times in a row
-	SAML configuration

To retrieve these user settings with the management API, send:
- a GET request to the [/management/v4/<tenantId>/config/cloud_directory/advanced_password_management](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.get_cloud_directory_advanced_password_management){: external} endpoint to get the configuration of the advanced password management.

```sh
curl -X 'GET' \
  'https://<region>.appid.cloud.ibm.com/management/v4/<tenantId>/config/cloud_directory/advanced_password_management' \
  --header 'accept: application/json' \
  --header 'Authorization: <IAM_Token>'
```
{: codeblock}


- a GET request to the [/management/v4/<tenantId>/config/idps/saml](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp){: external} endpoint to get the SAML identity provider configuration, which includes the status and credentials.

```sh
curl -X 'GET' \
  'https://<region>.appid.cloud.ibm.com/management/v4/<tenantId>/config/idps/saml' \
  --header 'accept: application/json' \
  --header 'Authorization: <IAM_Token>'
```
{: codeblock}


In addition to keeping a backup of the configuration settings of your {{site.data.keyword.appid_short_notm}} instance, you must generate a backup of your Cloud Directory users and user profiles. To achieve this task, it is recommended that you use the management API.

-	To export Cloud Directory users, use the [cloud_directory/export/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExportAll){: external} API endpoint. To download the export, use the [cloud_directory/export/download](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryDownloadExport){: external} API. For more details about how to export Cloud Directory users with the Management API, read the [Exporting all users](/docs/appid?topic=appid-cd-users&interface=api&en#cd-export-all) documentation.
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

```
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

-	To export Cloud Directory users, use the [cloud_directory/export/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExportAll){: external} API endpoint. To download the export, use the [cloud_directory/export/download](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryDownloadExport){: external} API. For more details about how to export Cloud Directory users with the Management API see [Exporting all users](/docs/appid?topic=appid-cd-users&interface=api&en#cd-export-all).
-	To export users profiles, use the [users/export](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesExport){: external} endpoint.
-	These two export APIs generate two backup files, which you must store to use later in the restore process.


## Restoring your {{site.data.keyword.appid_short_notm}} instance
{: #backup-restore}

The process to restore an {{site.data.keyword.appid_short_notm}} instance in a secondary location is the opposite of the process of backing up of an {{site.data.keyword.appid_short_notm}} instance in a primary location. Similarly to the backup process, you can restore your {{site.data.keyword.appid_short_notm}} instance by using only the management API, or combination of the Terraform provider and the management API. 


### Restoring your {{site.data.keyword.appid_short_notm}} instance by using the API
{: backup-restore-api}
{: api}

First, you must manually provision a new instance of {{site.data.keyword.appid_short_notm}} in the secondary region. Then, you can restore your {{site.data.keyword.appid_short_notm}} settings by reading the backup files and by using the management API request to setup the {{site.data.keyword.appid_short_notm}} instance in the secondary region.

Continuing with the scenario that is included in the backup section, you can restore the SAML configuration and the password policies by sending the following to the management API:

- a PUT request to the [/management/v4/<tenantId>/config/cloud_directory/advanced_password_management](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_advanced_password_management){: external} endpoint to update the advanced password management configuration. Pass the data that is stored in the backup as the HTTP request body.

```sh
curl -X 'PUT' \
  'https://<region>.appid.cloud.ibm.com/management/v4/<tenantId>/config/cloud_directory/advanced_password_management' \
  --header 'accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'Authorization: <IAM_Token>' \
  -d '<Data_from_your_backup_file>'
```
{: codeblock}

- a PUT request to the [/management/v4/<tenantId>/config/idps/saml](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp){: external} endpoint to update the SAML IdP configuration. Pass the data that is stored in the backup as the HTTP request body.

```sh
curl -X 'PUT' \
  'https://<region>.appid.cloud.ibm.com/management/v4/<tenantId>/config/idps/saml' \
  --header 'accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'Authorization: <IAM_Token>' \
  -d '<Data_from_your_backup_file>'
```
{: codeblock}

To restore the backups of your Cloud Directory users and their profiles, if available, it is recommended that you use the management API:

-	To import Cloud Directory users, use the [cloud_directory/import/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImportAll){: external} API endpoint. For more details about how to import Cloud Directory users with the Management API read the [Importing all users](/docs/appid?topic=appid-cd-users&interface=api&locale=en#cd-import-all) documentation.
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
-	To import Cloud Directory users, use the [cloud_directory/import/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImportAll){: external} API endpoint. For more details about how to import Cloud Directory users with the management API, see [Importing all users](/docs/appid?topic=appid-cd-users&interface=api&locale=en#cd-import-all).
-	To import the users profiles, use the [users/import](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesImport){: external} endpoint.





