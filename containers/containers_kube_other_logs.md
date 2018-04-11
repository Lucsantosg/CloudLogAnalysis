---

copyright:
  years: 2017, 2018

lastupdated: "2018-03-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Enabling automatic collection of cluster logs
{: #containers_kube_other_logs}

To be able to view and analyse cluster logs in the {{site.data.keyword.loganalysisshort}} service, you must configure your cluster to forward those logs to the {{site.data.keyword.loganalysisshort}} service. 
{:shortdesc}

## Step 1: Check permissions for your user ID
{: step1}

Your user ID must have the following permissions so you can add a logging configuration to the cluster:

* IAM policy for the {{site.data.keyword.containershort}} with **Viewer** permissions.
* IAM policy for the cluster instance with **Administrator** or **Operator** permissions.

To check that your user ID has these IAM policies, complete the following steps:

**Note:** Only the account owner or users with permissions to assign policies can perform this step.

1. Log in to the {{site.data.keyword.Bluemix_notm}} console. Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. From the menu bar, click **Manage > Account > Users**.  The *Users* window displays a list of users with their email addresses for the currently selected account.
	
3. Select the userID, and verify that the user ID has both policies.




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
	bx cs cluster-config ClusterName
	```
	{: codeblock}

    The output of running this command provides the command that you must run in your terminal to set the path to your configuration file. For example, for a cluster named *MyCluster*:

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

4. Copy and paste the command to set the environment variable in your terminal, and then press **Enter**.



## Step 3: Configure your cluster
{: step3}

You can choose which cluster logs you forward to the {{site.data.keyword.loganalysisshort}} service. 

* To enable automatic log collection and forwarding of stdout and stderr, see [Enabling automatic log collection and forwarding of container logs](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#containers).
* To enable automatic log collection and forwarding of application logs, see [Enabling automatic log collection and forwarding of application logs](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#apps).
* To enable automatic log collection and forwarding of worker logs, see [Enabling automatic log collection and forwarding of worker logs](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#workers).
* To enable automatic log collection and forwarding of the Kubernetes system component logs, see [Enabling automatic log collection and forwarding of the Kubernetes system component logs](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#system).
* To enable automatic log collection and forwarding of the Kubernetes ingress controller logs, see [Enabling automatic log collection and forwarding of the Kubernetes ingress controller logs](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#controller).



## Step 4: Set permissions for the {{site.data.keyword.containershort_notm}} key owner
{: #step4}


The {{site.data.keyword.containershort}} key owner needs the following AIM policies:

* IAM policy for the {{site.data.keyword.containershort}} with **Administartor** role.
* IAM policy for the {{site.data.keyword.loganalysisshort}} service with **Administrator** role.

Complete the following steps: 

1. Log in to the {{site.data.keyword.Bluemix_notm}} console. Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. From the menu bar, click **Manage > Account > Users**.  The *Users* window displays a list of users with their email addresses for the currently selected account.
	
3. Select the userID for the {{site.data.keyword.containershort_notm}} key owner, and verify that the user ID has both policies.


When you forward logs to a space domain, you must also grant Cloud Foundry (CF) permissions to the {{site.data.keyword.containershort}} key owner in the organization and space. The key owner needs *orgManager* role for the organization, and *SpaceManager* or *Developer* for the space.

Complete the following steps:

1. Identify the user in the account that is the {{site.data.keyword.containershort}} key owner. From a terminal, run the following command:

    ```
    bx cs api-key-info ClusterName
    ```
    {: codeblock}
    
    where *ClusterName* is the name of the cluster.
    
2. Verify that the user that is identified as the {{site.data.keyword.containershort}} key owner has the *orgManager* role for the organization, and *SpaceManager* and *Developer* for the space.

    Log in to the {{site.data.keyword.Bluemix_notm}} console. Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window} After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

    From the menu bar, click **Manage > Account > Users**.  The *Users* window displays a list of users with their email addresses for the currently selected account.
	
    Select the ID of the user, and verify that the user has the *orgManager* role for the organization, and *SpaceManager* or *Developer* for the space.
 
3. If the user does not have the correct permissions, complete the following steps:

    1. Grant the user the following permissions: *orgManager* role for the organization, and *SpaceManager* and *Developer* for the space. For more information, see [Granting a user permissions to view space logs by using the IBM Cloud UI](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_space).
    
    2. Refresh the logging configuration. Run the following command:
    
        ```
        bx cs logging-config-refresh ClusterName
        ```
        {: codeblock}
        
        where *ClusterName* is the name of the cluster.
  




## Enabling automatic log collection and forwarding of container logs 
{: #containers}

Run the following command to send *stdout* and *stderr* log files to the {{site.data.keyword.loganalysisshort}} service:

```
bx cs logging-config-create ClusterName --logsource container --namespace '*' --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

where 

* *ClusterName* is the name of the cluster.
* *EndPoint* is the URL to the logging service in the region where the {{site.data.keyword.loganalysisshort}} service is provisioned. For a list of endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls).
* *OrgName* is the name of the organization where the space is available.
* *SpaceName* is the name of the space where the {{site.data.keyword.loganalysisshort}} service is provisioned.


For example, to create a logging configuration that forwards stdout and stderr logs to the account domain in the German region, run the following command:

