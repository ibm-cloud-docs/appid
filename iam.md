---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-21"

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



# Managing access for {{site.data.keyword.appid_short_notm}}
{: #service-access-management}

With {{site.data.keyword.appid_full}} and {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), account owners can manage user access in your account.
{: shortdesc}

As an account owner, you can set policies within your account to create different levels of access for different users. For example, certain users can have **Read only** access to one instance, but **Write** access to another. You can decide who is allowed to create, update, and delete instances of {{site.data.keyword.appid_short_notm}}.

For more information about IAM, see [IAM Access](/docs/account?topic=account-userroles).


## User roles
{: #iam-roles}

The scope of an access policy is based on a users assigned role.
{: shortdesc}

Policies enable access to be granted at different levels. Some of the options include:

* Access across all instances of the service in your account
* Access to an individual service instances in your account
* Access to a specific resource within an instance
* Access to all IAM-enabled services in your account


### Platform roles
{: #iam-platform-roles}

Platform management roles enable users to perform tasks on service resources at the platform level. For example, roles can be assigned to determine who can create or delete IDs, create instances, and bind instances to apps. The following table details the actions as they correlate to platform management roles.

<table>
  <caption>Table 1. Platform roles, permissions, and the example actions that each role can take</caption>
  <tr>
    <th>Platform role</th>
    <th>Permissions</th>
    <th>Example actions</th>
  </tr>
  <tr>
    <td><i>Viewer</i></td>
    <td>View {{site.data.keyword.appid_short_notm}} instances.</td>
    <td>You can see that instances of the service exist, but not the information that is contained within them.</td>
  </tr>
  <tr>
    <td><i>Editor</i></td>
    <td>View and bind {{site.data.keyword.appid_short_notm}} instances.</td>
    <td>You can bind applications to an instance of {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><i>Operator</i></td>
    <td>Create, delete, edit, suspend, resume, view, or bind {{site.data.keyword.appid_short_notm}} instances.</td>
    <td>You can create or delete an {{site.data.keyword.appid_short_notm}} instance from the catalog.</td>
  </tr>
  <tr>
    <td><i>Administrator</i></td>
    <td>All management actions for all services in the account.</td>
    <td>You can perform all operator actions and the ability to assign policies to other users.</td>
  </tr>
</table>

### Service access roles
{: #iam-service-roles}

The following table details actions that are mapped to service access roles. Service access roles enable users to access {{site.data.keyword.appid_short_notm}} as well as the ability to call the {{site.data.keyword.appid_short_notm}} API.

<table>
  <caption>Table 2. Service roles and the actions that the role can take</caption>
  <tr>
    <th>Service role</th>
    <th>Example actions</th>
  </tr>
  <tr>
    <td>Reader</td>
    <td>
      <ul>
        <li>View the post-authentication redirect URLs that are configured in your instance.</li>
        <li>View the identity provider configuration or a view the configuration for a single identity provider.</li>
        <li>View recent authentication activity for your app.</li>
        <li>View the current configuration of the Login Widget including the logo, color, and language.</li>
        <li>View the current configuration of your tokens.</li>
        <li>View the action URLs that are configured for Cloud Directory.</li>
        <li>View a single action URL that is configured for Cloud Directory.</li>
        <li>View advanced password policy configurations.</li>
        <li>View a Cloud Directory password policy in regex form.</li>
        <li>View the current email template configuration.</li>
        <li>View Cloud Directory email sender details.</li>
        <li>View user information from your app configuration.</li>
        <li>View your Cloud Directory users and their data.</li>
        <li>View a user profile.</li>
        <li>Search all of your user profiles and get a count of any anonymous users.</li>
        <li>View all of the apps that are registered with your instance of App ID.</li>
        <li>View a specific app that is registered with App ID.</li>
        <li>View the email provider configuration.</li>
        <li>View a JSON object that contains the auditing status of the tenant.</li>
        <li>View all of the MFA channels.</li>
        <li>View an MFA channel.</li>
        <li>View the current MFA configuration.</li>
        <li>View the Cloud Directory SSO configuration.</li>
        <li>View a Cloud Directory user and their information.</li>
        <li>View your rate limit configuration.</li>
        <li>View the roles that are associated with a scope.</li>
        <li>View the roles that are assigned to a specific user.</li>
        <li>View a registered extension's configuration.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Writer</td>
    <td>
      <ul>
        <li>All Reader actions.</li>
        <li>Add or update post-authentication redirection URLs.</li>
        <li>Configure your identity provider options.</li>
        <li>Configure your Login Widget appearance including the logo, color and language.</li>
        <li>Configure your tokens.</li>
        <li>Delete an action URL that is configured for Cloud Directory.</li>
        <li>Configure advanced password policies.</li>
        <li>Update a Cloud Directory password policy in regex form.</li>
        <li>Get the metadata that is used to link your SAML provider.</li>
        <li>Start the sign up process for a new Cloud Directory user.</li>
        <li>View the result of a new user sign up.</li>
        <li>Start the forgot password email flow for a Cloud Directory user.</li>
        <li>Check whether the forgot password email was successfully sent.</li>
        <li>Resend an email to a Cloud Directory user.</li>
        <li>Start the change password email flow for a Cloud Directory user.</li>
        <li>Update your email template configuration.</li>
        <li>Delete an email template configuration.</li>
        <li>Set Cloud Directory email sender details configuration.</li>
        <li>Update a user profile with the information from your application.</li>
        <li>Create a new Cloud Directory user.</li>
        <li>Update a Cloud Directory user's information.</li>
        <li>Delete a user from Cloud Directory.</li>
        <li>Update a user profile.</li>
        <li>Create a future user.</li>
        <li>Revoke a users refresh token.</li>
        <li>Register a new app with App ID.</li>
        <li>Update an app that is registered with App ID.</li>
        <li>Delete an app that is registered with App ID.</li>
        <li>Configure or update your own email provider.</li>
        <li>Test your email provider configuration.</li>
        <li>Update your auditing status.</li>
        <li>Update an MFA channel.</li>
        <li>Update your MFA configuration.</li>
        <li>Update your Cloud Directory SSO configuration.</li>
        <li>Initiate SSO logout for Cloud Directory.</li>
        <li>Test your MFA configuration for SMS.</li>
        <li>Remove Cloud Directory users and their profiles.</li>
        <li>Update your rate limit configuration.</li>
        <li>Add a scope to an application.</li>
        <li>Get the scopes that are associated with an application.</li>
        <li>Delete a scope that is associated with an application.</li>
        <li>Add a role.</li>
        <li>Update the roles in your instance of App ID.</li>
        <li>Delete a role.</li>
        <li>Update the roles that are assigned to a specific user.</li>
        <li>Update the status of a registered extension for an instance of App ID to enabled or disabled.</li>
        <li>Update a registered extension's configuration.</li>
        <li>Test a registered extensions configuration.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Manager</td>
    <td>
      <ul>
        <li>All Writer actions.</li>
        <li>Export your Cloud Directory users and their data from your App ID instance.</li>
        <li>Import your Cloud Directory users into a new instance of App ID.</li>
        <li>Export all of the user profiles in an instance of App ID.</li>
        <li>Import all of the user profiles that you exported into a new instance of App ID.</li>
      </ul>
    </td>
  </tr>
</table>

For more information about assigning user roles in the UI, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).




