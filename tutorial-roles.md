---

copyright:
  years: 2014, 2019
lastupdated: "2019-01-04"

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



# Tutorial: Setting user roles
{: #tutorial-roles}

With this tutorial, you can see a step-by-step guide to obtaining roles and scopes from an external identity provider and then applying them to a user's profile within your application.
{: shortdesc}

As an example, this tutorial uses an app for a fictional theme park called Cloud Land. The app allows users to sign in with a username and password or by using social login. You can only imagine all of the ways that you could use an app like this. For example, you ask your user to provide information about the group of people that are going to be attending the theme park. This allows for you to create a suggested schedule that fits your users age range, thrill level, and dietary preferences. This example is a little bit more simple, but the logic can be applied across any type of role or scope that you want to apply.


## Objectives
{: #objectives}

For the duration of the tutorial, you play the role of the Cloud Land app developer and you will:

- Add a role for a user before they've signed in to your app
- Obtain roles from an external identity provider
- Apply the roles to the users profile
- Test the configuration


## Time required
{: #time}

XX minutes


## Audience
{: #audience}

This tutorial is intended for software developers who are assigning scopes and roles for the first time.
{: shortdesc}

## Prerequisites

- Ensure you have an instance of the App ID service.
- Check to see if you have the **Administrator** {{site.data.keyword.Bluemix_notm}} IAM platform role.
- Android pre reqs
- Already set up to work with GitHub


## Lesson 1: Configuring the sample app
{: #configure-app}

Before you can start adding roles and scopes for your Cloud Land users, you need to download and configure the application code.
{: shortdesc}

1. Clone the following repository.
  ```
  https://github.com/rotembr/Cloud-Land-sample.git
  ```
  {: codeblock}

2. Navigate to your instance of the App ID service and make the following configurations.

  1. In the Identity Providers tab, enable Cloud Directory, Facebook, and Google.
  2. In the Cloud Directory > Email Verification tab, set Allow users to sign-in to your app without first verifying their email address to Yes.

3. Navigate to the Service Credentials tab and click View credentials. Copy the tenantId GUID number.

4. By using Android Studio, open the GitHub project that you cloned in step 1.

5. Open the credentials.xml file and replace App-ID-tenantId with your tenant ID.

6. If your instance of App ID is not in the US South region, open the MainActivity.java file and update the region to match the region in which your instance is located.





## What's next?
{: #next}
