---

copyright:
  years: 2017, 2020
lastupdated: "2020-03-19"

keywords: password policies, password strength, advanced, sign in, lock out, reset password, email, expiration, credentials, password reuse, wrong credentials, secure apps, registry, cloud directory, regex

subcollection: appid

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
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


# Defining password policies
{: #cd-strength}

Password policies, such as strength requirements, help you to enforce more secure applications. By defining advanced policies, you can define the rules that a user must conform to when they set their password or attempt to sign in to your app. For example, you can set the number of times that a user can try to sign in before they are locked out of their account.
{: shortdesc}


## Policy: password strength
{: #cd-password-strength}

A strong password makes it difficult, or even improbable for someone to guess the password in either a manual or automated way. To set requirements for the strength of a user's password, you can use the following steps.
{: shortdesc}

To set this configuration by using the GUI:

1. Go to the **Cloud Directory > Password policies** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. In the **Define password strength** box, click **Edit**. A screen opens.

3. Enter a valid regex string in the **Password strength** box.

  Examples:
    - Must be at least 8 characters. (`^.{8,}$`)
    - Must have one number, one lowercase letter, and one capital letter. (`^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`)
    - Must have only English letters and numbers. (`^[A-Za-z0-9]*$`)
    - Must have at least one unique character. (`^(\w)\w*?(?!\1)\w+$`)

4. Click **Save**.

Password strength can be set in the Cloud Directory settings page in the {{site.data.keyword.appid_short_notm}} dashboard, or by using [the management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex){: external}.
{: note}


### Setting a custom error message
{: #cd-custom-error}

If you set your own password regex policy and a user chooses a password that does not meet your requirements, the default message is `The password doesn't meet the strength requirements.` You can also choose to set your own message by using the [`/management/v4/{tenantId}/config/cloud_directory/password_regex` endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex){: external}. 



## Advanced password policies
{: #cd-advanced-password}


You can enhance the security of your application by enforcing password constraints.
{: shortdesc}


You can create an advanced password policy that consists of any combination of the following five features:

 - Lockout after repeated wrong credentials
 - Avoid password reuse
 - Password expiration
 - Minimum period between password changes
 - Ensure that the password does not include user name


 When you enable this feature, extra billing for advanced security capabilities is activated. For more information, see [how does {{site.data.keyword.appid_short_notm}} calculate pricing](/docs/appid?topic=appid-faq#faq-pricing).
 {: important}


### Policy: Avoid Password Reuse
{: #cd-avoid-reuse}

You might want to prevent your users from choosing a recently used password when they attempt to create a new one. If they try to set their password to one that was recently used, an error is shown in the default Login Widget GUI and the user is prompted to enter another option. This setting allows for you to choose the number of passwords that a user must have before they're able to repeat a previously used password.
{: shortdesc}

To set this configuration by using the GUI:

1. Go to the **Cloud Directory > Password policies** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Toggle **Advanced password policy** to **Enabled**.

3. Specify **The number of times that a password can't be repeated**. You can use any whole value in range 1 - 10.

4. Toggle **The number of times that a password can't be repeated** to **Enabled**.

5. Click **Save**.

Previous passwords are securely stored in the same way that a user's current password is stored.
{: note}


### Policy: Lockout after repeated wrong credentials
{: #cd-lockout}

You might want to protect your users' accounts by temporarily blocking the ability to sign in when a suspicious behavior is detected, such as multiple consecutive sign-in attempts with an incorrect password. This measure can help to prevent a malicious party from gaining access to a user's account by guessing their password.
{: shortdesc}

If an account is locked, users are unable to sign in or complete any other self-service operations until the specified lockout period is complete. When the lockout period is over, the user is automatically unlocked.

To set this configuration by using the GUI:

1. Go to the **Cloud Directory > Password policies** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Toggle **Advanced password policy** to **Enabled**.

3. Specify **The number of times a user can try to sign in before getting locked out**. You can use any whole value in range 1 - 10.

4. Specify **The time a user will be locked out after trying to sign in with wrong credentials**. The time is specified in minutes. You can use any whole value in range 1 - 1440 (24 hours).

5. Toggle **The number of times a user can try to sign in before getting locked out** row to **Enabled**.

6. Click **Save**.


You can unlock a user before the lockout period is over. To see whether they are locked out, check whether the `active` field is set to `false`. You can also check to see whether their status on the **Users** tab of the service dashboard is set to `disabled`. To unlock a user, you must use [the API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) to set the `active` field to `true`.
{: note}


### Policy: Minimum period between password changes
{: #cd-minimum-time}

You might want to prevent your users from quickly switching passwords by setting a minimum time that a user must wait between password changes.
{: shortdesc}

This feature is especially useful when used with the `Avoid password reuse` policy. Without this limitation, a user might simply change their password multiple times in quick succession to circumvent the limitation of reusing recent passwords.

To set this configuration by using the GUI:

1. Go to the **Cloud Directory > Password policies** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Toggle **Advanced password policy** to **Enabled**.

3. Specify **The minimum time between password changes**. The time is specified in hours. You can use any whole value in range 1 - 720 (30 days).

4. Toggle **The minimum time between password changes** to **Enabled**.

5. Click **Save**.


### Policy: Password expiration
{: #cd-expiration}

For security reasons, you might want to enforce a password rotation policy. By setting an expiration for your users password, they are forced to update their password in order to retain access to your application. This lessens the chance that a user's credentials can cause long term damage to your application. When their password expires, your users are forced to reset it on their next sign-in attempt.
{: shortdesc}

To set this configuration by using the GUI:

1. Go to the **Cloud Directory > Password policies** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Toggle **Advanced password policy** to **Enabled**.

3. Specify a **Password expiration time**. The time is specified in days. You can use any whole value in range 1 - 90.

4. Toggle **Password expiration time** to **Enabled**.

5. Click **Save**.

When this option is first set to on, any existing user passwords do not have an expiration date. To ensure that all of your users are limited by the password rotation policy, you might encourage users to update their password after you configure this feature.
{: note}

**Custom sign in experience**

If you're using a custom sign-in experience, an error is triggered when a user attempts to sign in with an expired password. It is your responsibility to configure your application to provide the necessary user experience. You can call the change password API to set the new password.

The token endpoint response looks similar to the following:

```json
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}



### Policy: Ensure that the password does not include user name
{: #cd-no-username}

For stronger passwords, you might want to prevent users from creating a password that contains their username or the first part of their email address.
{: shortdesc}

To set this configuration by using the GUI:

1. Go to the **Cloud Directory > Password policies** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. Toggle **Advanced password policy** to **Enabled**.

3. Toggle **Password should not contain user ID** to **Enabled**.

4. Click **Save**.

This constraint is not case-sensitive. Users are not able to alter the case of some or all of the characters in order to use the personal information. To configure this option, toggle the switch to **on**.
{: note}