```
bx cs logging-config-create MyCluster --logsource container --type ibm --namespace '*' --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}

To create a logging configuration that forwards stdout and stderr logs to a space domain in the German region, run the following command:

```
bx cs logging-config-create MyCluster --logsource container --type ibm --namespace '*' --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org MyOrg --space MySpace
```
{: screen}



## Enabling automatic log collection and forwarding of application logs 
{: #apps}

Run the following command to send */var/log/apps/**/.log* and */var/log/apps/*/.err* log files to the {{site.data.keyword.loganalysisshort}} service:

```
bx cs logging-config-create ClusterName --logsource application --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName --app-containers --app-paths
```
{: codeblock}

where 

* *ClusterName* is the name of the cluster.
* *EndPoint* is the URL to the logging service in the region where the {{site.data.keyword.loganalysisshort}} service is provisioned. For a list of endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls).
* *OrgName* is the name of the organization where the space is available.
* *SpaceName* is the name of the space where the {{site.data.keyword.loganalysisshort}} service is provisioned.
* *app-containers* is an optional parameter that you can set to define a list of containers that you want to watch. These containers are the only ones from where logs will be forwarded into {{site.data.keyword.loganalysisshort}}. You can set one or more containers by separting them with commas.
* *app-paths* define the paths inside containers that you want to watch. You can set one or more paths separating them with commas. Wildcards such as '/var/log/*.log' are accepted. 

For example, to create a logging configuration that forwards application logs to a space domain in the German region, run the following command:

```
bx cs logging-config-create MyCluster --logsource application --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org MyOrg --space MySpace --app-paths /var/log/*.log
```
{: screen}

For example, to create a logging configuration that forwards application logs to the account domain in the German region, run the following command:

```
bx cs logging-config-create MyCluster --logsource application --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --app-paths /var/log/*.log
```
{: screen}



## Enabling automatic log collection and forwarding of worker logs 
{: #workers}


Run the following command to send */var/log/syslog* and */var/log/auth.log* log files to the {{site.data.keyword.loganalysisshort}} service:

```
bx cs logging-config-create ClusterName --logsource worker --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

where 

* *ClusterName* is the name of the cluster.
* *EndPoint* is the URL to the logging service in the region where the {{site.data.keyword.loganalysisshort}} service is provisioned. For a list of endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls).
* *OrgName* is the name of the organization where the space is available.
* *SpaceName* is the name of the space where the {{site.data.keyword.loganalysisshort}} service is provisioned.



For example, to create a logging configuration that forwards worker logs to a space domain in the German region, run the following command:

```
bx cs logging-config-create MyCluster --logsource worker  --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org OrgName --space SpaceName 
```
{: screen}

For example, to create a logging configuration that forwards worker logs to the account domain in the German region, run the following command:

```
bx cs logging-config-create MyCluster --logsource worker  --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}



## Enabling automatic log collection and forwarding of the Kubernetes system component logs
{: #system}

Run the following command to send */var/log/kubelet.log* and */var/log/kube-proxy.log* log files to the {{site.data.keyword.loganalysisshort}} service:

```
bx cs logging-config-create ClusterName --logsource kubernetes --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

where 

* *ClusterName* is the name of the cluster.
* *EndPoint* is the URL to the logging service in the region where the {{site.data.keyword.loganalysisshort}} service is provisioned. For a list of endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls).
* *OrgName* is the name of the organization where the space is available.
* *SpaceName* is the name of the space where the {{site.data.keyword.loganalysisshort}} service is provisioned.



For example, to create a logging configuration that forwards Kubernetes system component logs to a space domain in the German region, run the following command:

```
bx cs logging-config-create MyCluster --logsource kubernetes --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org OrgName --space SpaceName 
```
{: screen}

For example, to create a logging configuration that forwards Kubernetes system component logs to the account domain in the German region, run the following command:

```
bx cs logging-config-create MyCluster --logsource kubernetes --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}



## Enabling automatic log collection and forwarding of the Kubernetes ingress controller logs
{: #controller}

Run the following command to send */var/log/alb/ids/.log*, */var/log/alb/ids/.err*, */var/log/alb/customerlogs/.log*, and /var/log/alb/customerlogs/.err* log files to the {{site.data.keyword.loganalysisshort}} service:

```
bx cs logging-config-create ClusterName --logsource ingress --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName s
```
{: codeblock}

where 

* *ClusterName* is the name of the cluster.
* *EndPoint* is the URL to the logging service in the region where the {{site.data.keyword.loganalysisshort}} service is provisioned. For a list of endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls).
* *OrgName* is the name of the organization where the space is available.
* *SpaceName* is the name of the space where the {{site.data.keyword.loganalysisshort}} service is provisioned.



For example, to create a logging configuration that forwards ingress controller logs to a space domain in the German region, run the following command:

```
bx cs logging-config-create MyLoggingDemoCluster --logsource ingress --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org OrgName --space SpaceName 
```
{: screen}

For example, to create a logging configuration that forwards ingress controller logs to the account domain in the German region, run the following command:

```
bx cs logging-config-create MyLoggingDemoCluster --logsource ingress --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091  
```
{: screen}



