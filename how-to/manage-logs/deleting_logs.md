---

copyright:
  years: 2017, 2018

lastupdated: "2018-07-25"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deleting logs
{: #deleting_logs}

Use the [ibmcloud cf logging delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status) command to delete logs from Log Collection. 
{:shortdesc}

* You can delete logs within a specific time range.
* You can delete logs by type. Notice that each log file has only one type of log entries.
* You can delete logs for a space, or at the account domain.


## Deleting logs for a specific period of time
{: #fix_period}

Complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
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
{: #log_type}

Complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
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

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
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
	








