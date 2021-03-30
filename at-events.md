---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-30"

keywords: user events, track activity, manage events, analyze, administrative, runtime, sign in, settings, app security

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

# Auditing events for {{site.data.keyword.appid_short_notm}}
{: #at-events}

You can view, manage, and analyze user-initiated activities made in your {{site.data.keyword.appid_full}} service instance by using the {{site.data.keyword.at_short}} service.
{: shortdesc}

By integrating {{site.data.keyword.at_short}} with {{site.data.keyword.appid_short_notm}} you can track two different types of events, administrative and runtime. Administrative events are those that are specific to your instance of the service. Administrative events cover configuration changes such as updating your identity providers or changing the theme of your login widget. Runtime events are those activities that occur at runtime by the app user. A password reset request, authentication failures, or a user log out would all fall into the runtime category.

For more information about how the service works, see the [{{site.data.keyword.at_short}} docs](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-cloud_services).



## Viewing administrative events
{: #at-monitor-admin}

You can view, manage, and analyze configuration activity that is made in your {{site.data.keyword.appid_short_notm}} instance by using the {{site.data.keyword.at_short}} service.
{: shortdesc}

### Monitoring administrative activity
{: #at-monitor-admin-activity}

1. Log in to your {{site.data.keyword.cloud_notm}} account.
2. From the catalog, provision an instance of the {{site.data.keyword.at_short}} service in the same account and region as your {{site.data.keyword.appid_short_notm}} instance.
3. From the **Observability > Activity Tracker** tab, verify the information for the instance that you created.
4. Click **View Open Dashboard** and make sure you're on the **Everything** dashboard. Any events that meet the qualifications for your {{site.data.keyword.at_short}} payment plan are visible. You can filter your results by tags, sources, apps or levels. You can also search for specific events or jump to a specific timeframe.



## List of administrative events
{: #at-events-admin}

Check out the following table for a list of the events that are sent to {{site.data.keyword.at_short}}.

Some of the action names were changed as part of an alignment to new guidelines. [Learn more](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-event#action_field).
{: important}

<table>
  <caption>Table 1. Actions that you can take that are tracked by {{site.data.keyword.at_short}}</caption>
  <tr>
    <th>Action</th>
    <th>Description</th>
    <th>GUI action</th>
  </tr>
  <tr>
    <td><code>appid.recent-activity.read</code></td>
    <td>View recent activity.</td>
    <td>Can be found in the <strong>Activity Log</strong> box on the <strong>Overview</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.idp-config.read</code></td>
    <td>View the identity provider configuration.</td>
    <td>Can be found in the <strong>Manage authentication > Identity Providers</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.idp-config.update</code></td>
    <td>Update the identity provider configuration.</td>
    <td>Can be updated in the <strong>Manage authentication > Identity Providers</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.tokens-config.read</code></td>
    <td>View the token expiration configuration.</td>
    <td>Can be found in the <strong>Manage authentication > Authentication Settings</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.tokens-config.update</code></td>
    <td>Update the token expiration configuration.</td>
    <td>Can be found in the <strong>Manage authentication > Authentication Settings</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.redirect-uris.read</code></td>
    <td>View the current redirect URI configuration.</td>
    <td>Can be found in the <strong>Manage authentication > Authentication Settings</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.redirect-uris.update</code></td>
    <td>Update the redirect URIs configuration.</td>
    <td>Can be updated in the <strong>Manage authentication > Identity Providers</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.is-profiles-active.read</code></td>
    <td>View the user profile storage configuration.</td>
    <td>Can be found in the <strong>Profiles and roles > User Profiles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.is-profiles-active.update</code></td>
    <td>Update your user profile storage configuration.</td>
    <td>Can be found in the <strong>Profiles and roles > User Profiles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.users.read</code></td>
    <td>Search user profiles.</td>
    <td>Can be found in the <strong>Profiles and roles > User Profiles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.users.create</code></td>
    <td>Create pre-registered user profile.</td>
    <td>Can be found in the <strong>Profiles and roles > User Profiles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.users.get</code></td>
    <td>Export user profiles.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.refresh-token.revoke</code></td>
    <td>Revoke all the refresh tokens issued for the given user.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.users.import</code></td>
    <td>Import user profiles.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.user-profile.read</code></td>
    <td>View a user profile.</td>
    <td>Can be found in the <strong>Profiles and roles > User Profiles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.user-profile.update</code></td>
    <td>Update a user profile.</td>
    <td>Can be found in the <strong>Profiles and roles > User Profiles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.user-profile.bulkdelete</code></td>
    <td>Delete a list of user profiles.</td>
    <td>Can be found in the <strong>Profiles and roles > User Profiles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.user-roles.read</code></td>
    <td>View the user roles.</td>
    <td>Can be found in the <strong>Profiles and roles > User Profiles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.user-roles.update</code></td>
    <td>Update the user roles.</td>
    <td>Can be found in the <strong>Profiles and roles > User Profiles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.roles.read</code></td>
    <td>View the roles list.</td>
    <td>Can be found in the <strong>Profiles and roles > Roles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.roles.create</code></td>
    <td>Create a role.</td>
    <td>Can be found in the <strong>Profiles and roles > Roles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.role.read</code></td>
    <td>View the role.</td>
    <td>Can be found in the <strong>Profiles and roles > Roles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.role.update</code></td>
    <td>Update the role.</td>
    <td>Can be found in the <strong>Profiles and roles > Roles</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.applications.read</code></td>
    <td>View the applications list.</td>
    <td>Can be found in the <strong>Applications</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.applications.create</code></td>
    <td>Create an application.</td>
    <td>Can be found in the <strong>Applications</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.application.read</code></td>
    <td>View the application.</td>
    <td>Can be found in the <strong>Applications</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.application.update</code></td>
    <td>Update the application.</td>
    <td>Can be found in the <strong>Applications</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.application-scopes.read</code></td>
    <td>View the application scopes.</td>
    <td>Can be found in the <strong>Applications</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.application-scopes.update</code></td>
    <td>Update the application scopes.</td>
    <td>Can be found in the <strong>Applications</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.theme-text.read</code></td>
    <td>View the theme texts of the login widget.</td>
    <td>Can be found in the <strong>Login Customization</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.theme-text.update</code></td>
    <td>Update the theme texts of the login widget footnote.</td>
    <td>Can be updated in the <strong>Login Customization</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.theme-color.read</code></td>
    <td>View the theme color of the login widget header.</td>
    <td>Can be found in the <strong>Login Customization</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.theme-color.update</code></td>
    <td>Update the theme color of the login widget header.</td>
    <td>Can be Updated in the <strong>Login Customization</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.media.read</code></td>
    <td>View the image that is shown in the login widget.</td>
    <td>Can be found in the <strong>Login Customization</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.media.update</code></td>
    <td>Update the image that is shown in the login widget.</td>
    <td>Can be updated in the <strong>Login Customization</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.ui-configuration.read</code></td>
    <td>View the login widget UI configuration which includes header color and image.</td>
    <td>Can be found in the <strong>Login Customization</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.ui-languages.read</code></td>
    <td>View a list of supported languages.</td>
    <td>Must be viewed from the API.</td>
  </tr>
  <tr>
    <td><code>appid.ui-languages.update</code></td>
    <td>Update your supported languages.</td>
    <td>Must be updated through the API.</td>
  </tr>
  <tr>
    <td><code>appid.saml-metadata.read</code></td>
    <td>View the {{site.data.keyword.appid_short_notm}} SAML metadata.</td>
    <td>Can be found in the <strong>Identity Providers > SAML 2.0 Federation</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.cloud-directory-user.read</code></td>
    <td>View a Cloud Directory user.</td>
    <td>Can be found in the <strong>Cloud Directory > Users > View user details</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.cloud-directory-user.update</code></td>
    <td>Update a Cloud Directory User.</td>
    <td>Can be updated in the <strong>Users</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.cloud-directory-user.delete</code></td>
    <td>Delete a Cloud Directory user.</td>
    <td>Must be deleted through the API.</td>
  </tr>
  <tr>
    <td><code>appid.user.delete</code></td>
    <td>Delete a Cloud Directory user and profile.</td>
    <td>Must be deleted through the API.</td>
  </tr>
  <tr>
    <td><code>appid.cloud-directory-users.read</code></td>
    <td>View a list of your Cloud Directory users.</td>
    <td>Can be found in the <strong>Cloud Directory > Users</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.cloud-directory-user.update</code></td>
    <td>Update your list of Cloud Directory users.</td>
    <td>Can be updated in the <strong>Cloud Directory > Users</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.cloud-directory-user.delete</code></td>
    <td>Delete a list of Cloud Directory users.</td>
    <td>Must be deleted through the API.</td>
  </tr>
  <tr>
    <td><code>appid.users.bulkdelete</code></td>
    <td>Delete a list of Cloud Directory users and profiles.</td>
    <td>Must be deleted through the API.</td>
  </tr>
  <tr>
    <td><code>appid.cloud-directory-users.get</code></td>
    <td>Export Cloud Directory users.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.cloud-directory-users.import</code></td>
    <td>Import Cloud Directory users.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.cloud-directory-user-sso.set-off</code></td>
    <td>Invalidate all SSO sessions of the user.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.email-dispatcher.read</code></td>
    <td>View the email dispatcher configurations.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.email-dispatcher.update</code></td>
    <td>Update the email dispatcher configurations.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.email-dispatcher-test.send</code></td>
    <td>Test the email dispatcher.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.email-settings-test.send</code></td>
    <td>Test the email settings configurations.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.email-template.read</code></td>
    <td>View an email template.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.email-template.update</code></td>
    <td>Update an email template.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.email-template.delete</code></td>
    <td>Delete an email template to reset to the default.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.sender-details.read</code></td>
    <td>View the sender details.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.sender-details.update</code></td>
    <td>Update the sender details.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.resend-notification.send</code></td>
    <td>Resend user notifications.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.self-forgot-password.start</code></td>
    <td>Starts the forgot password process.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.forgot-password-result.read</code></td>
    <td>View the forgot password confirmation result.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.self-sign-up.start</code></td>
    <td>Starts the sign-up process.</td>
    <td>Can be found in the <strong>Cloud Directory > Settings</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.sign-up-result.read</code></td>
    <td>View the sign-up result confirmation.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.action_url.read</code></td>
    <td>View the custom URL that is called when an action is performed.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.action-url.update</code></td>
    <td>Update the custom URL that is called when an action is performed.</td>
    <td>Can be found in the <strong>Cloud Directory > Email Templates</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.password-regex.read</code></td>
    <td>View the password regex.</td>
    <td>Can be found in the <strong>Cloud Directory > Password Policies</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.password-regex.update</code></td>
    <td>Update the password regex.</td>
    <td>Can be found in the <strong>Cloud Directory > Password Policies</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.advanced-password-management.read</code></td>
    <td>View the advanced password policy configurations.</td>
    <td>Can be found in the <strong>Cloud Directory > Password Policies</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.advanced-password-management.update</code></td>
    <td>Update the advanced password policy configurations.</td>
    <td>Can be found in the <strong>Cloud Directory > Password Policies</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.user-password.update</code></td>
    <td>Set a new password for the Cloud Directory user.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.capture-runtime-activity.read</code></td>
    <td>View runtime activity toggle.</td>
    <td>Can be viewed in the <strong>Manage Authentication> Authentication Settings</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.capture-runtime-activity.update</code></td>
    <td>Toggle runtime activity monitoring.</td>
    <td>Can be updated in the <strong>Manage Authentication> Authentication Settings</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.mfa.read</code></td>
    <td>View your MFA configurations.</td>
    <td>Can be found in the <strong>Cloud Directory > Multi-factor Authentication</strong> tab.</td>
  </tr>
    <tr>
    <td><code>appid.mfa.update</code></td>
    <td>Update your MFA configurations.</td>
    <td>Can be found in the <strong>Cloud Directory > Multi-factor Authentication</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.mfa-channels.read</code></td>
    <td>View your MFA channels.</td>
    <td>Can be found in the <strong>Cloud Directory > Multi-factor Authentication</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.mfa-channel.read</code></td>
    <td>View your MFA channels configurations.</td>
    <td>Can be found in the <strong>Cloud Directory > Multi-factor Authentication</strong> tab.</td>
  </tr>
    <tr>
    <td><code>appid.mfa-channel.update</code></td>
    <td>Update your channels.</td>
    <td>Can be found in the <strong>Cloud Directory > Multi-factor Authentication</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.sms-dispatcher-test.send</code></td>
    <td>Test the SMS dispatcher configurations.</td>
    <td>Can be found in the <strong>Cloud Directory > Multi-factor Authentication > SMS Provider</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.mfa-extension-premfa.read</code></td>
    <td>View your pre-MFA extension configuration.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.mfa-extension-premfa.update</code></td>
    <td>Update your pre-MFA extension configuration.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.mfa-extension-postmfa.read</code></td>
    <td>View your post MFA extension configuration.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.mfa-extension-postmfa.update</code></td>
    <td>Update your post MFA extension configuration.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.sso.read</code></td>
    <td>View your SSO configuration.</td>
    <td>Can be found in the <strong>Identity Providers > Cloud Directory > Single Sign-On</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.sso.update</code></td>
    <td>Update your SSO configuration.</td>
    <td>Can be found in the <strong>Identity Providers > Cloud Directory > Single Sign-On</strong> tab.</td>
  </tr>
  <tr>
    <td><code>appid.rate-limit.read</code></td>
    <td>View your rate limit configurations.</td>
    <td>Must be done through the API.</td>
  </tr>
  <tr>
    <td><code>appid.rate-limit.update</code></td>
    <td>Update your rate limit configurations.</td>
    <td>Must be done through the API.</td>
  </tr>
</table>



## Viewing runtime events
{: #at-monitor-runtime}

With {{site.data.keyword.at_short}}, you can review runtime activity made by an app user, such as logins, password resets, and authentications.
{: shortdesc}

The reported events are per account, but there are limitations on the data rate and retention period of the collected runtime events. Increasing the limits might require an upgrade of the {{site.data.keyword.at_short}} service. For more information about the service limits, see the [{{site.data.keyword.at_short}} docs](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-service_plan).

This feature is available only for instances on graduated tier payment plan that were created after March 15, 2018. Using this feature incurs an extra charge. For more information on graduated tier pricing, see the [{{site.data.keyword.cloud_notm}} pricing docs](/docs/appid?topic=appid-faq#faq-pricing).
{: note}


### Monitoring runtime activity
{: #at-monitor-runtime-activity}

1. Log in to your {{site.data.keyword.cloud_notm}} account.
2. From the catalog, provision an instance of the {{site.data.keyword.at_short}} service in the same account as your {{site.data.keyword.appid_short_notm}} instance.
3. In the {{site.data.keyword.appid_short_notm}} dashboard, click **Manage authentication > Authentication settings**.
4. Scroll to the **Runtime Activity** panel and toggle the switch to enable tracking of runtime authentication activity. A message displays that notifies you that the feature is enabled and that you are charged differently. For more information, see [How does App ID calculate pricing](/docs/appid?topic=appid-faq#faq-pricing).
5. From the **Observability > Activity Tracker** tab in the console navigation, verify the information for the instance that you created.
6. Click **Open Dashboard**. When the dashboard loads, you see an overall view of all of the activity in your account. You can use the search operators to filter your results by tags, sources, apps or levels. You can also search for specific events or jump to a specific timeframe.
7. From the **All Apps** drop-down, select the instance of {{site.data.keyword.appid_short_notm}} that you want to track events for.


## List of runtime events
{: #at-runtime-events}

Check out the following table for a list of the runtime events that are sent to {{site.data.keyword.at_short}}.

Be sure that you have turn ON the **Runtime Activity** in order to see this events.
{: important}

<table>
  <caption>Table 2. Actions that can be tracked as authentication events at runtime</caption>
  <tr>
    <th>Description</th>
    <th>Action</th>
    <th>Outcome</th>
    <th><code>reason. reasonCode</code></th>
    <th><code>target.id</code></th>
    <th><code>target.name</code></th>
    <th><code>target.typeURI</code></th>
  </tr>
  <tr>
    <td>Cloud Directory authentication success</td>
    <td><code>appid.user.authenticate</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>[appid user CRN]</code></td>
    <td><code>cloud_directory:[GUID]</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>Cloud Directory authentication failure</td>
    <td><code>appid.user.authenticate</code></td>
    <td><code>failure</code></td>
    <td><code>401</code></td>
    <td><code>[appid user CRN]</code></td>
    <td><code>cloud_directory:[GUID]</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>Facebook authentication success</td>
    <td><code>appid.user.authenticate</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>[appid user CRN]</code></td>
    <td><code>facebook:[GUID]</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>Facebook authentication failure</td>
    <td><code>appid.user.authenticate</code></td>
    <td><code>failure</code></td>
    <td><code>401</code></td>
    <td><code>crn:unknown</code></td>
    <td><code>facebook:unknown</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>Google authentication success</td>
    <td><code>appid.user.authenticate</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>[appid user CRN]</code></td>
    <td><code>google:[GUID]</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>Google authentication failure</td>
    <td><code>appid.user.authenticate</code></td>
    <td><code>failure</code></td>
    <td><code>401</code></td>
    <td><code>crn:unknown</code></td>
    <td><code>google:unknown</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>SAML authentication success</td>
    <td><code>appid.user.authenticate</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>[appid user CRN]</code></td>
    <td><code>SAML:[GUID]</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>SAML authentication failure</td>
    <td><code>appid.user.authenticate</code></td>
    <td><code>failure</code></td>
    <td><code>401</code></td>
    <td><code>crn:unknown</code></td>
    <td><code>SAML:unknown</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>Client Credentials authentication success</td>
    <td><code>appid.application.authenticate</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>[appid application CRN]</code></td>
    <td><code>client_credentials:client_id</code></td>
    <td><code>appid/application</code></td>
  </tr>
  <tr>
    <td>Client Credentials authentication failure</td>
    <td><code>appid.application.authenticate</code></td>
    <td><code>failure</code></td>
    <td><code>401</code></td>
    <td><code>crn:undefined</code></td>
    <td><code>client_credentials:undefined</code></td>
    <td><code>appid/application</code></td>
  </tr>
  <tr>
    <td>Cloud Directory sign up</td>
    <td><code>appid.cloud-dir-user.create</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>[appid user CRN]</code></td>
    <td><code>cloud_directory:[GUID]</code></td>
    <td><code>appid/cloud_dir/user</code></td>
  </tr>
  <tr>
    <td>Cloud Directory signup failure</td>
    <td><code>appid.cloud-dir-user.create</code></td>
    <td><code>failure</code></td>
    <td><code>400</code></td>
    <td><code>crn:unknown</code></td>
    <td><code>cloud_directory:unknown</code></td>
    <td><code>appid/cloud_dir/user</code></td>
  </tr>
  <tr>
    <td>Cloud Directory signup confirmation</td>
    <td><code>appid.cloud-dir-user.allow</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>[appid user CRN]</code></td>
    <td><code>cloud_directory:[GUID]</code></td>
    <td><code>appid/cloud_dir/user</code></td>
  </tr>
  <tr>
    <td>Cloud Directory signup confirmation failure</td>
    <td><code>appid.cloud-dir-user.allow</code></td>
    <td><code>failure</code></td>
    <td><code>400</code></td>
    <td><code>crn:unknown</code></td>
    <td><code>cloud_directory:unknown</code></td>
    <td><code>appid/cloud_dir/user</code></td>
  </tr>
  <tr>
    <td>Cloud Directory reset or renew password</td>
    <td><code>appid.cloud-dir-user-credentials.renew</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>[appid user CRN]</code></td>
    <td><code>cloud_directory:[GUID]</code></td>
    <td><code>appid/cloud_dir/user</code></td>
  </tr>
  <tr>
    <td>Cloud Directory reset or renew password failure</td>
    <td><code>appid.cloud-dir-user-credentials.renew</code></td>
    <td><code>failure</code></td>
    <td><code>400</code></td>
    <td><code>crn:unknown</code></td>
    <td><code>cloud_directory:unknown</code></td>
    <td><code>appid/cloud_dir/user</code></td>
  </tr>
  <tr>
    <td>Cloud Directory change password</td>
    <td><code>appid.cloud-dir-user-credentials.update</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>[appid user CRN]</code></td>
    <td><code>cloud_directory:[GUID]</code></td>
    <td><code>appid/cloud_dir/user</code></td>
  </tr>
  <tr>
    <td>Cloud Directory change password failure</td>
    <td><code>appid.cloud-dir-user-credentials.update</code></td>
    <td><code>failure</code></td>
    <td><code>400</code></td>
    <td><code>crn:unknown</code></td>
    <td><code>cloud_directory:unknown</code></td>
    <td><code>appid/cloud_dir/user</code></td>
  </tr>
  <tr>
    <td>Revoke user tokens</td>
    <td><code>appid.user-tokens.revoke</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>appid user CRN</code></td>
    <td><code>idp:[GUID]</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>Revoke user tokens failure</td>
    <td><code>appid.user-tokens.revoke</code></td>
    <td><code>failure</code></td>
    <td><code>400</code></td>
    <td><code>appid user CRN</code></td>
    <td><code>idp:[GUID]</code></td>
    <td><code>appid/user</code></td>
  </tr>
  <tr>
    <td>Cloud Directory user SSO logout</td>
    <td><code>appid.cloud-dir-user.set-off</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>appid user CRN</code></td>
    <td><code>idp:[GUID]</code></td>
    <td><code>appid/user</code></td>
  </tr>
    <tr>
    <td>View user profile attributes</td>
    <td><code>appid.user-profile-attributes.read</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>crn:profiles:[User-ID]</code></td>
    <td><code>profiles:[User-ID]</code></td>
    <td><code>appid-user-profiles/attributes</code></td>
  </tr>
    <tr>
    <td>Update user profile attribute</td>
    <td><code>appid.user-profile-attributes.update</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>crn:profiles:[User-ID]</code></td>
    <td><code>profiles:[User-ID]</code></td>
    <td><code>appid-user-profiles/attribute/[Attribute-name]</code></td>
  </tr>
    <tr>
    <td>Delete user profile attribute</td>
    <td><code>appid.user-profile-attributes.delete</code></td>
    <td><code>success</code></td>
    <td><code>200</code></td>
    <td><code>crn:profiles:[User-ID]</code></td>
    <td><code>profiles:[User-ID]</code></td>
    <td><code>appid-user-profiles/attribute/[Attribute-name]</code></td>
  </tr>
</table>

## Analyzing runtime events
{: #at-runtime-analyze}

A user that generates a runtime event is identified as a GUID rather than by name or email. As the account owner, you can use the GUID to identify a specific user and then you can search to see all of the events that the user has triggered.
{: shortdesc}


The following scenario works only for Cloud Directory users. If the user is defined by an external IdP such as Google or Facebook, only that identity provider can interpret the GUID.
{: note}


### Extracting user information from the GUID
{: #at-extract-information}

An event in the {{site.data.keyword.at_short}} console contains the following fields.

<table>
  <caption>Table 3. Example fields that can be found in an event from the {{site.data.keyword.at_short}} console</caption>
  <tr>
    <th>Field</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>initiator.id</td>
    <td>cb967e0d-43c1-454a-968d-0efa24766846</td>
    <td>The tenant ID.</td>
  </tr>
  <tr>
    <td>target.name</td>
    <td>cloud_directory:34e1ea6d-cc02-4941-9462-7e9c5a40b360</td>
    <td>The user ID.</td>
  </tr>
</table>

</br>

To find the user information that aligns with the event GUID, use the following steps.

1. In the **Credentials** tab of the {{site.data.keyword.appid_short_notm}} dashboard, copy and save the information in the `apiKey` and `tenantID` fields. The tenant ID should match the ID of the event. If no credentials exist, create a set.

2. Obtain an IAM token for the `apiKey` by inserting the key into the following command:

  ```
  curl -k -X POST \
      --header "Content-Type: application/x-www-form-urlencoded" \
      --header "Accept: application/json" \
      --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
      --data-urlencode "apikey=THE_API_KEY" \
      "https://iam.cloud.ibm.com/identity/token"
  ```
  {: codeblock}

3. Copy the IAM token from the **access_token** field in the response.

4. Select a region. Region options include: `au-syd`, `eu-de`, `eu-gb`, `jp-tok`, and `us-south`.

5. Insert the IAM token, the tenant ID, and the user ID, into the following command to obtain the user information.

  ```
  curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <IAM_TOKEN>' \
  'https://REGION.appid.cloud.ibm.com/TENANT_ID/cloud_directory/Users/THE_USER_ID'
  ```
  {: codeblock}

  You can also run this command by using the [management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/getAuditStatus){: external}. Your output would look similar to the following:

  ```
    {
    "displayName": "test test",
    "active": true,
    "userName": "test0001",
    "mfaContext": {},
    "emails": [
      {
        "value": "mytest@yahoo.com",
        "primary": true
      }
    ],
    "meta": {
      "lastLogin": "2018-12-10T16:05:36.665Z",
      "created": "2018-08-21T08:55:50.643Z",
      "location": "/v1/cb967e0d-43c1-454a-968d-0efa24766846/Users/34e1ea6d-cc02-4941-9462-7e9c5a40b360",
      "lastModified": "2018-12-10T16:05:36.675Z",
      "resourceType": "User"
    },
    "schemas": [
      "urn:ietf:params:scim:schemas:core:2.0:User"
    ],
    "name": {
      "givenName": "test",
      "familyName": "test",
      "formatted": "test test"
    },
    "id": "34e1ea6d-cc02-4941-9462-7e9c5a40b360"
  }
  ```
  {: screen}





### Finding user related events
{: #at-finding-user-events}

You can track the events of specific Cloud Directory users in {{site.data.keyword.at_short}} by using their email. Before you can begin tracking, the email must be mapped to a Cloud Directory GUID.


1. Obtain an IAM token, a tenant ID and a region as described in the previous section.
2. Insert the IAM token, the tenant ID, and the email into the following command to obtain the user information.

  ```
  curl -X GET --header 'Accept: application/json' --header 'Authorization: Bearer <IAM_TOKEN>' 'https://REGION.appid.cloud.ibm.com/TENANT_ID/users?email=EMAIL_ADDRESS'
  ```
  {: codeblock}

  The email address should be escaped. For example `myTest%40yahoo.com` instead of `myTest@yahoo.com`.
  {: note}

  Alternatively, you can use the [Management APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/getAuditStatus){: external}. Your output would look similar to the following:

  ```
  {
    "users": [
      {
        "idp": "cloud_directory",
        "id": "1e123399-3499-4a5c-b5a9-93843a91dc80"
      },
      {
        "idp": "cloud_directory",
        "id": "2a7abbe5-0fce-402e-9ddf-265246b415c8"
      }
    ]
  }
  ```
  {: screen}

3. Search for a **cloud_directory:id** value in the **target.name_str** field in the {{site.data.keyword.at_short}} console.
