---

copyright:
  years: 2017, 2024
lastupdated: "2024-11-01"

keywords: user events, track activity, manage events, analyze, administrative, runtime, sign in, settings, app security

subcollection: appid

---

{{site.data.keyword.attribute-definition-list}}


# Activity tracking events for {{site.data.keyword.appid_short_notm}} 
{: #at_events}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.appid_short_notm}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services. For information about migrating from {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: important}

## Locations where activity tracking events are generated
{: #at-locations}


### Locations where activity tracking events are sent to {{site.data.keyword.at_full_notm}} hosted event search
{: #at-legacy-locations}


{{site.data.keyword.appid_short_notm}} sends activity tracking events to {{site.data.keyword.at_full_notm}} hosted event search in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #at-table-1}
{: tab-title="Americas"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #at-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [No]{: tag-red} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #at-table-3}
{: tab-title="Europe"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

### Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}

{{site.data.keyword.appid_short_notm}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [No]{: tag-red} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}




## Viewing activity tracking events for {{site.data.keyword.appid_short_notm}}
{: #at-viewing}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.


### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)


## List of management events
{: #at_actions}

The following table conveys information regarding the actions that a user can take through the service GUI.

| Action | Description | GUI action |
|-----|----| ---- |
| `appid.recent-activity.read` | View recent activity. | Can be found in the **Activity Log** box on the **Overview** tab. |
| `appid.idp-config.read` | View the identity provider configuration. | Can be found in the **Manage authentication > Identity Providers** tab. |
| `appid.idp-config.update` | Update the identity provider configuration. | Can be updated in the **Manage authentication > Identity Providers** tab. |
| `appid.tokens-config.read` | View the token expiration configuration. | Can be found in the **Manage authentication > Authentication Settings** tab. |
| `appid.tokens-config.update` | Update the token expiration configuration. | Can be found in the **Manage authentication > Authentication Settings** tab. |
| `appid.redirect-uris.read` |  View the current redirect URI configuration. | Can be found in the **Manage authentication > Authentication Settings** tab. |
| `appid.redirect-uris.update` | Update the redirect URI configuration. | Can be updated in the **Manage authentication > Identity Providers** tab. |
| `appid.is-profiles-active.read` | View the user profile storage configuration. | Can be found in the **Profiles and roles > User Profiles** tab. |
| `appid.is-profiles-active.update` | Update your user profile storage configuration. | Can be found in the **Profiles and roles > User Profiles** tab. |
| `appid.users.read` | Search user profiles. | Can be found in the **Profiles and roles > User Profiles** tab. |
| `appid.users.create` | Create pre-registered user profile. | Can be found in the **Profiles and roles > User Profiles** tab. |
| `appid.users.get` | Export user profiles. | Must be done through the API. |
| `appid.refresh-token.revoke` | Revoke all the refresh tokens that are issued for the user. | Must be done through the API. |
| `appid.users.import` | Import user profiles. | Must be done through the API. |
| `appid.user-profile.read` | View a user profile. | Can be found in the **Profiles and roles > User Profiles** tab. |
| `appid.user-profile.update` | Update a user profile. | Can be found in the **Profiles and roles > User Profiles** tab. |
| `appid.user-profile.bulkdelete` | Delete a list of user profiles. | Can be found in the **Profiles and roles > User Profiles** tab. |
| `appid.user-roles.read` | View the user roles. | Can be found in the **Profiles and roles > User Profiles** tab. |
| `appid.user-roles.update` | Update the user roles. | Can be found in the **Profiles and roles > User Profiles** tab. |
| `appid.roles.read` | View the roles list. | Can be found in the **Profiles and roles > Roles** tab. |
| `appid.roles.create` | Create a role. | Can be found in the **Profiles and roles > Roles** tab. |
| `appid.role.read` | View the role. | Can be found in the **Profiles and roles > Roles** tab. |
| `appid.role.update` | Update the role. | Can be found in the **Profiles and roles > Roles** tab. |
| `appid.applications.read` | View the applications list. | Can be found in the **Applications** tab. |
| `appid.applications.create` | Create an application. | Can be found in the **Applications** tab. |
| `appid.application.read` | View the application. | Can be found in the **Applications** tab. |
| `appid.application.update` | Update the application. | Can be found in the **Applications** tab. |
|  `appid.application-scopes.read` | View the application scopes. | Can be found in the **Applications** tab. |
| `appid.application-scopes.update` | Update the application scopes. | Can be found in the **Applications** tab. |
| `appid.theme-text.read` | View the theme texts of the login widget. | Can be found in the **Login Customization** tab. |
| `appid.theme-text.update` | Update the theme texts of the login widget footnote. | Can be updated in the **Login Customization** tab. |
| `appid.theme-color.read` | View the theme color of the login widget header. | Can be found in the **Login Customization** tab. |
| `appid.theme-color.update` | Update the theme color of the login widget header. | Can be Updated in the **Login Customization** tab. |
| `appid.media.read` | View the image that is shown in the login widget. | Can be found in the **Login Customization** tab. |
| `appid.media.update` | Update the image that is shown in the login widget. | Can be updated in the **Login Customization** tab. |
| `appid.ui-configuration.read` | View the login widget UI configuration, which includes header color and image. | Can be found in the **Login Customization** tab. |
| `appid.ui-languages.read` | View a list of supported languages. | Must be viewed from the API. |
| `appid.ui-languages.update` | Update your supported languages. | Must be updated through the API. |
| `appid.saml-metadata.read` | View the {{site.data.keyword.appid_short_notm}} SAML metadata. | Can be found in the **Identity Providers > SAML 2.0 Federation** tab. |
| `ppid.cloud-directory-user.read` | View a Cloud Directory user. | Can be found in the **Cloud Directory > Users > View user details** tab. |
| `appid.cloud-directory-user.update` | Update a Cloud Directory User. | Can be updated in the **Users** tab. |
| `appid.cloud-directory-user.delete` | Delete a Cloud Directory user. | Must be deleted through the API. |
| `appid.user.delete` | Delete a Cloud Directory user and profile. | Must be deleted through the API. |
| `appid.cloud-directory-users.read` | View a list of your Cloud Directory users. | Can be found in the **Cloud Directory > Users** tab. |
| `appid.cloud-directory-user.update` | Update your list of Cloud Directory users. | Can be updated in the **Cloud Directory > Users** tab. |
| `appid.cloud-directory-user.delete` | Delete a list of Cloud Directory users. | Must be deleted through the API. |
| `appid.users.bulkdelete` | Delete a list of Cloud Directory users and profiles. | Must be deleted through the API. |
| `appid.cloud-directory-users.get` |Export Cloud Directory users. | Must be done through the API. |
| `appid.cloud-directory-users.import` | Import Cloud Directory users. | Must be done through the API. |
| `appid.cloud-directory-user-sso.set-off` | Invalidate all SSO sessions of the user. | Must be done through the API. |
|  `appid.email-dispatcher.read` | View the email dispatcher configurations. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.email-dispatcher.update` | Update the email dispatcher configurations. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.email-dispatcher-test.send` | Test the email dispatcher. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.email-settings-test.send` | Test the email settings configurations. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.email-template.read` | View an email template. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.email-template.update` | Update an email template. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.email-template.delete` | Delete an email template to reset to the default. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.sender-details.read` | View the sender details. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.sender-details.update` | Update the sender details. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.resend-notification.send` | Resend user notifications. | Must be done through the API. |
| `appid.self-forgot-password.start` | Starts the forgot password process. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.forgot-password-result.read` | View the forgot password confirmation result. | Must be done through the API. |
| `appid.self-sign-up.start` | Starts the sign-up process. | Can be found in the **Cloud Directory > Settings** tab. |
| `appid.sign-up-result.read` | View the sign-up result confirmation. | Must be done through the API. |
| `appid.action_url.read` | View the custom URL that is called when an action is performed. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.action-url.update` | Update the custom URL that is called when an action is performed. | Can be found in the **Cloud Directory > Email Templates** tab. |
| `appid.password-regex.read` | View the password regex. | Can be found in the **Cloud Directory > Password Policies** tab. |
| `appid.password-regex.update` | Update the password regex. | Can be found in the **Cloud Directory > Password Policies** tab. |
| `appid.advanced-password-management.read` | View the advanced password policy configurations. | Can be found in the **Cloud Directory > Password policies** tab. |
| `appid.advanced-password-management.update` | Update the advanced password policy configurations. | Can be found in the **Cloud Directory > Password Policies** tab. |
| `appid.user-password.update` | Set a new password for the Cloud Directory user. | Must be done through the API. |
| `appid.capture-runtime-activity.read` | View runtime activity toggle. | Can be viewed in the **Manage Authentication> Authentication Settings** tab. |
| `appid.capture-runtime-activity.update` | Toggle runtime activity monitoring. | Can be updated in the **Manage Authentication> Authentication Settings** tab. |
| `appid.mfa.read` | View your MFA configurations. | Can be found in the **Cloud Directory > Multi-factor Authentication** tab. |
| `appid.mfa.update` | Update your MFA configurations. | Can be found in the **Cloud Directory > Multi-factor Authentication** tab. |
| `appid.mfa-channels.read` | View your MFA channels. | Can be found in the **Cloud Directory > Multi-factor Authentication** tab. |
| `appid.mfa-channel.read` | View your MFA channels configurations. | Can be found in the **Cloud Directory > Multi-factor Authentication** tab. |
| `appid.mfa-channel.update` | Update your channels. | Can be found in the **Cloud Directory > Multi-factor Authentication** tab. |
| `appid.sms-dispatcher-test.send` | Test the SMS dispatcher configurations. | Can be found in the **Cloud Directory > Multi-factor Authentication > SMS Provider** tab. |
| `appid.mfa-extension-premfa.read` | View your pre-MFA extension configuration. | Must be done through the API. |
| `appid.mfa-extension-premfa.update` | Update your pre-MFA extension configuration. | Must be done through the API. |
| `appid.mfa-extension-postmfa.read` | View your post MFA extension configuration. | Must be done through the API. |
| `appid.mfa-extension-postmfa.update` | Update your post MFA extension configuration. | Must be done through the API. |
| `appid.is-mfa-extension-active.update` | Update the status of your registered extension. | Must be done through the API. |
| `appid.mfa-extension-test.send` | Test your registered extension configuration. | Must be done through the API. |
| `ppid.sso.read` | View your SSO configuration. | Can be found in the **Identity Providers > Cloud Directory > Single Sign-On** tab. |
| `appid.sso.update` | Update your SSO configuration. | Can be found in the **Identity Providers > Cloud Directory > Single Sign-On** tab. |
| `appid.rate-limit.read` | View your rate limit configurations. | Must be done through the API. |
| `appid.rate-limit.update` | Update your rate limit configurations. | Must be done through the API. |
{: caption="Actions that generate management events" caption-side="bottom"}


## Viewing runtime events
{: #at-monitor-runtime}

Runtime events allow you to track activity that is made by user's to your application, such as logins, password resets, and authentication requests.

| Description | Action | Outcome | `reason. reasonCode` | `target.id` | `target.name` | `target.typeURI` |
|-----|----| ----- | ------- | ------- | ------- | ------ |
| Cloud Directory authentication success | `appid.user.authenticate` | `success` | `200` | `[appid user CRN]` |  `cloud_directory:[GUID]` | `appid/user` |
| Cloud Directory authentication failure | `appid.user.authenticate` | `failure` | `401` | `[appid user CRN]` | `cloud_directory:[GUID]` | `appid/user` |
| Facebook authentication success | `appid.user.authenticate` | `success` | `200` | `[appid user CRN]` | `facebook:[GUID]` | `appid/user` |
| Facebook authentication failure | `appid.user.authenticate` | `failure` | `401` | `crn:unknown` | `facebook:unknown` | `appid/user` |
| Google authentication success | `appid.user.authenticate` | `success` | `200` | `[appid user CRN]` | `google:[GUID]` | `appid/user` |
| Google authentication failure | `appid.user.authenticate` | `failure` | `401` | `crn:unknown` | `google:unknown` | `appid/user` |
| SAML authentication success | `appid.user.authenticate` |  `success` | `200` | `[appid user CRN]` | `SAML:[GUID]` | `appid/user` |
| SAML authentication failure | `appid.user.authenticate` | `failure` | `401` | `crn:unknown` | `SAML:unknown` | `appid/user` |
| Client Credentials authentication success | `appid.application.authenticate` | `success` | `200` | `[appid application CRN]` | `client_credentials:client_id` | `appid/application` |
| Client Credentials authentication failure | `appid.application.authenticate` | `failure` | `401` | `crn:undefined` | `client_credentials:undefined` | `appid/application` |
| Cloud Directory sign up | `appid.cloud-dir-user.create` | `success` | `200` | `[appid user CRN]` | `cloud_directory:[GUID]` | `appid/cloud_dir/user` |
|Cloud Directory signup failure | `appid.cloud-dir-user.create` | `failure` | `400` | `crn:unknown` | `cloud_directory:unknown` | `appid/cloud_dir/user`|
| Cloud Directory signup confirmation | `appid.cloud-dir-user.allow` | `success` | `200` | `[appid user CRN]` | `cloud_directory:[GUID]` | `appid/cloud_dir/user` |
| Cloud Directory signup confirmation failure | `appid.cloud-dir-user.allow` | `failure` | `400` | `crn:unknown` | `cloud_directory:unknown`| `appid/cloud_dir/user` |
| Cloud Directory reset or renew password | `appid.cloud-dir-user-credentials.renew` | `success` | `200` | `[appid user CRN]` | `cloud_directory:[GUID]` | `appid/cloud_dir/user`|
| Cloud Directory reset or renew password failure | `appid.cloud-dir-user-credentials.renew` | `failure` | `400` | `crn:unknown` | `cloud_directory:unknown` | `appid/cloud_dir/user` |
| Cloud Directory change password | `appid.cloud-dir-user-credentials.update` | `success` | `200` | `[appid user CRN]` | `cloud_directory:[GUID]` | `appid/cloud_dir/user`|
| Cloud Directory change password failure | `appid.cloud-dir-user-credentials.update` | | `failure` | `400` | `crn:unknown` | `cloud_directory:unknown` | `appid/cloud_dir/user` |
| Revoke user tokens | `appid.user-tokens.revoke` | `success` | `200` | `appid user CRN` | `idp:[GUID]` | `appid/user` |
| Revoke user tokens failure | `appid.user-tokens.revoke` | `failure` | `400` | `appid user CRN` | `idp:[GUID]` | `appid/user` |
| Cloud Directory user SSO logout | `appid.cloud-dir-user.set-off` | `success` | `200` | `appid user CRN` | `idp:[GUID]` | `appid/user` |
| View user profile attributes | `appid.user-profile-attributes.read` | `success` | `200` | `crn:profiles:[User-ID]` | `profiles:[User-ID]` | `appid-user-profiles/attributes` |
| Update user profile attribute | `appid.user-profile-attributes.update` | `success` | `200` | `crn:profiles:[User-ID]` | `profiles:[User-ID]` | `appid-user-profiles/attribute/[Attribute-name]` |
| Delete user profile attribute | `appid.user-profile-attributes.delete` | `success` | `200` | `crn:profiles:[User-ID]` | `profiles:[User-ID]` | `appid-user-profiles/attribute/[Attribute-name]` |
{: caption="Actions that can be tracked as authentication events at runtime" caption-side="top"}
