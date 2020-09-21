---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-21"

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

With {{site.data.keyword.appid_full}}, you can consistently enforce policy-driven security by using the Ingress networking capability in {{site.data.keyword.containerlong}} or {{site.data.keyword.openshiftshort}}. With this approach, you can enable authorization and authentication for all of the applications in your cluster at the same time, without ever changing your app code!
{: shortdesc}

Check out the following diagram to see the authentication flow.

![{{site.data.keyword.appid_short_notm}} Kubernetes integration architecture](images/kube-integration.png){: caption="Figure 1. {{site.data.keyword.appid_short_notm}} Kubernetes integration architecture" caption-side="bottom"}

1. A user opens your application and triggers a request to the web app or API.
2. For the API flow, the Ingress controller attempts to validate the supplied tokens. If the web flow is used, it kicks off a three-leg OIDC authentication process.
3. {{site.data.keyword.appid_short_notm}} begins the authentication process by displaying the Login Widget.
4. The user provides a username or email and password.
5. The Ingress controller obtains access and identity tokens from {{site.data.keyword.appid_short_notm}} for authorization.
6. Every request that is validated and forwarded by the Ingress Controller to your apps has an authorization header that contains the tokens.

The {{site.data.keyword.appid_short_notm}} Ingress annotation does not currently support refresh tokens. When access and identity tokens expire, user's must reauthenticate.
{: note}

