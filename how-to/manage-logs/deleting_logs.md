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
{:deprecated: .deprecated}

# Deleting logs
{: #deleting_logs1}

Use the [ibmcloud cf logging delete](/docs/services/CloudLogAnalysis/reference?topic=cloudloganalysis-logging_cli#status1) command to delete logs from Log Collection. 
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances, and all Lite plan instances are deleted. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.Bluemix_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}

* You can delete logs within a specific time range.
* You can delete logs by type. Notice that each log file has only one type of log entries.
* You can delete logs for a space, or at the account domain.


## Deleting logs for a specific period of time
{: #fix_period}

Complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
    
2. Run the *status* command to see the logs that are available in Log Collection.

    ```
    ibmcloud cf logging status
    ```
    {: codeblock}
    
    For example,
    
    ```
    $ ibmcloud cf logging status
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. Delete the logs that are stored on a specific day.

    ```
	ibmcloud cf logging delete -s StartDate -e EndDate
	```
	{: codeblock}
	
	where
	
	* *-s* sets the start date in Coordinated Universal Time (UTC): YYYY-MM-DD, for example, 2006-01-02.
    * *-e* sets the end date in Coordinated Universal Time (UTC): YYYY-MM-DD
    	
	For example, to delete the logs for 25 May 2017, run the following command:
	
	```
	ibmcloud cf logging delete -s 2017-05-25 -e 2017-05-25
	```
	{: screen}

	
## Deleting logs by log type for a specific period of time 
{: #log_type1}

Complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
    
2. Run the *status* command to see the logs that are available in Log Collection.

    ```
    ibmcloud cf logging status
    ```
    {: codeblock}
    
    For example,
    
    ```
    $ ibmcloud cf logging status
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. Delete the logs that are stored on a specific day.

    ```
	ibmcloud cf logging delete -s StartDate -e EndDate -t LogType
	```
	{: codeblock}
	
	where
	
	* *-s* sets the start date in Coordinated Universal Time (UTC): YYYY-MM-DD, for example, 2006-01-02.
    * *-e* sets the end date in Coordinated Universal Time (UTC): YYYY-MM-DD
	* *-t* sets the log type.
    	
	For example, to delete the logs of type linux_syslog for 25 May 2017, run the following command:
	
	```
	ibmcloud cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
	```
	{: screen}

		
	
## Deleting account logs by log type for a specific period of time 
{: #acc_log_type}

Complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
    
2. Run the *status* command to see the logs that are available in Log Collection at the account level.

    ```
    ibmcloud cf logging status  -a
    ```
    {: codeblock}
    
    For example,
    
    ```
    $ ibmcloud cf logging status -a
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. Delete the logs that are stored on a specific day.

    ```
	ibmcloud cf logging delete -s StartDate -e EndDate -t LogType -a
	```
	{: codeblock}
	
	where
	
	* *-s* sets the start date in Coordinated Universal Time (UTC): YYYY-MM-DD, for example, 2006-01-02.
    * *-e* sets the end date in Coordinated Universal Time (UTC): YYYY-MM-DD
	* *-t* sets the log type.
    	
	For example, to delete the logs of type linux_syslog for 25 May 2017 that are stored in Log Collection at account level, run the following command:
	
	```
	ibmcloud cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog -a
	```
	{: screen}
	








