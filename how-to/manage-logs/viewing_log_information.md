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

# Viewing log information
{: #viewing_log_status}

Use the [cf logging status](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status1) command to obtain information about the logs that are collected and stored in Log Collection.
{:shortdesc}

## Obtaining information about logs over a period of time
{: #viewing_logs1}

Use the `cf logging status` command to see the size, count, log types, and whether the logs are available or not for analysis in Kibana for logs that are stored in Log Collection. 

Use `cf logging status` command with the options **-s** to set the start day and **-e** to set the end date. For example:

* `cf logging status` provides information for the last 2 weeks.
* `cf logging status -s 2017-05-03` provides information from May 3rd, 2017 till the current date.
* `cf logging status -s 2017-05-03 -e 2017-05-08` provides information between May 3, 2017 and May 8, 2017. 

Complete the following steps to get information about logs:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Run the *status* command.

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


## Obtaining information about a type of log over a period of time
{: #viewing_logs_by_log_type1}

To obtain information about a type of log over a period of time, use the `cf logging status` command with the options **-t** to specify the type of log, **-s** to set the start day, and **-e** to set the end date. For example,

* `cf logging status -t syslog` provides information about logs of type *syslog* for the last 2 weeks.
* `cf logging status -s 2017-05-03 -t syslog` provides information about logs of type *syslog* from May 3rd, 2017 till the current date.
* `cf logging status -s 2017-05-03 -e 2017-05-08 -t syslog` provides information about logs of type *syslog* between May 3, 2017 and May 8, 2017. 

Complete the following steps to get information about a type of log over a period of time:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Run the *status* command.

    ```
    ibmcloud cf logging status -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    where
    
    * *-s* is used to set the start date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-e* is used to set the end date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-t* is used to set the log type.
    
    You can specify multiple log types by separating each type with a comma, for example, **log_type_1,log_type_2,log_type_3**. 
    
    For example,
    
    ```
    $ ibmcloud cf logging status -s 2017-05-24 -e 2017-05-25 -t log
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 |        log         |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}



## Obtaining account information about logs
{: #viewing_logs_account1}

To obtain information about logs over a period of time across the {{site.data.keyword.Bluemix_notm}} account, use the `cf logging status` command with the option **-a**. You can also specify the options **-t** to specify the type of log, **-s** to set the start day, and **-e** to set the end date. 

Complete the following steps to get account information about logs:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Run the *status* command.

    ```
    ibmcloud cf logging status -a -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    where
    
    * *-a* is used to specify account level information
    * *-s* is used to set the start date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-e* is used to set the end date in Universal Coordinated Time (UTC): *YYYY-MM-DD*
    * *-t* is used to set the log type.
    

    You can specify multiple log types by separating each type with a comma, for example, **log_type_1,log_type_2,log_type_3**. 
 
    For example,
    
    ```
    $ ibmcloud cf logging status -s 2017-05-24 -e 2017-05-25 -t log -a
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 |        log         |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}