## Video tutorial
{: #video-ingress}

Updating your Ingress annotation works the same way in both {{site.data.keyword.containerlong}} or {{site.data.keyword.openshiftshort}}. To see how quickly you can be up and running with {{site.data.keyword.openshiftshort}} check out the following video.

![Protecting IBM Kubernetes Service OpenShift Applications with {{site.data.keyword.appid_short_notm}}](https://www.youtube.com/embed/sqGS7naTkoU){: video output="iframe" data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

## Before you begin
{: #kube-prereqs}

Before you can get started, ensure that you have the following prerequisites.
{: shortdesc}


* An app or sample app.

* A standard Kubernetes cluster with at least two worker nodes per zone. If you are using Ingress in multizone clusters review the extra prerequisites in the [Kubernetes Service documentation](/docs/containers?topic=containers-ingress#config_prereqs).

* An instance of {{site.data.keyword.appid_short_notm}} in the same region in which your cluster is deployed. Ensure that the service name does not contain any spaces.

* The following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/containers?topic=containers-access_reference#access_reference):
  * Cluster: Administrator platform role
  * Kubernetes namespaces: Manager service role

* The following CLIs:

  * [{{site.data.keyword.cloud_notm}}](/docs/cli?topic=cli-getting-started)
  * [Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
  * [Docker](https://www.docker.com/products/container-runtime#/download)

* The following [CLI plug-ins](/docs/cli?topic=cli-install-devtools-manually#idt-install-kubernetes-cli-plugin):

  * {{site.data.keyword.containershort}}
  * {{site.data.keyword.registryshort_notm}}

For help with getting the CLIs and plug-ins downloaded and your Kubernetes Service environment configured, check out the tutorial [creating Kubernetes clusters](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial_lesson1).
{: tip}


## Binding {{site.data.keyword.appid_short_notm}} to your cluster
{: #kube-create-appid}

By binding your instance of {{site.data.keyword.appid_short_notm}} to your cluster, you can enforce protection for all of the apps that run in your cluster.



1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Follow the prompts in the CLI to complete logging in. If you're using a federated ID, be sure to append the `--sso` flag to the end of the command.

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: codeblock}

  <table>
    <caption>Table 1. Available {{site.data.keyword.cloud_notm}} regions</caption>
    <tr>
      <th>Region</th>
      <th>Endpoint</th>
    </tr>
    <tr>
      <td>Dallas</td>
      <td><code>us-south</code></td>
    </tr>
    <tr>
      <td>Frankfurt</td>
      <td><code>eu-de</code></td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>au-syd</code></td>
    </tr>
    <tr>
      <td>London</td>
      <td><code>eu-gb</code></td>
    </tr>
    <tr>
      <td>Tokyo</td>
      <td><code>jp-tok</code></td>
    </tr>
  </table>

2. Set the context for your cluster.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

3. Check to see whether you already have an Ingress controller in your default namespace. {{site.data.keyword.containerlong}} supports one Ingress per namespace. If you already have one, you can update the existing Ingress configuration or use a different namespace.

  ```
  kubectl get ingress
  ```
  {: codeblock}

4. Bind your instance of {{site.data.keyword.appid_short_notm}}. Binding creates a service key for the service instance. You can specify an existing service key by using the `-key` flag.

  ```
  ibmcloud ks cluster service bind --cluster <cluster_name_or_ID> --namespace <namespace> --service <App_ID_instance_name> [--key <service_instance_key>]
  ```
  {: codeblock}

  If you do not specify a namespace, the secret is created in the `default` namespace.
  {: tip}

  Example output:

  ```
  ibmcloud ks cluster service bind --cluster mycluster --namespace default --service appid1
  Binding service instance to namespace...
  OK
  Namespace:    default
  Secret name:  binding-appid1
  ```
  {: screen}


## Configuring Ingress
{: kube-ingress}

During cluster creation, both a private and a public IBM Kubernetes Service Application Load Balancer (ALB) are created for you. To add application protection for apps that run in your cluster, update your Ingress resource YAML.


To ensure the best performance of the integration, it is recommended that you always use the latest version of IBM Kubernetes Service Application Load Balancer (ALB). By default, auto-update is enabled for your cluster. For more information about auto-updates, see [On-demand ALB update feature on {{site.data.keyword.containershort}}](https://www.ibm.com/cloud/blog/on-demand-alb-update-feature-on-ibm-cloud-kubernetes-service).
{: tip}

1. Get the secret that was created in your cluster namespace when you bound {{site.data.keyword.appid_short_notm}} to your cluster. Your binding will look similar to the following: `binding-<appid_instance_name>`.

  ```
  kubectl get secrets --namespace=<namespace>
  ```
  {: codeblock}

  Example output:

  ```
  NAME                       TYPE                                  DATA      AGE
  binding-appid1             Opaque                                1         1m
  bluemix-default-secret     kubernetes.io/dockercfg               1         1h
  default-token-kf97z        kubernetes.io/service-account-token   3         1h
  ```
  {: screen}

  This is **not** your Container Registry namespace.
  {: tip}

2. Use the following example `yaml` file to create your Ingress configuration. For help with defining the rest of your deployment, check out [Deploying apps with the CLI](/docs/containers?topic=containers-deploy_app#app_cli).

  ```
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    name: myingress
    annotations:
      ingress.bluemix.net/appid-auth: "bindSecret=<bind_secret> namespace=<namespace> requestType=<request_type> serviceName=<myservice> idToken=true"
  spec:
    tls:
    - hosts:
      - mydomain
      secretName: mytlssecret
    rules:
    - host: mydomain
      http:
        paths:
        - path: /
          backend:
            serviceName: myservice
            servicePort: 8080
  ```
  {: screen}

  <table>
    <caption>Table 2. Understanding annotation components</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>bindSecret</code></td>
      <td>The Kubernetes secret that was created when you bound your {{site.data.keyword.appid_short_notm}} service instance to your cluster.</td>
    </tr>
    <tr>
      <td><code>namespace</code></td>
      <td>The namespace in which your <code>bindSecret</code> was created. If you did not specify a namespace, the <code>default</code> namespace is used.</td>
    </tr>
    <tr>
      <td><code>requestType</code></td>
      <td><p>The type of request that you want to send to {{site.data.keyword.appid_short_notm}}. Options include: <code>web</code> and <code>api</code>. If you set the request type to <code>web</code>, a web request that contains an {{site.data.keyword.appid_short_notm}} access token is validated. If token validation fails, the web request is rejected. If the request does not contain an access token, then the request is redirected to the {{site.data.keyword.appid_short_notm}} login page. For {{site.data.keyword.appid_short_notm}} web authentication to work, cookies must be enabled in the user's browser.</p><p>If you set the request type to <code>api</code>, an API request that contains an {{site.data.keyword.appid_short_notm}} access token is validated. If the request does not contain an access token, a <code>401: Unauthorized</code> error message is returned to the user.</p></td>
    </tr>
    <tr>
      <td><code>serviceName</code></td>
      <td><p>Required: The name of the Kubernetes service that you created for your app.</p> <p>To use multiple request types in the same cluster, configure an instance of {{site.data.keyword.appid_short_notm}} to use <code>web</code> and another to use <code>api</code>.</p></td>
    </tr>
    <tr>
      <td><code>idToken</code></td>
      <td>Required: The Liberty OIDC client is unable to parse both the access and the identity token at the same time. When working with Liberty, set this value to <code>false</code> so that the identity token is not sent to the Liberty server.</td>
    </tr>
  </table>

  You can add more instance of {{site.data.keyword.appid_short_notm}} to your annotation by adding two `bindSecret` lines, separated by a semicolon (;). For example: </br> `bindSecret=binding-app-id-instance namespace=default requestType=web serviceName=web-application; bindSecret=binding-another-app-id namespace=default requestType=web serviceName=another-web-application`
  {: tip}

3. Run the configuration file.

  ```
  kubectl apply -f <file-name>.yaml
  ```
  {: codeblock}


## Adding your redirect URIs
{: #kube-add-redirect}

A redirect URL is the location that your user is sent to after they successfully sign in to or out of your app. By adding the redirect URI to your whitelist, you are telling {{site.data.keyword.appid_short_notm}} that it is ok to send your users to that location. [Learn more about redirect URIs](/docs/appid?topic=appid-managing-idp#add-redirect-uri).


1. Navigate to the {{site.data.keyword.cloud_notm}} GUI and open your {{site.data.keyword.appid_short_notm}} dashboard.

2. In **Identity Providers > Manage**, set the providers that you want to use to **On**. If a provider is not enabled, then users are issued an access token that provides anonymous access to your app.

3. Click **Authentication Settings**.

4. Click the **+** symbol in the **Add web redirect URLs** box.

  * Custom domain:

    A URL that is registered with a custom domain might look like: `http://mydomain.net/myapp2path/appid_callback`. If the apps that you want to expose are within the same cluster but in different namespaces, you can use a wildcard to specify all of the apps in the cluster at once. This can be helpful during development, but you should exercise caution if you use wildcards in production. For example: `https://custom_domain.net/*`

  * Ingress subdomain:

    If your app is registered with an IBM Ingress subdomain, your callback URL might look like: `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback`



## Configuring log out
{: #kube-logout}

When you configure your application to use the Ingress Controller annotation, a session with the user's browser is established. To end the Ingress session, call the `/appid_logout` endpoint and then redirect your users to a home or sign in page. Be sure that the log out code is called as a reaction to the user clicking `Logout` in your app. Be sure that you add your log out URI to your [whitelisted redirect URIs](/docs/appid?topic=appid-managing-idp#add-redirect-uri). Your URI will look similar to `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_logout`.



## Next steps
{: #kube-next}

Now that your application is running in a Kubernetes cluster and Ingress is configured, you can try:

* Customizing the [Login Widget](/docs/appid?topic=appid-login-widget)
* Configuring [multi-factor authentication](/docs/appid?topic=appid-cd-mfa)
* Assigning [access](/docs/appid?topic=appid-access-control)



