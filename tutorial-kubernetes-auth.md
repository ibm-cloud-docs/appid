---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: authentication, authorization, identity, app security, secure, development, ingress, policy, networking, containers, kubernetes

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}


# Tutorial: Configuring Ingress to use {{site.data.keyword.appid_long_notm}}
{: #kube-auth}

You can consistently enforce policy-driven security by using the Ingress networking capability in {{site.data.keyword.containerlong}}. With this approach, you can enable authorization and authentication for all of the applications in your cluster at the same time, without ever changing your app code! With this step-by-step guide, you can learn how to configure your Ingress controller to use {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

Check out the following diagram to see the authentication flow:

![{{site.data.keyword.appid_short_notm}} Kubernetes integration architecture](images/kube-integration.png)

1. A user opens your application and triggers a request to the web app or API.
2. For the API flow, the Ingress controller attempts to validate the supplied tokens. If the web flow is used, it kicks off a three-leg OIDC authentication process.
3. {{site.data.keyword.appid_short_notm}} begins the authentication process by displaying the Login Widget.
4. The user provides a username or email and password.
5. The Ingress controller obtains access and identity tokens from {{site.data.keyword.appid_short_notm}} for authorization.
6. Every request that is validated and forwarded by the Ingress Controller to your apps will have an authorization header that contains the tokens.

For security reasons, {{site.data.keyword.appid_short_notm}} authentication only supports backends with TLS/SSL enabled.
{: note}


## Before you Begin
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

  * [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud/cloud-cli-install_use?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)
  * [Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
  * [Docker](https://www.docker.com/products/docker-engine#/download)

* The following [{{site.data.keyword.cloud_notm}} CLI plug-ins](/docs/cli/reference/ibmcloud?topic=cloud-cli-plug-ins#plug-ins):

  * Kubernetes Service
  * Container Registry

For help getting the CLIs and plug-ins downloaded and your Kubernetes Service environment configured, check out the tutorial [creating Kubernetes clusters](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial_lesson1).
{: tip}

Let's get started!

## Step 1: Binding {{site.data.keyword.appid_short_notm}} to your cluster
{: #kube-create-appid}

You can bind your instance of {{site.data.keyword.appid_short_notm}} to your cluster in order to allow all of the instances of your app that are deployed in your cluster to use. By binding your service instance to your cluster, your {{site.data.keyword.appid_short_notm}} metadata and credentials are available as soon as your application starts as Kubernetes secrets.
{: shortdesc}


1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Follow the prompts in the CLI to complete logging in.

  ```
  ibmcloud login -a https://api.<region>.bluemix.net
  ```
  {: codeblock}

  <table>
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

  1. Get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

  2. Copy the output beginning with `export` and paste it into your terminal to set the `KUBECONFIG` environment variable.

3. Check to see if you already have an Ingress controller in your default namespace. IBM Cloud Kubernetes Service supports one Ingress per namespace. If you already have one, you can update the existing Ingress configuration or use a different namespace.

  ```
  kubectl get ingress
  ```
  {: pre}

4. Bind your instance of {{site.data.keyword.appid_short_notm}}. This creates a service key for the service instance. You can specify an existing service key by using the `-key` flag.

  ```
  ibmcloud ks cluster-service-bind --cluster <cluster_name_or_ID> --namespace <namespace> --service <App-ID_instance_name> [--key <service_instance_key>]
  ```
  {: pre}

  If you do not specify a namespace, the secret is created in the `default` namespace.
  {: tip}

  Example output:

  ```
  ibmcloud ks cluster-service-bind --cluster mycluster --namespace default --service appid1
  Binding service instance to namespace...
  OK
  Namespace:    default
  Secret name:  binding-appid1
  ```
  {: screen}

Great work!

## Step 2: Pushing your app to Container Registry
{: #kube-registry}

In order for your application to run in Kubernetes, you must host it in a registry.
{: shortdesc}


1. Sign in to the Container Registry CLI plugin.

  ```
  ibmcloud cr login
  ```
  {: pre}

2. Create a Container Registry namespace.

  ```
  ibmcloud cr namespace-add <my_namespace>
  ```
  {: pre}

3. Build, tag, and push the app as an image to your namespace in Container Registry. Be sure to include the period (.) at the end of the command.

  ```
  ibmcloud cr build -t registry.<region>.bluemix.net/<namespace>/<app-name>:<tag> .
  ```
  {: pre}

Nice! You're almost ready to deploy.

## Step 3: Configuring Ingress
{: kube-ingress}

During cluster creation, both a private and a public Ingress ALB are created for you. To deploy your application and take advantage of your Ingress controller, create a deployment script.
{: shortdesc}

1. Get the secret that was created in your cluster namespace when you bound {{site.data.keyword.appid_short_notm}} to your cluster. Note: this is **not** your Container Registry namespace.

  ```
  kubectl get secrets --namespace=<namespace>
  ```
  {: pre}

  Example output:

  ```
  NAME                       TYPE                                  DATA      AGE
  binding-appid1             Opaque                                1         1m
  bluemix-default-secret     kubernetes.io/dockercfg               1         1h
  default-token-kf97z        kubernetes.io/service-account-token   3         1h
  ```
  {: screen}

2. Use the following example `yaml` file to create your Ingress configuration. For help defining the rest of your deployment, check out [Deploying apps with the CLI](/docs/containers?topic=containers-app#app_cli).

  ```
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    name: myingress
    annotations:
      ingress.bluemix.net/appid-auth: "bindSecret=<bind_secret> namespace=<namespace> requestType=<request_type> serviceName=<myservice> [idToken=false]"
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
      <td><p>The type of request that you want to send to {{site.data.keyword.appid_short_notm}}. Options include: <code>web</code> and <code>api</code>. If you set the request type to <code>web</code>, a web request that contains an {{site.data.keyword.appid_short_notm}} access token is validated. If token validation fails, the web request is rejected. If the request does not contain an access token, then the request is redirected to the {{site.data.keyword.appid_short_notm}} login page. For {{site.data.keyword.appid_short_notm}} web authentication to work, cookies must be enabled in the user's browser.</p><p>If you set the request type to <code>api</code>, an API request that contains an {{site.data.keyword.appid_short_notm}} access token is validated. If the request does not contain an access token, a 401: Unauthorized error message is returned to the user.</p></td>
    </tr>
    <tr>
      <td><code>serviceName</code></td>
      <td><p>Required: The name of the Kubernetes service that you created for your app. If a service name is not included, the annotation is enabled for all services.</p> <p>To use multiple request types in the same cluster, configure an instance of {{site.data.keyword.appid_short_notm}} to use <code>web</code> and another to use <code>api</code>.</p></td>
    </tr>
    <tr>
      <td><code>idToken</code></td>
      <td>Optional: The Liberty OIDC client is unable to parse both the access and the identity token at the same time. When working with Liberty, set this value to <code>false</code> so that the identity token is not sent to the Liberty server.</td>
    </tr>
    <tr>
      <td><code>secretName</code></td>
      <td>The TLS secret that is associated with your TLS certificate. If your certificate is hosted in IBM Cloud Certificate Manager, you can run <code>ibmcloud ks alb-cert-deploy --secret-name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn></code> to deploy it to your cluster. If you do not have a certificate, complete step 3 of [Exposing apps with Ingress](/docs/containers?topic=containers-ingress#ingress_expose_public).</td>
    </tr>
  </table>

3. Run the configuration file.

  ```
  kubectl apply -f <file-name>.yaml
  ```
  {: pre}

Great work!


## Step 4: Adding your redirect URLs
{: #kube-add-redirect}

A redirect URL is the URL for the site that you want {{site.data.keyword.appid_short_notm}} to send your users to after successful authentication.
{: shortdesc}

1. Navigate to the {{site.data.keyword.cloud_notm}} GUI and open your {{site.data.keyword.appid_short_notm}} dashboard.

2. In **Identity Providers > Manage**, set the providers that you want to use to **On**. If a provider is not enabled, then users are issued an access token that provides anonymous access to your app.

3. Click **Authentication Settings**.

4. Click the **+** symbol in the **Add web redirect URLs** box.

  * Custom domain:

    A URL that is registered with a custom domain might look like: `http://mydomain.net/myapp2path/appid_callback`. If the apps that you want Ingress to expose are in different namespaces in one cluster, you can use a wildcard, such as `https://custom_domain.net/*` to specify all of the apps in the cluster at once. This can be helpful during development, but should be used with caution in production.

  * Ingress subdomain:

    If your app is registered with an IBM Ingress subdomain, your callback URL might look like: `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback`

{{site.data.keyword.appid_short_notm}} offers a logout function: If `/logout` exists in your {{site.data.keyword.appid_short_notm}} path, cookies are removed and the user is sent back to the login page. To use this function, append `/appid_logout` to your domain in the format `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_logout` and include it in your redirect URLs.
{: note}


Excellent work! Now, you can verify that the deployment was successful by navigating to your Ingress subdomain or custom domain to try it out.


## Next steps
{: #kube-next}

Now that your application is running in a Kubernetes cluster and Ingress is configured, you can try:

* Using custom attributes to [set roles](/docs/services/appid?topic=appid-tutorial-roles)
* Configuring [multi-factor authentication](/docs/services/appid?topic=appid-cd-mfa)
* Customizing the [Login Widget](/docs/services/appid?topic=appid-login-widget)



