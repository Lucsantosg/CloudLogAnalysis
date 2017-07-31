---

copyright:
  years: 2017
lastupdated: "2017-07-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Migration considerations after the upgrade of the Elastic Stack to version 5.1 
{: #es17_to_es51}

In {{site.data.keyword.Bluemix}}, the ElasticSearch (ELK) stack is upgraded from version 1.7 to version 5.1. New features, new URLS to ingest logs, and new URLs to analyze logs in Kibana are available. For more information, see [ElasticSearch 5.1 ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html).
{:shortdesc}

This feature does not apply to users that use the logging service with Docker containers that are deployed in a Kubernetes cluster. These containers already use the Elastic version 2.3.

## Regions
{: #regions}

The Elastic version 5.1 is available in the following region:

* US South


## What's new
{: #features}

1. Different URLs to work with logs and metrics.

    In Elastic 1.7, the same URL was shared to display and monitor logs and metrics. With the upgrade to Elastic 5.1, you have separate URLS to view logs and metrics. For more information, see [logging URLs](#logging).
    
2. Support for Kibana 5.1. 

    You can launch Kibana from the {{site.data.keyword.Bluemix_notm}} UI, or directly from the new logging URL. For more information, see [Analyzing logs with Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana).
    
    Kibana 3 is deprecated. You can launch Kibana 3 through the [ELK 1.7 logging URL](#logging). There are different URLs per region. **Note:** Access to Kibana 3 dashboards is currently available for you to compare and migrate your Kibana 3 dashboards to Kibana 5.1 ones. 
    
    If you have Kibana dashboards that are built on the ELK 1.7 stack, you must migrate them to the ELK 5.1 environment.
    
    For more information about Kibana 5.1, see [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.
    
3. Added type-based suffixes to custom fields.

    You can configure custom fields as Kibana search fields. Each field that is available in a message is parsed to the type of field that matches is value. For example, each field in the following JSON message: 

    ```
    {"field1":"string type",
     "field2":123,
     "field3":false,
     "field4":"4567"
     }
    ```
    {: screen}
    
    is available as a field that you can use for filtering and searches:

    * field1 is parsed as field1_str of type string.
    * field2 is parsed as field1_int of type integer.
    * field3 is parsed as field3_bool of type boolean.
    * field4 is parsed as field4_str of type string.
    
    The sample JSON message is a log that you sent to the logging service. 

    **Note:** This feature is only available in Elastic 5.1. This feature is not available in Elastic 1.7 to avoid breaking Kibana3 dashboards.


## Logging 
{: #logging}

Different URLs are used to send logs into {{site.data.keyword.Bluemix_notm}} and to analyze data in Kibana.

The following table lists the new URL for the US South region:

<table>
  <caption>URLs for the US South region</caption>
    <tr>
      <th>Type</th>
      <th>ELK 1.7 </th>
	  <th>ELK 5.1 </th>
    </tr>
  <tr>
    <td>Ingestion URL for logs</td>
    <td>logs.opvis.bluemix.net:9091</td>
	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>Kibana URL to analyze logs</td>
    <td>https://logmet.ng.bluemix.net</td>
	<td>https://logging.ng.bluemix.net</td>
  </tr>
</table>

