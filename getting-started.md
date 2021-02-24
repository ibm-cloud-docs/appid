---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-09"

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

# Getting started with {{site.data.keyword.appid_short_notm}}
{: #getting-started}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

Application security can be incredibly complicated. For most developers, it's one of the hardest parts of creating an app. How can you be sure that you are protecting your users information? By integrating {{site.data.keyword.appid_full}} into your apps, you can secure resources and add authentication; even when you don't have a lot of security experience.
{: shortdesc}

By requiring users to sign in to your app, you can store user data such as app preferences or information from the public social profiles, and then use that data to customize each experience of your app. {{site.data.keyword.appid_short_notm}} provides a framework for you, but you can also bring your own branded sign in screens when working with cloud directory.

We’d love to hear from you with feedback and questions!

* If you have technical questions about {{site.data.keyword.appid_short_notm}}, post your question on <a href="https://stackoverflow.com" target="_blank">Stack Overflow <img src="../icons/launch-glyph.svg" alt="External link icon"></a> and tag your question with `ibm-appid`.
* Reach out directly to the development team on [Slack](https://www.ibm.com/cloud/blog/announcements/get-help-with-ibm-cloud-app-id-related-questions-on-slack){: external}! 

Getting started? Try walking through our [video tutorials](https://www.youtube.com/playlist?list=PLzpeuWUENMK2tmzSRRx7W_mplw1x4h7ch){: external}. 
{: note}


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

## Configure a sample app
{: #sample-app}
{: step}

You can use one of the preconfigured sample apps to get familiar with working with the service.
{: shortdesc}

Out of the box, the sample apps are configured with two identity providers and the ability to review authentication. Sample apps are offered in `iOS Swift`, `Android`, `Node.js`, `Java` and `Single-page application`. If you don't see a language in which you feel comfortable working, don't worry! You can integrate {{site.data.keyword.appid_short_notm}} into your own application by using the provided APIs.

To build a sample app:

1. Click **Download Sample**.
2. Click on the language of your choice to download the sample.
  Don't see the language you're looking for? Don't worry! You can take advantage of {{site.data.keyword.appid_short_notm}} through the APIs.
  {: tip}
3. Be sure that you have the prerequisites installed or completed.
4. Follow the **Build & Run** steps to set up your sample with {{site.data.keyword.appid_short_notm}}.
5. Click **Review Activity** to see any authentication events that occurred. Any type of sign in creates an event that is visible on this page.
6. Customize the sign in widget.
  1. Add an image such as a brand logo by clicking **Select** and browsing your local system for an image to upload.
  2. Choose a color scheme by either selecting one of the color options or specifying in a hex value.
  3. Change between web and mobile to see how the color scheme looks on each type of device.
  4. When you're happy with your choices, click **Save Changes**.
7. In a browser, refresh your login page. The changes that you made in the previous step are already visible.


## Next steps
{: #next}

Ready to jump in and get started with your own apps? Start by [adding the service to your app](/docs/appid?topic=appid-web-apps#web-apps). The service provides SDKs for the most used languages, but if you don't see an SDK for the language that your app is written in, you can still take advantage of {{site.data.keyword.appid_short_notm}} by using the APIs.
