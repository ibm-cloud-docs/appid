---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Getting started tutorial
{: #gettingstarted}

Application security can be incredibly complicated. For most developers, it's one of the hardest part of creating an app. How can you be sure that you are protecting your users information? By integrating IBM® Cloud App ID into your apps, you can secure resources and add authentication; even when you don't have a lot of security experience.
{: shortdesc}

By requiring users to sign in to your app, you can store user data such as app preferences or information from the public social profiles, and then use that data to customize each experience of your app. App ID provides a log in framework for you, but you can also bring your own branded sign in screens when working with cloud directory.


As an account owner, you can now set policies that define how members of your team can interact with instances of {{site.data.keyword.appid_short_notm}}. You can decide who can create, update, and delete instances of the service. For more information see [Service access management](/docs/services/appid/iam.html).
{:tip}

## Creating a service instance
{: #create}

Create and bind an instance of {{site.data.keyword.appid_short_notm}} to your app to get started.
{: shortdesc}

1. In the {{site.data.keyword.Bluemix}} catalog, select {{site.data.keyword.appid_short_notm}}. The service configuration screen opens.
2. Give your service instance a name, or use the preset name.
3. Select your pricing plan and click **Create**.
4. Bind your instance of {{site.data.keyword.appid_short_notm}}.
    1. To see a list of apps that you can bind to your service instance, click **Connections**.
    2. Click **Create connection**. A page opens with all of the apps that you have the option to bind.
    3. Click **Connect** on the app that you want to bind.
    4. Click **Restage** to apply the change.

That's it! You're ready to start configuring your application settings.


## Configuring a sample app
{: #sample-app}

You can use one of the preconfigured sample apps to get familiar with working with the service.
{: shortdesc}

Out of the box, the sample apps are configured with two identity providers and the ability to review authentication. You can also use the login widget feature to customize a sign-in page and see how quickly the updates that you make are shown in your app.

To configure a sample app from the GUI:

1. After you create an instance of the service, you can choose a sample app in a language in which you feel comfortable working. You can choose from iOS Swift, Android, Node.js, and Java. Don't want to use an SDK? Check out this example to start <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">using {{site.data.keyword.appid_short_notm}} with other languages, such as Python <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Follow the steps in the GUI to **Build and run** your sample app. Each language is configured slightly differently, so be sure to select the language of the app that you downloaded from the drop-down. Once your app is configured, you can open it in a browser and login by using your credentials. Be sure the prerequisites for your app language are installed.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 or higher </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools version 25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (version 1.1.0 or higher) </li><li> iOS 9 or higher </li><li> MacOS 10.11.5 </li><li> Xcode (version 9.0.1 or higher) </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> The Cloud Foundry CLI </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> The Cloud Foundry CLI </li><li> Maven </li></ul></dd>
  </dl>
3. Click **Review Activity** to see the authentication events that occurred. After you log in, you can see an event.
4. Customize your login experience. You can select an image, such as your logo and a header color. You can select one of the color options or insert a hex value. When you are happy with the preview, click **Save Changes**.
5. In your browser, refresh your login page. The changes that you made in the previous step are already visible.
