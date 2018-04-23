---

copyright:
  years: 2017, 2018

lastupdated: "2018-04-19"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Viewing log information
{: #viewing_log_status}

Use the [bx logging log-show](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#status) command to obtain information about the logs that are collected and stored in Log Collection. You can obtain information about the size, number of records, log types, and whether the logs are available or not for analysis in Kibana.
{:shortdesc}

## Obtaining information about logs over a period of time
{: #viewing_logs}

Use `bx logging log-show` command with the options **-s** to set the start day and **-e** to set the end date. For example:

* `bx logging log-show` provides information for the last 2 weeks.
* `bx logging log-show -s 2017-05-03` provides information from May 3rd, 2017 till the current date.
* `bx logging log-show -s 2017-05-03 -e 2017-05-08` provides information between May 3, 2017 and May 8, 2017. 

Complete the following steps to get information about logs that are stored in a space:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Run the following command:

    ```
    bx logging log-show
    ```
    {: codeblock}
    
    For example,
    
    ```
    $ bx logging log-show -s 2017-11-17 -e 2017-11-17
    Showing log status of resource: cedc73c5-1234-5678-abcd-378620d6fab5 ...

    Date         Size     Count   Searchable   Types   
    2017-11-17   794008   706     All          default   
    Logs of resource cedc73c5-1234-5678-abcd-378620d6fab5 is showed
    OK
    ```
    {: screen}


## Obtaining information about a type of log over a period of time
{: #viewing_logs_by_log_type}

To obtain information about a type of log over a period of time, use the `bx logging log-show` command with the options **-t** to specify the type of log, **-s** to set the start day, and **-e** to set the end date. For example,

* `bx logging log-show -t syslog` provides information about logs of type *syslog* for the last 2 weeks.
* `bx logging log-show -s 2017-05-03 -t syslog` provides information about logs of type *syslog* from May 3rd, 2017 till the current date.
* `bx logging log-show -s 2017-05-03 -e 2017-05-08 -t syslog` provides information about logs of type *syslog* between May 3, 2017 and May 8, 2017. 

Complete the following steps to get information about a type of log over a period of time:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Run the following command:

    ```
    bx logging log-show -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    where
    
    * *-s* is used to set the start date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-e* is used to set the end date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-t* is used to set the log type.
    
    You can specify multiple log types by separating each type with a comma, for example, **log_type_1,log_type_2,log_type_3**. 
    
    For example,
    
    ```
    $ bx logging log-show -s 2017-05-24 -e 2017-05-25 -t syslog
    Showing log status of resource: cedc73c5-1234-5678-abcd-378620d6fab5 ...

    Date         Size     Count   Searchable   Types   
    2017-11-17   794008   706     All          syslog   
    Logs of resource cedc73c5-1234-5678-abcd-378620d6fab5 is showed
    OK
    ```
    {: screen}



## Obtaining information about logs at account level
{: #viewing_logs_account}

To obtain information about logs that are available at account level over a period of time, use the `bx logging log-show` command with the option **-r account** and **-i** to set the ID of the account. You can also specify the options **-t** to specify the type of log, **-s** to set the start day, and **-e** to set the end date. 

Complete the following steps to get account information about logs:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Get the account ID.

    For more information, see [How do I get the GUID of an account](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Run the following command:

    ```
    bx logging log-show -r account -i AccountID -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    where
    
    * *-r account* is used to set the domain where you want to get information about the logs.
    * *-i AccountID* is used to set the ID of the account.
    * *-s* is used to set the start date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-e* is used to set the end date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-t* is used to set the log type.
    

    You can specify multiple log types by separating each type with a comma, for example, **log_type_1,log_type_2,log_type_3**. 
 
    For example, to show information about logs that are stored for November 17 2017 at the account domain for the account *123456789123456789567c9c8de6dece*, run the following command:
    
    ```
    $ bx logging log-show -r account -i 123456789123456789567c9c8de6dece -s 2017-05-24 -e 2017-05-25
	Showing log status of resource: 123456789123456789567c9c8de6dece ...

    Date         Size      Count   Searchable   Types   
	2017-11-17   794008    200     All          syslog  
    Logs of resource 123456789123456789567c9c8de6dece is showed
    OK
    ```
    {: screen}


## Obtaining information about logs at org level
{: #viewing_logs_org}

To obtain information about logs that are available at the organization level over a period of time, use the `bx logging log-show` command with the option **-r org** and **-i** to set the ID of the organization. You can also specify the options **-t** to specify the type of log, **-s** to set the start day, and **-e** to set the end date. 

Complete the following steps to get account information about logs:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Get the account ID.

    For more information, see [How do I get the GUID of an organization](/docs/services/CloudLogAnalysis/qa/cli_qa.html#org_guid).
    
3. Run the following command:

    ```
    bx logging log-show -r org -i OrgID -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    where
    
    * *-r org* is used to set the domain where you want to get information about the logs.
    * *-i OrgID* is used to set the ID of the organization.
    * *-s* is used to set the start date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-e* is used to set the end date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-t* is used to set the log type.
    

    You can specify multiple log types by separating each type with a comma, for example, **log_type_1,log_type_2,log_type_3**. 
 
    For example, to show information about logs that are stored for November 17 2017 at the org domain for the organization with ID *abcd56789123456789567c9c8de6dece*, run the following command:
    
    ```
    $ bx logging log-show -r org -i abcd56789123456789567c9c8de6dece -s 2017-05-24 -e 2017-05-25
	Showing log status of resource: abcd56789123456789567c9c8de6dece ...

    Date         Size      Count   Searchable   Types   
	2017-11-17   794008    200     All          syslog  
    Logs of resource abcd56789123456789567c9c8de6dece is showed
    OK
    ```
    {: screen}






