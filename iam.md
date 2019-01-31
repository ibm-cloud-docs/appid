---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-31"

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
{: #iam-service-access}

As an account owner, you can manage access to instances of {{site.data.keyword.security-advisor_long}}, by using {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). By setting policies within your account that create different levels of access for different users, you can ensure that each instance of {{site.data.keyword.security-advisor_short}} is secure.
{: shortdesc}

For more information about IAM, see [IAM Access](/docs/iam/users_roles.html).

## {{site.data.keyword.security-advisor_short}} access policies
{: #iam-access-policies}

Every user that accesses an instance of the {{site.data.keyword.security-advisor_short}} service in your account must be assigned an access policy with an IAM user role defined. The policy determines which actions that a user can perform within the context of that specific service instance.
{: shortdesc}

The actions are customized and defined by the {{site.data.keyword.Bluemix_notm}} service as operations that are allowed to be performed in the service. The actions are then mapped to IAM service user roles. In the following table, the actions and required permissions for {{site.data.keyword.security-advisor_short}} are mapped.

<table><caption>Which roles can perform which actions?</caption>
  <col width="40%">
  <col width="40%">
  <col width="20%">
  <tr>
    <th>Action</th>
    <th>Explanation</th>
    <th>Role</th>
  </tr>
  <tr>
    <td><code>security-advisor.findings.read</code></td>
    <td>View security report findings.</td>
    <td>Reader</br>Writer</br>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.findings.write</code></td>
    <td>Generate security report findings.</td>
    <td>Writer</br>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.findings.delete</code></td>
    <td>Delete security report findings.</td>
    <td>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.findings.update</code></td>
    <td>Edit security report findings.</td>
    <td>Writer</br>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.metadata.read</code></td>
    <td>View metadata.</td>
    <td>Reader</br>Writer</br>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.metadata.delete</code></td>
    <td>Delete metadata.</td>
    <td>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.metadata.write</code></td>
    <td>Generate metadata.</td>
    <td>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.metadata.update</code></td>
    <td>Update metadata.</td>
    <td>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.custom-solution.read</code></td>
    <td>Read custom solutions that have been added to the service.</td>
    <td>Reader</br>Writer</br>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.custom-solution.write</code></td>
    <td>Add a custom solution to the service.</td>
    <td>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.custom-solution.update</code></td>
    <td>Update an existing custom solution within the service.</td>
    <td>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.custom-solution.delete</code></td>
    <td>Delete a custom solution from the service.</td>
    <td>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.partner-solution.read</code></td>
    <td>View the partner solutions that you have added to your service instance.</td>
    <td>Reader</br>Writer</br>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.partner-solution.write</code></td>
    <td>Add a partner solution to your service instance.</td>
    <td>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.partner-solution.update</code></td>
    <td>Update a partner solution in your service instance.</td>
    <td>Manager</td>
  </tr>
  <tr>
    <td><code>security-advisor.partner-solution.delete</code></td>
    <td>Delete a partner solution from your service instance.</td>
    <td>Manager</td>
  </tr>
</table>

## API mappings
{: #api-map}

How do those roles correspond to the API? Check out the following table to see how the service actions are mapped to the API.


| Method | Endpoint                                                                  |  Service action                  |
|--------|---------------------------------------------------------------------------|----------------------------------|
| POST   | /v1/{account_id}/graph                                                    | security-advisor.findings.read   |
| POST   | /v1/{account_id}/providers/{provider_id}/notes                            | security-advisor.metadata.write  |
| GET    | /v1/{account_id}/providers/{provider_id}/notes                            | security-advisor.metadata.read   |
| GET    | /v1/{account_id}/providers/{provider_id}/notes/{note_id}                  | security-advisor.metadata.read   |
| PUT    | /v1/{account_id}/providers/{provider_id}/notes/{note_id}                  | security-advisor.metadata.update |
| DELETE | /v1/{account_id}/providers/{provider_id}/notes/{note_id}                  | security-advisor.metadata.delete |
| GET    | /v1/{account_id}/providers/{provider_id}/occurrences/{occurrence_id}/note | security-advisor.findings.read   |
| POST   | /v1/{account_id}/providers/{provider_id}/occurrences                      | security-advisor.findings.write  |
| GET    | /v1/{account_id}/providers/{provider_id}/occurrences                      | security-advisor.findings.read   |
| GET    | /v1/{account_id}/providers/{provider_id}/notes/{note_id}/occurrences      | security-advisor.findings.read   |
| GET    | /v1/{account_id}/providers/{provider_id}/occurrences/{occurrence_id}      | security-advisor.findings.read   |
| PUT    | /v1/{account_id}/providers/{provider_id}/occurrences/{occurrence_id}      | security-advisor.findings.update |
| DELETE | /v1/{account_id}/providers/{provider_id}/occurrences/{occurrence_id}      | security-advisor.findings.delete |
