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

# Analyzing logs in Kibana by using visualizations 
{:#kibana_visualizations}

Use the *Visualize* page in Kibana to create visualizations such as graphs and tables that you can use to analyze your log data and compare results. 
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.cloud_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}

You can use a visualization individually to analyze your logs. 

* You can create visualizations from a search that you define and save in the *Discover* page or from a new query that you define in the *Visualize* page. The search defines the subset of data that a visualization displays.

* The type of visualization that you choose determines how the data is displayed for analysis.

The following table lists different visualization types:

| Type of visualization | Description |
|-----------------------|-------------|
| Area chart | Displays graphically quantitative data. Use to compare two or more sets of aggregated data. |
| Data table | Displays raw data in tabular form for a composed aggregation. |
| Line chart | Displays time based data. Use to compare two or more sets of time-based aggregated data. |
| Markdown widget | Use to display text information. |
| Metric | Use to show a count of hits, or the exact average a numeric field. |
| Pie chart | Use to display different values of a field. | 
| Vertical bar chart | Displays data that is time-based and data that is not time-based. Use to group data. |
{: caption="Table 1. Visualization types" caption-side="top"}

In the Visualize page, you can perform any of the following tasks:

| Task | More information |
|------|------------------|
| [Create a new visualization](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-kibana_visualizations#create) | You can create visualizations from a search that you define and save in the *Discover* page or from a new query that you define in the *Visualize* page. |
| [Delete a visualization](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-kibana_visualizations#delete) | Delete visualizations that are not required. |
| [Export a visualization](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-kibana_visualizations#export) | You can export a visualization as a JSON file.  |
| [Import a visualization](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-kibana_visualizations#import1) | You can import a visualization as a JSON file.  |
| [Load a visualization](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-kibana_visualizations#reload2) | You can upload a visualization to either update its data, mofify it, analyze the data. |
| [Save a visualization](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-kibana_visualizations#save2) | You can save visualizations for later reuse. |
{: caption="Table 2. Tasks to work with visualizations" caption-side="top"}


## Creating visualizations from queries in Kibana
{: #create}

Complete the following steps to create a visualization from the Visualize page:

1. Launch Kibana, and then, select the **Visualize** page.

2. Choose a type of visualization, for example, *table*.

3. Select a visualization that you saved earlier from the **Or, From a Saved Search**, or select an index from the section **From a New Search, Select Index**.

4. Configure the query.

    * If you select **Or, From a Saved Search**, select a search query. The query is used to retrieve the data that is used for the visualization. 
	
	    After you select a search, the visualization builder opens and loads the data for the selected query. 
		
		**Note**: Any changes that you make to a saved search are automatically reflected in the visualization. To disable automatic updates that you make to the query that is linked to this visualization, double click the message *This visualization is linked to a saved search: your_search_name* 

    * If you select **From a New Search, Select Index**, define a new query. The query is used to define the subset of data that is retrieved and used by  the visualization.

        For more information, see [Filtering logs by defining custom queries](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-define_search#define_search).

For more information about Kibana, see the [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.


## Deleting a visualization
{: #delete}

To delete a visualization, complete the following steps in the **Management** page:

1. In the **Management** page, select **Saved Objects**.

2. In the **Visualizations** tab, select the visualizations that you want to delete.

3. Click **Delete**.


## Exporting a visualization
{: #export1}

To export a visualization as a JSON file, complete the following steps in the **Management** page:

1. In the **Management** page, select **Saved Objects**.

2. In the **Visualizations** tab, select the visualization that you want to export.

3. Click **Export**.

4. Save the file.

## Importing a visualization
{: #import1}

To import a visualization as a JSON file, complete the following steps in the **Management** page:

1. In the **Management** page, select **Saved Objects**.

2. In the **Visualizations** tab, select **Import**.

3. Select a file and click **Open**.

The visualization is added to the list of visualizations.


 
## Loading a visualization
{: #reload2}

Complete the following steps to load a saved visualization:

1. In the toolbar of the Visualize page, click **Open**.

2. Select the visualization that you want to load. 


## Saving a visualization
{: #save2}

Complete the following steps to save a visualization in the Visualize page:

1. In the toolbar of the Visualize page, click **Save**.

2. Enter a name for the visualization.

3. Click Save. 


