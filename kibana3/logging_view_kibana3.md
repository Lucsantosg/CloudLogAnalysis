---

copyright:
  years: 2015, 2018

lastupdated: "2018-01-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyzing logs in Kibana 3 (Deprecated)
{: #analyzing_logs_Kibana3}

In {{site.data.keyword.Bluemix}}, you can use Kibana, an open source analytics and visualization platform, to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. Use Kibana to perform advanced analytical tasks.
{:shortdesc}


## Filtering data in a Kibana dashboard
{: #filter_data_kibana_dashboard}

In {{site.data.keyword.Bluemix}}, you can analyze data by using the default Kibana dashboard that is provided per resource or by {{site.data.keyword.Bluemix}} space. By default, these dashboards display all the data that is available for the last 24 hours. However, you can constraint the information displayed through a dashboard. You can add queries and filters to a default dashboard, and then save it for future reuse.

In a dashboard, you can add multiple queries and filters. A query defines a subset of log entries.  A filter refines the data selection by including or excluding information. 

For Cloud Foundry apps, the following list outline examples of how to filter data:
* If you you are looking for information in your logs that include key terms, you can create queries to filter by those terms. With Kibana, you can compare queries visually on the dashboard. For more information, see [Filtering your Cloud Foundry App logs with queries in Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).

* If you are looking for information within a specific period of time, you can filter data within a time range. For more information, see [Filtering your Cloud Foundry App logs by time in Kibana](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter).

* If you are looking for information for a specific instance ID, you can filter data by instance ID. For more information, see [Filtering your Cloud Foundry App logs by instance ID in Kibana](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id) and [Filtering your Cloud Foundry App logs by known application ID in Kibana](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id).

* If you are looking for information for a specific component, you can filter data by component (log type). For more information, see [Filtering your Cloud Foundry App logs by log type in Kibana](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter).

* If you are looking for information, for example, error messages, you can filter data by message type. For more information, see [Filtering your Cloud Foundry App logs by message type in Kibana](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter).

## Customizing a Kibana dashboard
{: #customize_kibana_dashboard}

There are different types of dashboards that you can customize to visualize and analyze the data, for example:
* Single-cf-app dashboard: This is a dashboard that shows information for a single Cloud Foundry application.  
* Multi-cf-app dashboard: This is a dashboard that shows information for all the Cloud Foundry applications that are deployed in the same  {{site.data.keyword.Bluemix}} space. 

When you customize a dashboard, you can configure queries and filters to select a subset of the log data to show through the dashboard.

To visualize the data, you can configure panels. Kibana includes different panels such as table, trends, and histogram that you can use to analyze the information. You can add, remove, and rearrange panels in the dashboard. The objective of each panel varies. Some panels are organized into rows that provide the results of a one or more queries. Other panels display documents or custom information. For example, you can configure a bar chart, pie chart, or table to visualize the data and analyze it.  


## Saving a Kibana dashboard
{: #save_Kibana_dashboard}

Complete the following steps to save a Kibana dashboard after you customize it:

1. In the toolbar, click the **Save** icon.

2. Enter a name for the dashboard.

    **Note:** If you try to save a dashboard with a name containing blank spaces, it will not save.

3. Next to the name field, click the **Save** icon.



## Analyzing logs through a Kibana dashboard
{: #analyze_kibana_logs}

After you customize a Kibana dashboard, you can visualize and analyze the data through its panels. 

To search for information, you can pin or unpin queries. 

* You can pin a query to the dashboard and automatically the search is activated.
* To remove content from the dashboard, you can deactivate a query.

To filter information, you can enable or disable filters. 

* You can select the **Toggle** checkbox ![Toggle box to include a filter](images/logging_toggle_include_filter.jpg) in a filter to enable it.   
* You can unselect the **Toggle** checkbox ![Toggle box to include a filter](images/logging_toggle_exclude_filter.jpg) in a filter to disable it. 

The graphs and charts in your dashboard display the data. You can use the graphs and charts in your dashboard to monitor the data. 

For example, for a single-cf-app dashboard, the dashboard includes information about one Cloud Foundry application. The data that you can visualize and analyze is limited to that app. You can use the dashboard to analyze data for all instances of the app. You can compare instances. You can filter by instance ID the information. 

You can define and pin a query for each instance ID to the dashboard. 

![Dashboard with queries pinned](images/logging_kibana_dash_activate_query.jpg)

Then, you can activate or deactivate individual queries depending on the instance information that you want to see in the dashboard. 

The following figure shows one query activated and the other deactivated:

![Dashboard with queries pinned](images/logging_kibana_dash_deactivate_query.jpg)

If you want to compare 2 instances in a Histogram, you can define two queries in the same dashboard, one for each instance ID. You can give them an alias and a unique color to identify them easily. Kibana handles multiple queries by joining them with a logical OR. 

The following figure shows the panel to configure an alias and a color for a query, to pin it to the dashboard, and to deactivate it:

![Dashboard wizard to configure query](images/logging_kibana_query_def.jpg)


