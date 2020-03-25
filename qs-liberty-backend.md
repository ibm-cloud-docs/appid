---

copyright:
  years: 2017, 2020
lastupdated: "2020-03-19"

keywords: backend apps, java, liberty for java, liberty, identity provider, access management, protected endpoints, access tokens, security, back end

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



# Backend: Liberty for Java
{: #backend-liberty}

With {{site.data.keyword.appid_short_notm}}, you can easily protect your API endpoints and ensure the security of your Liberty for Java backend applications. With this guide, you can quickly get a simple authentication flow up and running in less than 20 minutes.
{: shortdesc}


![Backend Liberty for Java apps](images/backend_liberty.png){: caption="Figure 1. Backend Liberty for Java flow" caption-side="bottom"}

1. To make a request to a protected resource, a client must have an access token. In step 1, the client makes a request to {{site.data.keyword.appid_short_notm}} for a token. For more information about obtaining access tokens, see [Obtaining tokens](/docs/appid?topic=appid-obtain-tokens).
2. {{site.data.keyword.appid_short_notm}} returns the tokens.
3. Using the access token, the client makes a request to access the protected resource.
4. The resource validates the token including the structure, expiration, signature, audience, and any other present fields. If the token is not valid, the resource server denies access. If the token validation is successful, it returns the data.


## Video tutorial
{: #backend-liberty-video}

Check out the following video to see how you can use {{site.data.keyword.appid_short_notm}} to protect a simple Liberty for Java application. All of the information that is covered in the video can also be found in written form on this page.

<iframe class="embed-responsive-item" id="appid-liberty-backend-app" title="About {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/QA6DY2qqLaw?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

Don't have an app that you can try out the flow with? No problem! {{site.data.keyword.appid_short_notm}} provides a [simple Liberty for Java sample app](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02d-simple-liberty-backend-app).


## Before you begin
{: #liberty-before}

Before you get started with {{site.data.keyword.appid_short_notm}} in your Liberty for Java backend application you must have the following prerequisites:

* An instance of [the {{site.data.keyword.appid_short_notm}} service](https://cloud.ibm.com/catalog/services/app-id){: external}
* [The IBM Cloud CLI](/docs/cli?topic=cloud-cli-getting-started)
* [Apache Maven 3.5+](https://maven.apache.org/download.cgi){: external}
* [Java 8+](https://www.java.com/en/download/){: external}
* The [{{site.data.keyword.appid_short_notm}} Postman collection](https://github.com/ibm-cloud-security/appid-postman){: external} for testing

## Step 1: Obtain your credentials
{: #liberty-obtain-credentials}

You can obtain your credentials in one of two ways.

  * By navigating to the **Applications** tab of the {{site.data.keyword.appid_short_notm}} dashboard. If you don't already have one, you can click **Add application** to create a new one.

  * By making a POST request to the [`/management/v4/{tenantId}/applications` endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication){: external}.

    Request format:
    ```sh
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    Example response:
    ```json
    {
      "clientId": "xxxxx-34a4-4c5e-b34d-d12cc811c86d",
      "tenantId": "xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "secret": "ZDk5YWZkYmYt*******",
      "name": "app1",
      "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "profilesUrl": "https://us-south.appid.cloud.ibm.com",
      "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxxx-9b1f-433e-9d46-0a5521f2b1c4/.well-known/openid-configuration"
    }
    ```
    {: screen}


## Step 2: Configure your `server.xml` file
{: #liberty-configure-server}
 
1. Open your `server.xml` file.
2. Add the following features to the `featureManager` section. Some features might come built in with Liberty. If you receive an error when you run your server, you can install them by running `.installUtility install <name_of_server>` from the bin directory of your Liberty installation.

    ```xml
    <featureManager>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
    </featureManager>
    ```
    {: codeblock}

3. Configure SSL by adding the following to your `server.xml` file. 

    ```xml
    <keyStore id="defaultKeyStore" password="{password}"/>
    <keyStore id="RootCA" password="{password}" location="${server.config.dir}/resources/security/{myTrustStore}"/>
    <ssl id="{sslID}" keyStoreRef="defaultKeyStore" trustStoreRef="{truststore-ref}"/>
    ```
    {: codeblock}

4. Create an Open ID Connect Client feature and define the following placeholders. With the credentials that you obtained, fill the placeholders.

    ```xml
    <openidConnectClient 
        id="oidc-client-simple-liberty-backend-app" 		
        inboundPropagation="required"
        jwkEndpointUrl="{region}.appid.cloud.ibm.com/oauth/v4/{tenantID}/publickeys"
        issuerIdentifier="{region).appid.cloud.ibm.com/oauth/v4/{tenantID}"
        signatureAlgorithm="RS256"
        audiences="{client-id}"
        sslRef="oidcClientSSL"
    /> 	
    ```
    {: codeblock}

    <table>
    <caption>Table. OIDC element variables for Liberty for Java apps</caption>
        <tr>
            <th colspan="2"> Understanding the OIDC element variables </th>
        </tr>
        <tr>
            <td><code>id</code></td>
            <td>The name of your application.</td>
        </tr>
        <tr>
            <td><code>inboundPropagation</code></td>
            <td>In order to propagate the information received in the token, the value must be set to "required".</td>
        </tr>
        <tr>
            <td><code>jwkEndpointUrl</code></td>
            <td>The endpoint that is used to obtain keys in order to validate the token. Region options include: <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code>, and <code>us-south</code>. You can find your tenant ID in the credentials that you previously created.</td>
        </tr>
        <tr>
            <td><code>issuerIdentifier</code></td>
            <td>The issuer identifier defines your authorization server. Region options include: <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code>, and <code>us-south</code>. You can find your tenant ID in the credentials that you previously created.</td>
        </tr>
        <tr>
            <td><code>signatureAlgorithm</code></td>
            <td>Specified as "RS256".</td>
        </tr>
        <tr>
            <td><code>audiences</code></td>
            <td>By default, the token is issued for your {{site.data.keyword.appid_short_notm}} client ID that can be found in your application credentials.</td>
        </tr>
        <tr>
            <td><code>sslRef</code></td>
            <td>The name of the SSL configuration that you want to use.</td>
        </tr>
    </table>

5. Define your special subject type as `ALL_AUTHENTICATED_USERS`.

    ```xml
    <application 
        id="simple-liberty-backend-app" 
        location="location-of-your-war-file" 
        name="simple-liberty-backend-app" 
        type="war">

        <application-bnd>
            <security-role name="myrole">
                <special-subject type="ALL_AUTHENTICATED_USERS"/>
            </security-role>
        </application-bnd>
    </application>
    ```
    {: codeblock}


## Step 3: Configure your `web.xml` file
{: #liberty-configure-web}

In your `web.xml` file, define the areas of your application that you want to secure.

1. Define a security role. This should be the same role that you defined in the `server.xml` file.

    ```xml
    <security-role>
		<role-name>myrole</role-name>
	</security-role>
    ```
    {: codeblock}

2. Define a security constraint.

    ```xml
	<security-constraint>
		<display-name>Security Constraints</display-name>
		<web-resource-collection>
			<web-resource-name>ProtectedArea</web-resource-name>
			<url-pattern>/api/*</url-pattern>
		</web-resource-collection>
		<auth-constraint>
			<role-name>myrole</role-name>
		</auth-constraint>
		<user-data-constraint>
			<transport-guarantee>NONE</transport-guarantee>
		</user-data-constraint>
	</security-constraint>
    ```
    {: codeblock}


## Step 4: Test your configuration
{: #liberty-test}

Now that you've finished the initial installation, build the app and test your configuration to ensure that everything is working as expected.

1. Change into your application directory.

2. Build your application.

    ```
    server run
    ```
    {: codeblock}

3. Make a request to the protected endpoint. An error is returned.

4. [Obtain an access token](/docs/appid?topic=appid-obtain-tokens).

5. With the access token that you obtained in the previous step, make a request to the endpoint. You should now be able to access the protected endpoint. Verify that the response contains what you expect.


## Next steps
{: #liberty-next}

Ready to start perfecting your authentication experience? Try walking through [this blog](https://www.ibm.com/cloud/blog/perfecting-the-login-experience-with-liberty-oauth2-and-appid){: external} or learning more about [app-to-app communication](/docs/appid?topic=appid-app).


