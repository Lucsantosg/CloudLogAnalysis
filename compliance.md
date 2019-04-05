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
{:deprecated: .deprecated}


# Compliance
{: #compliance}

[The {{site.data.keyword.Bluemix}} provides a Cloud platform and services that are built to IBM's stringent security standards.](/docs/security/compliance.html#compliance). The {{site.data.keyword.loganalysislong}} service is a DevOps service that is built for the {{site.data.keyword.Bluemix_notm}}. 
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances, and all Lite plan instances are deleted. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.Bluemix_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}


## General Data Protection Regulation

The General Data Protection Regulation (GDPR) seeks to create a harmonized data protection law framework across the EU and aims to give citizens back the control of their personal data, whilst imposing strict rules on those hosting and ‘processing’ this data, anywhere in the world. The Regulation also introduces rules relating to the free movement of personal data within and outside the EU. 

**Disclaimer:** The {{site.data.keyword.loganalysisshort}} service stores and displays log records from Cloud resources that run in your account in the {{site.data.keyword.Bluemix_notm}}, and from logs that you might send from outside the {{site.data.keyword.Bluemix_notm}}. Personal information (PI) must not be included in any of the log entries stored in {{site.data.keyword.loganalysisshort}} as this data is accessible to other users within your Enterprise, as well as to {{site.data.keyword.IBM_notm}} to be able to support the Cloud Service.

### Regions
{: #regions}

The {{site.data.keyword.loganalysisshort}} service is compliant with GDPR in the {{site.data.keyword.Bluemix_notm}} Public regions where the service is available.


### Data retention
{: #data_retention}

The {{site.data.keyword.loganalysisshort}} service includes 2 data repositories where your data can be stored: 

* Log Search, that hosts the log data that is available for analysis through Kibana.
* Log Collection, that hosts the log data for long-term storage.

Depending on the {{site.data.keyword.loganalysisshort}} service plan, data is stored in Log Search, or in Log Search and Log Collection. The standard or lite plan only stores data in Log Search. The rest of the plans store data in Log Search and in Log Collection.

* Logs that are stored in Log Search are kept for 3 days.
* Logs that are stored in Log Collection are kept until you either configure a retention policy or delete them manually. By default, logs are kept indefinitely in Log Collection.



### Data deletion
{: #data_deletion}

Consider the following information:

* Logs that are stored in Log Search are deleted after 3 days.

* Logs that are stored in Log Collection are deleted after a number of days when you configure a retention policy, or when you delete them manually. 

    You can configure a log retention policy to define the number of days that you want to keep logs in Log Collection. For more information, see [Viewing and configuring the log retention policy by using the {{site.data.keyword.Bluemix_notm}} plugin](/docs/services/CloudLogAnalysis/how-to/manage-logs?topic=cloudloganalysis-configuring_retention_policy#configuring_retention_policy).

    You can use the [Log Collection API](https://console.bluemix.net/apidocs/948-ibm-cloud-log-collection-api?&language=node&env_id=ibm%3Ayp%3Aus-south#introduction){: new_window} or the [Log Collection CLI](/docs/services/CloudLogAnalysis/reference?topic=cloudloganalysis-log_analysis_cli#log_analysis_cli){: new_window} to delete logs manually from Log Collection. 

    You can use the CLI to delete logs manually from Log Collection. For more information, see [ibmcloud logging log-delete by using the {{site.data.keyword.Bluemix_notm}} plugin](/docs/services/CloudLogAnalysis/how-to/manage-logs?topic=cloudloganalysis-deleting_logs#deleting_logs).


If you change from a paid plan to the standard or lite plan, logs in Log Collection will be deleted in about one day.

At any time, you can open a support ticket and request that all your data is deleted from Log Search and log Collection. For information about opening an IBM support ticket, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).



### More information
{: #info}

For more information, see:

[{{site.data.keyword.Bluemix_notm}} security compliance](/docs/security/compliance.html#compliance)

[GDPR - {{site.data.keyword.IBM_notm}} official page](https://www.ibm.com/data-responsibility/gdpr/)



