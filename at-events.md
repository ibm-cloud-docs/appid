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


# {{site.data.keyword.cloudaccesstrailshort}} events
{: #at-events}

You can view, manage, and audit user-initiated activities made in your {{site.data.keyword.security-advisor_long}} service instance by using the {{site.data.keyword.cloudaccesstrailshort}} service.
{: shortdesc}

For more information about how the service works, see the [{{site.data.keyword.cloudaccesstrailshort}} docs](/docs/services/cloud-activity-tracker/index.html).


## Where to view events
{: #at-monitor}

Events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} region where the events are generated.

1. Log in to your {{site.data.keyword.Bluemix_notm}} account.
2. From the catalog, provision an instance of the {{site.data.keyword.cloudaccesstrailshort}} service in the same account as your instance of {{site.data.keyword.security-advisor_short}}.
3. On the **Manage** tab of the {{site.data.keyword.cloudaccesstrailshort}} dashboard, click the **View in Kibana**.
4. Set the time frame that you want to view logs for. The default is 15 min.
5. In the **Available Fields** list, click **type**. Click the magnifying glass icon for **Activity Tracker** to limit the logs to only those tracked by the service.
6. You can use the other available fields to narrow your search.

For users other than the account owner to view logs, you must use the premium plan. To let other users view events, see [Granting permissions to see account events](/docs/services/cloud-activity-tracker/how-to/grant_permissions.html#grant_permissions).
{: tip}

## List of events
{: #at-event-list}

Check out the following table for a list of the events that are sent to {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}

<table>
  <tr>
    <th>Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>security-advisor.metadata.read</code></td>
    <td>View a previously created note or notes.</td>
  </tr>
  <tr>
    <td><code>security-advisor.metadata.write</code></td>
    <td>Create a note.</td>
  </tr>
  <tr>
    <td><code>security-advisor.metadata.delete</code></td>
    <td>Delete a note.</td>
  </tr>
  <tr>
    <td><code>security-advisor.metadata.update</code></td>
    <td>Update a note.</td>
  </tr>
  <tr>
    <td><code>security-advisor.findings.read</code></td>
    <td>View one or more occurrences.</td>
  </tr>
  <tr>
    <td><code>security-advisor.findings.write</code></td>
    <td>Create an occurrence.</td>
  </tr>
  <tr>
    <td><code>security-advisor.findings.delete</code></td>
    <td>Delete an occurrence.</td>
  </tr>
  <tr>
    <td><code>security-advisor.findings.update</code></td>
    <td>Update an occurrence.</td>
  </tr>
  <tr>
    <td><code>security-advisor.custom-solution.read</code></td>
    <td>Read custom solutions that have been added to the service.</td>
  </tr>
  <tr>
    <td><code>security-advisor.custom-solution.write</code></td>
    <td>Add a custom solution to the service.</td>
  </tr>
  <tr>
    <td><code>security-advisor.custom-solution.update</code></td>
    <td>Update an existing custom solution within the service.</td>
  </tr>
  <tr>
    <td><code>security-advisor.custom-solution.delete</code></td>
    <td>Delete a custom solution from the service.</td>
  </tr>
  <tr>
    <td><code>security-advisor.partner-solution.read</code></td>
    <td>View the partner solutions that you have added to your service instance.</td>
  </tr>
  <tr>
    <td><code>security-advisor.partner-solution.write</code></td>
    <td>Add a partner solution to your service instance.</td>
  </tr>
  <tr>
    <td><code>security-advisor.partner-solution.update</code></td>
    <td>Update a partner solution in your service instance.</td>
  </tr>
  <tr>
    <td><code>security-advisor.partner-solution.delete</code></td>
    <td>Delete a partner solution from your service instance.</td>
  </tr>
</table>
