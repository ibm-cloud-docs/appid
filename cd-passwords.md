---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

subcollection: appid

---

{:new_window: target="_blank"}
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

You can set the requirements for the passwords that can be used with Cloud Directory. By defining specific requirements that your users must adhere to, you can ensure more secure applicaitons.
{: shortdesc}

## Policy: password strength
{: #cd-password-strength}

A strong password makes it difficult, or even improbable for someone to guess the password in either a manual or automated way. To set requirements for the stregnth of a users password, you can use the following steps.
{: shortdesc}

1. Navigate to the **Password Policies** tab of the App ID dashboard.

2. In the **Define password strength** box, click **Edit**. A screen displays.

3. Enter a valid regex string in the **Password strength** box.

  Examples:
    - Must be at least eight characters. Example regex: `^.{8,}$`
    - Must contain one number, one lowercase letter, and one capital letter. Example regex: `^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
    - Must contain only English letters and numbers. Example regex: `^[A-Za-z0-9]*$`
    - Must be at least one unique character. Example regex: `^(\w)\w*?(?!\1)\w+$`

4. Click **Save**.

Password strength can be set in the Cloud Directory settings page in {{site.data.keyword.appid_short_notm}} Console, or by using <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/set_cloud_directory_password_regex" target="_blank">the management APIs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{: note}


## Advanced password policies
{: #cd-advanced-password}


You can enhance the security of your application by enforcing additional password constraints.
{: shortdesc}


You can create an advanced password policy that consists of any combinatino of the following 5 features:

 - Lockout after repeated wrong credentials
 - Avoid password reuse
 - Password expiration
 - Minimum period between password changes
 - Ensure password does not include username


 If you enable this feature, additional billing for advanced security capabilities is activated. For more information, see the [How does {{site.data.keyword.appid_short_notm}} calculate pricing](/docs/services/appid?topic=appid-faq#faq-pricing).
 {: important}


### Policy: Avoid Password Reuse
{: #cd-avoid-reuse}

When your users are changing their password, you might want to prevent them from choosing a recently used password.
{: shortdesc}

By using the GUI or the API, you can choose the number of passwords that a user must have before they can repeat a previously used password. You can select any whole value in range 1 - 10.

If this option is turned on, a user cannot use a password that was recently used by them. If they try to set their password to a password that was recently used, they are shown an error in the default Login Widget GUI and are prompted to enter a different password.

Previous passwords are securely stored in the same way that a user's current password is stored.
{: note}


### Policy: Lockout after repeated wrong credentials
{: #cd-lockout}

You might want to protect your users' accounts by temporarily blocking the ability to sign in when a suspicious behavior is detected, such as multiples consecutive sign in attempts with an incorrect password. This measure can help to prevent a malicious party from gaining access to a user's account by guessing a user's password.
{: shortdesc}

By using the GUI or the API, you can set the maximum number of unsuccessful sign in attempts that a user can make before their account is temporarily locked. You can also set the amount of time that the account is locked for. You have the following options:

* Number of attempts: Any whole value 1 - 10.
* Lockout period: Any whole value specified in minutes in the range 1 minute to 1440 minutes (24 hours).

If an account is locked, users are unable to sign in or perform any other self service operations, such as changing their password until the specified lockout period has elapsed. When the lockout period has ended, the user is automatically unlocked.

You can unlock a user before the lockout period is over. To see whether they are locked out look to see whether the `active` field is set to `false`. You can also check to see whether their status on the **Users** tab of the service dashboard is set to `disabled`. To unlock a user, you must use [the API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) to set the `active` field to `true`.


### Policy: Minimum period between password changes
{: #cd-minimum-time}

You might want to prevent your users from quickly switching between passwords by setting a minimum period of time that a user must wait between password changes.
{: shortdesc}

This feature is especially useful when used with the "Avoid password reuse" policy. Without this limitation, a user could simply change their password multiple times in quick succession to circumvent the limitation of re-using recent passwords. You can select any value between 1 hour and 30 days, specified in hours.


### Policy: Password expiration
{: #cd-expiration}

For security reasons, you might want to enforce a password rotation policy, such that your users must change their password after a period of time.
{: shortdesc}

By using the GUI or the API, you can set a time period for which your user's passwords will remain valid. After a user's password expires, they are forced to reset their password on the next sign in. You can select any number of full days between 1 and 90.

You can quickly get started with the Login Widget by using the provided default GUI. The user is directed to supply a new password before the sign in is complete.

If you're using a custom sign in experience, an error is triggered when a user attempts to sign in with an expired password. It is your responsibility to configure your application to provide the necessary user experience. You can call the change password API to set the new password.

The token endpoint response looks similar to the following:

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

When this option is first set to on, any existing user passwords will not have an expiration date. The expiration period begins for the users when their password is changed. You might want to encourage users to update their password after you set this feature to on.
{: note}


### Policy: Ensure password does not include username
{: #cd-no-username}

For stronger passwords, you might want to prevent users that contain their username or the first part of their email address.
{: shortdesc}

This constraint is not case-sensitive, which means that users are not able to alter the case of some or all of the characters in order to use the personal information. To configure this option, toggle the switch to **on**.

