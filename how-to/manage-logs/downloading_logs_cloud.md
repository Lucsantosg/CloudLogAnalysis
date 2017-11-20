---

copyright:
  years: 2017
lastupdated: "2017-11-20"

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

Complete the following steps to download log data that is available in a space into a local file:

## Step 1: Log in to the {{site.data.keyword.Bluemix_notm}}
{: #step1}

Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

## Step 2: Identify what logs are available
{: #step2}

1. Use the `bx logging log-show` command to see what logs are available for the last 2 weeks. Run the following command:

    ```
    bx logging log-show
    ```
    {: codeblock}
    
    For example, the output of running this command is:
    
    ```
    bx logging log-show 
    Showing log status of resource: cedc73c5-1234-5678-abcd-378620d6fab5 ...

    Date         Size     Count   Searchable   Types   
    2017-11-16   794008   706     All          syslog, default   
	2017-11-17   794008   706     All          default   
    Logs of resource cedc73c5-1234-5678-abcd-378620d6fab5 is showed
    OK
    ```
    {: screen}

    **Note:** The {{site.data.keyword.loganalysisshort}} service is a global service that uses the Coordinated Universal Time (UTC). Days are define as UTC days. To get logs for a specific local-time day, you might need to download multiple UTC days.


## Step 3: Create a session
{: #step3}

A session is required to define the scope of log data that is available for a download, and to keep the status of the download. 

Use the command [cf logging session-create](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#session_create) to create a session. Optionally, you can specify start date, end date, and types of logs when you create a session:  

* When you specify the start date and the end date, the session provides access to logs between those inclusive dates. 
* When you specify the type of log (**-t**), the session provides access to a particular type of log. This is an important feature when you manage logs at scale, because you can scope a session to only a small subset of logs that you are interested in.

To create a session that is used to download all the logs that are available for the last 2 weeks, run the following command:

```
bx logging session-create 
```
{: codeblock}

The session returns the following information:

* The date range to be downloaded. The default is the current UTC date.
* The log types to be downloaded. By default, includes all log types that are available for the time period that you specify when you create the session. 
* Information about whether to include the entire account, or just the current space. By default, you get logs in the space where you are logged in.
* The session Id, that is required to download logs.

For example,

```
$ bx logging session-create
Creating session for lopezdsr@uk.ibm.com resource: cedc73c5-6d55-4193-a9de-378620d6fab5 ...

ID                                     Space                                  CreateTime                       AccessTime                       Start        End          Type   
944aec4d-61f4-43d1-8f3b-c040195122da   12345678-1234-5678-abcd-378620d6fab5   2017-11-17T14:17:25.611542863Z   2017-11-17T14:17:25.611542863Z   2017-11-04   2017-11-17   ANY_TYPE   
Session: 944aec4d-61f4-43d1-8f3b-c040195122da is created
```
{: screen}

**Tip:** To see the list of active sessions, run the command [bx logging sessions](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#session_list).

## Step 4: Download log data to a file
{: #step4}

To download the logs that are specified by the session parameters, run the following command:

```
bx logging log-download -o Log_File_Name Session_ID
```
{: codeblock}

where

* Log_File_Name is the name of the output file.
* Session_ID is the GUID of the session. You obtain this value in the previous step.

For example,

```
bx logging log-download -o helloLogs.gz -jshdjsunelsssr4566722==
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

After the download is complete, you must delete the session by using the [cf logging session delete](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#delete) command. 

Run the following command to delete a session:

```
bx logging session-delete Session_ID
```
{: codeblock}

Where Session_ID is the GUID of the session that you created in a previous step.

For example,

```
bx logging session-delete -jshdjsunelsssr4566722==
Deleting session: -jshdjsunelsssr4566722== of resource: 12345678-1234-5678-abcd-378620d6fab5 ...
Session: -jshdjsunelsssr4566722== is deleted

```
{: screen}




