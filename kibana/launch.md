---

copyright:
  years: 2017

lastupdated: "2017-07-31"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Navigating to the Kibana dashboard
{: #launch}

You can launch Kibana from the {{site.data.keyword.loganalysisshort}} service, from the {{site.data.keyword.Bluemix}} UI, or directly from a web browser.
{:shortdesc}

For CF apps, and Docker containers that are deployed in an {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure, you can launch Kibana from {{site.data.keyword.Bluemix_notm}} to view and analyze data in context to the resource from which you launch Kibana. For example, you can launch to your specific CF app logs in Kibana, in context to that specific App.
    
For any cloud resource such as a Docker container that are deployed in a Kubernetes infrastructure, you can launch Kibana from a direct browser link or from the {{site.data.keyword.loganalysisshort}} service dashboard to see aggregated log data from services within a provided {{site.data.keyword.Bluemix_notm}} space. The query that is used to filter the data that is displayed in the dashboard retrieves log entries for a space in the {{site.data.keyword.Bluemix_notm}} organization. The log information that Kibana displays includes records for  all resources that are deployed within the space of the {{site.data.keyword.Bluemix_notm}} organization that you are logged in. 

The following table lists some cloud resources and the supported navigation methods to launch Kibana:

<table>
<caption>Table 1. List of resources and supported navigation methods. </caption>
  <tr>
    <th>Resource</th>
	<th>Navigating to the Kibana dashboard from the {{site.data.keyword.loganalysisshort}} service dashboard</th>
    <th>Navigating to the Kibana dashboard from the Bluemix dashboard</th>
    <th>Navigating to the Kibana dashboard from a web browser</th>
  </tr>
  <tr>
    <td>CF app</td>
	<td>Yes</td>
    <td>Yes</td>
    <td>Yes</td>
  </tr>  
  <tr>
    <td>Container deployed in a Kubernetes cluster</td>
	<td>Yes</td>
    <td>No</td>
    <td>Yes</td>
  </tr>  
  <tr>
    <td>Container deployed in a {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure</td>
	<td>Yes</td>
    <td>Yes</td>
    <td>Yes</td>
  </tr>  
</table>

For more information about Kibana, see the [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.
    

##  Navigating to Kibana from the dashboard of the Log Analysis service
{: #launch_Kibana_from_log_analysis}

The query that is used to filter the data that is displayed in Kibana retrieves log entries for that space in the {{site.data.keyword.Bluemix_notm}} organization. 
	
The log information that Kibana displays includes records for all resources that are deployed within the space of the {{site.data.keyword.Bluemix_notm}} organization that you are logged in.

Complete the following steps to launch Kibana from the dashboard of the {{site.data.keyword.loganalysisshort}} service:

1. Log in to {{site.data.keyword.Bluemix_notm}}, and then click the {{site.data.keyword.loganalysisshort}} service from the {{site.data.keyword.Bluemix_notm}} dashboard. 
    
2. Select the **Managed** tab in the {{site.data.keyword.Bluemix_notm}} UI.

3. Click **LAUNCH**. The Kibana dashboard opens.

By default, the **Discover** page loads with the default index pattern selected and a time filter set to the last 15 minutes. 

If the Discover page does not show any log entries, adjust the time picker. For more information, see [Setting a time filter](filter_logs.html#set_time_filter).

	
	
##  Navigating to Kibana from a web browser
{: #launch_Kibana_from_browser}

The query that is used to filter the data that is displayed in Kibana retrieves log entries for that space in the {{site.data.keyword.Bluemix_notm}} organization. 
	
The log information that Kibana displays includes records for all resources that are deployed within the space of the {{site.data.keyword.Bluemix_notm}} organization that you are logged in.

Complete the following steps to launch Kibana from a browser:

1. Open a web browser and launch Kibana. Then, log in to the Kibana user interface.
    
    For example, the following table lists the URL that you must use to launch Kibana per region:
      
    <table>
          <caption>Table 1. URLs to launch Kibana per region</caption>
           <tr>
            <th>Region</th>
            <th>URL</th>
          </tr>
          <tr>
            <td>US South</td>
            <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net) </td>
          </tr>
		  <tr>
            <td>United Kingdom</td>
            <td>[https://logmet.eu-gb.bluemix.net](https://logmet.eu-gb.bluemix.net)</td>
          </tr>
		  <tr>
            <td>Frankfurt</td>
            <td>[https://logging.eu-de.bluemix.net](https://logging.eu-de.bluemix.net)</td>
          </tr>
    </table>
	
	The Discover page in Kibana opens.
	
2. Select the index pattern for the {{site.data.keyword.Bluemix_notm}} space from where you want to view and analyze log data.

    1. Click **default-index**.
	
	2. Select the index pattern for the space. The format of the index pattern is the following:
	
	    ```
	    [logstash-Space_ID-]YYYY.MM.DD 
	    ```
        {screen}
	
	    where *Space_ID* is the GUID of the {{site.data.keyword.Bluemix_notm}} space where you want to view and analyze log data. 
	
If the Discover page does not show any log entries, adjust the time picker. For more information, see [Setting a time filter](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).


	
##  Navigating to Kibana from the dashboard of a CF app
{: #launch_Kibana_from_cf_app}

The query that is used to filter the data that is displayed in Kibana retrieves log entries for the {{site.data.keyword.Bluemix_notm}} CF app from where you launch Kibana.

To see the logs of a Cloud Foundry application in Kibana, complete the following steps:

1. Log in to {{site.data.keyword.Bluemix_notm}}, and then click the app name or container from the {{site.data.keyword.Bluemix_notm}} dashboard. 
    
2. Open the log tab in the {{site.data.keyword.Bluemix_notm}} UI.

    For CF apps, click **Logs** in the navigation bar. 
    The logs tab opens.  

3. Click **Advanced view**. The Kibana dashboard opens.

    By default, the **Discover** page loads with the default index pattern selected and a time filter set to the last 30 seconds. The search query is set to match all entries for the your CF app.

    If the Discover page does not show any log entries, adjust the time picker. For more information, see [Setting a time filter](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).


##  Navigating to Kibana from the dashboard of a container
{: #launch_Kibana_for_containers}

This method applies only to containers that are deployed in the {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure.

The query that is used to filter the data that is displayed in Kibana retrieves log entries for the container from where you launch Kibana.

To see the logs of a Docker container in Kibana, complete the following steps:

1. Log in to {{site.data.keyword.Bluemix_notm}}, and then click the container from the {{site.data.keyword.Bluemix_notm}} dashboard. 
    
2. Open the log tab in the {{site.data.keyword.Bluemix_notm}} UI.

    For containers that are deployed in the {{site.data.keyword.IBM_notm}}-managed Cloud infrastructure, select **Monitoring and logs** in the navigation bar and then, click the **Logging** tab. 
    
    The logs tab opens.  

3. Click **Advanced view**. The Kibana dashboard opens.

    By default, the **Discover** page loads with the default index pattern selected and a time filter set to the last 30 seconds. The search query is set to match all entries for the Docker container.

    If the Discover page does not show any log entries, adjust the time picker. For more information, see [Setting a time filter](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).

	



