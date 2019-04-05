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

# Deleting logs
{: #deleting_logs}

Use the [ibmcloud logging log-delete](/docs/services/CloudLogAnalysis/reference?topic=cloudloganalysis-log_analysis_cli#delete) command to delete logs from Log Collection. 
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances, and all Lite plan instances are deleted. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.Bluemix_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}

* You can delete logs within a specific time range.
* You can delete logs by type. Notice that each log file has only one type of log entries.
* You can delete logs for a space, for an organization, or at the account domain.


## Deleting all logs for a specific period of time
{: #time_range}

Complete the following steps to delete all the logs that are stored in a space domain for a specific period of time:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
    
2. Run the following command to see the logs that are available in Log Collection.

    ```
    ibmcloud logging log-show
    ```
    {: codeblock}
    
    For example,
    
    ```
    $ ibmcloud logging log-show
    Showing log status of resource: 12345678-abcd-4193-aere-378620d6fab5 ...

    Date         Size       Count   Searchable          Types   
	2017-05-24   16         3020    None                default
	2017-05-25   1224       76115   All                 linux_syslog,log
    2017-05-26   19663113   17639   All                 default,linux_syslog  
    ```
    {: screen}
	
3. Delete the logs that are stored on a specific day.

    ```
	ibmcloud logging log-delete -s StartDate -e EndDate
	```
	{: codeblock}
	
	where
	
	* *-s* sets the start date in Coordinated Universal Time (UTC): YYYY-MM-DD, for example, 2006-01-02.
    * *-e* sets the end date in Coordinated Universal Time (UTC): YYYY-MM-DD
    	
	For example, to delete the logs for 25 May 2017, run the following command:
	
	```
	ibmcloud logging log-delete -s 2017-05-25 -e 2017-05-25
	```
	{: screen}

	
## Deleting logs by log type for a specific period of time 
{: #log_type}

Complete the following steps to delete logs by log type that are stored in a space domain for a specific period of time:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
    
2. Run the following command to see the logs that are available in Log Collection.

    ```
    ibmcloud logging log-show
    ```
    {: codeblock}
    
    For example,
    
    ```
    $ ibmcloud logging log-show
    Showing log status of resource: 12345678-1234-2edr-a9de-378620d6fab5 ...

    Date         Size       Count   Searchable          Types   
	2017-05-24   16         3020    None                default
	2017-05-25   1224       76115   All                 linux_syslog,log
    2017-05-26   19663113   17639   All                 default,linux_syslog  
    ```
    {: screen}
	
3. Delete the logs that are stored on a specific day.

    ```
	ibmcloud logging log-delete -s StartDate -e EndDate -t LogType
	```
	{: codeblock}
	
	where
	
	* *-s* sets the start date in Coordinated Universal Time (UTC): YYYY-MM-DD, for example, 2006-01-02.
    * *-e* sets the end date in Coordinated Universal Time (UTC): YYYY-MM-DD
	* *-t* sets the log type.
    	
	For example, to delete the logs of type linux_syslog for 25 May 2017, run the following command:
	
	```
	ibmcloud logging log-delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
	```
	{: screen}

		
	
## Deleting account logs by log type for a specific period of time 
{: #time_range_acc}

Complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
	
2. Get the account ID.

    For more information, see [How do I get the GUID of an account](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#account_guid).
    
3. Run the following command to see the logs that are available in Log Collection at the account level.

    ```
    ibmcloud logging log-show  -r account -i AccountID
    ```
    {: codeblock}
    
    For example,
    
    ```
    $ ibmcloud logging log-show -r account -i 123456789123456789567c9c8de6dece -s 2017-05-24 -e 2017-05-25
	Showing log status of resource: 123456789123456789567c9c8de6dece ...

    Date         Size       Count   Searchable          Types   
	2017-05-24   16         3020    All                 default
	2017-05-25   2000       76115   All                 linux_syslog,log
    2017-05-26   195678     17639   All                 default,linux_syslog    
    Logs of resource 123456789123456789567c9c8de6dece is showed
    OK
    ```
    {: screen}
	
4. Delete the logs that are stored on a specific day.

    ```
	ibmcloud logging log-delete -s StartDate -e EndDate -t LogType -r account -i AccountID
	```
	{: codeblock}
	
	where
	
	* *-s* sets the start date in Coordinated Universal Time (UTC): YYYY-MM-DD, for example, 2006-01-02.
    * *-e* sets the end date in Coordinated Universal Time (UTC): YYYY-MM-DD
	* *-t* sets the log type.
    	
	For example, to delete the logs of type linux_syslog for 25 May 2017 that are stored in Log Collection at account level, run the following command:
	
	```
	ibmcloud logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog -r account -i 123456789123456789567c9c8de6dece
	```
	{: screen}
	








