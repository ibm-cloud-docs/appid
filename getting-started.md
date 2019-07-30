---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-30"

keywords: Authentication, authorization, identity, app security, secure, development,

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

# Getting started tutorial
{: #getting-started}

Application security can be incredibly complicated. For most developers, it's one of the hardest parts of creating an app. How can you be sure that you are protecting your users information? By integrating {{site.data.keyword.appid_full}} into your apps, you can secure resources and add authentication; even when you don't have a lot of security experience.
{: shortdesc}

Getting started? Try walking through our [video tutorials](https://www.youtube.com/watch?v=EZWl1ij3dAE&list=UUdWhdi8GES-V-TFuTwjobrA){: external}. 
{: note}

By requiring users to sign in to your app, you can store user data such as app preferences or information from the public social profiles, and then use that data to customize each experience of your app. {{site.data.keyword.appid_short_notm}} provides a framework for you, but you can also bring your own branded sign in screens when working with cloud directory.

We’d love to hear from you with feedback and questions!
* If you have technical questions about {{site.data.keyword.appid_short_notm}}, post your question on <a href="https://stackoverflow.com" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and tag your question with `ibm-appid`.
* For questions about the service and getting started instructions, use the <a href="https://developer.ibm.com" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> forum. Include the `appid` tag.
* Reach out directly to the development team on [Slack](https://ibm-container-service.slack.com)! 

## Creating a service instance
{: #create}

Create and bind an instance of {{site.data.keyword.appid_short_notm}} to your app to get started.
{: shortdesc}

1. In the {{site.data.keyword.cloud_notm}} catalog, select {{site.data.keyword.appid_short_notm}}. The service configuration screen opens.
2. Give your service instance a name, or use the preset name.
3. Select your pricing plan and click **Create**.
4. Bind your instance of {{site.data.keyword.appid_short_notm}}.
    1. To see a list of apps that you can bind to your service instance, click **Connections**.
    2. Click **Create connection**. A page opens with all of the apps that you have the option to bind.
    3. Click **Connect** on the app that you want to bind.
    4. Click **Re-stage** to apply the change.

That's it! You're ready to start configuring your application settings.

## Configuring a sample app
{: #sample-app}

You can use one of the preconfigured sample apps to get familiar with working with the service.
{: shortdesc}

Out of the box, the sample apps are configured with two identity providers and the ability to review authentication. Sample apps are offered in `iOS Swift`, `Android`, `Node.js`, and `Java`. If you don't see a language in which you feel comfortable working, don't worry! You can integrate {{site.data.keyword.appid_short_notm}} into your own sample application by using the provided APIs.

To build a sample app:

1. Click **Download Sample**.
2. Click on the language of your choice to download the sample.
  Don't see the language you're looking for? Don't worry! You can take advantage of {{site.data.keyword.appid_short_notm}} through the APIs.
  {: tip}
3. Be sure that you have the pre-requisites installed or completed.
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

Ready to jump in and get started with your own apps? Start by [adding the service to your app](/docs/services/appid?topic=appid-web-apps#web-apps). The service provides SDKs for the most used languages, but if you don't see an SDK for the language that your app is written in, you can still take advantage of {{site.data.keyword.appid_short_notm}} by using the APIs.
