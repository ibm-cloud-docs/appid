---

copyright:
  years:  2017
lastupdated: "2017-11-20"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.appid_short_notm}} Service Access Management

## Managing user access with Identity and Access Management

Access to {{site.data.keyword.appid_short_notm}} service instances for users in your account is controlled by {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.appid_short_notm}} service in your account must be assigned an access policy with an IAM user role defined. That policy determines what actions the user can perform within the context of the service or instance you select.

The actions are customized and defined by the {{site.data.keyword.Bluemix_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles. For {{site.data.keyword.appid_short_notm}}, the following actions exist:

<table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the parameter in column one and the description that matches in column two.">
  <thead>
    <th colspan=2><img src="images/idea.png"/> Permissions by service operation </th>
  </thead>
  <tbody>
    <tr>
      <td> <code> appid-mgmt-get-redirect-uris </code></td>
      <td> View post-authentication redirection urls </td>
      <td> Reader, Writer, Manager </td>
    </tr>
    </tr>
    <tr>
      <td> <code> appid-mgmt-set-redirect-uris </code></td>
      <td> Add or update post-authentication redirection urls </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td> <code> appid-mgmt-set-idps </code></td>
      <td> Update details of Identity Providers </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td> <code> appid-mgmt-get-idps </code></td>
      <td> View details of Identity Providers </td>
      <td> Reader, Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-get-recent-activities </code></td>
      <td> View a list with details of recent authentications activity </td>
      <td> Reader, Writer, Manager </td>
    </tr>
    <tr>
      <td><code>  appid-mgmt-get-ui-config </code></td>
      <td> View application UI settings such as logo and theme color </td>
      <td> Reader, Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-set-ui-config </code></td>
      <td> Update application UI settings such as logo and theme color </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-get-user-profile-config </code></td>
      <td> View user profiles configuration </td>
      <td> Reader, Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-set-user-profile-config </code></td>
      <td> Change user profile configuration </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-get-cd-users </code></td>
      <td> View Cloud Directory users details </td>
      <td> Reader, Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-add-cd-user </code></td>
      <td> Add new users to Cloud Directory </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-set-cd-user </code></td>
      <td> Update Cloud Directory users details </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-delete-cd-user </code></td>
      <td> Delete users from Cloud Directory </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-get-email-template </code></td>
      <td> View Cloud Directory email templates </td>
      <td> Reader, Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-update-email-template </code></td>
      <td> Update Cloud Directory email templates </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-delete-email-template </code></td>
      <td> Delete Cloud Directory email templates </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-get-saml-metadata </code></td>
      <td> View Cloud Directory's SAML Service Provider (SP) metadata </td>
      <td> Reader, Writer, Manager </td>
    </tr>
    <tr>
      <td><code> appid-mgmt-post-saml-logo </code></td>
      <td> Set or update a logo for SAML Identity Provider (IPD) which will appear in the login widget </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td><code> | appid-mgmt-send-email-cd | Trigger sending an e-mail to a user based on a template  | Writer, Manager | </code></td>
      <td> Delete Cloud Directory email templates </td>
      <td> Writer, Manager </td>
    </tr>
    <tr>
      <td><code> | appid-mgmt-get-sender-details-cd | View e-mails sender details  | Reader, Writer, Manager | </code></td>
      <td> View Cloud Directory's SAML Service Provider (SP) metadata </td>
      <td> Reader, Writer, Manager </td>
    </tr>
    <tr>
      <td><code> | appid-mgmt-set-sender-details-cd | Update e-mail sender details | Writer, Manager | </code></td>
      <td> Set or update a logo for SAML Identity Provider (IPD) which will appear in the login widget </td>
      <td> Writer, Manager </td>
    </tr>
  </tbody>
</table>

## policies

Policies enable access to be granted at different levels. Some of the options include the following:

* Access across all instances of the service in your account
* Access to an individual service instance in your account
* Access to a specific resource within an instance
* Access to all IAM-enabled services in your account

After you define the scope of the access policy, you assign a role. Review the following tables which outline what actions each role allows within the {{site.data.keyword.appid_short_notm}} service.

The following table details actions that are mapped to platform management roles. Platform management roles enable users to perform tasks on service resources at the platform level, for example assign user access for the service, create or delete service IDs, create instances, and bind instances to applications.

<table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the parameter in column one and the description that matches in column two.">
  <thead>
    <th colspan=2><img src="images/idea.png"/>Management roles, permissions and example actions at the platform level </th>
  </thead>
  <tbody>
    <tr>
      <td> <i> Viewer </i> </td>
      <td> View {{site.data.keyword.appid_short_notm}} instances. </td>
      <td> <ul><li>View Cloud Directory user data.</li><li>View IDP information.</li></ul> </td>
    </tr>
    <tr>
      <td> <i> Editor </i></td>
      <td> View and bind {{site.data.keyword.appid_short_notm}} instances. </td>
      <td><ul><li> Bind applications to an instance of {{site.data.keyword.appid_short_notm}}. </li></ul></td>
    </tr>
    <tr>
      <td> <i> Operator </i></td>
      <td> Create, delete, edit, suspend, resume, view, bind {{site.data.keyword.appid_short_notm}} instances. </td>
      <td><ul><li> Create an {{site.data.keyword.appid_short_notm}} instance from the catalog.</li><li>Delete an {{site.data.keyword.appid_short_notm}} instance from your account. </li></ul></td>
    </tr>
    <tr>
      <td><i> Administrator </i></td>
      <td> All management actions for services. </td>
      <td><ul><li> All operator actions.</li><li>Assign policies to other users in the account. </li></ul></td>
    </tr>
  </tbody>
</table>


The following table details actions that are mapped to service access roles. Service access roles enable users access to {{site.data.keyword.appid_short_notm}} as well as the ability to call the {{site.data.keyword.appid_short_notm}} API.


<table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the parameter in column one and the description that matches in column two.">
  <thead>
    <th colspan=2><img src="images/idea.png"/>Access roles, permissions and example actions at the service level </th>
  </thead>
  <tbody>
    <tr>
      <td> <i> Reader </i> </td>
      <td> View {{site.data.keyword.appid_short_notm}} instance data. </td>
      <td><ul><li> View Cloud Directory user data. </li><li> View identity provider information. </li></ul></td>
    </tr>
    <tr>
      <td> <i> Writer or Manager </i></td>
      <td> View and change an {{site.data.keyword.appid_short_notm}} instance. </td>
      <td><ul><li> All Reader actions. </li><li> Update identity provider settings. </li></ul></td>
    </tr>
  </tbody>
</table>


For information about assigning user roles in the UI, see [Managing IAM access](/docs/iam/mngiam.html#iammanidaccser) **This link is not live in production yet. Use https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage until the link above is available in production**.
