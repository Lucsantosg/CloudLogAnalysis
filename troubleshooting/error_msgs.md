---

copyright:
  years: 2017

lastupdated: "2017-07-19"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Error messages
{: #error_msgs}

You might see these error messages when using the {{site.data.keyword.loganalysisshort}} service on {{site.data.keyword.Bluemix}}:
{:shortdesc}

## BXNLG020001W
{: #BXNLG020001W}

**Message description**

You have reached the daily quota that is allocated to the Bluemix space {Space GUID} for the {{site.data.keyword.loganalysisfull}} instance {Instance GUID}. Your current daily allotment is 500MB for Log Search storage, which is retained in Log Search storage for a period of 3 days, during which it can be searched for in Kibana. To upgrade your plan so that you can store more data in Log Search storage per day, and also retain all logs in Log Collection storage, upgrade the {{site.data.keyword.loganalysisshort}} service plan for this space. For more information about service plans and how to upgrade your plan, see [Plans](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).


**Message explanation** 

You can get a message with ID *BXNLG020001W* when you reach the Log Search storage quota that is allocated for the Lite service plan. The Lite plan is the complementary service plan that is set by default when you provision the {{site.data.keyword.loganalysisshort}} service in a {{site.data.keyword.Bluemix_notm}} space. Your current daily allotment is 500MB for Log Search storage, which is retained in Log Search storage for a period of 3 days, during which it can be searched for in Kibana.

**Recovery**

To upgrade your plan so that you can store more data in Log Search storage per day, and also retain all logs in Log Collection storage, upgrade the {{site.data.keyword.loganalysisshort}} service plan for this space. For more information about service plans and how to upgrade your plan, see [Plans](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).


## BXNLG020002W 
{: #BXNLG020002W}


**Message description**

You have reached the daily quota that is allocated to the Bluemix space {Space GUID} for the  {{site.data.keyword.loganalysisfull}} instance {Instance GUID}.  Your current daily allotment is XXX for Log Search storage, which is retained for a period of 3 days, during which it can be searched for in Kibana. This does not affect your log retention policy in Log Collection storage. To upgrade your plan so that you can store more data in Log Search storage per day, upgrade the {{site.data.keyword.loganalysisshort}} service plan for this space. For more information about service plans and how to upgrade your plan, see [Plans](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

XXX represents the size of the searchable data for your current plan.

**Message explanation** 

You have reached the daily quota that is allocated to the {{site.data.keyword.Bluemix_notm}} space {Space GUID} for the {{site.data.keyword.loganalysisfull}} instance {Instance GUID}.  Your current daily allotment is 500MB, 2 GB, 5 GB, or 10 GB for Log Search storage, which is retained for a period of 3 days, during which it can be searched for in Kibana. This does not affect your log retention policy in Log Collection storage.

**Recovery**

To upgrade your plan so that you can store more data in Log Search storage per day, upgrade the {{site.data.keyword.loganalysisshort}} service plan for this space. For more information about service plans and how to upgrade your plan, see [Plans](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).




