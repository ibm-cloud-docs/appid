---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-09"

keywords: authentication, authorization, identity, app security, secure, access, platform, management, permissions

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}


# Managing service access
{: #service-access-management}

With {{site.data.keyword.appid_full}} and {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), account owners can manage user access in your account.
{: shortdesc}

As an account owner, you can set policies within your account to create different levels of access for different users. For example, certain users can have **Read only** access to one instance, but **Write** access to another. You can decide who is allowed to create, update, and delete instances of {{site.data.keyword.appid_short_notm}}.

For more information about IAM, see [IAM Access](/docs/iam?topic=iam-userroles).

## User roles
{: #iam-roles}

The scope of an access policy is based on a users assigned role.
{: shortdesc}

Policies enable access to be granted at different levels. Some of the options include:
<ul><ul>
  <li>Access across all instances of the service in your account</li>
  <li>Access to an individual service instances in your account</li>
  <li>Access to a specific resource within an instance</li>
  <li>Access to all IAM-enabled services in your account</li>
</ul></ul>

### Platform roles
{: #iam-platform-roles}

Platform management roles enable users to perform tasks on service resources at the platform level. For example, roles can be assigned to determine who can create or delete IDs, create instances, and bind instances to apps. The following table details the actions as they correlate to platform management roles.

<table>
  <tr>
    <th>Platform role</th>
    <th>Permissions</th>
    <th>Example actions</th>
  </tr>
  <tr>
    <td><i>Viewer</i></td>
    <td>View {{site.data.keyword.appid_short_notm}} instances.</td>
    <td>You can see a Cloud Directory user's data or the identity provider configuration.</td>
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
  <tr>
    <th>Service role</th>
    <th>Permissions</th>
    <th>Example actions</th>
  </tr>
  <tr>
    <td><i>Reader</i></td>
    <td>View {{site.data.keyword.appid_short_notm}} instance data.</td>
    <td>Can view the details of the service instance such as user data or identity provider information.</td>
  </tr>
  <tr>
    <td> <i>Writer or Manager</i></td>
    <td>View and change an {{site.data.keyword.appid_short_notm}} instance.</td>
    <td>Can perform all Reader actions and edit the service instance, such as editing the identity provider configuration. </li></ul></td>
  </tr>
</table>

For more information about assigning user roles in the UI, see [Managing IAM access](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).


## {{site.data.keyword.appid_short_notm}} access policies
{: #iam-access}

Every user that accesses the {{site.data.keyword.appid_short_notm}} service in your account must be assigned an access policy with an IAM user role defined. That policy determines what actions the user can perform within the context of the service or instance you select.
{: shortdesc}

The actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that are allowed to be performed in the service. The actions are then mapped to IAM user roles. Some of the actions taken you can track with the {{site.data.keyword.cloudaccesstrailshort}} service. In the following table, the actions and required permissions for {{site.data.keyword.appid_short_notm}} are mapped.

<table>
  <tr>
    <th>Action</th>
    <th>Explanation</th>
    <th>Required role</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>View the post-authentication redirect URLs.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>Add or update post-authentication redirection URLs.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>Update your identity provider configuration.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>View your identity provider configuration.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>View any recent authentication events as a list.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>View the login widget configuration, such as logo and colors.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>Update the login widget configuration.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>View the user profile configuration.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>Change the user profile configuration.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>View the user profile configuration.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>Add new users to cloud directory.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>Update a cloud directory user's details.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>Delete a user from cloud directory.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>View the cloud directory email templates.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>Update the email template with your own content.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>Delete a cloud directory email template.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>View cloud directory's SAML service provider (SP) metadata.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>Set or update the image in the login widget for the SAML identity provider.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>Send an email to a user based on a template.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>View the sender details for the email.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>Update the sender details.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>Revoke a user's refresh token with their user ID.</td>
    <td>Writer, Manager</td>
  </tr>
</table>

</br>

## Example: Giving another user access to an instance of {{site.data.keyword.appid_short_notm}}
{: #iam-example}

In this scenario, an administrator created an instance of {{site.data.keyword.appid_short_notm}} and needs to grant viewer access to another team member.
{: shortdesc}

Before you begin:
* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

To update access permissions, the admin completes the following steps:

1. Log in to the {{site.data.keyword.cloud_notm}} console.

2. Give the employee view access by following the steps that are laid out in the [IAM documentation](/docs/iam?topic=iam-iammanidaccser).

3. Navigate to the **Service credentials** tab of the {{site.data.keyword.appid_short_notm}} dashboard. Click **View credentials** and copy the **tentantID**.

4. Sign in with the {{site.data.keyword.cloud_notm}} CLI in your terminal.

    ```
    ibmcloud login -api -a https://api.<region>.cloud.ibm.com
    ```
    {: codeblock}

    <table>
      <tr>
        <th>Region</th>
        <th>Endpoint</th>
      </tr>
      <tr>
        <td>Dallas</td>
        <td><code>us-south</code></td>
      </tr>
      <tr>
        <td>Frankfurt</td>
        <td><code>eu-de</code></td>
      </tr>
      <tr>
        <td>Sydney</td>
        <td><code>au-syd</code></td>
      </tr>
      <tr>
        <td>London</td>
        <td><code>eu-gb</code></td>
      </tr>
      <tr>
        <td>Tokyo</td>
        <td><code>jp-tok</code></td>
      </tr>
    </table>

5. Get an IAM token and make a note of it.

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

6. Verify that the team member cannot make changes.

    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/facebook'
    ```
    {: codeblock}

    The result is a 403 unauthorized message.

To view the {{site.data.keyword.appid_short_notm}} configurations from the CLI, the team member completes the following steps:

1. Using the {{site.data.keyword.cloud_notm}} CLI in your terminal, sign in.

    ```
    ibmcloud login -a api.<region>.console.cloud.ibm.com
    ```
    {: codeblock}

2. Get an IAM token and make a note of it.

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

3. View the identity provider configuration for Facebook by using cURL.

    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/facebook'
    ```
    {: codeblock}

    The result is a 200 message that contains the identity provider information.
