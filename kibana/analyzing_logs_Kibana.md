---

copyright:
  years: 2017, 2018

lastupdated: "2018-02-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Viewing and analyzing logs (Kibana)
{:#analyzing_logs_Kibana}

You can use Kibana 5.1, an open source analytics and visualization platform, to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. Use Kibana to perform advanced analytical tasks.
{:shortdesc}

Kibana is a browser-based interface where you can analyze data interactively and customize dashboards that you can then use to analyze log data and perform advance management tasks. For more information, see [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.

The data that a Kibana page displays is constrained by a search. The default data set is defined by the pre-configured index pattern. To filter the information, you can add new search queries and apply filters to the default data set. Then, you can save the search for future reuse. 

Kibana includes different pages that you can use to analyze your logs:

| Kibana page | Description |
|-------------|-------------|
| Discover | Use this page to define searches and analyze your logs interactively through a table and a histogram. |
| Visualize | Use this page to create visualizations such as graphs and tables that you can use to analyze your log data and compare results.  |
| Dashboard | Use this page to analyze your logs through collections of saved visualizations and searches.  |
{: caption="Table 1. Kibana pages" caption-side="top"}

**Note:** You can only analyze 1 complete day at a time through the Visualize page or the Dashboard page, even though you can go back 3 days. Log data is stored for 3 days by default. 

| Kibana page | Time period information |
|-------------|-------------------------|
| Discover | Analyze data for a maximum of 3 days. |
| Visualize | Analyze data for a period of 24 hours. <br> You can filter log data for a custom period that elapses 24 hours.  |
| Dashboard | Analyze data for a period of 24 hours. <br> You can filter log data for a custom period that elapses 24 hours. <br> The time picker that you set is applied to all visualizations that are included in the dashboard. |
{: caption="Table 2. Time period information" caption-side="top"}

For example, this is how you can use Kibana to show information about a CF app or container in your space through the different pages:

## Navigate to the Kibana dashboard
{: #launch_Kibana}

You can launch Kibana in any of the following ways:

* From the {{site.data.keyword.loganalysisshort}} service dashboard

    You can launch Kibana so the data that you see aggregates logs from services within a provided space.
	
	For more information, see [Navigating to Kibana from the dashboard of the Log Analysis service](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_log_analysis).

* From the {{site.data.keyword.Bluemix_notm}}

    You can launch to your specific CF app logs in Kibana, within the context of that specific App. For more information, see [Navigating to Kibana from the dashboard of a CF app](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_cf_app).
    
    You can launch to your specific Docker container logs in Kibana, within the context of that specific container. This feature applies only to containers that are deployed in the {{site.data.keyword.Bluemix_notm}}-managed infrastructure. For more information, see [Navigating to Kibana from the dashboard of a container](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_for_containers).
    
    For CF apps, the query that is used to filter the data that is available for analysis in Kibana retrieves log entries for the Cloud Foundry application. The log information that Kibana displays by default is all related to a single Cloud Foundry application and all its instances. 
    
    For containers, the query that is used to filter the data that is available for analysis in Kibana retrieves log entries for all instances of the container. The log information that Kibana displays by default is all related to a single container or to a container group and all its instances. 
    
    

* From a direct browser link

    You may want to launch Kibana so the data that you see aggregates logs from services within a provided space.
    
    The query that is used to filter the data that is displayed in the dashboard retrieves log entries for a space in the 
    {{site.data.keyword.Bluemix_notm}} organization. The log information that Kibana displays includes records for 
    all resources that are deployed within the space of the {{site.data.keyword.Bluemix_notm}} organization that you are logged in. 
    
    For more information, see [Navigating to the Kibana dashboard from a web browser](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser).
    
    

## Analyze data interactively
{: #analyze_discover}

In the Discover page, you can define new search queries and apply filters per query. The log data is displayed through a table and a  histogram. You can use these visualizations to analyze the data interactively. For more information, see [Analyzing logs interactively in Kibana](analize_logs_interactively.html#analize_logs_interactively).

You can configure filters from log fields, for example, message_type and instance_ID, and set a time period. You can enable or disable dynamically these filters. The table and histogram will display the log entries that meet the query and filtering criteria that you enable. For more information, see [Filtering logs in Kibana](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).

## Analyze data through a visualization
{: #analyze_visualize}
    
In the Visualize page, you can define new search queries and visualizations. You can also open saved visualizations, or save a visualization.

To analyze the data, you can create visualizations based on an existing search or a new search. Kibana includes different types of visualizations such as table, trends, and histogram that you can use to analyze the information. The objective of each visualization varies. Some visualizations are organized into rows that provide the results of a one or more queries. Other visualizations display documents or custom information. The data in a visualization can be fixed or change if a search query is updated. You can embed the visualization in a web page or share it. 

For more information, see [Analyzing logs by using visualizations](/docs/services/CloudLogAnalysis/kibana/kibana_visualizations.html#kibana_visualizations).

## Analyze data in a dashboard
{: #analyze_dashboard}

In the Dashboard page, you can customize, save, and share multiple visualizations and searches simultaneously. 

You can add, remove, and rearrange visualizations in the dashboard. For more information, see [Analyzing logs in Kibana through a dashboard](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#analize_logs_dashboard).
    
After you customize a Kibana dashboard, you can analyze the data through its visualizations and save it for future reuse. For more information, see [Saving a Kibana dashboard](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#save).

## Customize Kibana
{: #analyze_management}

You can also configure and manage Kibana resources from the **Management** page. 

You can complete any of the following tasks:

* Save, delete, export, and import searches. 
* Save, delete, export, and import visualizations.
* Save, delete, export, and import dashboards.
* [Refresh the field list.](/docs/services/CloudLogAnalysis/kibana/analize_logs_interactively.html#discover_view_reload_fields)

## Limitations
{: #limitations}

In Kibana, you can share a Visualization or a Dashboard only with members of the same organization or account.

The following Kibana features are not supported:

* Sharing a search.
* Creating new index patterns. 


## Roles that are required by a user to view logs
{: #roles}

In the {{site.data.keyword.Bluemix_notm}}, you can assign one or more roles to users. These roles define what tasks are enabled for that user to work with the {{site.data.keyword.loganalysisshort}} service. 

The following tables list the roles that a user must have to view logs:

<table>
  <caption>Permissions required by an **account owner** to see logs</caption>
  <tr>
    <th>Action</th>
	<th>CF space roles</th>
	<th>CF organization roles</th>
	<th>IAM roles</th>
  </tr>
  <tr>
    <td>View logs in a space domain</td>
	<td>*Manager* </br>*Developer* </br>*Auditor*</td>
	<td></td>
	<td></td>
  </tr>
  <tr>
    <td>View logs in the account domain</td>
	<td></td>
	<td></td>
	<td>*Administrator*</td>
  </tr>
  <tr>
    <td>View logs in an organization domain</td>
	<td></td>
	<td>*Manager* </br>*Billing manager*  </br>*Auditor*</td>
	<td></td>
  </tr>
</table>

<table>
  <caption>Permissions required by an **auditor** to see logs</caption>
  <tr>
    <th>Action</th>
	<th>CF space roles</th>
	<th>CF organization roles</th>
	<th>IAM roles</th>
  </tr>
  <tr>
    <td>View logs in a space domain</td>
	<td>*Auditor*</td>
	<td></td>
	<td></td>
  </tr>
  <tr>
    <td>View logs in the account domain</td>
	<td></td>
	<td></td>
	<td>*Viewer*</td>
  </tr>
  <tr>
    <td>View logs in an organization domain</td>
	<td></td>
	<td>*Auditor*</td>
	<td></td>
  </tr>
</table>

<table>
  <caption>Permissions required by an **admin** to see logs</caption>
  <tr>
    <th>Action</th>
	<th>CF space roles</th>
	<th>CF organization roles</th>
	<th>IAM roles</th>
  </tr>
  <tr>
    <td>View logs in a space domain</td>
	<td>*Developer*</td>
	<td></td>
	<td></td>
  </tr>
  <tr>
    <td>View logs in the account domain</td>
	<td></td>
	<td></td>
	<td>*Viewer*</td>
  </tr>
  <tr>
    <td>View logs in an organization domain</td>
	<td></td>
	<td>*Manager*</td>
	<td></td>
  </tr>
</table>

<table>
  <caption>Permissions required by a **developer** to see logs</caption>
  <tr>
    <th>Action</th>
	<th>CF space roles</th>
	<th>CF organization roles</th>
	<th>IAM roles</th>
  </tr>
  <tr>
    <td>View logs in a space domain</td>
	<td>*Developer*</td>
	<td></td>
	<td></td>
  </tr>
  <tr>
    <td>View logs in the account domain</td>
	<td></td>
	<td></td>
	<td>*Viewer*</td>
  </tr>
  <tr>
    <td>View logs in an organization domain</td>
	<td></td>
	<td>*Auditor*</td>
	<td></td>
  </tr>
</table>



## URLs to launch Kibana
{: #urls_kibana}

The following table lists the URLs to launch Kibana, and the versions of Kibana per region:

<table>
    <caption>URLs to launch Kibana</caption>
    <tr>
      <th>Region</th>
      <th>URL</th>
      <th>Kibana version</th>
    </tr>
	<tr>
      <td>Frankfurt</td>
	  <td>[https://logging.eu-fra.bluemix.net](https://logging.eu-fra.bluemix.nett)</td>
	  <td>Kibana 5.1</td>
    </tr>
	<tr>
      <td>Sydney</td>
	  <td>[https://logging.au-syd.bluemix.net](https://logging.au-syd.bluemix.net)</td>
	  <td>Kibana 5.1</td>
    </tr>
	<tr>
      <td>United Kingdom</td>
	  <td>[https://logging.eu-gb.bluemix.net](https://logging.eu-gb.bluemix.net)</td>
	  <td>Kibana 5.1</td>
    </tr>
    <tr>
      <td>US South</td>
      <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
	  <td>Kibana 5.1</td>
    </tr>
</table>




