---

copyright:
  years: 2017, 2018

lastupdated: "2018-07-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Analyzing logs in Kibana through a dashboard
{:#analize_logs_dashboard}

Use the *Dashboard* page in Kibana to display collections of visualizations that are grouped in dashboards. Use the dashboards to analyze your log data and compare results.
{:shortdesc}

In the {{site.data.keyword.Bluemix}}, there are different types of dashboards that you can define and customize to visualize and analyze the data. For example, the following table lists some common dashboard types:

| Type of dashboard | Description |
|-------------------|-------------|
| Single-cf-app dashboard | This is a dashboard that shows information for a single Cloud Foundry application. |
| Single container dashboard  | This is a dashboard that shows information for a single container.  |
| Container group dashboard  | This is a dashboard that shows information for a specific container group.  |
| Multi-cf-app dashboard | This is a dashboard that shows information for all the Cloud Foundry applications that are deployed in the same space.  | 
| Multi-container dashboard | This is a dashboard that shows information for all the containers that are deployed in the same space.  |
| Space dashboard | This is a dashboard that shows logging data that is available in a space.  | 
{: caption="Table 1. Samples of dashboard types" caption-side="top"}

To visualize the data in a dashboard, you configure panels. Kibana includes different visualizations such as table, trends, and histogram that you can use to analyze the information. A visualization is added as a panel to a dashboard. You can add, remove, and rearrange panels in the dashboard. The objective of each panel varies. Some panels are organized into rows that provide the results of a one or more queries. Other panels display documents or custom information. Each panel is based on a search. The search defines the subset of data that the panel displays. For example, you can configure a bar chart, pie chart, or table to visualize the data and analyze it.  

The following table lists different tasks that you can perform in the Dashboard page:

| Task | More information |
|------|------------------|
| [Add a visualization](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#add_visualization) | You can add an existing visualization or search to a dashboard.|
| [Create a new dashboard](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#new) | You can create multiple dashboards. Each dashboard can be designed to include different searches, visualizations, and a different subset of log data.  |
| [Delete a dashboard](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#delete) | Delete dashboards that are not required. |
| [Export a dashboard](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#export) | You can export a dashboard as a JSON file. |
| [Import a dashboard](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#import) | You can import a dashboard as a JSON file. |
| [Load a dashboard](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#reload) | You can upload a dashboard to either update its data, modify it, or analyze the data. |
| [Save a dashboard](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#save) | You can save a dashboard for later reuse. |
{: caption="Table 2. Tasks to work with dashboards" caption-side="top"}

For more information about Kibana, see the [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.


## Adding a new search or visualization
{: #add_visualization}

Complete the following steps to add an existing visualization or search:

1. In the toolbar of the Dashboard page, click **Add**. 

    **Note**: You can add visualizations and searches. 

2. Select the **Visualizations** tab to add a visualization or select the **Searches** tab to add a search.

3. Click the search or visualization that you want to add.

    A panel for that search or visualization is added to the dashboard.

	
## Creating a new Kibana dashboard
{: #new}

Complete the following steps to create a new dashboard:

1. In the toolbar of the Dashboard page, click **Add**. 

2. Add one or more searches and visualizations. For more information, see [Adding a new search or visualization](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#add_visualization).

    When you add a search or a visualization, a panel is added in the dashboard.

3. Drag a panel and drop in the part of the dashboard where you want to position it.
 
4. Save the dashboard for future reuse. For more information, see [Saving a Kibana dashboard](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#save).


## Deleting a Kibana dashboard
{: #delete}

To delete a dashboard, complete the following steps in the **Management** page:

1. In the **Management** page, select **Saved Objects**.

2. In the **Dashboards** tab, select the dashboard that you want to delete.

3. Click **Delete**.

## Exporting a Kibana dashboard
{: #export}

To export a dashboard as a JSON file, complete the following steps in the **Management** page:

1. In the **Management** page, select **Saved Objects**.

2. In the **Dashboard** tab, select the dashboard that you want to export.

3. Click **Export**.

4. Save the file.

## Importing a Kibana dashboard
{: #import}

To import a dashboard as a JSON file, complete the following steps in the **Management** page:

1. In the **Management** page, select **Saved Objects**.

2. In the **Dashboard** tab, select **Import**.

3. Select a file and click **Open**.

The dashboard is added to the list of dashboards.

## Loading a Kibana dashboard
{: #reload}

Complete the following steps to load a saved dashboard:

1. In the toolbar of the Dashboard page, click **Open**.

2. Select a dashboard from the list of available dashboards that is shown under the field *Name*.

You can also search for a dashboard from the Search bar.

## Saving a Kibana dashboard
{: #save}

Complete the following steps to save a Kibana dashboard after you customize it:

1. In the toolbar, click **Save**.

2. Enter a name for the dashboard.

    **Note:** The name must not contain spaces.

3. Click **Save**.




