---

copyright:
  years: 2017, 2023
lastupdated: "2023-03-02"

keywords: getting started tutorial, getting started, App ID, sample app, authentication, sign in flow, authorization, app security, identity

subcollection: appid

content-type: tutorial
account-plan: lite
completion-time: 10m

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

# Getting started with {{site.data.keyword.appid_short_notm}}
{: #getting-started}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

Application security can be incredibly complicated. For most developers, it's one of the hardest parts of creating an app. How can you be sure that you are protecting your users information? By integrating {{site.data.keyword.appid_full}} into your apps, you can secure resources and add authentication; even when you don't have a lot of security experience.
{: shortdesc}

By requiring users to sign in to your app, you can store user data such as app preferences or information from the public social profiles, and then use that data to customize each experience of your app. {{site.data.keyword.appid_short_notm}} provides a framework for you, but you can also bring your own branded sign in screens when working with cloud directory.

We’d love to hear from you with feedback and questions!

* If you have technical questions about {{site.data.keyword.appid_short_notm}}, post your question on [Stack Overflow](https://stackoverflow.com){: external} and tag your question with `ibm-appid`.
* Reach out directly to the development team on [Slack](https://www.ibm.com/cloud/blog/announcements/get-help-with-ibm-cloud-app-id-related-questions-on-slack){: external}! 

## Create a service instance
{: #create}
{: step}

Create and bind an instance of {{site.data.keyword.appid_short_notm}} to your app to get started.
{: shortdesc}

1. Check to be sure that you have the [IBM Cloud prerequisites](/docs/overview?topic=overview-prereqs-platform). 
2. In the {{site.data.keyword.cloud_notm}} catalog, select {{site.data.keyword.appid_short_notm}}. The service configuration screen opens.
3. Give your service instance a name, or use the preset name.
4. Select your pricing plan and click **Create**.

That's it! You're ready to start configuring your application settings.


## Next steps
{: #next}

Ready to jump in and get started with your own apps? Start taking advantage of {{site.data.keyword.appid_short_notm}} by using the [APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}.
