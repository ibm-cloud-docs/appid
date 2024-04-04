---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-04"

keywords: user access, control access, permissions, roles, scopes, runtime, access token, authentication, identity, app security

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
{:terraform: .ph data-hd-interface='terraform'}
{:release-note: data-hd-content-type='release-note'}


# Controlling access
{: #access-control}

With {{site.data.keyword.appid_full}}, you can define which users and applications can access specific features or perform specific actions in your apps. To control access, you can create scopes and group them into a role. Then, assign the role to one or more of your app users and applications.
{: shortdesc}

A scope is a runtime action in your application that you register with {{site.data.keyword.appid_short_notm}} to create an access permission. A role is a collection of scopes that assigns varying permissions to different types of app users and applications. For example, if your company employs developers, they might create a role that allows them to read and write to the code. If you employ auditors, you might have a view only role as shown in the following image.

![{{site.data.keyword.appid_short_notm}} access control](images/access-control.png){: caption="Figure 1. How {{site.data.keyword.appid_short_notm}} access control works" caption-side="bottom"}

1. Register runtime actions that can occur in your application with {{site.data.keyword.appid_short_notm}}.
2. Compile scopes into groups to form roles.
3. Control access permissions by assigning roles to your users or applications.
4. Configure your application to verify the scopes that are returned in your users access token at run time (or in your applications token if client credentials flow).

For more information about applications, see [Application identity and authorization](/docs/appid?topic=appid-app).

## Before you begin
{: #before-access}

* You must have an application.
* Make sure you have an understanding of how each type of role and scope can impact your application. Because you're granting access, you want to be sure that you're granting it to only the people that need it. 
* Be aware of the [limits](/docs/appid?topic=appid-known-issues-limits) that are in place. 



## Creating scopes with the UI
{: #create-scopes-gui}
{: ui}

A scope is a runtime action in your application that can be taken by users who are granted the required permissions to complete them. Scopes are created when you register your application with {{site.data.keyword.appid_short_notm}}. If your app is already registered, you can edit it to include scopes. 

The values of scope names must meet the following requirements:

* Be alphanumeric
* Be lowercase
* Not start with `appid` or `openid`
* Not contain special characters other than periods (`.`) or underscores (`_`)
* Be fewer than 50 characters.

To create a scope, you can use the {{site.data.keyword.appid_short_notm}} UI.

1. Go to **Applications** in the {{site.data.keyword.appid_short_notm}} dashboard.
2. Click **Add application** to open the configuration screen. If you already have credentials that you want to use, click **Edit** from the Actions menu in the row that you want to update.
3. Give your app a name, and select the type of application that you have.
4. Enter a value for your custom scope, and click the plus symbol (**+**). An example scope value might be `read` or `write`.
5. Repeat the previous step until you add all your scopes to the app.
6. Click **Save**.

## Creating scopes with the API
{: #create-scopes-api}
{: api}

A scope is a runtime action in your application that can be taken by users who are granted the required permissions to complete them. Scopes are created when you register your application with {{site.data.keyword.appid_short_notm}}. If your app is already registered, you can edit it to include scopes. 

The values of scope names must meet the following requirements:

* Be alphanumeric
* Be lowercase
* Not start with `appid` or `openid`
* Not contain special characters other than periods (`.`) or underscores (`_`)
* Be fewer than 50 characters.

To create a scope, you can use the {{site.data.keyword.appid_short_notm}} UI.

1. Create the scopes by making the following request to the `/scopes` endpoint.

   ```sh
   curl -X PUT "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/applications/<clientID>/scopes" 
   -H "accept: application/json" 
   -H "Content-Type: application/json" 
   -d "{\ "scopes":\ [\ <scopesObject>}" ]}"
   ```
   {: codeblock}

   | Variable | Description |
   | -------- | ----------- |
   | `region` | The region in which your instance of {{site.data.keyword.appid_short_notm}} is provisioned. Learn more about the [available regions](/docs/appid?topic=appid-regions-endpoints). |
   | `tenantID` | The unique identifier for your instance of {{site.data.keyword.appid_short_notm}}. You can find this value in the credentials for your app as they're listed in the **Applications** tab of the service dashboard. |
   | `clientID` | The unique identifier for your application. You can find this value in the credentials for your app as they're listed in your **Applications** in the service dashboard. |
   | `scopesObject` | A JSON object of all the scopes that you want to create for your application. |
   {: caption="Table 1. Required variables to call the `/scopes` endpoint" caption-side="top"}


2. Optional: Confirm that the scopes were created.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/applications/<clientID>/scopes" 
   -H "accept: application/json" 
   -H "Content-Type: application/json"
   ```
   {: codeblock}


## Creating roles with the UI
{: #create-roles-gui}
{: ui}

A role is a group of scopes that apply to the same type of user. For example, if you create an admin role, the scopes section might allow for that role to perform read, write, or create actions. But, if you create another role that is called `viewer`, the users who are assigned that role have read only access. To create a role, you can use the {{site.data.keyword.appid_short_notm}} UI.


1. Go to **Profiles and roles > Roles** in the {{site.data.keyword.appid_short_notm}} dashboard. 
2. Click **Create role** to open the configuration screen.
3. Give the role a name and description.
4. By using the scopes that you created in the previous section, assign the scopes to a role by using the following format. Click the **+** to add the scope.

   ```sh
   <appName>/<scope>
   ```
   {: screen}

   If you have only one application, you do not need to specify your app name. You can add the scope by itself.
   {: tip}

5. Repeat the previous step to add more scopes.
6. Click **Save**.


## Creating roles with the API
{: #create-roles-api}
{: api}

A role is a group of scopes that apply to the same type of user. For example, if you create an admin role, the scopes section might allow for that role to perform read, write, or create actions. But, if you create another role that is called `viewer`, the users who are assigned that role would have read only access. To create a role, you can use the {{site.data.keyword.appid_short_notm}} APIs.

1. Make a request to the `/roles` endpoint to create the role.

   ```sh
   curl -X POST "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/roles" 
   -H "accept: application/json" 
   -H "Content-Type: application/json" 
   -d { \"name\": \"<roleName>\", \"description\": \"<roleDescription>\", \"access\": [ { \"application_id\": \"<applicationID>\", \"scopes\": [ \"<scopes>" ] } ]}"
   ```
   {: codeblock}

   | Variable | Description |
   | -------- | ----------- |
   | `region` | The region in which your instance of {{site.data.keyword.appid_short_notm}} is provisioned. Learn more about the [available regions](/docs/appid?topic=appid-regions-endpoints). |
   | `tenantID` | The unique identifier for your instance of {{site.data.keyword.appid_short_notm}}. You can find this value in the credentials for your app as they're listed in the **Applications** tab of the service dashboard. |
   | `clientID` | The unique identifier for your application. You can find this value in the credentials for your app as they're listed in **Applications**. |
   | `roleName` | The name that you want to assign to your role. |
   | `roleDescription` | A short phrase that describes what your role is meant to do. | 
   | `applicationID` | The unique identifier for your application. You can find this value in the credentials for your app as they're listed in **Applications**. |
   | `scopes` | A JSON object of all the scopes that you want to apply to a role.|
   {: caption="Table 2. Required variables to call the `/scopes` endpoint" caption-side="top"}
 
2. Optional: Confirm that the roles were created.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/roles -H "accept: application/json"
   ```
   {: codeblock}

   The response looks similar to the following example:

   ```json
   {
      "roles": [
      {
         "id": "12345678-1234-1234-1234-123456789012",
         "name": "admin",
         "description": "Can perform administrative tasks.",
         "access": [
            {
            "application_id": "de33d272-f8a7-4406-8fe8-ab28fd457be5",
            "scopes": [
               "create",
               "update",
               "write",
               "read"
            ]
            }
         ]
      }
      {
         "id": "123454231-1234-1234-3334-12345687012",
         "name": "developer",
         "description": "Can perform administrative tasks.",
         "access": [
            {
            "application_id": "de33d272-f8a7-4406-8fe8-ab28fd457be5",
            "scopes": [
               "write",
               "read"
            ]
            }
         ]
      }
      ]
   }
   ```
   {: screen}



## Assigning roles to users with the UI
{: #assign-roles-gui}
{: ui}

After you create roles, you can assign them to your user's profile. You can also assign roles when you create a future user.

1. Go to **Profiles and roles > User profiles** in your {{site.data.keyword.appid_short_notm}} dashboard.
2. From the Actions menu in the row of the specific user you're assigning a role to, click **Assign role**.
3. Select the role or roles that you want to add from the list of available roles.
4. Optional: If you don't see the role that you're looking for, click **Create role** and provide the information to add another option.
5. Click **Save**.



## Assigning roles to users with the API
{: #assign-roles-api}
{: api}

After you create roles, you can assign them to your user's profile. You can also assign roles when you create a future user.

1. Get your user ID by searching your {{site.data.keyword.appid_short_notm}} users with an identifying query, such as an email address.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/Users?query=<identifyingSearchQuery>" \
   -H "accept: application/json" \
   -H "authorization: Bearer <token>"
   ```
   {: codeblock}

   Example:

   ```sh
   curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@domain.com 
   -H "accept: application/json" 
   -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
   ```
   {: screen}

2. Optional: Get the role ID or role name. If you already know your role ID or name, skip to the next step.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/roles" \
   -H "accept: application/json" \
   -H "authorization: Bearer <token>"
   ```
   {: codeblock}

3. Make a request to the `/roles` endpoint that contains a JSON object of the roles that you want to assign.

   ```sh
   curl -X PUT "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/users/<userID>/roles" 
   -H "accept: application/json" 
   -H "Content-Type: application/json" 
   -d "{ \"roles\": { \"ids\": [ \"<roleIDs>\" ] }}" 
   -H "authorization: Bearer <token>"
   ```
   {: codeblock}

To remove a role from a user, make the PUT request again, but remove the role ID.
{: tip}


## Adding user roles to tokens
{: #role-tokens}

By default, roles are not returned in a users token. It is recommended that your runtime decisions are configured based on scopes. But, if you would like to use roles, you can map them to your tokens by using [custom claims mapping](/docs/appid?topic=appid-customizing-tokens).


When you authenticate, be sure that you use `username : client ID` and `password : secret` for the application and user that you configured controls for.
{: tip} 


## Assigning roles to an application
{: #assign-roles-app}

After you create roles, you can assign them to your applications by using the {{site.data.keyword.appid_short_notm}} APIs.

Application roles are only valid in the client credentials flow.
{: note}

1. Get your application client ID by querying the list of applications. You can also get this value from the **Applications** tab of the {{site.data.keyword.appid_short_notm}} UI.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/applications" \
   -H "accept: application/json" \
   -H "authorization: Bearer <token>"
   ```
   {: codeblock}

   Example:

   ```sh
   curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/applications 
   -H "accept: application/json" 
   -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
   ```
   {: screen}

2. Get the role ID.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/roles" \
   -H "accept: application/json" \
   -H "authorization: Bearer <token>"
   ```
   {: codeblock}

3. Make a request to the `/roles` endpoint that contains a JSON object of the roles that you want to assign. This request replaces current roles with the provided role IDs. Be sure that you're assigning the correct roles.

   ```sh
   curl -X PUT "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/applications/<clientID>/roles" 
   -H "accept: application/json" 
   -H "Content-Type: application/json" 
   -d "{ \"roles\": { \"ids\": [ \"<roleIDs>\" ] }}" 
   -H "authorization: Bearer <token>"
   ```
   {: codeblock}

To remove a role from a user, make the PUT request again, but remove the role ID.
{: tip}



## Controlling access at run time
{: #control-acesss-runtime}

When a user or application attempts to access one of your protected resources, tokens are created and returned by {{site.data.keyword.appid_short_notm}}. Any scopes that a user or application is assigned are returned in the access token. You can use the access token to make decisions at run time. Depending on the strategy that you're using to protect your applications, how you verify that scopes can differ.


### When using web app strategy
{: #access-webapp-strategy}

You can use [web app strategy](/docs/appid?topic=appid-key-concepts#term-web-strategy) to check whether a request contains any scopes by using the `hasScope` method. When a user with an assigned role signs in, they are granted access by an {{site.data.keyword.appid_short_notm}} token that contains all the scopes that are defined in the role. For example, if you're working with the Node.js SDK, your code snippet would look similar to the following:
 
```javascript
app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res){
    if(WebAppStrategy.hasScope(req, "read write")){
              res.json(req.user);
    }
    else {
        res.send("insufficient scopes");
    }
});
```
{: codeblock}



### When using API strategy
{: #access-api-strategy}

You can define the scopes that are required to access a specific endpoint by adding a scope variable to your [API strategy](/docs/appid?topic=appid-key-concepts#term-api-strategy) code. For instance, if you have an application that is written in Node.js and you're working with the Node.js SDK, your code snippet might look similar to the following.

```javascript
app.get("/api/protected",
        passport.authenticate(APIStrategy.STRATEGY_NAME, {
                audience: "myApp",
                scope: "read write update"
        }),
        function(req, res) {
                res.send("Hello from protected resource");
        }
);
```
{: codeblock}

| Variable | Description |
|-----|----|
| `scope` | The required scopes, which are separated by a space. |
| `audience` | The application client ID. |
{: caption="Table 3. Understanding the variables used with API strategy" caption-side="top"}


## Removing access
{: #remove-access}

You can delete any scope or role that's no longer needed. 


### Deleting scopes with the UI
{: #delete-scope-gui}
{: ui}

If you no longer need a scope, you can delete it by using the {{site.data.keyword.appid_short_notm}} UI.

When you delete a scope, it is removed from all the roles that it is associated with.
{: important}

You can use the {{site.data.keyword.appid_short_notm}} service dashboard to delete scopes. 

1. Go to **Applications** in the {{site.data.keyword.appid_short_notm}} dashboard.
2. From the Actions menu in the row of the application that you want to edit the scopes for, click **Edit**.
3. Click the **X** in the box for the scope that you want to remove.
4. Click **Save**.



### Deleting scopes with the API
{: #delete-scope-api}
{: api}

If you no longer need a scope, you can delete it by using the {{site.data.keyword.appid_short_notm}} API. To delete a scope, remove it from your JSON object and make a new PUT request to the `/scopes` endpoint.

When you delete a scope, it is removed from all the roles that it is associated with.
{: important}


1. Change or delete a scope by the following request to the `/scopes` endpoint. Be sure to update your scopes JSON object to contain only the scopes that you want to allow.

   ```sh
   curl -X PUT "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/applications/<clientID>/scopes" 
   -H "accept: application/json" 
   -H "Content-Type: application/json" 
   -d "{\ "scopes":\ [\ <scopesObject>" ]}"
   ```
   {: codeblock}



### Deleting roles with the UI
{: #delete-role-gui}
{: ui}

If you no longer need a specific role, you can delete it by using the {{site.data.keyword.appid_short_notm}} UI. 

Deleting a role removes access from all the users and applications that are currently using the role.
{: note}

1. Go to **Profiles and roles > Roles** in the service dashboard.
2. In the row for the role that you want to delete, select **Delete** from the Actions menu.
3. Confirm you understand that deleting the role affects all users and applications that are currently using the role.
4. Click **Delete**.

### Deleting roles with the API
{: #delete-role-api}
{: api}


If you no longer need a specific role, you can delete it by using the {{site.data.keyword.appid_short_notm}} APIs. 

Deleting a role removes access from all the users and applications that are currently using the role.
{: note}


1. Get the role ID or role name. If you already know your role ID or name, skip to the next step.

   ```sh
   curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/roles" 
   -H "accept: application/json"
   ```
   {: codeblock}

2. Make a request to the `/roles` endpoint that contains a JSON object of the roles that you want to assign.

   ```sh
   curl -X DELETE "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/roles/<roleID>" 
   -H "accept: application/json"
   ```
   {: codeblock}




