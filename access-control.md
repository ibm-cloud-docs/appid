---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-21"

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



# Controlling access
{: #access-control}


With {{site.data.keyword.appid_full}}, you can define which users can access specific features or perform specific actions in your apps. To control access, you can create scopes and group them into a role. Then, assign the role to one or more of your app users.
{: shortdesc}

A scope is a runtime action in your application that you register with {{site.data.keyword.appid_short_notm}} to create an access permission. A role is a collection of scopes that assigns varying permissions to different types of app users. For example, if your company employs developers, they might create a role that allows them to read and write to the code. If you employ auditors, you might have a view only role as shown in the following image.

![{{site.data.keyword.appid_short_notm}} access control](images/access-control.png){: caption="Figure 1. How {{site.data.keyword.appid_short_notm}} access control works" caption-side="bottom"}

1. Register runtime actions that can occur in your application with {{site.data.keyword.appid_short_notm}}.
2. Compile scopes into groups to form roles.
3. Control access permissions by assigning roles to your users.
4. Configure your application to verify the scopes that are returned in your users access token at runtime.

For more information about applications, see [Application identity and authorization](/docs/appid?topic=appid-app).

## Before you begin
{: #before-access}

* You must have an application.
* Make sure you have an understanding of the way in which each type of role and scope can impact your application. Because you're granting access, you want to be sure that you're granting it to only the people that need it. 
* Be aware of the [limits](/docs/appid?topic=appid-limits) that are in place. 


## Creating scopes
{: #create-scopes}

A scope is a runtime action in your application that can be taken by users who are granted the required permissions to complete them. Scopes are created when you register your application with {{site.data.keyword.appid_short_notm}}. If your app is already registered, you can edit it to include scopes. 

The values of scope names must meet the following requirements:

* Be alphanumeric
* Be lowercase
* Not start with `appid` or `openid`
* Not contain special characters other than periods (`.`) or underscores (`_`)
* Be fewer than 50 characters.

### Creating scopes in the UI
{: #create-scopes-gui}

You can use the {{site.data.keyword.appid_short_notm}} service dashboard to create scopes. 

1. Go to **Applications** in the {{site.data.keyword.appid_short_notm}} dashboard.
2. Click **Add application** to open the configuration screen. If you already have credentials that you want to use, click **Edit** from the Actions menu in the row that you want to update.
3. Give your app a name, and select the type of application that you have.
4. Enter a value for your custom scope, and click the plus symbol (**+**). An example scope value might be `read` or `write`.
5. Repeat the previous step until you add all of your scopes to the app.
6. Click **Save**.

### Creating scopes by using the API
{: #create-scopes-api}

You can use the {{site.data.keyword.appid_short_notm}} APIs to create scopes.

1. Create the scopes by making the following request to the `/scopes` endpoint.

  ```sh
  curl -X PUT "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/applications/<client_ID>/scopes" -H "accept: application/json" -H "Content-Type: application/json" -d "{\ "scopes":\ [\ <scopes_object>" ]}"
  ```
  {: codeblock}

  <table>
    <caption>Table 2. Required variables to call the /scopes endpoint</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>region</code></td>
      <td>The region in which your instance of {{site.data.keyword.appid_short_notm}} is provisioned. Options include <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code>, and <code>us-south</code>.</td>
    </tr>
    <tr>
      <td><code>tenant_ID</code></td>
      <td>The unique identifier for your instance of {{site.data.keyword.appid_short_notm}}. You can find this value in the credentials for your app as they're listed in the <b>Applications</b> tab of the service dashboard.</td>
    </tr>
    <tr>
      <td><code>client_ID</code></td>
      <td>The unique identifier for your application. You can find this value in the credentials for your app as they're listed in your <b>Applications</b> in the service dashboard.</td>
    </tr>
    <tr>
      <td><code>scopes_object</code></td>
      <td>A JSON object of all of the scopes that you want to create for your application. For example, </br> <pre class="screen"><code class="hljs">
        {
          "scopes": [
            "read",
            "write",
            "delete"
          ]
        }
      </code></pre></td>
    </tr>
  </table>

2. Optional: Confirm that the scopes were created.

  ```sh
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/applications/<client_ID>/scopes" -H "accept: application/json" -H "Content-Type: application/json"
  ```
  {: codeblock}


## Creating roles
{: #create-roles}

A role is a group of scopes that apply to the same type of user. For example, if you create an admin role, the scopes section might allow for that role to perform read, write, or create actions. But, if you were to create another role called `viewer`, those assigned that role would have read only access.

### Creating roles in the UI
{: #create-roles-gui}

You can use the {{site.data.keyword.appid_short_notm}} service dashboard to create roles.

1. Go to **Profiles and roles > Roles** in the {{site.data.keyword.appid_short_notm}} dashboard. 
2. Click **Create role** to open the configuration screen.
3. Give the role a name and description.
4. By using the scopes that you created in the previous section, assign the scopes to a role by using the following format. Click the **+** to add the scope.

  ```
  <app_name>/<scope>
  ```
  {: screen}

  If you have only one application, you do not need to specify your app name. You can add the scope by itself.
  {: tip}

5. Repeat the previous step to add more scopes.
6. Click **Save**.


### Creating roles by using the API
{: #create-roles-api}

You can use the {{site.data.keyword.appid_short_notm}} APIs to create roles.

1. Make a request to the /roles endpoint to create the role.

  ```sh
  curl -X POST "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/roles" -H "accept: application/json" -H "Content-Type: application/json" -d { \"name\": \"<role_name>\", \"description\": \"<role_description>\", \"access\": [ { \"application_id\": \"<application_ID>\", \"scopes\": [ \"<scopes>" ] } ]}"
  ```
  {: codeblock}

  <table>
    <caption>Table 1. Required variables to call the <code>/scopes</code> endpoint</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>region</code></td>
      <td>The region in which your instance of {{site.data.keyword.appid_short_notm}} is provisioned. Options include <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code>, and <code>us-south</code>.</td>
    </tr>
    <tr>
      <td><code>tenant_ID</code></td>
      <td>The unique identifier for your instance of {{site.data.keyword.appid_short_notm}}. You can find this value in the credentials for your app as they're listed in the <b>Applications</b> tab of the service dashboard.</td>
    </tr>
    <tr>
      <td><code>client_ID</code></td>
      <td>The unique identifier for your application. You can find this value in the credentials for your app as they're listed in <b>Applications</b>.</td>
    </tr>
    <tr>
      <td><code>role_name</code></td>
      <td>The name that you want to assign to your role.</td>
    </tr>
    <tr>
      <td><code>role_description</code></td>
      <td>A short phrase that describes what your role is meant to do. </td>
    </tr>
    <tr>
      <td><code>application_ID</code></td>
      <td>The unique identifier for your application. You can find this value in the credentials for your app as they're listed in <b>Applications</b></td>
    </tr>
    <tr>
      <td><code>scopes</code></td>
      <td>A JSON object of all of the scopes that you want to apply to a role. For example, </br> <pre class="screen"><code class="hljs">
        {
          "scopes": [
            "create",
            "update",
            "read"
          ]
        }
      </code></pre></td>
    </tr>
  </table>

2. Optional: Confirm that the roles were created.

  ```sh
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/roles -H "accept: application/json"
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
              "read"
            ]
          }
        ]
      }
      {
        "id": "12345678-1234-1234-1234-123456789012",
        "name": "developer",
        "description": "Can perform day to day coding tasks.",
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


## Assigning roles to a user
{: #assign-roles}

After you create roles, you can assign them to your user's profile. You can also assign roles when you create a future user.


### Assigning roles in the UI
{: #assign-roles-gui}

1. Go to **Profiles and roles > User profiles** in your {{site.data.keyword.appid_short_notm}} dashboard.
2. From the Actions menu in the row of the specific user you're assigning a role to, click **Assign role**.
3. Select the role or roles that you want to add from the list of available roles.
4. Optional: If you don't see the role that you're looking for, click **Create role** and provide the information to add another option.
5. Click **Save**.



### Assigning roles by using the API
{: #assign-roles-api}

You can assign a role to a user with the API.

1. Get your user ID by searching your {{site.data.keyword.appid_short_notm}} users with an identifying query, such as an email address.

  ```sh
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/Users?query=<identifying-search-query>" \
  -H "accept: application/json" \
  -H "authorization: Bearer <token>"
  ```
  {: codeblock}

  Example:

  ```sh
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@domain.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

2. Optional: Get the role ID or role name. If you already know your role ID or name, skip to the next step.

  ```sh
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/roles" -H "accept: application/json"
  ```
  {: codeblock}

3. Make a request to the `/roles` endpoint that contains a JSON object of the roles that you want to assign.

  ```sh
  curl -X PUT "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/users/<user_ID>/roles" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"roles\": { \"ids\": [ \"<role_IDs>\" ] }}"
  ```
  {: codeblock}

To remove a role from a user, make the PUT request again, but remove the role ID.
{: tip}



## Controlling access at runtime
{: #control-acesss-runtime}

When a user attempts to access one of your protected resources, tokens are created and returned by {{site.data.keyword.appid_short_notm}}. Any scopes that a user is assigned are retuned in the access token. You can use the access token to make decisions at runtime. Depending on the strategy that you're using to protect your applications, how you verify scopes can differ.


### When using web app strategy
{: #access-webapp-strategy}

You can use [web app strategy](/docs/appid?topic=appid-key-concepts#term-web-strategy) to check whether a request contains any scopes by using the `hasScope` method. When a user with an assigned role signs in, they are granted access by an {{site.data.keyword.appid_short_notm}} token that contains all of the scopes that are defined in the role. For example, if you're working with the Node.js SDK, your code snippet would look similar to the following:
 
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

<table>
    <caption>Table 3. Understanding the variables used with API strategy</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>scope</code></td>
      <td>The required scopes, which are separated by a space.</td>
    </tr>
    <tr>
      <td><code>audience</code></td>
      <td>The application client ID.</td>
    </tr>
  </table>


## Removing access
{: #remove-access}

You can delete any scope or role that's no longer needed. 

### Deleting scopes
{: #delete-scope}

If you no longer need a scope, you can delete it.

When you delete a scope, it is removed from all of the roles that it is associated with.
{: important}


#### Deleting scopes in the UI
{: #delete-scope-gui}

You can use the {{site.data.keyword.appid_short_notm}} service dashboard to delete scopes. 

1. Go to **Applications** in the {{site.data.keyword.appid_short_notm}} dashboard.
2. From the Actions menu in the row of the application that you want to edit the scopes for, click **Edit**.
3. Click the **X** in the box for the scope that you want to remove.
4. Click **Save**.



#### Deleting scopes by using the API
{: #delete-scope-api}

You can delete a scope by removing it from your JSON object and making a new PUT request to the `/scopes` endpoint.

1. Change or delete a scope by the following request to the `/scopes` endpoint. Be sure to update your scopes JSON object to contain only the scopes that you want to allow.

  ```sh
  curl -X PUT "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/applications/<client_ID>/scopes" -H "accept: application/json" -H "Content-Type: application/json" -d "{\ "scopes":\ [\ <scopes_object>" ]}"
  ```
  {: codeblock}



### Deleting roles
{: #deleting-roles}

If you no longer have a need for a specific role, you can delete it. 

Be aware that deleting a role removes access from all of the users and applications that are currently using the role.
{: note}

#### Deleting roles in the UI
{: #delete-role-gui}

You can delete roles by using the App ID dashboard.

1. Go to **Profiles and roles > Roles** in the service dashboard.
2. In the row for the role that you want to delete, select **Delete** from the Actions menu.
3. Confirm you understand that deleting the role affects all users and applications that are currently using the role.
4. Click **Delete**.

#### Deleting roles by using the API
{: #delete-role-API}

You can delete roles by using the APIs.

1. Get the role ID or role name. If you already know your role ID or name, skip to the next step.

  ```sh
  curl -X GET "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/roles" -H "accept: application/json"
  ```
  {: codeblock}

2. Make a request to the `/roles` endpoint that contains a JSON object of the roles that you want to assign.

  ```sh
  curl -X DELETE "https://<region>.appid.cloud.ibm.com/management/v4/<tenant_ID>/roles/<role_ID>" -H "accept: application/json"
  ```
  {: codeblock}



## Adding user roles to tokens
{: #role-tokens}

By default, roles are not returned in a users token. It is recommended that your runtime decisions are configured based on scopes. But, if you would like to use roles, you can map them to your tokens by using [custom claims mapping](/docs/appid?topic=appid-customizing-tokens).

