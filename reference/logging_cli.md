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

# IBM Cloud Log Analysis CLI (CF plugin)
{: #logging_cli}

The {{site.data.keyword.loganalysislong}} CLI is a plug-in to manage the logs for cloud resources running in a space of a {{site.data.keyword.Bluemix}} organization.
{: shortdesc}

**Prerequisites**
* Before running the logging commands, log in to the {{site.data.keyword.Bluemix_notm}} with the `ibmcloud login` command to generate a {{site.data.keyword.Bluemix_short}}
 access token and authenticate your session. For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).

To find out about how to use the {{site.data.keyword.loganalysisshort}} CLI, see [Managing logs](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_analysis_ov#log_analysis_ov).

<table>
  <caption>Commands for managing logs</caption>
  <tr>
    <th>Command</th>
    <th>When to use it</th>
  </tr>
  <tr>
    <td>[ibmcloud cf logging](#base)</td>
    <td>Use this command to get information about the CLI, such as version or the list of commands.</td>
  </tr>
  <tr>
    <td>[ibmcloud cf logging auth](#auth)</td>
    <td>Use this command to get the logging token that you can use to send logs to the {{site.data.keyword.loganalysisshort}} service.</td>
  </tr>
  <tr>
    <td>[ibmcloud cf logging delete](#delete)</td>
    <td>Use this command to delete logs that are stored in Log Collection.</td>
  </tr>
  <tr>
    <td>[ibmcloud cf logging download (Beta)](#download)</td>
    <td>Use this command to download logs from Log Collection to a local file, or pipe logs to another program such an Elastic Stack. </td>
  </tr>
  <tr>
    <td>[ibmcloud cf logging help](#help)</td>
    <td>Use this command to get help on how to use the CLI, and a  list of all of the commands.</td>
  </tr>
  <tr>
    <td>[ibmcloud cf logging option](#option)</td>
    <td>Use this command to view or set the retention period for logs that are available in a space or account.</td>
  </tr>
  <tr>
    <td>[ibmcloud cf logging session create (Beta)](#session_create1)</td>
    <td>Use this command to create a new session.</td>
  <tr>
  <tr>
    <td>[ibmcloud cf logging session delete (Beta)](#session_delete1)</td>
    <td>Use this command to delete a session.</td>
  <tr>  
  <tr>
    <td>[ibmcloud cf logging session list (Beta)](#session_list1)</td>
    <td>Use this command to list active sessions and their IDs.</td>
  <tr>  
  <tr>
    <td>[ibmcloud cf logging session show (Beta)](#session_show1)</td>
    <td>Use this command to show the status of a single session.</td>
  <tr>  
  <tr>
    <td>[ibmcloud cf logging status](#status1)</td>
    <td>Use this command to get information about the logs that are collected in a space or account.</td>
  </tr>
  </table>


## ibmcloud cf logging
{: #base1}

Provides information about the version of the CLI and how to use the CLI.

```
ibmcloud cf logging [parameters]
```
{: codeblock}

**Parameters**

<dl>
<dt>--help, -h</dt>
<dd>Set this parameter to show the list of commands, or to get help for one command.
</dd>

<dt>--version, -v</dt>
<dd>Set this parameter to print the version of the CLI.</dd>
</dl>

**Examples**

To get the list of commands, run the following command:

```
ibmcloud cf logging --help
```
{: codeblock}

To get the version of the CLI, run the following command:

```
ibmcloud cf logging --version
```
{: codeblock}


## ibmcloud cf logging auth
{: #auth}

Returns a logging token that you can use to send logs to the {{site.data.keyword.loganalysisshort}} service. 

**Note:** The token does not expire.

```
ibmcloud cf logging auth
```
{: codeblock}

**Returns**

<dl>
  <dt>Logging Token</dt>
  <dd>For example, `jec8BmipiEZc`.
  </dd>
  
  <dt>Organization ID</dt>
  <dd>GUID of the {{site.data.keyword.Bluemix_notm}} organization where you are logged in.
  </dd>
  
  <dt>Space ID</dt>
  <dd>GUID of the space within the organization where you are logged in.
  </dd>
</dl>

## ibmcloud cf logging delete
{: #delete2}

Deletes logs that are stored in Log Collection.

```
ibmcloud cf logging delete [parameters]
```
{: codeblock}

**Parameters**

<dl>
  <dt>--start value, -s value</dt>
  <dd>(Optional) Sets the start date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to 2 weeks ago.
  </dd>
  
  <dt>--end value, -e value</dt>
  <dd>(Optional)  Sets the end date in Coordinated Universal Time (UTC): *YYYY-MM-DD* <br>The UTC format of the date is **YYYY-MM-DD**, for example, `2006-01-02`. <br>The default value is set to the current date.
  </dd>
  
  <dt>--type value, -t value</dt>
  <dd>(Optional) Sets the log type. <br>For example, *syslog* is a type of log. <br>The default value is set to **\***. <br>You can specify multiple log types by separating each type with a comma, for example, **log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>--at-account-level, -a </dt>
  <dd>(Optional) Sets the scope of the log information that is provided to the account level. <br>If this parameter is not specified, the default value is set to provide log information about the current space only.
  </dd>
</dl>

**Example**

To delete the logs of type *linux_syslog* for 25 May 2017, run the following command:
```
ibmcloud cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
```
{: codeblock}



## ibmcloud cf logging download (Beta)
{: #download4}

Downloads logs from Log Collection to a local file or pipes logs to another program such an Elastic Stack. 

**Note:** To download files, you need to create a session first. A session defines which logs to download based on date range, log type, and account type. You download logs within the context of a session. For more information, see [ibmcloud cf logging session create (Beta)](/docs/services/CloudLogAnalysis/reference?topic=cloudloganalysis-logging_cli#session_create1).

```
ibmcloud cf logging download [parameters] [arguments]
```
{: codeblock}

**Parameters**

<dl>
<dt>--output value, -o value</dt>
<dd>(Optional) Sets the path and filename for the local output file where the logs are downloaded. <br>The default value is a hyphen (-). <br>Set this parameter to the default value to output logs to standard output.</dd>
</dl>

**Arguments**

<dl>
<dt>session_ID</dt>
<dd>Set to the session ID value that you get when you run the command `ibmcloud cf logging session create`. This value indicates which session to use when downloading logs. <br>**Note:** The `ibmcloud cf logging session create` command provides the parameters that control which logs are downloaded. </dd>
</dl>

**Note:** After the download completes, running the same command again will refuse to do anything. To download the same data again, you must use a different file or a different session.

**Examples**

In a Linux system, to download logs into a file called mylogs.gz, run the following command:

```
ibmcloud cf logging download -o mylogs.gz guBeZTIuYtreOPi-WMnbUg==
```
{: screen}

To download logs into your own Elastic Stack, run the following command:

```
ibmcloud cf logging download guBeZTIuYtreOPi-WMnbUg== | gunzip | logstash -f logstash.conf
```
{: screen}

The following file is an example of a logstash.conf file:

```
input {
  stdin {
    codec => json_lines {}
  }
}
output {
  elasticsearch {
    hosts => [ "127.0.0.1:9200" ]
  }
}
```
{: screen}


## ibmcloud cf logging help
{: #help1}

Provides information on how to use a command.

```
ibmcloud cf logging help [command]
```
{: codeblock}

**Parameters**

<dl>
<dt>Command</dt>
<dd>Set the command name for which you want to get help.
</dd>
</dl>


**Examples**

To get help on how to run the command to view the status of logs, run the following command:

```
ibmcloud cf logging help status
```
{: codeblock}


## ibmcloud cf logging option
{: #option}

Displays or changes the retention period for logs that are available in a space or account. 

* The period is set in number of days.
* The default value is **-1**. 

**Note:** By default, all the logs are stored. You must delete them manually by using the **delete** command. Set a retention policy to delete logs automatically.

```
ibmcloud cf logging option [parameters]
```
{: codeblock}

**Parameters**

<dl>
<dt>--retention value, -r value</dt>
<dd>(Optional) Sets the number of retention days. <br> The default value is *-1* days.</dd>

<dt>--at-account-level, -a </dt>
  <dd>(Optional) Sets the scope to account level. <br>If this parameter is not specified, the default value is set to *-1* for the current space, that is the space where you logged in by using the command `ibmcloud cf login`.
  </dd>
</dl>

**Examples**

To see the default current retention period for the space where you are logged in, run the following command:

```
ibmcloud cf logging option
```
{: codeblock}

The output is:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-ibmcloud cfgh436902a3 |        -1 |
+--------------------------------------+-----------+
```
{: screen}


To change the retention period to 25 days for the space where you are logged in, run the following command:

```
ibmcloud cf logging option -r 25
```
{: codeblock}

The output is:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-ibmcloud cfgh436902a3 |        25 |
+--------------------------------------+-----------+
```
{: screen}


## ibmcloud cf logging session create (Beta)
{: #session_create1}

Creates a new session.

**Note:** You can have up to 30 concurrent sessions in a space. The session is created for a user. Sessions cannot be shared between users in a space.

```
ibmcloud cf logging session create [parameters]
```
{: codeblock}

**Parameters**

<dl>
  <dt>--start value, -s value</dt>
  <dd>(Optional) Sets the start date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to 2 weeks ago.
  </dd>
  
  <dt>--end value, -e value</dt>
  <dd>(Optional)  Sets the end date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to the current date.
  </dd>
  
  <dt>--type value, -t value</dt>
  <dd>(Optional) Sets the log type. <br>For example, *syslog* is a type of log. <br>The default value is set to asterisk (*). <br>You can specify multiple log types by separating each type with a comma, for example, *log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>--at-account-level, -a </dt>
  <dd>(Optional) Sets the scope to account level. <br>If this parameter is not specified, the default value is set to the current space only, that is, the space where you logged in by using the command `ibmcloud cf login`.
  </dd>
</dl>

**Returned values**

<dl>
<dt>Access-Time</dt>
<dd>Timestamp that indicates when the session was last used.</dd>

<dt>Create-Time</dt>
<dd>Timestamp that corresponds to the date and time when the session was created.</dd>

<dt>Date-Range</dt>
<dd>Indicates the days that are used to filter logs. Logs identified in this date range are available for management through the session.</dd>

<dt>ID</dt>
<dd>Session ID.</dd>

<dt>Space</dt>
<dd>Space ID where the session is active.</dd>

<dt>Type-Account</dt>
<dd>Log types that are downloaded through the session.</dd>

<dt>Username</dt>
<dd>{{site.data.keyword.IBM_notm}} ID of the user who created the session.</dd>
</dl>


**Example**

To create a session that includes logs between 20 May 2017 and May 26 2017 for a log type of *log*, run the following command:

```
ibmcloud cf logging session create -s 2017-05-20 -e 2017-05-26 -t log
```
{: screen}


## ibmcloud cf logging session delete (Beta)
{: #session_delete1}

Deletes a session, specified by session id.

```
ibmcloud cf logging session delete [arguments]
```
{: codeblock}

**Arguments**

<dl>
<dt>session ID</dt>
<dd>ID of the session that you want to delete. <br>You can use the command `ibmcloud cf logging session list` to get all the active session IDs.</dd>
</dl>

**Example**

To delete a session with session ID *cI6hvAa0KR_tyhjxZZz9Uw==*, run the following command:

```
ibmcloud cf logging session delete cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}



## ibmcloud cf logging session list (Beta)
{: #session_list1}

Lists the active sessions and their IDs.

```
ibmcloud cf logging session list 
```
{: codeblock}

**Returned values**

<dl>
<dt>ID</dt>
<dd>Session ID.</dd>

<dt>SPACE</dt>
<dd>Space ID where the session is active.</dd>

<dt>USERNAME</dt>
<dd>{{site.data.keyword.IBM_notm}} ID of the user who created the session.</dd>

<dt>CREATE-TIME</dt>
<dd>Time stamp that corresponds to the date and time when the session was created.</dd>

<dt>ACCESS-TIME</dt>
<dd>Time stamp that indicates when the session was last used.</dd>
</dl>
 

## ibmcloud cf logging session show (Beta)
{: #session_show1}

Shows the status of a single session.

```
ibmcloud cf logging session show [arguments]
```
{: codeblock}

**Arguments**

<dl>
<dt>session_ID</dt>
<dd>ID of the active session for which you want to get information.</dd>
</dl>

**Returned values**

<dl>
<dt>Access-Time</dt>
<dd></dd>

<dt>Create-Time</dt>
<dd>Timestamp that corresponds to the date and time when the session was created.</dd>

<dt>Date-Range</dt>
<dd>Indicates the days that are used to filter logs. Logs identified in this date range are available for management through the session.</dd>

<dt>ID</dt>
<dd>Session ID.</dd>

<dt>Space</dt>
<dd>Space ID where the session is active.</dd>

<dt>Type-Account</dt>
<dd>Log types that are downloaded through the session.</dd>

<dt>Username</dt>
<dd>{{site.data.keyword.IBM_notm}} ID of the user who created the session.</dd>
</dl>

**Example**

To show details of a session with session ID *cI6hvAa0KR_tyhjxZZz9Uw==*, run the following command:

```
ibmcloud cf logging session show cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}


## ibmcloud cf logging status
{: #status1}

Returns information about the logs that are collected in a space or account.

```
ibmcloud cf logging status [parameters]
```
{: codeblock}

**Parameters**

<dl>
  <dt>--start value, -s value</dt>
  <dd>(Optional) Sets the start date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to 2 weeks ago.
  </dd>
  
  <dt>--end value, -e value</dt>
  <dd>(Optional)  Sets the end date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to the current date.
  </dd>
  
  <dt>--type value, -t value</dt>
  <dd>(Optional) Sets the log type. <br>For example, *syslog* is a type of log. <br>The default value is set to asterisk (*). <br>You can specify multiple log types by separating each type with a comma, for example, *log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>--at-account-level, -a </dt>
  <dd>(Optional) Sets the scope to account level. <br> **Note:** Set this value to get account information. <br>If this parameter is not specified, the default value is set to the current space only, that is, the space where you logged in by using the command `ibmcloud cf login`.
  </dd>
  
  <dt>--list-type-detail, -l</dt>
  <dd>(Optional) Set this parameter to list the subtotal of log types for each day.
  </dd>
</dl>

**Note:** The `ibmcloud cf logging status` command reports only the last 2 weeks of logs that are stored in Log Collection when no start and end dates are specified.


