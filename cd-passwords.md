---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-23"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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

# Defining password policies
{: #cd-strength}

You can set the requirements for the passwords that can be used with Cloud Directory. By defining specific requirements that your users must adhere to, you can ensure more secure applications.
{: shortdesc}

## Policy: password strength
{: #cd-password-strength}

A strong password makes it difficult, or even improbable for someone to guess the password in either a manual or automated way. To set requirements for the strength of a user's password, you can use the following steps.
{: shortdesc}

1. Go to the **Password policies** tab of the {{site.data.keyword.appid_short_notm}} dashboard.

2. In the **Define password strength** box, click **Edit**. A screen opens.

3. Enter a valid regex string in the **Password strength** box.

  Examples:
    - Must be at least 8 characters. (`^.{8,}$`)
    - Must have one number, one lowercase letter, and one capital letter. (`^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`)
    - Must have only English letters and numbers. (`^[A-Za-z0-9]*$`)
    - Must have at least one unique character. (`^(\w)\w*?(?!\1)\w+$`)

4. Click **Save**.

Password strength can be set in the Cloud Directory settings page in {{site.data.keyword.appid_short_notm}} Console, or by using <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">the management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{: note}

### Setting a custom error message
{: #cd-custom-error}

If you set your own password regex policy and a user chooses a password that does not meet your requirements, the default message is "The password doesn't meet the strength requirements." You can also choose to set your own message by using the [`/management/v4/{tenantId}/config/cloud_directory/password_regex` endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex){: external}. 



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


 When you enable this feature, extra billing for advanced security capabilities is activated. For more information, see [how does {{site.data.keyword.appid_short_notm}} calculate pricing](/docs/services/appid?topic=appid-faq#faq-pricing).
 {: important}


### Policy: Avoid Password Reuse
{: #cd-avoid-reuse}

When your users are changing their password, you might want to prevent them from choosing a recently used password.
{: shortdesc}

By using the GUI or the API, you can choose the number of passwords that a user must have before they are able to repeat a previously used password. Setting options include any whole value in range 1 - 10.

If this option is turned on, a user can't use a password that they recently used. If they try to set their password to one that was recently used, an error is shown in the default Login Widget GUI and the user is prompted to enter another option.

Previous passwords are securely stored in the same way that a user's current password is stored.
{: note}


### Policy: Lockout after repeated wrong credentials
{: #cd-lockout}

You might want to protect your users' accounts by temporarily blocking the ability to sign in when a suspicious behavior is detected, such as multiple consecutive sign-in attempts with an incorrect password. This measure can help to prevent a malicious party from gaining access to a user's account by guessing a user's password.
{: shortdesc}

By using the GUI or the API, you can set the maximum number of unsuccessful sign-in attempts that a user makes before their account is temporarily locked. You can also define the amount of time that the account is locked for. You have the following options:

* Number of attempts: Any whole value 1 - 10.
* Lockout period: Any whole value that is specified in minutes in the range 1 minute to 1440 minutes (24 hours).

If an account is locked, users are unable to sign in or complete any other self-service operations, such as changing their password until the specified lockout period is complete. When the lockout period is over, the user is automatically unlocked.

You can unlock a user before the lockout period is over. To see whether they are locked out, check whether the `active` field is set to `false`. You can also check to see whether their status on the **Users** tab of the service dashboard is set to `disabled`. To unlock a user, you must use [the API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) to set the `active` field to `true`.


### Policy: Minimum period between password changes
{: #cd-minimum-time}

You might want to prevent your users from quickly switching passwords by setting a minimum time that a user must wait between password changes.
{: shortdesc}

This feature is especially useful when used with the "Avoid password reuse" policy. Without this limitation, a user might simply change their password multiple times in quick succession to circumvent the limitation of reusing recent passwords. You can select any value in the range 1 and 720 hours (30 days). The field is specified in hours.


### Policy: Password expiration
{: #cd-expiration}

For security reasons, you might want to enforce a password rotation policy, such that your users must change their password after a specified amount of time.
{: shortdesc}

By using the GUI or the API, you can set a time period for which your user's passwords remain valid. After a user's password expires, they are forced to reset their password on the next sign-in. You can select any number of full days in range 1 and 90.

You can quickly get started with the Login Widget by using the provided default GUI. The user is directed to supply a new password before the sign-in is complete.

If you're using a custom sign-in experience, an error is triggered when a user attempts to sign in with an expired password. It is your responsibility to configure your application to provide the necessary user experience. You can call the change password API to set the new password.

The token endpoint response looks similar to the following:

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

When this option is first set to on, any existing user passwords do not have an expiration date. The expiration period begins for the users when their password is changed. You might want to encourage users to update their password after you set this feature to on.
{: note}


### Policy: Ensure that the password does not include user name
{: #cd-no-username}

For stronger passwords, you might want to prevent users that contain their user name or the first part of their email address.
{: shortdesc}

This constraint is not case-sensitive. Users are not able to alter the case of some or all of the characters in order to use the personal information. To configure this option, toggle the switch to **on**.
{: note}

