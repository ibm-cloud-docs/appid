---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-08"

keywords: Authentication, authorization, identity, app security, secure, access, platform, management, permissions

subcollection: appid

---

{:external: target="_blank" .external}
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


# Managing service instances
{: #service-instance-management}

There are times when you might need to have more than one instance of {{site.data.keyword.appid_short_notm}} or migrate to a new instance. You might need to have an instance of {{site.data.keyword.appid_short_notm}} in multiple regions or different versions for different types of users. No problem! You can easily export your identity provider configuration. 
{: shortdesc}


## Migrating to another instance
{: #migrate-service}

You can migrate the information in one instance of {{site.data.keyword.appid_short_notm}} to another.
{: shortdesc}

1. Create a new instance of the service.

2. Duplicate your identity provider configuration by using the GUI.

3. Migrate your users. If you're using Cloud Directory as your identity provider, migrate your user information by [exporting and importing your users](/docs/services/appid?topic=appid-cd-users#user-migration). Users are exported as a JSON object. You can choose to import the entire object into the new instance or break it up and divide the users as you see fit if you have more than one.

  If you're using another federated identity provider, users are added to your new instance at their next sign in to your application. Currently, there is no export or import process in place for users outside of Cloud Directory. Any profiles associated with users that are federated by another provider are lost.
  {: note}

4. Create application credentials to invoke the new service instance.

  1. In the service dashboard navigate to the **Applications** tab.

  2. Click **Add Application** and give your application a name. Then, click **Save**.

  3. Click **View credentials** in the table and copy the output.

  4. Paste your new credentials into your application.

5. Update your application to use the new credentials including any URLs. 

6. Depending on your configuration, you might need to redeploy or unbind and rebind your application.

