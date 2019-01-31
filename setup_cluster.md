---

copyright:
  years: 2019
lastupdated: "2019-01-31"

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

# Setting up Network Analytics (beta)
{: #cluster-install}

You can try out the network analytics feature of the service by installing a {{site.data.keyword.security-advisor_short}} in to a {{site.data.keyword.containerlong_notm}} cluster.
{: shortdesc}

Network Analytics is a preview feature that is available only in the US-South region.
{: note}

When you set up {{site.data.keyword.security-advisor_short}} in a cluster, the following actions take place:

* Cluster metadata is collected and used to complete the installation of worker node IP addresses, subnets, Ingress URL and IP address, cluster CRN, Log Analysis endpoint, space, and token.
* An Identity and Access Management (IAM) service ID and API key are generated in your {{site.data.keyword.Bluemix_notm}} account so that your cluster can be identified by {{site.data.keyword.security-advisor_short}}.
* {{site.data.keyword.security-advisor_short}} components are deployed in the **monitoring** namespace in your cluster.

If you have more than one cluster, be sure to run the installation for each cluster to generate service IDs and API keys for each cluster.


Want to learn more about how network analytics work in {{site.data.keyword.security-advisor_short}}? [Check out the docs](network-analytics.html).
{: tip}

</br>

## Prerequisites
{: #cluster_prereqs}

Before you begin, be sure you have the following prerequisites in place.
{: shortdesc}

The account owner must complete the installation steps. If that is not you, check to see who the owner of your {{site.data.keyword.Bluemix_notm}} account is and have them assist with the install.
{: tip}

Then, be sure you have the following prerequisites:

* A Mac, Linux, or [Windows 10](https://win10faq.com/install-run-ubuntu-bash-windows-10/) developer workstation.
* [Node.js](https://nodejs.org/en/) 6 or higher
* [jQ](https://stedolan.github.io/jq/download/)
* The required CLIs and plugins in the minimum required version:
  * [{{site.data.keyword.Bluemix_notm}} CLI](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started) v0.6.5 or higher
  * [Kubernetes CLI (kubectl)](https://kubernetes.io/docs/tasks/tools/install-kubectl/) v1.7 or higher</br> The installer has been tested with the {{site.data.keyword.containerlong_notm}} default stable version `v1.10.11`. The installer has not been tested with `v1.11.5` or the latest version `v1.12.3`.
  * [{{site.data.keyword.containerlong_notm}} plug-in](https://console.bluemix.net/docs/containers/cs_cli_install.html#cs_cli_install)
  * [Kubernetes Helm (package manager)](https://docs.helm.sh/using_helm/#from-script)
* [A free or standard Kubernetes cluster](https://console.bluemix.net/containers-kubernetes/catalog/cluster) in the **US South** {{site.data.keyword.Bluemix_notm}} region

Need help creating and configuring a cluster? Try running through this [tutorial](/docs/containers/cs_tutorials.html#cs_cluster_tutorial).
{: tip}

</br>

## Setting up Helm
{: #setup-helm}

1.  Log in to {{site.data.keyword.Bluemix_notm}}.

  ```
  ibmcloud login -a https://api.ng.bluemix.net --sso
  ```
  {: pre}

2.  List all of the clusters in the account to get the name of the cluster that you want to work with.

  ```
  ibmcloud ks clusters
  ```
  {: pre}

3.  Target your CLI to the cluster.

  1. Run the following command to configure the cluster. You are going to use the output in the next step.

    ```
    ibmcloud ks cluster-config <cluster-name-or-id>
    ```
    {: pre}

  2. Use the output of the previous command to set the path to the local Kubernetes configuration file as an environment variable.

  Example:

    ```
    export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/container-service/clusters/<cluster_name>/kube-config-prod-dal10-<cluster_name>.yml
    ```
    {: screen}

4.  Install tiller to your cluster so that you can work with Helm charts.

  ```
  helm init
  ```
  {: pre}

Be sure to keep this command line window open as you continue.
{: tip}

</br>

## Installing {{site.data.keyword.security-advisor_short}} components
{: #cluster-components}

After your cluster is configured to work with Helm, you can install {{site.data.keyword.security-advisor_short}} components.
{: shortdesc}


To install the components continue in the same CLI window and complete the following steps:

1. Download and extract the [installation package](https://github.com/IBM-Bluemix-Docs/security-advisor/blob/master/installation.tar.gz?raw=true).
2. Continuing in the same CLI window from the previous section, navigate to the extracted archive location and install the package.

  ```
  ./install.sh
  ```
  {: pre}

3.  Verify that the components are properly installed by checking the [{{site.data.keyword.security-advisor_short}} dashboard](https://console.bluemix.net/security-advisor/#/dashboard).

</br>

## Removing {{site.data.keyword.security-advisor_short}} components
{: #cluster-uninstall}

Remove the {{site.data.keyword.security-advisor_short}} components from your cluster and the service ID and API key from your {{site.data.keyword.Bluemix_notm}} account.

1. Log in to {{site.data.keyword.Bluemix_notm}}.

  ```
  ibmcloud login -a https://api.ng.bluemix.net --sso
  ```
  {: pre}

2. List all of the clusters in the account to get the name of the cluster.

  ```
  ibmcloud ks clusters
  ```
  {: pre}

3. Target your CLI to the cluster.

  ```
  ibmcloud ks cluster-config <cluster-name-or-id>
  ```
  {: pre}

4. Set the path to the local Kubernetes configuration file as an environment variable. Example:

  ```
  export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/container-service/clusters/<cluster_name>/kube-config-prod-dal10-<cluster_name>.yml
  ```
  {: pre}

5. Navigate to the extracted archive location and run the uninstaller script.

  ```
  ./uninstall.sh
  ```
  {: pre}

6. Optional: Uninstall the Helm server component from the cluster.

  ```
  helm reset
  ```
  {: pre}
