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


# Transitioning to {{site.data.keyword.la_full_notm}}
{: #transition}

{{site.data.keyword.loganalysisshort}} is deprecated on 30 April 2019. [Learn more](https://www.ibm.com/blogs/bluemix/2019/03/deprecating-ibm-cloud-log-analysis/). The service is replaced by {{site.data.keyword.la_full_notm}}. [Learn more](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.cloud_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}


Complete the following steps to transition to {{site.data.keyword.la_full_notm}}: 

1. Save a copy of the logs that are stored in {{site.data.keyword.loganalysisshort_notm}} for long term search. You can use the CLI or the API. 

    Ensure that you save space logs for each Cloud Foundry space where you have a legacy {{site.data.keyword.loganalysisshort_notm}} instance, and for each account domain in each region that you currently monitor.

    * [Downloading logs by using the CLI](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-downloading_logs).

    * [Downloading logs by using the API](https://cloud.ibm.com/apidocs/log-analysis-api#download-logs-to-a-local-file).

2. Provision an instance of the [{{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-provision).

    You can provision 1 or more instances per region.

3. [Optional] Configure collection of {{site.data.keyword.cloud_notm}} service logs per region. [Learn more](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-config_svc_logs). 

    You can have multiple {{site.data.keyword.la_full_notm}} instances in a region. However, only 1 instance in a region can be configured to receive logs from [enabled services in the {{site.data.keyword.cloud_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-cloud_services#cloud_services) in that region.

4. [Optional] Configure your custom log sources to send logs to {{site.data.keyword.la_full_notm}}.

    You must configure logDNA agents for any log sources that you want to monitor. [Learn more](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-config_agent). 
    
    Notice that logs can be routed to both the legacy and LogDNA service instances at the same time.

5. Create and configure access groups to manage permissions in the {{site.data.keyword.cloud_notm}}. [Learn more](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-iam#groups)

6. Define views and dashboards in {{site.data.keyword.la_full_notm}} to analyze and manage logs. [Learn more](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-view_logs).

    Migration of Kibana dashboards to LogDNA dashboards is not automated. You have to manually implement new dashboards. 

    Notice that in LogDNA, histograms ands pies are the only visualizations that you can implement.

6. [Optional] Configure archiving for your {{site.data.keyword.la_full_notm}} instance. 

    You can archive logs to {{site.data.keyword.cos_full_notm}} (COS). [Learn more](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-archiving).

    **Note:** You are responsible for provisioning a COS instance that is used to archive logs and for maintaining archived logs.

    This step is only required for {{site.data.keyword.la_full_notm}} instances that have a paid plan.

8. Explore other features such as [alerting](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-alerts).


When you are ready to stop monitoring your Cloud logs through your legacy {{site.data.keyword.loganalysisshort_notm}} instances, delete the legacy {{site.data.keyword.loganalysisshort_notm}} instances from the {{site.data.keyword.cloud_notm}} console and remove any permissions to users to work with these legacy instances.


