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

# Defining custom search queries
{:#define_search}

In the search bar of the Discover page, you can define and save search queries by using the Lucene query language. For each search, you can apply filters to refine the entries that are available for analysis.
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances, and all Lite plan instances are deleted. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.Bluemix_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}

Complete the following tasks to define a custom search:

1. Launch Kibana.

    For Cloud Foundry (CF) apps, see [launch Kibana from the dashboard of a CF app](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-launch#launch_Kibana_from_cf_app).

	For containers that run in the {{site.data.keyword.Bluemix_notm}}-managed infrastructure, see [launch Kibana from the dashboard of a container](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-launch#launch_Kibana_for_containers).
    
    For all cloud resources, for example containers that run in a Kubernetes cluster, see [launch Kibana from the browser](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-launch#launch_Kibana_from_browser). 
	
	When you access Kibana, the default search is applied. You can see the logs for the list of instances of the resource that you are querying. You can filter the logs for any or all of the {{site.data.keyword.Bluemix_notm}} resources in that space.

2. Look at the Discover page to see what subset of your data it displays. For more information, see [Identifying the data that is displayed in your Kibana Discover page](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analize_logs_interactively#identify_data). Then, modify the default query to filter entries.

    **Note:** Use the Lucene query language to define your custom query. For more information, see [Apache Lucene - Query Parser Syntax  ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}
    
    When Kibana is launched from the {{site.data.keyword.Bluemix_notm}} UI, to modify the query and define multiple search criteria, you can use the logical terms **AND** and **OR**. These operators must be in uppercase.    
    
    * To search for a keyword, or part of a keyword, enter a word followed by an asterisk (*), which is a wildcard; for example, `Java*`. 
    * To search for a particular phrase, enter that phrase in double quotation marks (" "); for example, `"Java/1.8.0"`.
    * To create more complex searches, you can use the logical terms AND and OR; for example `"Java/1.8.0" OR "Java/1.7.0"`.
    * To search for a value within a particular field, enter your search in the following form: *log_field_name:search_term*; for example, `instance_id:"1"`.
    * To search for a range of values for a particular log field, enter your search in the following form: *log_field_name:[start_of_range TO end_of_range]*; for example, `instance_id:["1" TO "2"]`.

     For example, for a CF app, you can create a query `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]`  that lists entries for instances *0* and *1* only. 

3. Save the query so you can reuse it later. For more information, see [Saving a search](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-define_search#save_search1). 

**Note:** If you need to delete a query, see [Deleting a search](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-define_search#delete_search).



## Deleting a search
{: #delete_search}

To delete a search, complete the following steps in the Settings page:

1. In the Settings page, select the **Objects** tab.

2. In the **Searches** tab, select the search that you want to delete.

3. Click **Delete**.


## Exporting a search
{: #export_search}

To export a search, complete the following steps in the Settings page:

1. In the Settings page, select the **Objects** tab.

2. In the **Searches** tab, select the search that you want to export.

3. Click **Export**.

4. Save the file.

 
## Importing a search
{: #import_search}

To import a search, complete the following steps in the Settings page:

1. In the Settings page, select the **Objects** tab.

2. In the **Searches** tab, select **Import**.

3. Select a file and click **Open**.

The search is added to the list of searches.

## Refreshing the content of a search
{: #refresh_search}

To manually refresh the content of a search, you can click the magnifying glass that is available in the search bar. 

To refresh automatically the data that is shown in the Discover page, you can configure a refresh interval. The current value of the refresh interval is displayed in the menu bar of the Discover page. By default, auto-refresh is set to **OFF**.

Complete the following steps to set a refresh interval:

1. In the Discover page, click the **Time Filter** that is available in the menu bar.

2. Click **Auto Refresh** ![Auto Refresh](images/auto_refresh_icon.jpg "Auto Refresh").

3. Choose a refresh interval from the list. 

**Note**: After you enable an auto-refresh interval, you can pause it by clicking the pause button ![Pause](images/auto_refresh_pause_icon.jpg "Pause").


## Reloading a search
{: #reload_search1}

Complete the following steps to load a saved search:

1. In the toolbar of the Discover page, click the **Load Search** button ![Load search](images/load_icon.jpg "Load search").

2. Select the search that you want to load. 

## Starting a new search
{: #k4_new_search}

To start a new search, click the **New Search** button ![New search](images/new_search_icon.jpg "New search") in the Discover page toolbar.

## Saving a search 
{: #save_search1}

Consider the following information about saving custom searches in Kibana:

* When you save a search, the search query string and the currently selected index pattern are saved.
* When you open a search in the *Discover* page, and modify it, you can choose to save it with the same name, or you can save the modified custom search with a different name. By default, the search name that is provided is the one that corresponds to the custom search that you opened initially.

    * To save the modified custom search with the same name, click **Save**. Note that the original custom search is overwritten. 
	
	* To save the modified custom search with a different name, enter a new name in the field **Save Search**, and then, click **Save**. 


Complete the following steps to save the current search in the Discovery page:

1. In the toolbar of the Discover page, click the **Save Search** button ![Save search](images/save_search_icon.jpg "Save search").

2. Enter a name for the search.

    **Note:** When you click **Save**, there is no warning on over-write, thus if you specify an existing name, the save will replace that version without any indication.

3. Click **Save**. 
