---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, logging

subcollection: cloudloganalysis

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}


# {{site.data.keyword.containershort_notm}}
{: #containers_kubernetes}

In the {{site.data.keyword.cloud_notm}}, you can use the {{site.data.keyword.loganalysisshort}} service to store and analyze container logs and Kubernetes cluster logs that are collected automatically by the {{site.data.keyword.containershort}} in Public, and in Dedicated.
{:shortdesc}

You can have 1 or more Kubernetes clusters in an account. Logs are collected automatically by the {{site.data.keyword.containershort}} as soon as the cluster is provisioned. 

To forward logs to the {{site.data.keyword.loganalysisshort}} from {{site.data.keyword.containershort}} you must create a logging configuration. You can enable logging through the [command line](/docs/containers/cs_health.html#logging), or through the cluster overview page in your {{site.data.keyword.containershort}} dashboard. With a configuration in place, logs are collected by {{site.data.keyword.containershort}} when the cluster is provisioned, or as soon as a pod is deployed. Information that a container prints to `stdout` or `stderr` is also automatically collected. By default, logs are forwarded to specific regions based on the location of the cluster.

* Application logs are collected as soon as the pod is deployed. 
* Information, that a container process prints to stdout (standard output) and stderr (standard error), is collected automatically by the {{site.data.keyword.containershort}}.

Check out the following table to see which regions that  {{site.data.keyword.loganalysisshort}} sends logs to depending on where the cluster is deployed.
 * Information, that a container process prints to stdout (standard output) and stderr (standard error), is collected automatically by the {{site.data.keyword.containershort}}.
 
 <table>
   <tr>
     <th>Cluster region</th>
     <th>Service region</th>
   </tr>
   <tr>
     <td>US South</td>
     <td>US South</td>
   </tr>
   <tr>
     <td>US East</td>
     <td>US South</td>
   </tr>
   <tr>
     <td>Germany</td>
     <td>Germany</td>
   </tr>
   <tr>
     <td>Sydney</td>
     <td>Sydney</td>
   </tr>
   <tr>
     <td>United Kingdom</td>
     <td>Germany</td>
   </tr>
 </table>
 
 Be sure to target the correct region, org, and space when attempting to view logs. You might also check that you're targeting the correct org and space through the {{site.data.keyword.loganalysisshort}} GUI.
 {: tip}

You can forward logs to the {{site.data.keyword.loganalysisshort}} account or space domain in your account. Consider the following information when deciding where to forward logs:

* When you send logs to the account domain, the search quota is 500MB per day, and you cannot store logs in Log Collection for long term storage.
* When you send logs to a space domain, you can choose a {{site.data.keyword.loganalysisshort}} service plan that defines the search quota per day, and a you can store logs in Log Collection for long term storage.

**Note:** By default, sending logs from a cluster to the {{site.data.keyword.loganalysisshort}} service is not automatically enabled. To enable logging, you must create one or more logging configurations in the cluster to automatically forward logs into the {{site.data.keyword.loganalysisshort}} service. You can enable logging through the command line, by using the `ibmcloud cs logging-config-create` command, or through the cluster dashboard available in the {{site.data.keyword.cloud_notm}} UI. For more information, see [Enabling automatic collection of cluster logs](/docs/services/CloudLogAnalysis/containers?topic=cloudloganalysis-containers_kube_other_logs#containers_kube_other_logs).

When you work with a Kubernetes cluster, the namespaces *ibm-system* and *kube-system* are reserved. Do not create, delete, modify, or change permissions of resources that are available in these namespaces. Logs for these namespaces are for {{site.data.keyword.IBM_notm}} use.
{: tip}



### Forwarding logs to a space domain
{: #space}

When you configure your cluster to forward logs into {{site.data.keyword.loganalysisshort}}, consider the following information:

* You must define a Cloud Foundry organization and space where those logs will be forwarded. 
* The organization and space can be available in any {{site.data.keyword.IBM_notm}} Public Cloud region.

**Note:** For clusters that are provisioned on **{{site.data.keyword.cloud_notm}} Dedicated**, it is not possible to configure your cluster to forward cluster logs to Cloud Foundry spaces that are available on your dedicated account.

To analyze log data in Kibana for a cluster that forwards logs to a space domain, consider the following information:

* You must launch Kibana in the Public region where the organization and the space collecting the cluster logs are available.
* To increase your Kibana search quota and store logs in Log Collection for long-term storage, you must provision the {{site.data.keyword.loganalysisshort}} service in the space where logs are being forwarded with a plan that meets your requirements. 
* Your user ID must have permissions to view logs. To see logs in the space domain, a user needs a CF role. **Auditor** is the lowest role that can be granted to view logs. For more information, see [Roles that are required by a user to view logs](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analyzing_logs_Kibana#roles).

To manage cluster log data that is stored in long-term storage (Log Collection), you user ID must have an IAM policy to work with the {{site.data.keyword.loganalysisshort}} service. Your user ID must have **Administrator**, **Operator**, or **Editor** permissions.  For more information, see [Roles that are required by a user to manage logs](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-manage_logs#roles1).


The following figure shows a high level view of logging in Public for the {{site.data.keyword.containershort}} when the cluster forwards logs to a space domain:

![High level component overview for containers deployed in a Kubernetes cluster](images/containers_kube_1.png "High level component overview for containers deployed in a Kubernetes cluster")

   

### Forwarding logs to the account domain
{: #acc_public}

You can configure your cluster to forward logs to the account domain whether your account is in the {{site.data.keyword.cloud_notm}} public or dedicated environment.
{: shortdesc}


To analyze log data in Kibana for a cluster that forwards logs to the account domain, consider the following information:

* You must launch Kibana in the region in which the cluster is sending logs to the {{site.data.keyword.loganalysisshort}} service.
* To manage cluster log data that is stored in long-term in Log Collection, you must have an IAM role that allows you to work with the {{site.data.keyword.loganalysisshort}} service. Your user ID must have **Administrator**, **Operator**, or **Editor** permissions. To see logs, you need **Viewer** permissions.


In the following image, you can see a high level view of how forwarding logs to an account works in a public environment.

![High level component overview for containers deployed in a Kubernetes cluster](images/containers_kube.png "High level component overview for containers deployed in a Kubernetes cluster")

In the following image, you can see a high-level view of how forwarding logs to an account works in a dedicated environment.

![High level component overview for containers deployed in a Kubernetes cluster](images/containers_kube_dedicated.png "High level component overview for containers deployed in a Kubernetes cluster")



## Configuring a cluster to forwards logs into {{site.data.keyword.loganalysisshort}}
{: #config_forward_logs}

You can choose which cluster logs to forward to the {{site.data.keyword.loganalysisshort}} service. 

For more information about how to configure your cluster to forward log files to the {{site.data.keyword.loganalysisshort}} service, see the section [Enabling automatic collection of cluster logs](/docs/services/CloudLogAnalysis/containers?topic=cloudloganalysis-containers_kube_other_logs#containers_kube_other_logs).

* To enable automatic log collection and forwarding of stdout and stderr, see [Enabling automatic log collection and forwarding of container logs](/docs/services/CloudLogAnalysis/containers?topic=cloudloganalysis-containers_kube_other_logs#containers).
* To enable automatic log collection and forwarding of application logs, see [Enabling automatic log collection and forwarding of application logs](/docs/services/CloudLogAnalysis/containers?topic=cloudloganalysis-containers_kube_other_logs#apps). 
* To enable automatic log collection and forwarding of worker logs, see [Enabling automatic log collection and forwarding of worker logs](/docs/services/CloudLogAnalysis/containers?topic=cloudloganalysis-containers_kube_other_logs#workers). 
* To enable automatic log collection and forwarding of the Kubernetes system component logs, see [Enabling automatic log collection and forwarding of the Kubernetes system component logs](/docs/services/CloudLogAnalysis/containers?topic=cloudloganalysis-containers_kube_other_logs#system). 
* To enable automatic log collection and forwarding of the Kubernetes ingress controller logs, see [Enabling automatic log collection and forwarding of the Kubernetes ingress controller logs](/docs/services/CloudLogAnalysis/containers?topic=cloudloganalysis-containers_kube_other_logs#controller).





## Configuring network traffic for custom firewall configurations in the {{site.data.keyword.cloud_notm}}
{: #ports}

When you have an additional firewall set up, or you have customized the firewall settings in your {{site.data.keyword.cloud_notm}} infrastructure (SoftLayer), you must allow outgoing network traffic from the worker node to the {{site.data.keyword.loganalysisshort}} service.

You must open TCP port 443 and TCP port 9091 from each worker to the {{site.data.keyword.loganalysisshort}} service for the following IP addresses in your customized firewall:

<table>
  <tr>
    <th>Region</th>
    <th>Ingestion URL</th>
	<th>Public IP addresses</th>
  </tr>
  <tr>
    <td>Germany</td>
	<td>ingest-eu-fra.logging.bluemix.net</td>
	<td>158.177.88.43 <br>159.122.87.107</td>
  </tr>
  <tr>
    <td>United Kingdom</td>
	<td>ingest.logging.eu-gb.bluemix.net</td>
	<td>169.50.115.113</td>
  </tr>
  <tr>
    <td>US South</td>
	<td>ingest.logging.ng.bluemix.net</td>
	<td>169.48.79.236 <br>169.46.186.113</td>
  </tr>
  <tr>
    <td>Sydney</td>
	<td>ingest-au-syd.logging.bluemix.net</td>
	<td>130.198.76.125 <br>168.1.209.20</td>
  </tr>
</table>


## Forwarding custom application logs
{: #forward_app_logs}

To enable log forwarding of custom application logs in a cluster to the {{site.data.keyword.loganalysisshort}} service, you must define a cluster logging configuration with **Log source** set to **application**. You can define this configuration by using the `ibmcloud cs logging-config-create` command or through the cluster UI.

When you configure the cluster to forward custom logs, you can specify a list of containers running in your cluster from which you want to forward custom logs, and the paths inside those containers where custom file logs are located.

* You must specify the **app-paths** parameter to set the list of paths inside containers that you want to watch. Logs located in these paths are forwarded to the {{site.data.keyword.loganalysisshort}} service. 

    To set this parameter, define a comma separated list of paths that are available inside your containers. Wildcards such as '/var/log/*.log' are accepted.

* Optionally, you can can set the **app-containers** parameter to specify the list of containers from where to collect and forward logs to the {{site.data.keyword.loganalysisshort}} service.

    To set this parameter, define a comma separated list of containers.

**Tip:** You can define multiple cluster logging configurations with **Log source** set to **application** in a cluster. If containers in a cluster have different paths where logs are hosted, consider defining a cluster logging configuration for each group of containers whose logs are located on the same path. 



## Log Sources
{: #log_sources}


You can configure your cluster to forward logs to the {{site.data.keyword.loganalysisshort}} service. The following table lists the different log sources that you can enable to forward logs into the {{site.data.keyword.loganalysisshort}} service:

<table>
  <caption>Log sources for a Kuberenetes cluster</caption>
  <tr>
    <th>Log source</th>
	<th>Description</th>
	<th>Log Paths</th>
  </tr>
  <tr>
    <td>Container</td>
	<td>Container logs.</td>
	<td>Standard output (stdout) and standard erro (stderr) logs.</td>
  </tr>
  <tr>
    <td>Application</td>
	<td>Logs for your own application that runs in a Kubernetes cluster.</td>
	<td>`/var/log/apps/**/*.log`  </br>`/var/log/apps/**/*.err`</br>**NOTE:** On a pod, logs can be written in `/var/logs/apps/` or in any subdirectory under `/var/logs/apps/`. On the worker, you must mount `/var/log/apps/` to the directory in the pod where your app is writing logs in the pod.</td>
  </tr>
  <tr>
    <td>Worker</td>
	<td>Logs for virtual machine worker nodes within a Kubernetes cluster. </td>
	<td>`/var/log/syslog` </br>`/var/log/auth.log`</td>
  </tr>
  <tr>
    <td>Kubernetes system component</td>
	<td>Logs for the Kubernetes system component.</td>
	<td>*/var/log/kubelet.log* </br>*/var/log/kube-proxy.log*</td>
  </tr>
  <tr>
    <td>Ingress controller</td>
	<td>Logs for an Ingress controller that manages network traffic coming into a Kubernetes cluster.</td>
	<td>`/var/log/alb/ids/*.log` </br>`/var/log/alb/ids/*.err` </br>`/var/log/alb/customerlogs/*.log` </br>`/var/log/alb/customerlogs/*.err`</td>
  </tr>
</table>

## Searching logs
{: #log_search}

By default, you can use Kibana to search up to 500 MB of logs per day in the {{site.data.keyword.cloud_notm}}. 

To search for larger logs, you can use the {{site.data.keyword.loganalysisshort}} service. The service provides multiple plans. Each plan has different log search capabilities, for example, the *Log Collection* plan allows you to search up to 1 GB of data per day. For more information about the plans that are available, see [Service plans](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#plans).

When you search your logs, consider the following fields that are available in Kibana:

Fields that are common to any log entry:

<table>
  <caption>List of common fields</caption>
  <tr>
    <th>Field name</th>
	  <th>Description</th>
	  <th>Value</th>
  </tr>
  <tr>
    <td>ibm-containers.region_str</td>
	  <td>Region where the cluster is available</td>
	  <td>For example, `us-south` is the value for a cluster that is available in the US South region.</td>
  </tr>
  <tr>
    <td>ibm-containers.account_id_str</td>
	  <td>Account ID</td>
	  <td></td>
  </tr>
  <tr>
    <td>ibm-containers.cluster_id_str</td>
	  <td>Cluster ID</td>
	  <td></td>
	</tr>
  <tr>
    <td>ibm-containers.cluster_name_str</td>
	  <td>Cluster name</td>
	  <td></td>
  </tr>
</table>

Fields that might be useful when analyzing container stdout and stderr logs:

<table>
  <caption>List of fields for applications</caption>
  <tr>
    <th>Field name</th>
	<th>Description</th>
	<th>Value</th>
  </tr>
  <tr>
    <td>kubernetes.container_name_str</td>
	<td>Name of the container</td>
	<td></td>
  </tr>
  <tr>
    <td>kubernetes.namespace_name_str</td>
	<td>Namespace name where the application is running in the cluster</td>
	<td></td>
  </tr>
  <tr>
    <td>stream_str</td>
	<td>Type of log</td>
	<td>*stdout* </br>*stderr*</td>
  </tr>
</table>

Fields that might be useful when analyzing worker logs:

<table>
  <caption>List of fields that are relevant to workers</caption>
  <tr>
    <th>Field name</th>
	<th>Description</th>
	<th>Value</th>
  </tr>
  
  <tr>
    <td>filename_str</td>
	<td>Path and name of the file</td>
	<td>*/var/log/syslog*  </br>*/var/log/auth.log*</td>
  </tr>
  <tr>
    <td>tag_str</td>
	<td>Type of log</td>
	<td>*logfiles.worker.var.log.syslog* </br>*logfiles.worker.var.log.auth.log*</td>
  </tr>
  <tr>
    <td>worker_str</td>
	<td>Worker name</td>
	<td>For example, *w1*</td>
  </tr>
</table>

Fields that might be useful when analyzing Kubernetes system component logs:

<table>
  <caption>List of fields that are relevant to the Kubernetes system component</caption>
  <tr>
    <th>Field name</th>
	<th>Description</th>
	<th>Value</th>
  </tr>
  <tr>
    <td>tag_str</td>
	<td>Type of log</td>
	<td>*logfiles.kubernetes.var.log.kubelet.log* </br>*logfiles.kubernetes.var.log.kube-proxy.log*</td>
  </tr>
  <tr>
    <td>filename_str</td>
	<td>Path and name of the file</td>
	<td>*/var/log/kubelet.log* </br>*/var/log/kube-proxy.log*</td>
  </tr>
 </table>

Fields that might be useful when analyzing Ingress controller logs:
 
<table>
  <caption>List of fields that are relevant to the Ingress controller</caption>
  <tr>
    <th>Field name</th>
	<th>Description</th>
	<th>Value</th>
  </tr>
 <tr>
    <td>tag_str</td>
	<td>Type of log</td>
	<td></td>
  </tr>
  <tr>
    <td>filename_str</td>
	<td>Path and name of the file</td>
	<td>*/var/log/alb/ids/*.log* </br>*/var/log/alb/ids/*.err* </br>*/var/log/alb/customerlogs/*.log* </br>*/var/log/alb/customerlogs/*.err*</td>
  </tr>
</table>


## Sending logs so you can use the fields in a message as Kibana search fields
{: #send_data_in_json}

By default, logging is automatically enabled for containers. Every entry in the Docker log file is displayed in Kibana in the field **message**. If you need to filter and analyze your data in Kibana by using a specific field that is part of the container log entry, configure your application to send valid JSON formatted output. For example, log the message in JSON format to `stdout` and `stderr`.
 
Each field that is available in the message is parsed to the type of field that matches its value.
 
For example, each field in the following JSON message is available as a field that you can use for filtering and searches.
Each field that is available in the message is parsed to the type of field that matches is value. For example, each field in the following JSON message:
    
```
{"field1":"string type",
 "field2":123,
 "field3":false,
 "field4":"4567"
}
```
{: codeblock}
    
is available as a field that you can use for filtering and searches:
    
* `field1` is parsed as `field1_str` of type string.
* `field2` is parsed as `field1_int` of type integer.
* `field3` is parsed as `field3_bool` of type boolean.
* `field4` is parsed as `field4_str` of type string.
    



## Security
{: #security}


To forward cluster logs into {{site.data.keyword.loganalysisshort}}, you must grant {{site.data.keyword.cloud_notm}} permissions to the {{site.data.keyword.containershort}} key owner and to the user ID that is configuring the logging cluster configurations.

The user ID that configures the logging cluster configurations must have the following permissions:

* IAM policy for the {{site.data.keyword.containershort}} with **Viewer** permissions.
* IAM policy for the cluster instance with **Administrator** or **Operator** permissions.

For a cluster to forwards logs into a {{site.data.keyword.loganalysisshort}} **space domain**, the following permissions are required for the {{site.data.keyword.containershort}} key owner:

* IAM policy for the {{site.data.keyword.containershort}} with **Administartor** role.
* IAM policy for the {{site.data.keyword.loganalysisshort}} service with **Administrator** role.
* Cloud Foundry (CF) **orgManager** role for the organization where the space is available.
* CF **SpaceManager** role or **Developer** role for the space where logs are forwarded from the cluster.


For a cluster to forwards logs into the {{site.data.keyword.loganalysisshort}} **account domain**, the following permissions are required for the {{site.data.keyword.containershort}} key owner:

* IAM policy for the {{site.data.keyword.containershort}} with **Administartor** role.
* IAM policy for the {{site.data.keyword.loganalysisshort}} service with **Administrator** role.



## Storing logs in Log Collection
{: #log_collection1}

Consider the following information about the default behavior in the {{site.data.keyword.cloud_notm}} when working with logs:

* Log data is stored for up to 3 days.
* A maximum of 500MB of data is stored per day. Any logs beyond that 500 MB cap are discarded. Cap allotments reset each day at 12:30 AM UTC.
* Up to 1.5 GB of data is searchable for a maximum of 3 days. Log data rolls over (First In, First Out) after either 1.5 GB of data is reached or after 3 days.
* Logs are not stored in Log Collection for long term storage.

The {{site.data.keyword.loganalysisshort}} service provides additional plans that allow you to store logs in Log Collection for as long as you require. For more information about the price of each plan, see [Service plans](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#plans). 

To manage logs in Log Collection, consider the following information:

* You can configure a log retention policy that you can use to define the number of days that you want to keep logs in Log Collection. For more information, see [Log Retention policy](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-manage_logs#log_retention_policy).
* You can delete logs manually by using the Log Collection CLI or the Log Collection API. 
* To manage logs in log collection, a user needs an IAM policy with permissions to work with the {{site.data.keyword.loganalysisshort}} service in the {{site.data.keyword.cloud_notm}}. For more information, see [IAM roles](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-security_ov#iam_roles).

## Viewing and analyzing logs
{: #logging_containers_ov_methods}

To analyze log data, use Kibana to perform advanced analytical tasks. Kibana is an open source analytics and visualization platform, that you can use to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. For more information, see [Analyzing logs in Kibana](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analyzing_logs_Kibana#analyzing_logs_Kibana).

* You can launch Kibana directly from a web browser. For more information, see [Navigating to Kibana from a web browser](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser).
* You can launch Kibana from the {{site.data.keyword.cloud_notm}} UI within the context of a cluster. For more information, see [Navigating to Kibana from the dashboard of a container that is deployed in a Kubernetes cluster](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-launch#launch_Kibana_for_containers_kube).

If you forward the log data of an app that runs in a container to the Container runtime log collector in JSON format, you can search and analyze log data in Kibana by using JSON fields. For more information, see [Sending logs so you can use the fields in a message as Kibana search fields](/docs/services/CloudLogAnalysis/containers?topic=cloudloganalysis-containers_kubernetes#send_data_in_json).

To view logs in Kibana, consider the following information:

* To see logs in a space domain, the user must have the **auditor** role or the **developer** role in the space that is associated with the cluster.
* To see logs in the account domain, the user must have an IAM policy to work with the {{site.data.keyword.loganalysisshort}} service. The minimum role that allows viewing log entries is **Viewer**.



## Tutorial: Analyze logs in Kibana for an app that is deployed in a Kubernetes cluster
{: #tutorial1}

To learn how to use Kibana to analyze the logs of a container that is deployed in a Kubernetes cluster, see [Analyze logs in Kibana for an app that is deployed in a Kubernetes cluster](/docs/services/CloudLogAnalysis/tutorials?topic=cloudloganalysis-container_logs#container_logs).
