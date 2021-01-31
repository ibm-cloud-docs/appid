---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-31"

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



# Containerized apps with Ingress
{: #kube-auth}

With {{site.data.keyword.appid_full}}, you can consistently enforce policy-driven security by using the Ingress networking capability in {{site.data.keyword.containerlong}} or {{site.data.keyword.openshiftshort}}. With this approach, you can enforce authentication and authorization policies for all of the applications in your cluster at the same time, without ever changing your app code!
{: shortdesc}

The Kubernetes Service custom Ingress image is [deprecated as of 01 December 2020](/docs/containers?topic=containers-ingress-types). This tutorial is updated to use the community Kubernetes Ingress image. To see the previous version of this documentation, see the [Kubernetes Service documentation](/docs/containers?topic=containers-ingress_annotation#appid-auth).
{: note}


![{{site.data.keyword.appid_short_notm}} Kubernetes integration architecture](images/kube-integration.png){: caption="Figure 1. {{site.data.keyword.appid_short_notm}} Kubernetes integration architecture" caption-side="bottom"}

1. A user opens your application and triggers a request to the web app or API.
2. In the API flow, the Ingress controller attempts to validate the supplied tokens. If the web flow is used, it kicks off a three-leg OIDC authentication process.
3. {{site.data.keyword.appid_short_notm}} begins the authentication process by displaying the Login Widget.
4. The user provides a username or email and password.
5. The Ingress controller obtains access and identity tokens from {{site.data.keyword.appid_short_notm}} for authorization.
6. Every request that is validated and forwarded by the Ingress Controller to your apps has an authorization header that contains the tokens.

The {{site.data.keyword.appid_short_notm}} Ingress annotation does not currently support refresh tokens. When access and identity tokens expire, user's must reauthenticate.
{: note}


## Before you begin
{: #kube-prereqs}

Before you can get started, ensure that you have the following prerequisites.
{: shortdesc}

* An instance of App ID that is provisioned in the same region in which your cluster is deployed. The service name must contain only alphanumeric characters or hyphens (-), and cannot contain spaces.
* A standard Kubernetes Service cluster with at least 2 worker nodes in each available zone. For help configuring Ingress resouce for your cluster, see [Setting up Kubernetes Ingress](/docs/containers?topic=containers-ingress-types).

* The following {{site.data.keyword.cloud_notm}} IAM roles:
  * Cluster: **Administrator** platform role
  * Kubernetes namespaces: **Manager** service role
  * App ID: **Editor** platform role and **Writer** Service role
* The following CLIs:
  * [{{site.data.keyword.cloud_notm}}](/docs/cli?topic=cli-getting-started)
  * [Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
  * [Docker](https://www.docker.com/products/container-runtime#/download)
* The {{site.data.keyword.containershort}} and {{site.data.keyword.registryshort_notm}} [CLI plug-ins](/docs/cli?topic=cli-install-devtools-manually#idt-install-kubernetes-cli-plugin)

To ensure the best performance of the integration, it is recommended that you always use the latest version of IBM Cloud Kubernetes Service Application Load Balancer (ALB). By default, auto-update is enabled for your cluster. For more information about auto-updates, see [On-demand ALB update feature on {{site.data.keyword.containershort}}](https://www.ibm.com/cloud/blog/on-demand-alb-update-feature-on-ibm-cloud-kubernetes-service).
{: tip}

## Adding redirect URLs
{: #ingress-redirect}

A redirect URL is the callback endpoint of your app. To prevent phishing attacks, App ID validates requested URLs against an allowlist of redirect URLs that you add to the service.

A redirect URL is the callback endpoint of your app; the location a user is sent after successfully signing in or out of your app. To prevent phishing attacks, App ID validates requested URLs against an allowlist of redirect URLs that you add to the service. By adding a URL to your allowlist, you give App ID permission to forward your users to that location. [Learn more about redirect URIs](/docs/appid?topic=appid-managing-idp#add-redirect-uri).

1. In the IBM Cloud console, select your instance of App ID from your resource list.
2. Navigate to the **Manage authentication** tab of your instance of App ID.
3. In the **Identity providers** tab, be sure that you've selected an identity provider.

  If no provider is selected, the user is not authenticated, but is still issued an access token for anonymous access to the app.
  {: note}

4. In the **Authentication settings** tab, add your redirect URLs and click the `+` symbol to save your changes.

  * Custom domain:

    A URL that is registered with a custom domain might look like: `http://mydomain.net/myapp2path/appid_callback`. If the apps that you want to expose are within the same cluster but in different namespaces, you can use a wildcard to specify all of the apps in the cluster at once. This can be helpful during development, but you should exercise caution if you use wildcards in production. For example: `https://custom_domain.net/*`

  * Ingress subdomain:

    If your app is registered with an IBM Ingress subdomain, your callback URL might look like: `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback`

  * Log out functionality:

    If `/logout` or `/sign out` exist in your path, cookies are removed and the user is sent back to the login page. To redirect users after they sign out, append `/sign_out` to your domain in the format `http://<hostname>/oauth2-<App_ID_service_instance_name>/sign_out` or `https://<hostname>/oauth2-<App_ID_service_instance_name>/sign_out`. Be sure that the log out code in your application is is called as a reaction to the user clicking **Sign out** or **Log out** in your app.

    

## Binding {{site.data.keyword.appid_short_notm}} to your cluster
{: #kube-create-appid}

By binding your instance of {{site.data.keyword.appid_short_notm}} to your cluster, you create the connection between the Kubernetes Service and App ID that allows you to enforce authentication for all of the apps that run in your cluster at the same time.



1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Follow the prompts in the CLI to complete logging in. If you're using a federated ID, be sure to append the `--sso` flag to the end of the command.

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: codeblock}

2. Set the context for your cluster.

  ```
  ibmcloud ks cluster config --cluster <cluster_name_or_ID>
  ```
  {: codeblock}

3. Bind the App ID service instance to your cluster. The command creates a service key for the service instance, or you can include the `--key` flag to use existing service key credentials. Be sure to bind the service instance to the same namespace that your Ingress resources exist in. Note that all letters in the service instance name must specified as lowercase.

  ```
  ibmcloud ks cluster service bind --cluster <cluster_name_or_ID> --namespace <namespace> --service <App_ID_instance_name> [--key <service_instance_key>]
  ```
  {: codeblock}

  Example output:

  ```
  ibmcloud ks cluster service bind --cluster mycluster --namespace default --service appid1
  Binding service instance to namespace...
  OK
  Namespace:    default
  Secret name:  binding-appid1
  ```
  {: screen}


## Updating your Ingress resource
{: #define-annotation}

Your Ingress resource is used to define the way in which you want to expose your applications. The resource contains the rules that define how to route incoming requests to your applications. To add App ID authenticaton to your apps, add the following annotations to the `metadata.annotations` section of your resource.


1. Add the following `auth-url` annotation. Change only the placeholder for your App ID service instance name. Note that all letters in the service instance name must specified as lowercase.

  ```
  ...
  annotations:
  nginx.ingress.kubernetes.io/auth-url: https://oauth2-<App_ID_service_instance_name>.<namespace of the Ingress resource>.svc.cluster.local/oauth2-<App_ID_service_instance_name>/auth
  ...
  ```
  {: codeblock}

  You can add more instance of {{site.data.keyword.appid_short_notm}} to your annotation by using a semicolon (;). 
  {: tip}

2. Choose which tokens to send in the authorization header to your app.

  * To send only the ID token, add the `nginx.ingress.kubernetes.io/auth-response-headers: Authorization` annotation.
  * To send only the access token, add the following information to the `access_by_lua_block{}` in the `configuration-snippet` annotation.
    ```
    ...
    annotations:
    nginx.ingress.kubernetes.io/configuration-snippet: |
      auth_request_set $access_token $upstream_http_x_auth_request_access_token;
      access_by_lua_block {
        if ngx.var.access_token ~= "" then
          ngx.req.set_header("Authorization", "Bearer " .. ngx.var.access_token)
        end
      }
    ...
    ```
    {: codeblock}

  * To send both the access token and the ID token, add the following information to `the access_by_lua_block{}` in the `configuration-snippet` annotation.
    ```
    ...
    annotations:
    nginx.ingress.kubernetes.io/configuration-snippet: |
      auth_request_set $access_token $upstream_http_x_auth_request_access_token;
      auth_request_set $id_token $upstream_http_authorization;
      access_by_lua_block {
        if ngx.var.id_token ~= "" and ngx.var.access_token ~= "" then
          ngx.req.set_header("Authorization", "Bearer " .. ngx.var.access_token .. " " .. ngx.var.id_token:match("%s*Bearer%s*(.*)"))
        end
      }
    ...
    {: codeblock}

3. Optional: If your app supports the web app strategy in addition to, or instead of, the API strategy, add the `nginx.ingress.kubernetes.io/auth-signin: https://$host/oauth2-<App_ID_service_instance_name>/start?rd=$escaped_request_uri` annotation. 

  All letters in the service instance name must specified as lowercase.
  {: note}




## Applying your resource with authentication enabled
{: kube-ingress}

Now that your Ingress resource is updated with the annotation, you can start enforcing authentication by reapplying it.

1. Enable the ALB OAuth Proxy add-on in your cluster.

  ```
  ibmcloud ks cluster addon enable alb-oauth-proxy --cluster <cluster_name_or_ID>
  ```
  {: codeblock}

  To verify that your addon is ready, you can run the following command.

  ```
  ibmcloud ks cluster addon ls --cluster <cluster_name_or_ID>
  ```
  {: codeblock}

2. Re-apply your Ingress resources to enforce App ID authentication. 

  ```
  kubectl apply -f <app_ingress_resource>.yaml -n namespace
  ```
  {: codeblock}

  After an Ingress resource with the appropriate annotations is re-applied, the ALB OAuth Proxy add-on deploys an OAuth2-Proxy deployment, creates a service for the deployment, and creates a separate Ingress resource to configure routing for the OAuth2-Proxy deployment messages. Do not delete these add-on resources.
  {: note}

3. Optional: You can customize the default behavior of the OAuth2-Proxy by creating a Kubernetes ConfigMap. For more information on customization, see the [Kubernetes Service annotation docs](/docs/containers?topic=containers-comm-ingress-annotations#app-id).

4. Verify that App ID authentication is enforced for your apps.

  * If your app supports the web app strategy: Access your app's URL in a web browser. If App ID is correctly applied, you are redirected to an App ID authentication log-in page.
  * If your app supports the API strategy: Specify your bearer access token in the Authorization header of requests to the apps. To get your access token, see [Obtaining tokens](/docs/appid?topic=appid-obtain-tokens). If App ID is correctly applied, the request is successfully authenticated and is routed to your app. If you send requests to your apps without an access token in the authorization header, or if the access token is not accepted by App ID, then the request is rejected.




## Next steps
{: #kube-next}

Now that your application is running in a Kubernetes cluster and Ingress is configured, you can try:

* Customizing the [login widget](/docs/appid?topic=appid-login-widget)
* Configuring [multi-factor authentication](/docs/appid?topic=appid-cd-mfa)
* Defining the information that you want to include in your [user profiles](/docs/appid?topic=appid-user-admin)



