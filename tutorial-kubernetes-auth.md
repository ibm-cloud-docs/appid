---

copyright:
  years: 2017, 2023
lastupdated: "2023-05-30"

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

      A URL that is registered with a custom domain might look like: `http://mydomain.net/myapp2path/oauth2-myappid/callback`. If the apps that you want to expose are within the same cluster but in different namespaces, you can use a wildcard to specify all of them. This can be helpful during development, but it is recommended that you exercise caution when you use wildcards in production. For example, `https://custom_domain.net/*/oauth2-myappid/callback`

   * Ingress subdomain:

      If your app is registered with an IBM Kubernetes Ingress subdomain, your callback URL might look like: `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/oauth2-myappid/callback`




## Updating your Ingress resource
{: #define-annotation}

Your Ingress resource is used to define how you want to expose your applications. The resource contains the rules that define how to route incoming requests to your applications. To add {{site.data.keyword.appid_short_notm}} authentication to your apps, follow the steps in the [IBM Cloud Kubernetes Service documentation](/docs/containers?topic=containers-comm-ingress-annotations#app-id-auth).

   



## Next steps
{: #kube-next}

Now that your application is running in a Kubernetes cluster and Ingress is configured, you can try:

* Customizing the [login widget](/docs/appid?topic=appid-login-widget)
* Configuring [multi-factor authentication](/docs/appid?topic=appid-cd-mfa)
* Defining the information that you want to include in your [user profiles](/docs/appid?topic=appid-user-admin)



