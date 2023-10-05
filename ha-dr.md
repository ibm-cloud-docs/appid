---

copyright:
  years: 2017, 2023
lastupdated: "2023-10-05"

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

{{site.data.keyword.appid_short_notm}} is a highly available, regional service that runs in the following regions:

* Dallas (`us-south`)
* Frankfurt (`eu-de`)
* London (`eu-gb`)
* Osaka (`jp-osa`)
* Sao Paulo (`br-sao`)
* Sydney (`au-syd`)
* Tokyo (`jp-tok`)
* Toronto (`ca-tor`)
* Washington (`us-east`)

In each supported region, the service exists in multiple availability zones with no single point of failure. However, because {{site.data.keyword.appid_short_notm}} is a regional service, there is no automatic cross-regional failover or cross-regional disaster recovery. If all the availability zones in a region fail, {{site.data.keyword.appid_short_notm}} becomes unavailable in that location. To establish cross-region high availability and implement a recovery plan, you need to create and maintain backup instances in multiple regions. To synchronize a service instance in one region with an instance in another region, you can use either:
- the [Management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/)
or
- the [Management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/) plus the [IBM Cloud Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs) provider. This is because Terraform can not be used to export Cloud Directory users and users profiles.

The basic steps to backup and restore your {{site.data.keyword.appid_short_notm}} instance and ensure cross-regional availability, are:
-	You must generate and store backup of how your {{site.data.keyword.appid_short_notm}} instance is configurated and the data (e.g. user profiles and cloud directory users) stored in it. The backup needs to be created before that {{site.data.keyword.appid_short_notm}} becomes unavailable in your primary location. For this reason, it is recommended to automate the process to generate the backup and run it periodically.
-	You must have an instance of {{site.data.keyword.appid_short_notm}} in another region (e.g. a secondary location).
-	You must have a process to load the backup and restore it in the {{site.data.keyword.appid_short_notm}} instance in the secondary location.

To learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}, see [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime) or [Service Level Agreements](/docs/overview?topic=overview-slas).

# Backup and Restore your {{site.data.keyword.appid_short_notm}} Instance using Terraform provider and the Management API

In this section we are going to explain how you can create backups of an {{site.data.keyword.appid_short_notm}} instance in a primary region, and restore these backups in another {{site.data.keyword.appid_short_notm}} instance in a secondary region using the combination of IBM Cloud Terraform provider and Management API. Terraform can be used to backup/restore the {{site.data.keyword.appid_short_notm}} instance configurations, while the Management API is used to backup/restore the data about Cloud Directory users and users profiles.

### Backup your {{site.data.keyword.appid_short_notm}} Instance

To create a backup of your {{site.data.keyword.appid_short_notm}} configurations and data, you could use both the Management API and the Terraform provider. 
To backup your {{site.data.keyword.appid_short_notm}} settings, you can write Terraform scripts which generates files containing the information about how you have setup your {{site.data.keyword.appid_short_notm}} instance. Store these files somewhere secure since you will need to use them to restore the {{site.data.keyword.appid_short_notm}} instance in a secondary region.
Defining what is needed to be backed up depends on what you have setup in your {{site.data.keyword.appid_short_notm}} instance, e.g. your use case.

For example, suppose you have customised your {{site.data.keyword.appid_short_notm}} instance with:
-	password policies, such as “locking the user profile for 60 minutes if the user has input a wrong password for three times in a row”
-	SAML configuration

The terraform script could retrieve your current configuration and store it into files:
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


