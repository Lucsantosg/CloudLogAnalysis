---

copyright:
  years: 2017

lastupdated: "2017-11-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Enabling automatic collection of cluster logs
{: #containers_kube_other_logs}

To be able to view and analyse cluster logs in the {{site.data.keyword.loganalysisshort}} service, you must configure your cluster to forward those logs to the {{site.data.keyword.loganalysisshort}} service. 
{:shortdesc}

## Step 1: Check permissions
{: step1}

Only users with an IAM policy for the {{site.data.keyword.containershort}} with permissions to manage clusters can enable this feature. Any of the following roles is required: *Administrator*, *Operator*

To check that your user ID has an IAM policy assigned to manage clusters, complete the following steps:

**Note:** Only the account owner or users with permissions to assign policies can perform this step.

1. Log in to the {{site.data.keyword.Bluemix_notm}} console. Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. From the menu bar, click **Manage > Account > Users**.  The *Users* window displays a list of users with their email addresses for the currently selected account.
	
3. Select the userID, and verify that it has a policy for the {{site.data.keyword.containershort}}.

## Step 2: Setup the cluster context.
{: #step2}

Complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Initialize the {{site.data.keyword.loganalysisshort}} service plug-in.

	```
	bx cs init
	```
	{: codeblock}

3. Set your terminal context to your cluster.
    
	```
	bx cs cluster-config MyCluster
	```
	{: codeblock}

    The output of running this command provides the command that you must run in your terminal to set the path to your configuration file. For example:

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

4. Copy and paste the command to set the environment variable in your terminal, and then press **Enter**.

## Step 3: Configure your cluster
{: step3}

You can choose which cluster logs you forward to the {{site.data.keyword.loganalysisshort}} service. 

* To enable automatic log collection and forwarding of application logs, see [Enabling automatic log collection and forwarding of application logs](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#apps).
* To enable automatic log collection and forwarding of worker logs, see [Enabling automatic log collection and forwarding of worker logs](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#workers).
* To enable automatic log collection and forwarding of the Kubernetes system component logs, see [Enabling automatic log collection and forwarding of the Kubernetes system component logs](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#system).
* To enable automatic log collection and forwarding of the Kubernetes ingress controller logs, see [Enabling automatic log collection and forwarding of the Kubernetes ingress controller logs](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#controller).

## Enabling automatic log collection and forwarding of application logs 
{: #apps}

Run the following command to send */var/log/apps/**/.log* and */var/log/apps/*/.err* log files to the {{site.data.keyword.loganalysisshort}} service:

```
bx cs logging-config-create ClusterName --logsource application --type ibm
```
{: codeblock}

where *ClusterName* is the name of the cluster.

For example, 

```
bx cs logging-config-create MyCluster --logsource application --type ibm
```
{: screen}

## Enabling automatic log collection and forwarding of worker logs 
{: #workers}


Run the following command to send */var/log/syslog* and */var/log/auth.log* log files to the {{site.data.keyword.loganalysisshort}} service:

```
bx cs logging-config-create ClusterName --logsource worker --type ibm
```
{: codeblock}

where *ClusterName* is the name of the cluster.

For example:

```
bx cs logging-config-create MyCluster --logsource worker  --type ibm
```
{: screen}


## Enabling automatic log collection and forwarding of the Kubernetes system component logs
{: #system}

Run the following command to send */var/log/kubelet.log* and */var/log/kube-proxy.log* log files to the {{site.data.keyword.loganalysisshort}} service:

```
bx cs logging-config-create ClusterName --logsource kubernetes --type ibm
```
{: codeblock}

where *ClusterName* is the name of the cluster.

For example:

```
bx cs logging-config-create MyCluster --logsource kubernetes --type ibm
```
{: screen}


## Enabling automatic log collection and forwarding of the Kubernetes ingress controller logs
{: #controller}

Run the following command to send */var/log/alb/ids/.log*, */var/log/alb/ids/.err*, */var/log/alb/customerlogs/.log*, and /var/log/alb/customerlogs/.err* log files to the {{site.data.keyword.loganalysisshort}} service:

```
bx cs logging-config-create ClusterName --logsource ingress --type ibm
```
{: codeblock}

where *ClusterName* is the name of the cluster.

For example:

```
bx cs logging-config-create MyLoggingDemoCluster --logsource ingress --type ibm
```
{: screen}


