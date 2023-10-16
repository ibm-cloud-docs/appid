---

copyright:
  years: 2017, 2023
lastupdated: "2023-10-09"

keywords: user access, account settings, iam, user roles, platform roles, service roles, reader, writer, operator, editor, viewer, administrator, manager, permissions

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

# Managing access for {{site.data.keyword.appid_short_notm}}
{: #service-access-management}

With {{site.data.keyword.appid_full}} and {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), account owners can manage user access in your account.
{: shortdesc}

As an account owner, you can set policies within your account to create different levels of access for different users. For example, certain users can have **Read only** access to one instance, but **Write** access to another. You can decide who is allowed to create, update, and delete instances of {{site.data.keyword.appid_short_notm}}.

For more information about IAM, see [IAM Access](/docs/account?topic=account-userroles).


## User roles
{: #iam-roles}

The scope of an access policy is based on a user's assigned role.
{: shortdesc}

Policies enable access to be granted at different levels. Some options include:

* Access across all instances of the service in your account
* Access to an individual service instances in your account
* Access to a specific resource within an instance
* Access to all IAM-enabled services in your account


### Platform roles
{: #iam-platform-roles}

Platform management roles enable users to perform tasks on service resources at the platform level. For example, roles can be assigned to determine who can create or delete IDs, create instances, and bind instances to apps. The following table details the actions as they correlate to platform management roles.

| Platform role | Permissions | Example actions |
|-----|----| ----- |
| ***Viewer*** | View {{site.data.keyword.appid_short_notm}} instances. | You can see that instances of the service exist, but not the information that is contained within them. | 
| ***Editor*** | View and bind {{site.data.keyword.appid_short_notm}} instances. | You can bind applications to an instance of {{site.data.keyword.appid_short_notm}}. |
| ***Operator*** | Create, delete, edit, suspend, resume, view, or bind {{site.data.keyword.appid_short_notm}} instances. | You can create or delete an {{site.data.keyword.appid_short_notm}} instance. |
| ***Administrator*** | All management actions for all services in the account. | You can perform all operator actions and the ability to assign policies to other users. |
{: caption="Table 1. Platform roles, permissions, and the example actions that each role can take" caption-side="top"}

### Service access roles
{: #iam-service-roles}

The following table details actions that are mapped to service access roles. Service access roles enable users to access {{site.data.keyword.appid_short_notm}} and to call the {{site.data.keyword.appid_short_notm}} API.

| Service role | Example actions |
| ------------ | --------------- |
| Reader | * View the post-authentication redirect URLs that are configured in your instance. \n * View the identity provider configuration or a view the configuration for a single identity provider. \n * View the overview page of your app. \n * View the current configuration of the Login Widget including the logo, color, and language. \n * View the current configuration of your tokens. \n * View the action URLs that are configured for Cloud Directory. \n * View a single action URL that is configured for Cloud Directory. \n * View advanced password policy configurations. \n * View a Cloud Directory password policy in regex form. \n * View the current email template configuration. \n * View Cloud Directory email sender details. \n * View user information from your app configuration. \n * View your Cloud Directory users and their data. \n * View a user profile. \n * Search all your user profiles and get a count of any anonymous users. \n * View all the apps that are registered with your instance of {{site.data.keyword.appid_short_notm}}. \n * View a specific app that is registered with {{site.data.keyword.appid_short_notm}}. \n * View the email provider configuration. \n * View a JSON object that contains the auditing status of the tenant. \n * View all the MFA channels. \n * View an MFA channel. \n * View the current MFA configuration. \n * View the Cloud Directory SSO configuration. \n * View a Cloud Directory user and their information. \n * View your rate limit configuration. \n * View the roles that are associated with a scope. \n * View the roles that are assigned to a specific user. \n * View a registered extension's configuration. | 
| Writer | * All Reader actions. \n * Add or update post-authentication redirection URLs. \n * Configure your identity provider options. \n * Configure your Login Widget appearance which includes the logo, color, and language. \n * Configure your tokens. \n * Delete an action URL that is configured for Cloud Directory. \n * Configure advanced password policies. \n * Update a Cloud Directory password policy in regex form. \n * Get the metadata that is used to link your SAML provider. \n * Start the sign-up process for a new Cloud Directory user. \n * View the result of a new user sign-up. \n Start the forgot password email flow for a Cloud Directory user. \n * Check whether the forgot password email was successfully sent. \n * Resend an email to a Cloud Directory user. \n * Start the change password email flow for a Cloud Directory user. \n * Update your email template configuration. \n * Delete an email template configuration. \n * Set Cloud Directory email sender details configuration. \n * Update a user profile with the information from your application. \n * Create a new Cloud Directory user. \n * Update a Cloud Directory user's information. \n * Delete a user from Cloud Directory. \n * Update a user profile. \n * Create a future user. \n * Revoke a users refresh token. \n * Register a new app with {{site.data.keyword.appid_short_notm}}. \n * Update an app that is registered with {{site.data.keyword.appid_short_notm}}. \n * Delete an app that is registered with {{site.data.keyword.appid_short_notm}}. \n * Configure or update your own email provider. \n * Test your email provider configuration. \n * Update your auditing status. \n * Update an MFA channel. \n * Update your MFA configuration. \n * Update your Cloud Directory SSO configuration. \n * Initiate SSO logout for Cloud Directory. \n * Test your MFA configuration for SMS. \n * Remove Cloud Directory users and their profiles. \n * Update your rate limit configuration. \n * Add a scope to an application. \n * Get the scopes that are associated with an application. \n * Delete a scope that is associated with an application. \n * Add a role. \n * Update the roles in your instance of {{site.data.keyword.appid_short_notm}}. \n * Delete a role. \n * Update the roles that are assigned to a specific user. \n * Update the status of a registered extension for an instance of {{site.data.keyword.appid_short_notm}} to enabled or disabled. \n * Update a registered extension's configuration. \n * Test a registered extensions configuration. | 
| Manager | * All Writer actions. \n * Export your Cloud Directory users and their data from your {{site.data.keyword.appid_short_notm}} instance. \n * Import your Cloud Directory users into a new instance of {{site.data.keyword.appid_short_notm}}. \n * Export all the user profiles in an instance of {{site.data.keyword.appid_short_notm}}. \n * Import all the user profiles that you exported into a new instance of {{site.data.keyword.appid_short_notm}}. |
{: caption="Table 2. Service roles and the actions that the role can take" caption-side="top"}

For more information about assigning user roles in the UI, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).




