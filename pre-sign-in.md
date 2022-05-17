---

copyright:
  years: 2017, 2022
lastupdated: "2022-05-17"

keywords: user registration, new user, add user, custom attributes, profiles, user profile, user, user information, identity provider, authentication, authorization, personalize app, app security

subcollection: appid

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

# Preregistering future users
{: #preregister}

With {{site.data.keyword.appid_full}}, you can start building a profile for users that you know are going to need access to your app before their initial sign-in.
{: shortdesc}

To learn more about the security considerations that might apply when you work with custom attributes, see [Storing and accessing user profiles](/docs/appid?topic=appid-profiles).
{: tip}


## Understanding preregistration
{: #preregister-understand}

There might be times when you are developing an application that you already know who your app users are going to be. These users are known as "future users". You might know ahead of time that certain users need specific permission levels or a specific food preference before they ever start interacting with your app. For example, you work for a development company and you hire a new person to function as a team lead. You might want to assign that user `admin` access to your app before they start so that when they sign in the first time, they can immediately start working without any further interaction on your part. Say that same person is a vegetarian. By noting it as a custom attribute in their profile, the preference can be pulled for all team lunches without them having to remind you.

By default, the ability for users to change their own custom attributes through the application is set to off. You can give your users that ability, but before you do be sure that you understand and have considered the [security issues](/docs/appid?topic=appid-profiles#profile-set-custom) that can arise.

To assign custom attributes for future users, you can use either [the GUI](/docs/appid?topic=appid-preregister#preregister-gui) or the [preregistration endpoint](/docs/appid?topic=appid-preregister#preregister-api).


### How are users identified?
{: #preregister-identify-user}

You can identify your users by using one of the following:

* The email address with which the user signs in to your app.
* If available, the user's unique ID, called the **GUID**, in the identity provider. Although this identifier always exists and is guaranteed to be unique, it is not always readily available or easy to understand. For instance, Cloud Directory uses a random 16-byte GUID.


### What information do the identity providers provide?
{: #preregister-idp-provide}

Check out the following table to see which type of identity information that you can use.

| Identity provider | GUID | Email | Sub | 
|-----|----| -----| ---|
| Cloud Directory | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | |
| Facebook | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | | 
| Google | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | | 
| SAML | | ![Checkmark icon](../../icons/checkmark-icon.svg) | | 
| Custom | | | ![Checkmark icon](../../icons/checkmark-icon.svg) |
{: caption="Table 1. Types of identity information that can be used with each provider" caption-side="top"}


### How is Cloud Directory handled?
{: #preregister-cd}

To ensure the integrity of a future user, Cloud Directory places extra requirements on preregistration. 

* You must use an email, not a user name, to add the user. If you don't have any users yet, switch to email and password mode to add future users. If you do have users, you must wait until the user has signed in to assign custom attributes.
* The user must confirm their identity through verification. When you add a future user with specific attributes, those attributes are intended for that person. Any user that signs in by using an email that is registered to a future user must verify their email address before they are granted access to your app. To complete the verification requirements, you can send an email to have the user verify or manually verify their address on their behalf. To allow for self-verification, set **Email verification** to **On** in the **Cloud Directory** tab of the service dashboard. This sends an email to the user to request verification on their initial sign-in. To verify users manually, you must be an administrator. Make a request to the Cloud Directory [management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser){: external} to set the `status` field in the payload to `CONFIRMED`.  

If a future user is added by you and signs in to your app without verifying their email, their custom attributes are deleted and the profile is created from scratch.
{: important}




### Is there anything special that I need to do when I use a custom identity provider?
{: #preregister-custom}

When you add user information to your application in advance, you can use any unique identifier that is provided by the authentication flow. The identifier must _exactly_ match the `sub` of the signed JSON Web Token that is sent during the authorization request. If the identifier does not match, then the profile that you want to add is not linked successfully.


## Adding a future user
{: #preregister-add-info}

Now that you've learned about the process and considered your security implications, try adding a user. 


A user's predefined attributes are empty until their first authentication. Although they're empty, the user is still fully authenticated. You can use their profile ID just as you would someone who has already signed in. For instance, you can modify, search, or delete the profile.
{: tip}



### Before you begin
{: #preregister-before}

Before you get started, you must have the following information:

* Which identity provider that the user will sign in with.
* The email of the user that you want to add or their [unique identifier](/docs/appid?topic=appid-preregister#preregister-idp-provide).
* The [custom attribute](/docs/appid?topic=appid-profiles) information that you want to assign.


### With the GUI
{: #preregister-gui}

You can add a future user and their custom attributes by using the GUI.

The ability to add future users is disabled for the user name and password configuration of Cloud Directory.
{: note}

1. Go to the **User Profiles** tab of the {{site.data.keyword.appid_short_notm}} dashboard.
2. Click **Future users**. If you already have future users, you see a table with a list of the user's that you already added. To add another user, click **Build a profile**. If you don't have any users yet, click **Get Started**. A screen opens.
3. Enter your user's email.
4. Select the identity provider that they sign in with from the **Identity Provider** drop down.
5. Add custom attributes by entering the information in a JSON object as shown in the following example.

   ```json
   { 
      "food": "Pizza", 
      "preference": "Vegetarian",
      "points": "37"
   }
   ```
   {: screen}

6. Click **Save**. The table displays and the user is assigned an identifier.


### With the API
{: #preregister-api}

You can add a future user and their custom attributes by using the API.

1. Log in to IBM Cloud.

   ```sh
   ibmcloud login
   ```
   {: codeblock}

2. Find your IAM token by running the following command.

   ```sh
   ibmcloud iam oauth-tokens
   ```
   {: codeblock}

3. Make a POST request to the `/users` endpoint that contains a description of the user and the attributes that you want to set as a JSON object.

   Header:

   ```sh
   POST <managementUrl>/management/v4/<tenantID>/users
         Host: <managementServerURL>
         Authorization: 'Bearer <IAMToken>'
         Content-Type: application/json
   ```
   {: codeblock}

   Body:

   ```json
   {
         "idp": "<identityProvider>",
         "idp-identity": "<userUniqueIdentifier>",
         "profile": {
            "attributes": {
               "mealPreference":"vegeterian"
            }
         }
   }
   ```
   {: codeblock}

   | Components | Description |
   | ---------- | ----------- |
   | `idp` | The identity provider that the user authenticates with. Options include: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid`. |
   | `idp-identity` | The unique identifier provided by the identity provider. |
   | `profile` | The user's profile that contains the custom attribute JSON mapping. |
   {: caption="Table 2. The components of the POST request" caption-side="top"}

   Example request:
   ```sh
   $ curl --request POST \
         --url 'https://<managementURI>/users \
         --header 'Authorization: Bearer <IAMToken>' \
         --header 'Content-Type: application/json' \
         --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
         "frequent_flyer_points": 1000 }}}'
   ```
   {: screen}

4. Verify that registration was successful.

   * Check for the user profile that was created.

      ```sh
      curl --request GET https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/users/<userProfileId>/profile \
      --header 'Authorization: Bearer <IAMToken>' \
      --header 'Content-Type: application/json' \
      ```
      {: codeblock}
      
   * Check for the user ID in the response.

      ```sh
      {
         "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
         "identities": [],
         "attributes": {
            "role": "manager"
         }
      }
      ```
      {: screen}
  



## Next steps
{: #preregister-next}

Now that you associated a future user with specific attributes, try [accessing or updating attributes](/docs/appid?topic=appid-profiles)!


</br>
