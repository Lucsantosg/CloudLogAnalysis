---

copyright:
  years: 2017, 2019

lastupdated: "2019-05-01"

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
{:deprecated: .deprecated}

# Virtual Machines
{: #logging_vm_ov}

Logging capabilities are not enabled automatically for virtual machines (VMs). However, you can configure your VM to send logs into Log Collection. To collect and send log data from a VM into the {{site.data.keyword.loganalysisshort}} service, you must configure a Multi-Tenant Logstash Forwarder (mt-logstash-forwarder). Then, you can view, filter, and analyze logs in Kibana.
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.cloud_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}

## Log ingestion
{: #log_ingestion2}

The {{site.data.keyword.loganalysisshort}} service offers different plans. All plans, with the exception of the *Lite* plan, include the ability to send logs into Log Collection. For more information about the plans, see [Service plans](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#plans).

You can send logs into the {{site.data.keyword.loganalysisshort}} by using the mt-logstash-forwarder. For more information, see [Send log data by using a Multi-Tenant Logstash Forwarder (mt-logstash-forwarder)](/docs/services/CloudLogAnalysis/how-to/send-data?topic=cloudloganalysis-send_data_mt#send_data_mt).


## Log collection
{: #log_collection2}

By default, the {{site.data.keyword.Bluemix_notm}} stores log data for up to 3 days:   

* A maximum of 500 MB per space of data is stored per day. Any logs beyond that 500 MB cap are discarded. Cap allotments reset each 
day at 12:30 AM UTC.
* Up to 1.5 GB of data is searchable for a maximum of 3 days. Log data rolls over (First In, First Out) after either 1.5 GB of data is reached or after 3 days.

The {{site.data.keyword.loganalysisshort}} service provides additional plans that allow you to store logs in Log Collection for as long as you require. For more information about the price of each plan, see [Service plans](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#plans).

* You can configure a log retention policy that you can use to define the number of days that you want to keep logs in Log Collection. For more information, see [Log Retention policy](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-manage_logs#log_retention_policy).
* You can delete logs manually by using the Log Collection CLI or the API.


## Log search
{: #log_search2}

By default, you can use Kibana to search up to 500 MB of logs per day in the {{site.data.keyword.Bluemix_notm}}. 

{{site.data.keyword.loganalysisshort}} service provides multiple plans. Each plan has different log search capabilities, for example, the *Log Collection* plan allows you to search up to 1 GB of data per day. For more information about the plans, see [Service plans](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#plans).


## Log analysis
{: #log_analysis}

To analyze log data, use Kibana to perform advanced analytical tasks. You can use Kibana, an open source analytics and visualization platform, to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. For more information, see [Analyzing logs in Kibana](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analyzing_logs_Kibana#analyzing_logs_Kibana).
