---

copyright:
  years: 2017

lastupdated: "2017-11-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Logging for a container that is managed by the IBM Cloud (Deprecated)
{: #containers_bluemix}

You can view, filter, and analyze logs for Docker containers that are deployed in the {{site.data.keyword.IBM}}-managed infrastructure.
{:shortdesc}

Container logs are monitored and forwarded from outside of the container by using crawlers. The data is sent by the crawlers to a multi-tenant Elasticsearch in the {{site.data.keyword.Bluemix_notm}}.

The following figure shows a high level view of logging for the {{site.data.keyword.containershort}}:

![High level component overview for containers deployed in the {{site.data.keyword.Bluemix_notm}}-managed infrastructure](images/container_bmx.gif "High level component overview for containers deployed in the {{site.data.keyword.Bluemix_notm}}-managed infrastructure")

By default, the following logs are collected for a container that is deployed in the {{site.data.keyword.Bluemix_notm}}-managed cloud infrastructure:

<table>
  <caption>Table 2. Logs collected for containers deployed in the {{site.data.keyword.Bluemix_notm}}-managed infrastructure</caption>
  <tbody>
    <tr>
      <th align="center">Log</th>
      <th align="center">Description</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> By default, Docker messages are stored in the /var/log/messages folder of the container. This log includes system messages.
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">This log is the Docker log. <br> The Docker log file is not stored as a file inside of the container, but it is collected anyway. This log file is collected by default as it is the standard Docker convention for exposing the stdout (standard output) and stderr (standard error) information for the container. Information that any container process prints to stdout or stderr is collected. 
      </td>
     </tr>
  </tbody>
</table>




## Analyzing logs
{: #logging_containers_ov_methods}

To analyze container log data, use Kibana to perform advanced analytical tasks. You can use Kibana, an open source analytics and visualization platform, to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. For more information, see [Analyzing logs in Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana).


## Collecting custom logs
{: #collect_custom_logs}

To collect additional logs, add the **LOG_LOCATIONS** environment variable with a path to the log file when you create the container. 

You can add multiple log files by separating them with commas. 

For more information, see [Collecting non-default log data from a container](logging_containers_other_logs.html#logging_containers_collect_data).


## Searching logs
{: #log_search}

By default, you can use Kibana to search up to 500 MB of logs per day in {{site.data.keyword.Bluemix_notm}}. 

{{site.data.keyword.loganalysisshort}} service provides multiple plans. Each plan has different log search capabilities, for example, the *Log Collection* plan allows you to search up to 1 GB of data per day. For more information about the plans, see [Service plans](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).


## Sending logs so you can use the fields in a message as Kibana search fields
{: #send_data_in_json}

By default, logging is automatically enabled for containers. Every entry in the Docker log file is displayed in Kibana in the field `message`. If you need to filter and analyze your data in Kibana by using a specific field that is part of the container log entry, configure your application to send valid JSON formatted output.

Complete the following steps to send logs where container log entries are parsed into individual fields:

1. Log the message to a file. 
2. Add the log file to the list of non-default logs that are available for analysis from a container. For more information, see [Collecting non-default log data from a container](logging_containers_other_logs.html#logging_containers_collect_data). 
    
When JSON log entries are sent to the Docker log file of a container as STDOUT, they are not parsed as JSON. 
    
If you log the message to a file, and a message is determined to be valid JSON, the fields are parsed and new fields are created for each field in the message. Only string-type field values are available for filtering and sorting in Kibana

## Storing logs in Log Collection
{: #store_logs}

By default, the {{site.data.keyword.Bluemix_notm}} stores log data for up to 3 days:   

* A maximum of 500MB per space of data is stored per day. Any logs beyond that 500 MB cap are discarded. Cap allotments reset each 
day at 12:30 AM UTC.
* Up to 1.5 GB of data is searchable for a maximum of 3 days. Log data rolls over (First In, First Out) after either 1.5 GB of data is reached or after 3 days.

The {{site.data.keyword.loganalysisshort}} service provides additional plans that allow you to store logs in Log Collection for as long as you require. For more information about the price of each plan, see [Service plans](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

If you need to store logs or search bigger logs, you can provision the {{site.data.keyword.loganalysisshort}} service, and choose a different service plan. Additional plans allow you to store logs in Log Collection for as long as you require, and search bigger log sizes. For more information, see [Service plans](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).


## Viewing logs
{: #logging_containers_ov_methods_view_bmx}

You can view the latest logs for a container that is deployed in the {{site.data.keyword.Bluemix_notm}}-managed infrastructure by using any of the following methods:

* View logs through the {{site.data.keyword.Bluemix_notm}} UI to monitor the latest activity of the container.
    
    You can view, filter, and analyze logs through the **Monitoring and Logs** tab that is available for each container. 
	
	To see the deployment or runtime logs of a Docker container that is deployed in the {{site.data.keyword.IBM_notm}}-managed infrastructure, complete the following steps:

    1. From the Apps dashboard, click the single container or container group. 
    
    2. From the app details page, click **Monitoring and Logs**.

    3. Select the **Logging** tab. From the **Logging** tab, you can view the recent logs for your container or tail logs in real time. 
	
* View logs by using the {{site.data.keyword.containershort}} CLI. Use commands to manage logs programmatically.
    
    You can view, filter, and analyze logs through the command line interface by using the **cf ic logs** command. 
	
	Use the `bx cf ic logs` command to display logs from a container in the {{site.data.keyword.Bluemix_notm}}. For example, you can use the logs to analyze why a container has stopped or for reviewing the container output. 
	
	To see application errors for the app that runs in a container through the `cf ic logs` command, the application must write its logs to the standard output (STDOUT) and standard error (STDERR) output streams. If you design your application to write to these standard output streams, you can view the logs via the command line even if the container shuts down or crashes.

    For more information about the `cf ic logs` command, see [cf ic logs command](/docs/containers/container_cli_reference_cfic.html#container_cli_reference_cfic__logs).



