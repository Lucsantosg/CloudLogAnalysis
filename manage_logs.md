---

copyright:
  years: 2017

lastupdated: "2017-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Managing logs
{: #manage_logs}

You can use the {{site.data.keyword.loganalysisshort}} CLI and the {{site.data.keyword.loganalysisshort}} API to manage logs that are stored in Log Collection.
{:shortdesc}


## Configuring a log retention policy
{: #log_retention_policy}

You can use the {{site.data.keyword.loganalysisshort}} CLI to view and configure a log retention policy. The policy specifies the number of days that logs are kept in Log Collection. 

* By default, when you select a paid plan, logs are collected and kept in Log Collection. 
* When you set a retention period, after the retention period has expired, logs are deleted automatically from Log Collection and they cannot be recovered.
* You can specify a retention period for an account. The retention period is automatically configured for all the spaces in that account. 
* You can specify a retention period for a space.
* You can change at any time the retention policy.
* You can disable the policy by setting its value to *-1*. 

**Note:** When you disable the log retention policy, you must maintain the logs in Log Collection. You can use the CLI command [cf logging delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#delete) to delete old logs.

For more information, see [Viewing and configuring the log retention policy](/docs/services/CloudLogAnalysis/how-to/manage-logs/configuring_retention_policy.html#configuring_retention_policy).


## Deleting logs
{: #log_deletion}

Logs that are stored in Log Search are deleted after 3 days.

Logs that are stored in Log Collection are kept until you either configure a retention policy or delete them manually. 

* You can configure a log retention policy to define the number of days that you want to keep logs in Log Collection. For more information, see [Log Retention policy](/docs/services/CloudLogAnalysis/manage_logs.html#log_retention_policy).

    You can disable the policy by setting its value to *-1*. 

* You can use the [Log Collection API](https://console.bluemix.net/apidocs/948-ibm-cloud-log-collection-api?&language=node&env_id=ibm%3Ayp%3Aus-south#introduction){: new_window} or the [Log Collection CLI](/docs/services/CloudLogAnalysis/reference/logging_cli.html#logging_cli){: new_window} to delete logs manually from Log Collection. 

    For more information about deleting logs manually through the CLI, see [cf logging delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#delete).


## Downloading logs
{: #download_logs}

You can search logs for the last 3 days in Kibana. To be able to analyze older log data, you can download logs to a local file, or you can pipe these logs to other programs such as a local Elastic Stack. 

For more information, see [Downloading logs](/docs/services/CloudLogAnalysis/how-to/manage-logs/downloading_logs.html#downloading_logs).


## Getting information about your logs
{: #info_about_logs}

To obtain general information about your logs, use the `cf logging status` command. For more information, see [Viewing log information](/docs/services/CloudLogAnalysis/how-to/manage-logs/viewing_log_information.html#viewing_log_status).

For example, to keep cost under control, you might want to monitor the size of the logs of your apps over a period of time. For example, you might want to know the size of each log type during a week for a {{site.data.keyword.Bluemix_notm}} space to identify if any app or service is generating more logs than expected. To check the size of your logs, use the `cf logging status` command.

You might also be interested in geeting other types of information such as:

* [Information about logs over a period of time](/docs/services/CloudLogAnalysis/how-to/manage-logs/viewing_log_information.html#viewing_logs).
* [Information about a type of log over a period of time](/docs/services/CloudLogAnalysis/how-to/manage-logs/viewing_log_information.html#viewing_logs_by_log_type).
* [Account information about logs](/docs/services/CloudLogAnalysis/how-to/manage-logs/viewing_log_information.html#viewing_logs_account).


## Installing the {{site.data.keyword.loganalysisshort_notm}} CLI
{: #install_cli}

To learn how to install the CLI, see [Installing the logging CLI](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#config_log_collection_cli).

To check the version of the CLI, run the command [bx cf logging](/docs/services/CloudLogAnalysis/reference/logging_cli.html#base) with the parameter * -version*.

To get help on how to run commands, see [Getting command line help to run commands](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#cli_help).


## Logging endpoints
{: #endpoints}

The following table lists the logging URLs per region:

<table>
    <caption>Endpoints per region</caption>
    <tr>
      <th>Region</th>
      <th>URL</th>
      <th>Kibana version</th>
    </tr>
	<tr>
      <td>Frankfurt</td>
	  <td>[https://logging.eu-de.bluemix.net](https://logging.eu-de.bluemix.net)</td>
	  <td>Kibana 4</td>
    </tr>
	<tr>
      <td>Sydney</td>
	  <td>[https://logmet.au-syd.bluemix.net](https://logmet.au-syd.bluemix.net)</td>
	  <td>Kibana 5.1</td>
    </tr>
	<tr>
      <td>United Kingdom</td>
	  <td>[https://logmet.eu-gb.bluemix.net](https://logmet.eu-gb.bluemix.net)</td>
	  <td>Kibana 4, Kibana 3 (Deprecated)</td>
    </tr>
    <tr>
      <td>US South</td>
      <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
	  <td>Kibana 5.1</td>
    </tr>
</table>



