---
copyright:
  years: 2018
lastupdated: "2018-07-26"
---
{:new_window: target="____blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

## User Profile Preregistration
{: #overview}

{{site.data.keyword.appid_full}} allows you to associate attributes with a user that has not yet signed in to your application through the process of user preregistration.

This workflow is useful in scenarios where you as the developer already know your user base and would like to set certain default attributes on them. In most cases, you may not want a user to modify these default attributes in which case it is important to turn off user profiles. See [Security Considerations] for more details on the best practices for user preregistration.

To preregister custom attributes for a specific user using {{site.data.keyword.appid_short_notm}}'s [/users Management API endpoint](link to endpoint or swagger), the developer must know two pieces of information:

1. The identity provider the user will use to authenticate to the app.

2. The Identity Provider (IdP) provided unique identifier of the user to preregister.

{{site.data.keyword.appid_short_notm}} allows you to identify a user in multiple ways depending on your identity provider. See [Identifying Users using their IdP-Identity](#supported-ipds) for information on the supported Ids.

When they sign in to the application for the first time, {{site.data.keyword.appid_short_notm}} will search its database of preregistered users. If found, the user will inherit the preregistered {{site.data.keyword.appid_short_notm}} identity and, with it, all of the custom attributes that were set in the process.

### Security Considerations

Each {{site.data.keyword.appid_short_notm}} user profile contains two types of user information that can be retrieved by the `/profile` endpoint.

1. The IdP profile claims that are directly obtained from the IdP and cannot be modified by the developer or the application

2. Custom attributes that are explicitly set by the developer or the application using a valid access token

During preregistration, it is these custom attributes that are being set.

Unlike the IdP profile attributes, custom attributes are modifiable and only protected by an {{site.data.keyword.appid_short_notm}} access token. This means that without taking proper precautions either the user or the application can update their custom attributes immediately following their first login leading to unintended consequences. For example, a user could potentially change their role from user to admin exposing administrative privileges to malicious users.

*WARNING* If you are setting administrative or another read-only attribute, you _must_ disable `User Profiles` from the dashboard to prevent clients from modifying their access rights.

### Example Use Case
{: #use-cases}

Consider an application where you are using {{site.data.keyword.appid_short_notm}} to federate existing users from your SAML identity provider. You may want certain users to have `admin` access immediately upon signing in to the application for the first time.

Once you have configured your SAML connection and disabled `User Profiles` to mitigate privilege changes, you can use the preregistration endpoint to set a custom `admin` attribute for specific users. After these users have signed-in, they will have inherited the `admin` attribute granting them access to your administration console without any action.

### API Usage
{: #usage}

The registration process starts with a POST request to the [/users endpoint](link to endpoint or swagger) containing a JSON payload describing the user and the custom profile attributes to set.

```
POST /<tenantId>/users HTTP/1.1
     Host: <management-server-url>
     Authorization: 'Bearer <IAM_TOKEN>'
     Content-Type: application/json
```
{: pre}

You can retrieve your IAM token using the [IBM Cloud command line tools](https://console.bluemix.net/docs/cli/reference/bluemix_cli/bx_cli.html#ibmcloud_iam_oauth_tokens)
{:tip}

##### Request Body
```
 {
     "idp": "<Identity Provider>",
     "idp-identity": "<User's unique identifier>",
     "profile": {
         "attributes": {}
     }
 }
```
{: pre}

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the components</th>
  </thead>
  <tbody>
    <tr>
      <td><code><em>idp</em></code></td>
      <td>The identity provider the user will authenticate with. One of `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid`</td>
    </tr>
    <tr>
      <td><code><em>idp-identity</em></code></td>
      <td>The unique identifier provided by the IdP. See [Identifying the User](#supported-idps) for details.</td>
    </tr>
    <tr>
      <td><code><em>profile</em></code></td>
      <td>The preregistered user's profile containing the custom attribute JSON mapping.</td>
    </tr>
  </tbody>
</table>

##### Example Request

```curl
$ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
```
{: pre}

#### Identifying Users Using their IdP-identity
{: #supported-idps}

{{site.data.keyword.appid_short_notm}} allows you to identify your user in different ways depending on the identity provider.

For each IdP, preregistration supports at least one of the following identifiers:

1. The user's unique ID, called the **GUID**, in the identity provider.

    Although this identifier always exists and is guaranteed to be unique, it is not always readily available or easy to understand. For instance, Cloud Directory uses a random 16 byte random GUID.

2. User's **email** or **username** depending on the identity provider.

    This user-friendly and convenient identifier is generally available, but not guaranteed to be supported.

When you preregister a user, you may identify the user in any of the supported methods available for the specific identity provider. Because multiple Ids are supported for many of the IdPs, it is possible (but not recommended!) to preregister the same users multiple times using different identifiers. If this occurs, {{site.data.keyword.appid_short_notm}} will prioritize the IdP's GUID when an authenticated user signs in for the first time.

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Idea icon"/> Supported Identity Providers</th>
    </thead>
    <tbody>
      <tr>
        <td rowspan=3 colspan=2>
            <div>
                <h5>Cloud Directory</h5>
                <p>\*See additional details [here]()</p>
            </div>
        </td>
        <td>guid</td>
      </tr>
      <tr>
        <td>email</td>
      </tr>
      <tr>
        <td>username</td>
      </tr>
      <tr>
        <td colspan=2>
            <div>
                <h5>Custom Identity</h5>
                <p>\*See additional implementation details [here]()</p>
            </div>
        </td>
        <td>sub</td>
      </tr>
      <tr>
        <td rowspan=2 colspan=2>Facebook / Google</td>
        <td>guid</td>
      </tr>
      <tr>
        <td>email</td>
      </tr>
      <tr>
        <td colspan=2>SAML</td>
        <td>email</td>
      </tr>
    </tbody>
</table>

##### Cloud Directory
{: #cloud-directory}

Cloud Directory users can be preregistered using their user's `GUID`, `email`, or `username`.

Keep in mind that Cloud Directory restricts applications to either `email` or `username` based authentication. During the registration flow, {{site.data.keyword.appid_short_notm}} enforces this restriction in addition to `email` and custom `username` formatting requirements.

When your database is empty, you can change your Cloud Directory instance authorization method from the dashboard or using the <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Identity_Providers/set_cloud_directory_idp" target="____blank">Management APIs<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{: tip}


##### Custom Identity
{: #custom-identity}

Preregistering a user using custom authentication can use any unique identifier provided by its authentication flow. This identifier must *exactly* match the `sub` of the signed JWT sent during the authorization request to ensure the nominated profile is linked successfully.

> For more information on the Custom Identity Flow see our [documentation](./custom).

### Preregistered Users
{: #preregistered-users}

During a successful registration request, a new {{site.data.keyword.appid_short_notm}} user profile will be created with the provided custom attributes. In response, the server will return the user's {{site.data.keyword.appid_short_notm}} user Id.

```
{
    "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
}
```
{: pre}

Since a new {{site.data.keyword.appid_short_notm}} user profile is created for each preregistered user, you can use their unique Id just as you would fully authenticated users.

For instance, you can modify, search, and delete authenticated and preregistered user profiles enabling you to keep your current workflow.

Keep in mind that their IdP profile attributes will be empty until their first authentication.

### Next Steps
Now that you have nominated your users, try setting up a custom login page to streamline their sign-up experience!