In the example above the files containing the backups are stored locally. However, you could store them in any other storage location that you would like to use, such as [IBM Cloud Object Storage](https://www.ibm.com/cloud/object-storage).

To generate a backup of Cloud Directory users and users’ profiles, it is recommended to use the Management API:
-	To export Cloud Directory users, use the [cloud_directory/export/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExportAll) API endpoint and to download the export, use the [cloud_directory/export/download](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryDownloadExport) API. For more details about how to export Cloud Directory users with the Management API read the [Exporting all users](https://cloud.ibm.com/docs/appid?topic=appid-cd-users&interface=api&locale=en#cd-export-all) documentation.
-	To export users profiles, use the [users/export](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesExport) endpoint.
-	Those two APIs generate two backup files, which you need to store and use later in the restore process.



### Restore your {{site.data.keyword.appid_short_notm}} Instance

The process to restore an {{site.data.keyword.appid_short_notm}} instance in a secondary location is the exact opposite of making a backup of an {{site.data.keyword.appid_short_notm}} instance in a primary location. The first thing needed in your Terraform script is to provision a new instance of {{site.data.keyword.appid_short_notm}} in the secondary region. Then, you can restore your {{site.data.keyword.appid_short_notm}} settings just reading the backup from files and using the specific terraform commands to setup the {{site.data.keyword.appid_short_notm}} instance in the secondary region.

Indeed, based on the example in the “Backup your {{site.data.keyword.appid_short_notm}} Instance” paragraph, you can restore the SAML configuration and the password policies with the following script:
```
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

To restore Cloud Directory users and users’ profiles, it is recommended to use the Management API:
-	To import Cloud Directory users, use the [cloud_directory/import/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImportAll) API endpoint. For more details about how to import Cloud Directory users with the Management API read the [Importing all users](https://cloud.ibm.com/docs/appid?topic=appid-cd-users&interface=api&locale=en#cd-import-all) documentation.
-	To import the users profiles, use the [users/import](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesImport) endpoint.



# Backup and Restore your {{site.data.keyword.appid_short_notm}} Instance using the Management API

In this section we are going to explain how you can create backups of an {{site.data.keyword.appid_short_notm}} instance in a primary region, and restore these backups in another {{site.data.keyword.appid_short_notm}} instance in a secondary region using only the [Management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/).

### Backup your {{site.data.keyword.appid_short_notm}} Instance

To backup your {{site.data.keyword.appid_short_notm}} configuration, you can write a script which calls the {{site.data.keyword.appid_short_notm}} API and generates some files containing the information about how you have setup your {{site.data.keyword.appid_short_notm}} instance. You should store these files somewhere secure since you will need to use them to restore the {{site.data.keyword.appid_short_notm}} instance in a secondary region.
Defining what is needed to be backed up depends on what you have setup in your {{site.data.keyword.appid_short_notm}} instance, e.g. your use case.

For example, suppose you have customised your {{site.data.keyword.appid_short_notm}} instance with:
-	password policies, such as “locking the user profile for 60 minutes if the user has input a wrong password for three times in a row”
-	SAML configuration

To retrieve these customer setting, you should use the Management API:
- a GET request to [/management/v4/{tenantId}/config/cloud_directory/advanced_password_management](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.get_cloud_directory_advanced_password_management) endpoint to get the configuration of the advanced password management
```
curl -X 'GET' \
  'https://{region}.appid.cloud.ibm.com/management/v4/{tenantId}/config/cloud_directory/advanced_password_management' \
  --header 'accept: application/json' \
  --header 'Authorization: {IAM_Token}'
```
- a GET request to [/management/v4/{tenantId}/config/idps/saml](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp) endpoint to get the SAML identity provider configuration, including status and credentials.
```
curl -X 'GET' \
  'https://{region}.appid.cloud.ibm.com/management/v4/{tenantId}/config/idps/saml' \
  --header 'accept: application/json' \
  --header 'Authorization: {IAM_Token}'
```

Besides keeping a backup of how your {{site.data.keyword.appid_short_notm}} instance is configured, you need to generate a backup of Cloud Directory users and users’ profiles. To achieve this, it is recommended to use the Management API:
-	To export Cloud Directory users, use the [cloud_directory/export/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExportAll) API endpoint and to download the export, use the [cloud_directory/export/download](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryDownloadExport) API. For more details about how to export Cloud Directory users with the Management API read the [Exporting all users](https://cloud.ibm.com/docs/appid?topic=appid-cd-users&interface=api&locale=en#cd-export-all) documentation.
-	To export users profiles, use the [users/export](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesExport) endpoint.
-	Those two APIs generate two backup files, which you need to store and use later in the restore process.


### Restore your {{site.data.keyword.appid_short_notm}} Instance

The process to restore an {{site.data.keyword.appid_short_notm}} instance in a secondary location is the exact opposite of making a backup of an {{site.data.keyword.appid_short_notm}} instance in a primary location. The first thing needed in to manually provision a new instance of {{site.data.keyword.appid_short_notm}} in the secondary region. Then, you can restore your {{site.data.keyword.appid_short_notm}} settings just reading the backup from files and using the specific Management API to setup the {{site.data.keyword.appid_short_notm}} instance in the secondary region.


Indeed, based on the example in the “Backup your {{site.data.keyword.appid_short_notm}} Instance” paragraph, you can restore the SAML configuration and the password policies with the following Management API:
- a PUT request to [/management/v4/{tenantId}/config/cloud_directory/advanced_password_management](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_advanced_password_management) endpoint to update the advanced password management configuration. You should pass the data stored in the backup as the body of the HTTP request.
```
curl -X 'PUT' \
  'https://{region}.appid.cloud.ibm.com/management/v4/{tenantId}/config/cloud_directory/advanced_password_management' \
  --header 'accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'Authorization: {IAM_Token}' \
  -d '{Data_from_your_backup_file}'
```
- a PUT request to [/management/v4/{tenantId}/config/idps/saml](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) endpoint to Update SAML IDP configuration. You should pass the data stored in the backup as the body of the HTTP request.
```
curl -X 'PUT' \
  'https://{region}.appid.cloud.ibm.com/management/v4/{tenantId}/config/idps/saml' \
  --header 'accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'Authorization: {IAM_Token}' \
  -d '{Data_from_your_backup_file}'
```

If you have the backups of your Cloud Directory users and users’ profiles, to restore them is recommended to use the Management API:
-	To import Cloud Directory users, use the [cloud_directory/import/all](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImportAll) API endpoint. For more details about how to import Cloud Directory users with the Management API read the [Importing all users](https://cloud.ibm.com/docs/appid?topic=appid-cd-users&interface=api&locale=en#cd-import-all) documentation.
-	To import the users profiles, use the [users/import](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesImport) endpoint.
