---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Managing service access
{: #service-access-management}

With {{site.data.keyword.appid_full}} and {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) account owners can manage user access in your account.
{: shortdesc}

As an account owner, you can set policies within your account to create different levels of access for different users. For example, certain users can have **Read only** access to one instance, but **Write** access to another. You can decide who is allowed to create, update, and delete instances of {{site.data.keyword.appid_short_notm}}.

For more information about IAM, see [IAM Access](/docs/iam/users_roles.html).

## User roles
{: #roles}

The scope of an access policy is based on a users assigned role.
{: shortdesc}

Policies enable access to be granted at different levels. Some of the options include:
<ul><ul>
  <li>Access across all instances of the service in your account</li>
  <li>Access to an individual service instances in your account</li>
  <li>Access to a specific resource within an instance</li>
  <li>Access to all IAM-enabled services in your account</li>
</ul></ul>

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

</br>
</br>
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

For more information about assigning user roles in the UI, see [Managing IAM access](/docs/iam/mngiam.html#iammanidaccser).


## {{site.data.keyword.appid_short_notm}} access policies
{: #access}

Every user that accesses the {{site.data.keyword.appid_short_notm}} service in your account must be assigned an access policy with an IAM user role defined. That policy determines what actions the user can perform within the context of the service or instance you select.
{: shortdesc}

The actions are customized and defined by the {{site.data.keyword.Bluemix_notm}} service as operations that are allowed to be performed in the service. The actions are then mapped to IAM user roles. Some of the actions taken you can track with the {{site.data.keyword.cloudaccesstrailshort}} service. In the following table, the actions and required permissions for {{site.data.keyword.appid_short_notm}} are mapped.

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
    <td>code>appid-mgmt-revoke-refresh-token</code></td>
    <td>Revoke user's refresh token by user ID.</td>
    <td>Writer, Manager</td>
  </tr>
</table>

## Tracking changes to your instances of {{site.data.keyword.appid_short_notm}}
{: #tracking}

You can monitor administrative activity that is made in {{site.data.keyword.appid_short_notm}} such as changes to the dashboard configuration, by using the {{site.data.keyword.cloudaccesstrailshort}} service.
{: shortdesc}

To monitor administrative activity:

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.
2. From the catalog, provision an instance of the {{site.data.keyword.cloudaccesstrailshort}} service in the same account as your {{site.data.keyword.appid_short_notm}} instance.
3. In the {{site.data.keyword.cloudaccesstrailshort}} dashboard, click the **Manage** tab.
4. From the drop-down list, select the following configurations to search for any events that were generated by {{site.data.keyword.appid_short_notm}}.
  <table>
    <tr>
      <th> Field </th>
      <th> Configuration </th>
    </tr>
    <tr>
      <td>View logs</td>
      <td>Account logs</td>
    </tr>
    <tr>
      <td>Search</td>
      <td>target.name</td>
    </tr>
    <tr>
      <td>Filter</td>
      <td>appid</td>
    </tr>
  </table>
5. Click **Filter**.



For more information about how the service works see the [{{site.data.keyword.cloudaccesstrailshort}} docs](/docs/services/cloud-activity-tracker/index.html).

</br>
</br>

## Example: Giving another user access to an instance of {{site.data.keyword.appid_short_notm}}
{: #example}

In this scenario, an administrator created an instance of {{site.data.keyword.appid_short_notm}} and needs to grant viewer access to another team member.
{: shortdesc}

Before you begin:
* Install the [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html).

To update access permissions, the admin completes the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}} console.
2. Give the employee view access by following the steps that are laid out in the [IAM documentation](/docs/iam/iamusermanage.html#iamusermanage).
3. Navigate to the **Service credentials** tab of the {{site.data.keyword.appid_short_notm}} dashboard. Click **View credentials** and copy the **tentantID**.
4. Sign in with the {{site.data.keyword.Bluemix_notm}} CLI in your terminal.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. Get an IAM token and make a note of it.
    ```
    bx iam oauth-tokens
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
    'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    The result is a 403 unauthorized message.

To view the {{site.data.keyword.appid_short_notm}} configurations from the CLI, the team member completes the following steps:

1. Using the {{site.data.keyword.Bluemix_notm}} CLI in your terminal, sign in.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. Get an IAM token and make a note of it.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. View the identity provider configuration for Facebook by using cURL.
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    The result is a 200 message that contains the identity provider information.
