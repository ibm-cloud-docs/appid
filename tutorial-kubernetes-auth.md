---

copyright:
  years: 2017, 2023
lastupdated: "2023-05-22"

keywords: ingress controller, ingress, istio, access, subdomain, custom domain, service, containerized apps, containers, kube, networking, policy, policies, secure apps, authentication, authorization

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


# Containerized apps with Ingress
{: #kube-auth}

With {{site.data.keyword.appid_full}}, you can consistently enforce policy-driven security by using the Ingress networking capability in {{site.data.keyword.containerlong_notm}}. With this approach, you can enforce authentication and authorization policies for all the applications in your cluster at the same time, without ever changing your app code!
{: shortdesc}

The {{site.data.keyword.containershort_notm}} custom Ingress image is deprecated as of 01 December 2020. This tutorial is updated to use the community Kubernetes Ingress image. To see the previous version of this documentation, see the [{{site.data.keyword.containershort_notm}} documentation](/docs/containers?topic=containers-comm-ingress-annotations#app-id-authentication).
{: note}


![{{site.data.keyword.appid_short_notm}} Kubernetes integration architecture](images/kube-integration.png){: caption="Figure 1. {{site.data.keyword.appid_short_notm}} Kubernetes integration architecture" caption-side="bottom"}

1. A user opens your application and triggers a request to the web app or API.
2. In the API flow, the Ingress controller attempts to validate the supplied tokens. If the web flow is used, it starts a three-leg OIDC authentication process.
3. {{site.data.keyword.appid_short_notm}} begins the authentication process by displaying the login widget.
4. The user provides a username or email and password.
5. The Ingress controller obtains access and identity tokens from {{site.data.keyword.appid_short_notm}} for authorization.
6. Every request that is validated and forwarded by the Ingress controller to your apps has an authorization header that contains the tokens.


## Before you begin
{: #kube-prereqs}

Before you can get started, ensure that you have the following prerequisites.
{: shortdesc}

* An instance of {{site.data.keyword.appid_short_notm}} that is provisioned in the same region in which your cluster is deployed. The service name must contain only alphanumeric characters or hyphens (-), and cannot contain spaces.
* A standard {{site.data.keyword.containershort_notm}} cluster with at least two worker nodes in each available zone.

* The following {{site.data.keyword.cloud_notm}} IAM roles:
   * Cluster: **Administrator** platform role
   * Kubernetes namespaces: **Manager** service role
   * {{site.data.keyword.appid_short_notm}}: **Editor** platform role and **Writer** Service role
* The following CLIs:
   * [{{site.data.keyword.cloud_notm}}](/docs/cli?topic=cli-getting-started)
   * [Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* The {{site.data.keyword.containershort}} and {{site.data.keyword.registryshort_notm}} [CLI plug-ins](/docs/cli?topic=cli-install-devtools-manually#idt-install-kubernetes-cli-plugin)

To ensure the best performance of the integration, it is recommended that you always use the latest version of IBM Cloud {{site.data.keyword.containershort_notm}} Application Load Balancer (ALB). By default, autoupdate is enabled for your cluster. For more information about autoupdates, see [OnDemand ALB update feature on {{site.data.keyword.containershort}}](https://www.ibm.com/cloud/blog/on-demand-alb-update-feature-on-ibm-cloud-kubernetes-service).
{: tip}

## Adding redirect URLs
{: #ingress-redirect}

A redirect URL is the callback endpoint of your app; the location where a user is sent after successfully signing in or out of your app. To prevent phishing attacks, {{site.data.keyword.appid_short_notm}} validates requested URLs against an allowlist of redirect URLs that you add to the service. By adding a URL to your allowlist, you give {{site.data.keyword.appid_short_notm}} permission to forward your users to that location. [Learn more about redirect URIs](/docs/appid?topic=appid-managing-idp#add-redirect-uri).

1. In the IBM Cloud console, select your instance of {{site.data.keyword.appid_short_notm}} from your resource list.
2. Navigate to the **Manage authentication** page of your instance of {{site.data.keyword.appid_short_notm}}.
3. In the **Identity providers** tab, be sure that an identity provider is set to on.

   If no provider is selected, the user is not authenticated, but is still issued an access token for anonymous access to the app.
   {: note}

4. In the **Authentication settings** tab, add your redirect URLs and click the `+` symbol to save your changes. Your redirect URL should be formatted similarly to the following example:

   ```sh
   https://<hostname>/oauth2-<AppIDServiceInstanceName>/callback
   ```
   {: screen}

   * Custom domain:

      A URL that is registered with a custom domain might look like: `http://mydomain.net/myapp2path/oauth2-myappid/callback`. If the apps that you want to expose are within the same cluster but in different namespaces, you can use a wildcard to specify all of them. This can be helpful during development, but it is recommended that you do not use wildcards in production without exercising caution. For example, `https://custom_domain.net/*/oauth2-myappid/callback`

   * Ingress subdomain:

      If your app is registered with an IBM Kubernetes Ingress subdomain, your callback URL might look like: `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/oauth2-myappid/callback`

 

## Binding {{site.data.keyword.appid_short_notm}} to your cluster
{: #kube-create-appid}

By binding your instance of {{site.data.keyword.appid_short_notm}} to your cluster, you create the connection between the {{site.data.keyword.containershort_notm}} and {{site.data.keyword.appid_short_notm}} that allows the enforcement of authentication for all the apps that run in your cluster at the same time.

1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Follow the prompts in the CLI to complete logging in. If you're using a federated ID, be sure to append the `--sso` flag to the end of the command.

   ```sh
   ibmcloud login -a cloud.ibm.com -r REGION
   ```
   {: codeblock}

2. Set the context for your cluster.

   ```sh
   ibmcloud ks cluster config --cluster CLUSTER_NAME_OR_ID
   ```
   {: codeblock}

3. Bind the {{site.data.keyword.appid_short_notm}} service instance to your cluster. The command creates a service key for the service instance, or you can include the `--key` flag to use existing service key credentials. Be sure to bind the service instance to the same namespace that your Ingress resources exist in. All the letters in the service instance name must specified as lowercase.

   ```sh
   ibmcloud ks cluster service bind --cluster CLUSTER_NAME_OR_ID --namespace NAMESPACE --service APPIDINSTANCENAME [--key SERVICEINSTANCEKEY]
   ```
   {: codeblock}

   Example output:

   ```sh
   ibmcloud ks cluster service bind --cluster mycluster --namespace default --service appid1
   Binding service instance to namespace...
   OK
   Namespace:    default
   Secret name:  binding-appid1
   ```
   {: screen}


## Updating your Ingress resource
{: #define-annotation}

Your Ingress resource is used to define how you want to expose your applications. The resource contains the rules that define how to route incoming requests to your applications. To add {{site.data.keyword.appid_short_notm}} authentication to your apps, add the following annotations to the `metadata.annotations` section of your resource.


1. Add the following `auth-url` annotation. Update the placeholder variable for your {{site.data.keyword.appid_short_notm}} service instance name and the namespace of your Ingress resource. 

   ```sh
   ...
   annotations:
   nginx.ingress.kubernetes.io/auth-url: https://oauth2-
   <AppIDServiceInstanceName>.<namespaceOfIngressResource>.svc.cluster.local/oauth2-<AppIDServiceInstanceName>/auth
   ...
   ```
   {: codeblock}

   All letters in the service instance name must be specified as lowercase characters.
   {: note}

2. Optional: If your app is a web app, in addition to or instead of, providing APIs, add the `nginx.ingress.kubernetes.io/auth-signin: https://$host/oauth2-<AppIDServiceInstanceName>/start?rd=$escaped_request_uri` annotation. 

3. Sometimes the authentication cookie used by `OAuth2-Proxy` exceeds 4 KB. Therefore it is split into two parts. The following snippet must be added to ensure that both cookies could be properly updated by `OAuth2-Proxy`.
    
    ```yaml
        ...
        annotations:
            nginx.ingress.kubernetes.io/configuration-snippet: |
            auth_request_set $_oauth2_<App_ID_service_instance_name>_upstream_1 $upstream_cookie__oauth2_<App_ID_service_instance_name>_1;
            access_by_lua_block {
                if ngx.var._oauth2_<App_ID_service_instance_name>_upstream_1 ~= "" then
                ngx.header["Set-Cookie"] = "_oauth2_<App_ID_service_instance_name>_1=" .. ngx.var._oauth2_<App_ID_service_instance_name>_upstream_1 .. ngx.var.auth_cookie:match("(; .*)")
                end
            }
        ...
    ```
    {: codeblock}


    Kubernetes Ingress Controllers (ALBs) on clusters created on or after 31 January 2022 do not process Ingress resources that have snippet annotations (for example, `nginx.ingress.kubernetes.io/configuration-snippet`) by default as all new clusters are deployed with `allow-snippet-annotations: "false"` configuration in the ALB's ConfigMap. If you want to customize the `Authorization` header using the previous configuration snippets, you need to edit the ALB's ConfigMap (`kube-system/ibm-k8s-controller-config`) and change `allow-snippet-annotations: "false"` to `allow-snippet-annotations: "true"`.
    {: note}

4. Choose which tokens to send in the `Authorization` header to your app. For more information about ID and access tokens, see the [{{site.data.keyword.appid_short_notm}} documentation](/docs/appid?topic=appid-tokens){: external}.
    
    * To send only the `ID Token`, add the following annotation:

        ```yaml
        ...
        annotations:
            nginx.ingress.kubernetes.io/auth-response-headers: Authorization
        ...
        ```
        {: codeblock}


    * To send only the `Access Token`, add the following information to the `configuration-snippet` annotation. (This extends the snippet from Step 5.2.)

    ```yaml
    ...
    annotations:
        nginx.ingress.kubernetes.io/configuration-snippet: |
        auth_request_set $_oauth2_<App_ID_service_instance_name>_upstream_1 $upstream_cookie__oauth2_<App_ID_service_instance_name>_1;
        auth_request_set $access_token $upstream_http_x_auth_request_access_token;
        access_by_lua_block {
            if ngx.var._oauth2_<App_ID_service_instance_name>_upstream_1 ~= "" then
            ngx.header["Set-Cookie"] = "_oauth2_<App_ID_service_instance_name>_1=" .. ngx.var._oauth2_<App_ID_service_instance_name>_upstream_1 .. ngx.var.auth_cookie:match("(; .*)")
            end
            if ngx.var.access_token ~= "" then
            ngx.req.set_header("Authorization", "Bearer " .. ngx.var.access_token)
            end
    @@ -653,14 +684,18 @@ ALB OAuth Proxy add-on version 1.0.0 uses configuration snippet annotations (`ng
    ```
    {: codeblock}


    * To send the `Access Token` and the `ID Token`, add the following information to the `configuration-snippet` annotation. (This extends the snippet from Step 5.2.)
    
    ```yaml
    ...
        annotations:
        nginx.ingress.kubernetes.io/configuration-snippet: |
        auth_request_set $_oauth2_<App_ID_service_instance_name>_upstream_1 $upstream_cookie__oauth2_<App_ID_service_instance_name>_1;
        auth_request_set $access_token $upstream_http_x_auth_request_access_token;
        auth_request_set $id_token $upstream_http_authorization;
        access_by_lua_block {
            if ngx.var._oauth2_<App_ID_service_instance_name>_upstream_1 ~= "" then
            ngx.header["Set-Cookie"] = "_oauth2_<App_ID_service_instance_name>_1=" .. ngx.var._oauth2_<App_ID_service_instance_name>_upstream_1 .. ngx.var.auth_cookie:match("(; .*)")
            end
            if ngx.var.id_token ~= "" and ngx.var.access_token ~= "" then
            ngx.req.set_header("Authorization", "Bearer " .. ngx.var.access_token .. " " .. ngx.var.id_token:match("%s*Bearer%s*(.*)"))
            end
    @@ -669,10 +704,7 @@ ALB OAuth Proxy add-on version 1.0.0 uses configuration snippet annotations (`ng
    ```
    {: codeblock}

5. Optional: If your app supports the [web app strategy](/docs/appid?topic=appid-key-concepts#term-web-strategy) in addition to or instead of the [API strategy](/docs/appid?topic=appid-key-concepts#term-api-strategy), add the `nginx.ingress.kubernetes.io/auth-signin: https://$host/oauth2-<App_ID_service_instance_name>/start?rd=$escaped_request_uri` annotation. Note that all letters in the service instance name must be in lowercase.
        * If you specify this annotation, and the authentication for a client fails, the client is redirected to the URL of the OAuth2-Proxy for your {{site.data.keyword.appid_short_notm}} instance. This OAuth2-Proxy, which acts as the OIDC Relying Party (RP) for {{site.data.keyword.appid_short_notm}}, redirects the client to your {{site.data.keyword.appid_short_notm}} login page for authentication.
        * If you don't specify this annotation, a client must authenticate with a valid bearer token. If the authentication for a client fails, the client's request is rejected with a `401 Unauthorized` error message.

## Applying your resource with authentication enabled
{: #kube-ingress}

Now that your Ingress resource is updated with the annotation, you can start enforcing authentication by reapplying it.

1. Enable the ALB OAuth Proxy add-on in your cluster.

   ```sh
   ibmcloud ks cluster addon enable alb-oauth-proxy --cluster CLUSTER_NAME_OR_ID
   ```
   {: codeblock}

   To verify that your add-on is ready, you can run the following command.

   ```sh
   ibmcloud ks cluster addon ls --cluster CLUSTER_NAME_OR_ID
   ```
   {: codeblock}

2. Reapply your Ingress resources to enforce {{site.data.keyword.appid_short_notm}} authentication. 

   ```sh
   kubectl apply -f APP_INGRESS_RESOURCE.yaml -n namespace
   ```
   {: codeblock}

   

3. Optional: You can customize the default behavior of the OAuth2-Proxy by creating a Kubernetes configmap. For more information about customization, see the [{{site.data.keyword.containershort_notm}} annotation docs](/docs/containers?topic=containers-comm-ingress-annotations#app-id-authentication).

4. Verify that {{site.data.keyword.appid_short_notm}} authentication is enforced for your apps.

   * If your app is a web app: Access your app's URL in a web browser. If {{site.data.keyword.appid_short_notm}} is correctly applied, you are redirected to an {{site.data.keyword.appid_short_notm}} authentication login page.
   * If you are providing APIs: Specify your bearer access token in the Authorization header of requests to the apps. To get your access token, see [Obtaining tokens](/docs/appid?topic=appid-obtain-tokens). If {{site.data.keyword.appid_short_notm}} is correctly applied, the request is successfully authenticated and is routed to your app. If you send requests to your apps without an access token in the authorization header, or if the access token is not accepted by {{site.data.keyword.appid_short_notm}}, then the request is rejected.




## Next steps
{: #kube-next}

Now that your application is running in a Kubernetes cluster and Ingress is configured, you can try:

* Customizing the [login widget](/docs/appid?topic=appid-login-widget)
* Configuring [multi-factor authentication](/docs/appid?topic=appid-cd-mfa)
* Defining the information that you want to include in your [user profiles](/docs/appid?topic=appid-user-admin)



