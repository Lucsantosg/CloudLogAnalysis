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

# Navigating to the logs of a Cloud Foundry app
{: #launch_logs_cloud_ui_cf}

In the {{site.data.keyword.Bluemix}} UI, you can view, filter, and analyze logs through the log tab that is available for each Cloud Foundry app or through the {{site.data.keyword.loganalysisshort}} service UI.
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.cloud_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}

To view CF app logs, consider the following information: 

<table>
  <caption>Information about CF app logs in the {{site.data.keyword.Bluemix_notm}}</caption>
  <tr>
    <th>UI options</th>
    <th>Information</th>
  </tr>
  <tr>
    <td>Log tab available thorugh the CF app UI </td>
    <td>The logs that are available for analysis include data for the last 24 hours.</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.loganalysisshort}} dashboard (Kibana)</td>
    <td>The logs that are available for analysis include data for the last 3 days. You can also specify a custom period.</td>
  </tr>
</table>


## Navigating to the CF app logs through the CF app dashboard 
{: #cfapp_ui}

To see the deployment or runtime logs of a Cloud Foundry app, complete the following steps:

1. From the Apps dashboard, click the name of your Cloud Foundry app. 
    
2. From the app details page, click **Logs**.
    
    From the **Logs** tab, you can view the recent logs for your app or tail logs in real time. In addition, you can filter logs by component (log type), by app instance ID, and by error.
    
By default, the logs that are available for analysis from the {{site.data.keyword.Bluemix_notm}} console include data for the last 24 hours.


## Navigating to the CF app logs through the {{site.data.keyword.loganalysisshort}} UI 
{: #cfapp_la}

To see the deployment or runtime logs of a Cloud Foundry app, complete the following steps:

1. From the Apps dashboard, click the name of your Cloud Foundry app. 
    
2. From the app details page, click **Logs**.
    
3. Click **View in Kibana**.

By default, the logs that are available for analysis include data for the last 15 minutes.

**Tip:** To analyze data for a custom period, see [Advanced log analysis with Kibana](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analyzing_logs_Kibana#analyzing_logs_Kibana). 


