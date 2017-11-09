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

# Analyzing logs in the {{site.data.keyword.Bluemix_notm}} UI
{: #analyzing_logs_bmx_ui}

In the {{site.data.keyword.Bluemix}}, you can view, filter, and analyze logs through the log tab that is available for each Cloud Foundry app or Docker container that runs in the {{site.data.keyword.Bluemix_notm}}-managed infrastructure.
{:shortdesc}

##  Navigating to the logs of a Cloud Foundry app
{: #launch_logs_tab_bmx_ui_cf}

To see the deployment or runtime logs of a Cloud Foundry app, complete the following steps:

1. From the Apps dashboard, click the name of your Cloud Foundry app. 
    
2. From the app details page, click **Logs**.
    
    From the **Logs** tab, you can view the recent logs for your app or tail logs in real time. In addition, you can filter logs by component (log type), by app instance ID, and by error.
    
By default, the logs that are available for analysis from the {{site.data.keyword.Bluemix_notm}} console include data for the last 24 hours.

**Tip:** To analyze data for a custom period that precedes the last 24 hours, see [Advanced log analysis with Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana). 





##  Navigating to the logs of a Docker container that is managed in the {{site.data.keyword.Bluemix_notm}}
{: #launch_logs_tab_bmx_ui_containers}

To see the deployment or runtime logs of a Docker container that is deployed in the {{site.data.keyword.IBM_notm}}-managed infrastructure, complete the following steps:

1. From the Apps dashboard, click the single container or container group. 
    
2. From the app details page, click **Monitoring and Logs**.

3. Select the **Logging** tab.
    
    From the **Logging** tab, you can view the recent logs for your container or tail logs in real time. 
	
	
	

## Log format for CF app logs
{: #log_format_cf}

Logs for {{site.data.keyword.Bluemix_notm}} Cloud Foundry apps are displayed in a fixed format, similar to the following pattern:

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>/<var class="keyword varname">message</var>/<var class="keyword varname">timestamp</var></code>

Each log entry contains the following fields:

| Field | Description |
|-------|-------------|
| Time stamp | The time of the log statement. The timestamp is defined up to the millisecond. |
| Component | The component that produces the log. For the list of the different components, see [Log sources for CF apps](cfapps/logging_cf_apps.html#logging_bluemix_cf_apps_log_sources). <br> Each component type is followed by a slash and a digit that indicates the application instance. 0 is the digit allocated to the first instance, 1 is the digit allocated to the second, and so on. |
| Message | The message that is issued by the component. The message varies depending on the context. |
{: caption="Table 1. CF app log entry fields" caption-side="top"}


## Log format for container logs
{: #log_format_containers}

Logs for containers are displayed in a fixed format, similar to the following pattern:

<code><var class="keyword varname">timestamp</var>/<var class="keyword varname">machine</var>/<var class="keyword varname">message</var>  </code>

Each log entry contains the following fields:

| Field | Description |
|-------|-------------|
| Date/Time | The time of the log statement. The time stamp is defined as a millisecond. |
| Machine | The host name where the container is running. |
| Message | The message that is issued. The message varies depending on the context. |
{: caption="Table 2. Docker container log entry fields" caption-side="top"}

