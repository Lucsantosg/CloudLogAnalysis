---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Downloading logs
{: #downloading_logs}

You can download logs to a local file or pipe data into another program. You download of logs within the context of a session. A session specifies which logs will be downloaded. If the download of the logs is interrupted, the session enables resuming the download from where it left off. After the download is completed, you must delete the session.
{:shortdesc}

Complete the following steps to download log data that is available in a {{site.data.keyword.Bluemix_notm}} space into a local file:

## Step 1: Log in to the IBM Cloud

Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

## Step 2: Identify what logs are available
{: #step2}

1. Use the `bx cf logging status` command to see what logs are available for the last 2 weeks. Run the following command:

    ```
    bx cf logging status
    ```
    {: codeblock}
    
    For example, the output of running this command is:
    
    ```
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}

    **Note:** The {{site.data.keyword.loganalysisshort}} service is a global service that uses the Coordinated Universal Time (UTC). Days are define as UTC days. To get logs for a specific local-time day, you might need to download multiple UTC days.


## Step 3: Create a session
{: #step3}

A session is required to define the scope of log data that is available for a download, and to keep the status of the download. 

Use the command [cf logging session create](/docs/services/CloudLogAnalysis/reference/logging_cli.html#session_create) to create a session. Optionally, you can specify start date, end date, and types of logs when you create a session:  

* When you specify the start date and the end date, the session provides access to logs between those inclusive dates. 
* When you specify the type of log (**-t**), the session provides access to a particular type of log. This is an important feature when you manage logs at scale, because you can scope a session to only a small subset of logs that you are interested in.

To create a session that is used to download logs of type *log*, run the following command:

```
bx cf logging session create -t log
```
{: codeblock}

The session returns the following information:

* The date range to be downloaded. The default is the current UTC date.
* The log types to be downloaded. By default, includes all log types that are available for the time period that you specify when you create the session. 
* Information about whether to include the entire account, or just the current space. By default, you get logs in the space where you are logged in.
* The session Id, that is required to download logs.

For example,

```
$ bx cf logging session create -t log     
+--------------+--------------------------------------+
|     NAME     |                VALUE                 |
+--------------+--------------------------------------+
| Access-Time  | 2017-05-25T18:04:21.743792338Z       |
| Create-Time  | 2017-05-25T18:04:21.743792338Z       |
| Date-Range   | {                                    |
|              |  "End": "2017-05-25T00:00:00Z",      |
|              |  "Start": "2017-05-25T00:00:00Z"     |
|              | }                                    |
| Id           | -jshdjsunelsssr4566722==             |
| Space        | fdgrghg3-b090-4567-vvfg-afbc436902a3 |
| Type-Account | {                                    |
|              |  "Type": "log"                       |
|              | }                                    |
| Username     | xxx@yyy.com                          |
+--------------+--------------------------------------+
```
{: screen}

**Tip:** To see the list of active sessions, run the command [cf logging session list](/docs/services/CloudLogAnalysis/reference/logging_cli.html#session_list).

## Step 4: Download log data to a file
{: #step4}

To download the logs that are specified by the session parameters, run the following command:

```
bx cf logging download -o Log_File_Name Session_ID
```
{: codeblock}

where

* Log_File_Name is the name of the output file.
* Session_ID is the GUID of the session. You obtain this value in the previous step.

For example,

```
bx cf logging download -o helloLogs.gz -jshdjsunelsssr4566722==
 160.00 KB / 380.33 KB [==============>------------------------]  42.07% 20.99 KB/s 10s
```
{: screen}

The progress indicator moves from 0 to 100% as the logs download.

**Note:** 

* The format of the downloaded data is compressed JSON. If you unzip the .gz file and open it, you can see the data in JSON format. 
* The compressed JSON is suitable for ingestion by ElasticSearch or Logstash. If -o is not given, the data will stream to stdout so that you can pipe it directly into your own ELK stack.
* You can also process the data with any program that can parse JSON. 

## Step 5: Delete the session
{: #step5}

After the download is complete, you must delete the session by using the [cf logging session delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#session_delete) command. 

Run the following command to delete a session:

```
bx cf logging session delete Session_ID
```
{: codeblock}

Where Session_ID is the GUID of the session that you created in a previous step.

For example,

```
bx cf logging session delete -jshdjsunelsssr4566722==
+---------+------------------------+
|  NAME   |         VALUE          |
+---------+------------------------+
| Message | Delete session success |
+---------+------------------------+
```
{: screen}




