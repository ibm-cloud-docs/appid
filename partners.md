---

copyright:
  years: 2019
lastupdated: "2019-01-31"

---

{:new_window: target="blank"}
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

# Partner solutions
{: #setup-partner}

Partner solutions are a way to extend your security by creating a link between {{site.data.keyword.security-advisor_long}} and other security tools.
{: shortdesc}

## Integration wizard
{: #setup-wizard}

As an administrator with administrative rights in both the {{site.data.keyword.cloud_short}} and Partner accounts, you can use the integration wizard to quickly get up and running. The wizard has four basic steps:

* Establish trust and associate your {{site.data.keyword.cloud_short}} and Partner accounts
* Copy the required information such as credentials and URLs between the accounts
* Install partner finding metadata into {{site.data.keyword.security-advisor_short}}
* Validate the pairing by posting a findings from the Partner into {{site.data.keyword.security-advisor_short}}

</br>

## Integrating NeuVector
{: #setup-neuvector}

**Before you begin**

* Ensure that you have an account with the partner that you want to integrate.
* Ensure that you have the required administrative permissions to generate the integration URL for the Partner service.
* Ensure that you have IAM administrative access to {{site.data.keyword.cloud_short}} and manager access to {{site.data.keyword.security-advisor_short}}.

**Integrating**

1. Navigate to **Integrations > Partner Integrations** and select **NeuVector** from the options provided.
2. Connect your accounts.
  1. Provide a name for your connection.
  2. Provide the NeuVector dashboard URL.
  3. Provide the NeuVector configuration URL.
    1. Login to NeuVector and navigate to settings.
    2. Click **Generate URL**.
    3. Copy the URL and paste it in the {{site.data.keyword.security-advisor_short}} integration wizard.
  4. Click **Next**.
3. Verify that you give permission for the service to generate a service ID and API key and create the connection with the service by clicking **Next**.
4. Click **Done**.
5. Go to your service dashboard to review a test finding that was sent to {{site.data.keyword.containershort_notm}} by NeuVector.


