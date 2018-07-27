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

# Log Analysis CLI ({{site.data.keyword.Bluemix_notm}} plugin)
{: #log_analysis_cli}

The {{site.data.keyword.loganalysislong}} CLI is an {{site.data.keyword.Bluemix_notm}} plug-in that you can use to manage logs that are stored in Log Collection.
{: shortdesc}

**Prerequisites**
* Before running the logging commands, log in to the {{site.data.keyword.Bluemix_notm}} with the `ibmcloud login` command to generate an access token and authenticate your session.

To find out about how to use the {{site.data.keyword.loganalysisshort}} CLI, see [Managing logs](/docs/services/CloudLogAnalysis/log_analysis_ov.html#log_analysis_ov).

<table>
  <caption>Commands for managing logs</caption>
  <tr>
    <th>Command</th>
    <th>When to use it</th>
  </tr>
  <tr>
    <td>[ibmcloud logging](#base)</td>
    <td>Use this command to get information about the CLI, such as the list of commands.</td>
  </tr>
  <tr>
    <td>[ibmcloud logging log-delete](#delete)</td>
    <td>Use this command to delete logs that are stored in Log Collection.</td>
  </tr>
  <tr>
    <td>[ibmcloud logging log-download](#download)</td>
    <td>Use this command to download logs from Log Collection to a local file, or pipe logs to another program such an Elastic Stack. </td>
  </tr>
  <tr>
    <td>[ibmcloud logging log-show](#status)</td>
    <td>Use this command to get information about the logs that are collected in a space, organization, or account.</td>
  </tr>
  <tr>
    <td>[ibmcloud logging help](#help)</td>
    <td>Use this command to get help on how to use the CLI, and a  list of all of the commands.</td>
  </tr>
  <tr>
    <td>[ibmcloud logging option-show](#optionshow)</td>
    <td>Use this command to view the retention period for logs that are available in a space, organization, or account.</td>
  </tr>
  <tr>
    <td>[ibmcloud logging option-update](#optionupdate)</td>
    <td>Use this command to set the retention period for logs that are available in a space, organization, or account.</td>
  </tr>
  <tr>
    <td>[ibmcloud logging quota-usage-show](#quotausage)</td>
    <td>Use this command to get the quota usage information for a space, organization, or account. You can also get the quota history information.</td>
  </tr>
  <tr>
    <td>[ibmcloud logging session-create](#session_create)</td>
    <td>Use this command to create a new session.</td>
  <tr>
  <tr>
    <td>[ibmcloud logging session-delete](#session_delete)</td>
    <td>Use this command to delete a session.</td>
  <tr>  
  <tr>
    <td>[ibmcloud logging sessions](#session_list)</td>
    <td>Use this command to list active sessions and their IDs.</td>
  <tr>  
  <tr>
    <td>[ibmcloud logging session-show](#session_show)</td>
    <td>Use this command to show the status of a single session.</td>
  <tr>  
  <tr>
    <td>[ibmcloud logging token-get](#tokenget)</td>
    <td>Use this command to get the logging token to send log data into the {{site.data.keyword.loganalysisshort}} service.</td>
  </tr>
</table>


## ibmcloud logging
{: #base}

Provides general information about the CLI.

```
ibmcloud logging 
```
{: codeblock}

**Examples**

To get the list of commands, run the following command:

```
ibmcloud logging 
NAME:
   ibmcloud logging - IBM Cloud Log Analysis Service
USAGE:
   ibmcloud logging command [arguments...] [command options]

COMMANDS:
COMMANDS:
   log-delete         Delete log
   log-download       Download a log
   log-show           Show the count, size, and type of logs per day
   session-create     Create a session
   session-delete     Delete session
   sessions           List sessions info
   session-show       Show a session info
   option-show        Show the log retention
   option-update      Show the log options
   token-get          Get a logging token for sending logs
   quota-usage-show   Show quota usage info
   help             
   
Enter 'ibmcloud logging help [command]' for more information about a command.
```
{: codeblock}




## ibmcloud logging log-delete
{: #delete}

Deletes logs that are stored in Log Collection.

```
ibmcloud logging log-delete [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-f, --force ]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Optional) Sets the type of resource. Valid values are: *space*, *account*, and *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Optional) Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in. 
  </dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>(Optional) Sets the start date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to 2 weeks ago.
  </dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>(Optional) Sets the end date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to the current date.
  </dd>
  
  <dt>-f, --force </dt>
  <dd>(Optional) Set this option to delete logs without having to confirm your action.
  </dd>
</dl>

**Example**

To delete the logs of type *linux_syslog* for 25 May 2017, run the following command:
```
ibmcloud logging log-delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
```
{: screen}



## ibmcloud logging log-download 
{: #download}

Downloads logs from Log Collection to a local file or pipes logs to another program such an Elastic Stack. 

**Note:** To download files, you need to create a session first. A session defines which logs to download based on date range, log type, and account type. You download logs within the context of a session. For more information, see [ibmcloud logging session create (Beta)](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#session_create).

```
 ibmcloud logging log-download  [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-o, --output OUTPUT] SESSION_ID

```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Optional) Sets the type of resource. Valid values are: *space*, *account*, and *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Optional) Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in. 
  </dd>
 
  <dt>-o, --output OUTPUT</dt>
  <dd>(Optional) Sets the path and filename for the local output file where the logs are downloaded. <br>The default value is a hyphen (-). <br>Set this parameter to the default value to output logs to standard output.</dd>

</dl>

**Arguments**

<dl>
  <dt>SESSION_ID</dt>
  <dd>This value indicates the ID of the session that you must use when downloading logs. <br>**Note:** The `ibmcloud logging session-create` command provides the parameters that control which logs are downloaded. </dd>
</dl>

**Note:** After the download completes, running the same command again will refuse to do anything. To download the same data again, you must use a different file or a different session.

**Examples**

In a Linux system, to download logs into a file called mylogs.gz, run the following command:

```
ibmcloud logging log-download -o mylogs.gz guBeZTIuYtreOPi-WMnbUg==
```
{: screen}

To download logs into your own Elastic Stack, run the following command:

```
ibmcloud logging log-download guBeZTIuYtreOPi-WMnbUg== | gunzip | logstash -f logstash.conf
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


## ibmcloud logging help
{: #help}

Provides information on how to use a command.

```
ibmcloud logging help [command] 
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
ibmcloud logging help log-show
NAME:
   log-show - Show the count, size, and type of logs per day

USAGE:
   ibmcloud logging log-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-l, --list-type-detail]

OPTIONS:
   -r, --resource-type     Resource type, the valid resource type is account, org, or space
   -i, --resource-id       Resource id, the target resource id
   -s, --start             Start Date, UTC time value included in format YYYY-MM-DD
   -e, --end               End Date, UTC time value included in format YYYY-MM-DD
   -t, --type              Log Type, for example "syslog"
   -l, --list-type-detail  List the detailed type

```
{: screen}


## ibmcloud logging option-show
{: #optionshow}

Displays the retention period for logs that are available in a space, organization, or account. 

* The period is set in number of days.
* The default value is **-1**. 

**Note:** By default, all the logs are stored. You must delete them manually by using the **delete** command. Set a retention policy to delete logs automatically.

```
ibmcloud logging option-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Optional) Sets the type of resource. Valid values are: *space*, *account*, and *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Optional) Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in. 
  </dd>

</dl>

**Examples**

To see the default current retention period for the space where you are logged in, run the following command:

```
ibmcloud logging option-show
```
{: screen}




## ibmcloud logging option-update
{: #optionupdate}

Changes the retention period for logs that are available in a space, organization, or account. 

* The period is set in number of days.
* The default value is **-1**. 

```
ibmcloud logging option-update [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] <-e,--retention RETENTION_VALUE>
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Optional) sets the type of resource. Valid values are: *space*, *account*, and *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Optional) Set this field to the ID of the space, the organization, or the account for which you want to get information. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in. 
  </dd>
  
  <dt>-e,--retention RETENTION_VALUE</dt>
  <dd>Sets the number of days that logs are kept. </dd>

</dl>

**Example**

To change the retention period to 25 days for the space where you are logged in, run the following command:

```
ibmcloud logging option-update -e 25
```
{: screen}


## ibmcloud logging quota-usage-show
{: #quotausage}

Informs about the quota usage of a space, organization, or account. You can also use it to get the history usage.

* The period is set in number of days.
* The default value is **-1**. 

```
ibmcloud logging quota-usage-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s,--history]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Optional) Sets the type of resource. Valid values are: *space*, *account*, and *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Optional) Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in. 
  </dd>
  
  <dt>-s,--history</dt>
  <dd>(Optional) Set this parameter to get the historical information about quota usage.</dd>

</dl>

**Example**

To get the historical quota usage for a space domain, run the following command:

```
ibmcloud logging quota-usage-show -r space -i js7ydf98-8682-430d-bav4-36b712341744 -s
Showing quota usage for resource: js7ydf98-8682-430d-bav4-36b712341744 ...
OK

Date         Allotmant   Usage   
2018.02.28   524288000   80405926   
2018.03.06   524288000   18955540   
2018.03.05   524288000   47262944   
2018.03.08   524288000   18311338   
2018.03.01   524288000   82416831   
2018.03.03   524288000   75045462   
2018.03.07   524288000   17386278   
2018.03.02   524288000   104316444   
2018.03.04   524288000   73125223   
```
{: screen}

## ibmcloud logging session-create
{: #session_create}

Creates a new session.

**Note:** You can have up to 30 concurrent sessions in a space. The session is created for a user. Sessions cannot be shared between users in a space.

```
ibmcloud logging session-create [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Optional) Sets the type of resource. Valid values are: *space*, *account*, and *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Optional) Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in. 
  </dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>(Optional) Sets the start date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to 2 weeks ago.
  </dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>(Optional)  Sets the end date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to the current date.
  </dd>
  
  <dt>-t, --type, LOG_TYPE</dt>
  <dd>(Optional) Sets the log type. <br>For example, *syslog* is a type of log. <br>The default value is set to asterisk (*). <br>You can specify multiple log types by separating each type with a comma, for example, *log_type_1,log_type_2,log_type_3*.
  </dd>

</dl>


**Returned values**

<dl>

    <dt>ID</dt>
    <dd>Session ID.</dd>
	
	<dt>Resource type</dt>
    <dd>Resource ID.</dd>

    <dt>AccessTime</dt>
    <dd>Timestamp that indicates when the session was last used.</dd>

    <dt>CreateTime</dt>
    <dd>Timestamp that corresponds to the date and time when the session was created.</dd>
	
	<dt>Start</dt>
    <dd>Indicates the first day that is used to filter logs. </dd>

    <dt>End</dt>
    <dd>Indicates the last day that is used to filter logs.</dd>

    <dt>Type</dt>
    <dd>Log types that are downloaded through the session.</dd>

</dl>


**Example**

To create a session that includes logs for November 13 2017, run the following command:

```
ibmcloud logging session-create -s 2017-11-13 -e 2017-11-13
Creating session for xxxxx@yyy.com resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

ID                                     Space                                  CreateTime                       AccessTime                       Start        End          Type   
1ef776d1-4d25-4297-9693-882606c725c8   xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   2017-11-16T11:52:06.376125207Z   2017-11-16T11:52:06.376125207Z   2017-11-13   2017-11-13   ANY_TYPE   
Session: 1ef776d1-4d25-4297-9693-882606c725c8 is created
```
{: screen}


## ibmcloud logging session-delete 
{: #session_delete}

Deletes a session, specified by session id.

```
ibmcloud session-delete [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] SESSION_ID
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Optional) Sets the type of resource. Valid values are: *space*, *account*, and *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Optional) Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in. 
  </dd>
 
</dl>

**Arguments**

<dl>
  <dt>SESSION_ID</dt>
  <dd>ID of the active session that you want to delete.</dd>
</dl>

**Example**

To delete a session with session ID *cI6hvAa0KR_tyhjxZZz9Uw==*, run the following command:

```
ibmcloud logging session-delete cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}



## ibmcloud logging sessions
{: #session_list}

Lists the active sessions and their IDs.

```
ibmcloud logging sessions [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**Parameters**

<dl>

  <dt>-r,--resource-type RESOURCE_TYPE</dt>
      <dd>(Optional) Sets the type of resource. Valid values are: *space*, *account*, and *org* </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
      <dd>(Optional)Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in.  </dd>
</dl>

**Return values**

<dl>	
    <dt>SESSION_ID</dt>
    <dd>ID of the active session.</dd>
	   
    <dt>Resource ID</dt>
    <dd>ID of the resource for which the session is valid.</dd>

    <dt>CreateTime</dt>
    <dd>Time stamp that corresponds to the date and time when the session was created.</dd>

    <dt>AccessTime</dt>
    <dd>Time stamp that indicates when the session was last used.</dd>
</dl>
 
**Example**

```
ibmcloud logging sessions
Listing sessions of resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

ID                                     Space                                  CreateTime                       AccessTime   
1ef776d1-4d25-4297-9693-882606c725c8   xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   2017-11-16T11:52:06.376125207Z   2017-11-16T11:52:06.376125207Z   
Listed the sessions of resource xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 
```
:{ screen}


## ibmcloud logging session-show
{: #session_show}

Shows the status of a single session.

```
ibmcloud logging session-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] SESSION_ID

```
{: codeblock}

**Parameters**

<dl>
   <dt>-r,--resource-type RESOURCE_TYPE</dt>
      <dd>(Optional) Sets the type of resource. Valid values are: *space*, *account*, and *org* </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
      <dd>(Optional) Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in.  </dd>
</dl>

**Arguments**

<dl>
   <dt>SESSION_ID</dt>
   <dd>ID of the active session for which you want to get information.</dd>
</dl>

**Example**

To show details of a session with session ID *cI6hvAa0KR_tyhjxZZz9Uw==*, run the following command:

```
ibmcloud logging session-show cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}

## ibmcloud logging token-get
{: #tokenget}

Returns the logging token that is required to send log data into {{site.data.keyword.loganalysisshort}}.

```
ibmcloud logging token-get [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Optional) Sets the type of resource where you plan to send log data. Valid values are: *space*, *account*, and *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Optional) Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in. 
  </dd>
</dl>


**Example**

```
ibmcloud logging token-get -r space -i js7ydf98-8682-430d-bav4-36b712341744
Getting log token of resource: js7ydf98-8682-430d-bav4-36b712341744 ...
OK

Tenant Id                              Logging Token   
js7ydf98-8682-430d-bav4-36b712341744   xxxxxxxxxx   
```
{: screen}


## ibmcloud logging log-show
{: #status}

Returns information about the logs that are collected in a {{site.data.keyword.Bluemix_notm}} space or account.

```
ibmcloud logging log-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-l, --list-type-detail]
```
{: codeblock}

* When the resource type is not specified, the command returns the details of the resource where you are logged in.
* If you specify a resource type, you must specify the resource ID.
* The command reports only information about the last 2 weeks of logs that are stored in Log Collection when no start and end dates are specified.

**Parameters**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>(Optional) Sets the type of resource. Valid values are: *space*, *account*, and *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>(Optional) Set this field to the ID of a space, an organization, or an account. <br>By default, if you do not specify this parameter, the command uses the ID of the resource where you are logged in. 
  </dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>(Optional) Sets the start date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to 2 weeks ago.
  </dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>(Optional)  Sets the end date in Coordinated Universal Time (UTC): *YYYY-MM-DD*, for example, `2006-01-02`. <br>The default value is set to the current date.
  </dd>
  
  <dt>-t, --type, LOG_TYPE</dt>
  <dd>(Optional) Sets the log type. <br>For example, *syslog* is a type of log. <br>The default value is set to asterisk (*). <br>You can specify multiple log types by separating each type with a comma, for example, *log_type_1,log_type_2,log_type_3*.
  </dd>
  
  <dt>-l, --list-type-detail</dt>
  <dd>(Optional) Set this parameter to list each log type individually.
  </dd>
</dl>


**Example**

```
ibmcloud logging log-show
Showing log status of resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

Date         Size        Count    Searchable   Types   
2017-11-07   1878197     1333     None         default   
2017-11-13   201653512   179391   All          default,linux_syslog   
2017-11-14   32134119    30425    All          default,linux_syslog   
2017-11-15   303901156   269689   All          linux_syslog,default   
2017-11-16   107253679   96648    All          default,linux_syslog   
```
{: screen}

```
 ibmcloud logging log-show -l
Showing log status of resource: cedc73c5-6d55-4193-a9de-378620d6fab5 ...

Date         Size        Count    Searchable   Type   
2017-11-14   30146764    26611    true         default   
2017-11-14   1987355     3814     true         linux_syslog   
2017-11-15   303004895   267890   true         default   
2017-11-15   896261      1799     true         linux_syslog   
2017-11-16   107918249   96278    true         default   
2017-11-16   912890      1794     true         linux_syslog   
```
{: screen}