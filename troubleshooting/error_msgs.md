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


# Error messages
{: #error_msgs}

You might see these error messages when using the {{site.data.keyword.loganalysisshort}} service on {{site.data.keyword.Bluemix}}:
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.cloud_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}

## BXNLG020001W
{: #BXNLG020001W}

**Message description**

You have reached the daily quota that is allocated to the Bluemix space {Space GUID} for the {{site.data.keyword.loganalysisfull}} instance {Instance GUID}. Your current daily allotment is 500MB for Log Search storage, which is retained in Log Search storage for a period of 3 days, during which it can be searched for in Kibana. To upgrade your plan so that you can store more data in Log Search storage per day, and also retain all logs in Log Collection storage, upgrade the {{site.data.keyword.loganalysisshort}} service plan for this space. For more information about service plans and how to upgrade your plan, see [Plans](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#plans).


**Message explanation** 

You can get a message with ID *BXNLG020001W* when you reach the Log Search storage quota that is allocated for the Lite service plan. The Lite plan is the complementary service plan that is set by default when you provision the {{site.data.keyword.loganalysisshort}} service in a space. Your current daily allotment is 500MB for Log Search storage, which is retained in Log Search storage for a period of 3 days, during which it can be searched for in Kibana.

**Recovery**

To upgrade your plan so that you can store more data in Log Search storage per day, and also retain all logs in Log Collection storage, upgrade the {{site.data.keyword.loganalysisshort}} service plan for this space. For more information about service plans and how to upgrade your plan, see [Plans](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#plans).


## BXNLG020002W 
{: #BXNLG020002W}


**Message description**

You have reached the daily quota that is allocated to the Bluemix space {Space GUID} for the  {{site.data.keyword.loganalysisfull}} instance {Instance GUID}.  Your current daily allotment is XXX for Log Search storage, which is retained for a period of 3 days, during which it can be searched for in Kibana. This does not affect your log retention policy in Log Collection storage. To upgrade your plan so that you can store more data in Log Search storage per day, upgrade the {{site.data.keyword.loganalysisshort}} service plan for this space. For more information about service plans and how to upgrade your plan, see [Plans](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#plans).

XXX represents the size of the searchable data for your current plan.

**Message explanation** 

You have reached the daily quota that is allocated to the space {Space GUID} for the {{site.data.keyword.loganalysisfull}} instance {Instance GUID}.  Your current daily allotment is 500MB, 2 GB, 5 GB, or 10 GB for Log Search storage, which is retained for a period of 3 days, during which it can be searched for in Kibana. This does not affect your log retention policy in Log Collection storage.

**Recovery**

To upgrade your plan so that you can store more data in Log Search storage per day, upgrade the {{site.data.keyword.loganalysisshort}} service plan for this space. For more information about service plans and how to upgrade your plan, see [Plans](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#plans).




