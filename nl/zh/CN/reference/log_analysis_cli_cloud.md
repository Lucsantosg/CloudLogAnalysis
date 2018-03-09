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

# Log Analysis CLI（{{site.data.keyword.Bluemix_notm}} 插件）
{: #log_analysis_cli}

{{site.data.keyword.loganalysislong}} CLI 是 {{site.data.keyword.Bluemix_notm}} 插件，可用于管理存储在“日志收集”中的日志。
{: shortdesc}

**先决条件**
* 运行日志记录命令之前，请先使用 `bx login` 命令登录到 {{site.data.keyword.Bluemix_notm}}，以生成访问令牌并对会话进行认证。

要了解如何使用 {{site.data.keyword.loganalysisshort}} CLI，请参阅[管理日志](/docs/services/CloudLogAnalysis/log_analysis_ov.html#log_analysis_ov)。

<table>
  <caption>用于管理日志的命令</caption>
  <tr>
    <th>命令</th>
    <th>何时使用</th>
  </tr>
  <tr>
    <td>[bx logging](#base)</td>
    <td>使用此命令可获取有关 CLI 的信息，例如命令列表。</td>
  </tr>
  <tr>
    <td>[bx logging log-delete](#delete)</td>
    <td>使用此命令可删除存储在“日志收集”中的日志。</td>
  </tr>
  <tr>
    <td>[bx logging log-download](#download)</td>
    <td>使用此命令可将“日志收集”中的日志下载到本地文件，或者通过管道将日志传递到其他程序，例如 Elastic 堆栈。</td>
  </tr>
  <tr>
    <td>[bx logging help](#help)</td>
    <td>使用此命令可获取有关如何使用 CLI 的帮助以及所有命令的列表。</td>
  </tr>
  <tr>
    <td>[bx logging option-show](#optionshow)</td>
    <td>使用此命令可查看空间、组织或帐户中可用的日志的保留期。</td>
  </tr>
  <tr>
    <td>[bx logging option-update](#optionupdate)</td>
    <td>使用此命令可设置空间、组织或帐户中可用的日志的保留期。</td>
  </tr>
  <tr>
    <td>[bx logging session-create](#session_create)</td>
    <td>使用此命令可创建新会话。</td>
  <tr>
  <tr>
    <td>[bx logging session-delete](#session_delete)</td>
    <td>使用此命令可删除会话。</td>
  <tr>  
  <tr>
    <td>[bx logging sessions](#session_list)</td>
    <td>使用此命令可列出活动会话及其标识。</td>
  <tr>  
  <tr>
    <td>[bx logging session-show](#session_show)</td>
    <td>使用此命令可显示单个会话的状态。</td>
  <tr>  
  <tr>
    <td>[bx logging log-show](#status)</td>
    <td>使用此命令可获取有关在空间、组织或帐户中收集的日志的信息。</td>
  </tr>
</table>


## bx logging
{: #base}

提供有关 CLI 的常规信息。

```
bx logging 
```
{: codeblock}

**示例**

要获取命令的列表，请运行以下命令：

```
bx logging
名称：
   bx logging - IBM Cloud Log Analysis 服务
用法：
   bx logging command [arguments...] [command options]

命令：
   log-delete       删除日志
   log-download     下载日志
   log-show         显示每天日志的计数、大小和类型
   session-create   创建会话
   session-delete   删除会话
   sessions         列出会话信息
   session-show     显示会话信息
   option-show      显示日志保留时间
   option-update    显示日志选项
   help

输入“bx logging help [command]”以获取命令的更多信息。
```
{: codeblock}




## bx logging log-delete
{: #delete}

删除存储在“日志收集”中的日志。

```
bx logging log-delete [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-f, --force ]
```
{: codeblock}

**参数**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>（可选）设置资源类型。有效值为：*space*、*account* 和 *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>（可选）将此字段设置为您要获取信息的空间、组织或帐户的标识。<br>缺省情况下，如果您未指定此参数，那么该命令使用您登录的资源的标识。</dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>（可选）设置开始日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*，例如 `2006-01-02`。<br>缺省值设置为 2 周前。</dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>（可选）设置结束日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*，例如 `2006-01-02`。<br>缺省值设置为当前日期。</dd>
  
  <dt>-f, --force </dt>
  <dd>（可选）设置此选项，以删除日志而无需确认操作。
</dd>
</dl>

**示例**

要删除 2017 年 5 月 25 日类型为 *linux_syslog* 的日志，请运行以下命令：
```
bx logging log-delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
```
{: screen}



## bx logging log-download 
{: #download}

将“日志收集”中的日志下载到本地文件，或者通过管道将日志传递到其他程序，例如 Elastic 堆栈。 

**注**：要下载文件，需要首先创建会话。会话会根据日期范围、日志类型和帐户类型来定义要下载的日志。您将在会话上下文中下载日志。有关更多信息，请参阅 [bx logging session create (Beta)](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#session_create)。

```
 bx logging log-download  [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-o, --output OUTPUT] SESSION_ID

```
{: codeblock}

**参数**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>（可选）设置资源类型。有效值为：*space*、*account* 和 *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>（可选）将此字段设置为您要获取信息的空间、组织或帐户的标识。<br>缺省情况下，如果您未指定此参数，那么该命令使用您登录的资源的标识。</dd>
 
  <dt>-o, --output OUTPUT</dt>
  <dd>（可选）设置日志下载到其中的本地输出文件的路径和文件名。<br>缺省值为连字符 (-)。<br>将此参数设置为缺省值会将日志输出到标准输出。</dd>

</dl>

**自变量**

<dl>
  <dt>SESSION_ID</dt>
  <dd>此值指示下载日志时必须使用的会话的标识。<br>**注**：`bx logging session-create` 命令提供用于控制下载哪些日志的参数。</dd>
</dl>

**注**：下载完成后，再次运行相同的命令将拒绝执行任何操作。要重新下载相同的数据，必须使用其他文件或其他会话。

**示例**

在 Linux 系统中，要将日志下载到名为 mylogs.gz 的文件中，请运行以下命令：

```
bx logging log-download -o mylogs.gz guBeZTIuYtreOPi-WMnbUg==
```
{: screen}

要将日志下载到自己的 Elastic 堆栈，请运行以下命令：

```
bx logging log-download guBeZTIuYtreOPi-WMnbUg== | gunzip | logstash -f logstash.conf
```
{: screen}

以下文件是 logstash.conf 文件的示例：

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


## bx logging help
{: #help}

提供有关如何使用命令的信息。

```
bx logging help [command] 
```
{: codeblock}

**参数**

<dl>
<dt>命令</dt>
<dd>设置要获取其帮助的命令名。
</dd>
</dl>


**示例**

要获取有关如何运行命令来查看日志状态的帮助，请运行以下命令：

```
bx logging help log-show
名称：
   log-show - 显示每天日志的计数、大小和类型

用法：
   bx logging log-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-l, --list-type-detail]

选项：
   -r, --resource-type     资源类型，有效资源类型为 account、org 或 space
   -i, --resource-id       资源标识，目标资源标识
   -s, --start             开始日期，格式 YYYY-MM-DD 中包含 UTC 时间值
   -e, --end               结束时间，格式 YYYY-MM-DD 中包含 UTC 时间值
   -t, --type              日志类型，例如“syslog”
   -l, --list-type-detail  列出详细类型

```
{: screen}


## bx logging option-show
{: #optionshow}

显示空间、组织或帐户中可用的日志的保留期。 

* 保留期以天数为单位进行设置。
* 缺省值为 **-1**。 

**注：**缺省情况下，将存储所有日志。日志必须使用 **delete** 命令手动删除。设置保留时间策略可自动删除日志。

```
bx logging option-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**参数**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>（可选）设置资源类型。有效值为：*space*、*account* 和 *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>（可选）将此字段设置为您要获取信息的空间、组织或帐户的标识。<br>缺省情况下，如果您未指定此参数，那么该命令使用您登录的资源的标识。</dd>

</dl>

**示例**

要查看所登录到的空间的缺省当前保留期，请运行以下命令：

```
bx logging option-show
```
{: screen}




## bx logging option-update
{: #optionupdate}

更改空间、组织或帐户中可用的日志的保留期。 

* 保留期以天数为单位进行设置。
* 缺省值为 **-1**。 

```
bx logging option-update [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] <-e,--retention RETENTION_VALUE>
```
{: codeblock}

**参数**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>（可选）设置资源类型。有效值为：*space*、*account* 和 *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>（可选）将此字段设置为您要获取信息的空间、组织或帐户的标识。<br>缺省情况下，如果您未指定此参数，那么该命令使用您登录的资源的标识。</dd>
  
  <dt>-e,--retention RETENTION_VALUE</dt>
  <dd>设置日志保留的天数。</dd>

</dl>

**示例**

要将所登录到的空间的保留期更改为 25 天，请运行以下命令：

```
bx logging option-update -e 25
```
{: screen}



## bx logging session-create
{: #session_create}

创建新的会话。

**注**：一个空间中最多可以有 30 个并发会话。会话是为用户创建的。因此，空间中的不同用户之间不能共享会话。

```
bx logging session-create [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE]
```
{: codeblock}

**参数**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>（可选）设置资源类型。有效值为：*space*、*account* 和 *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>（可选）将此字段设置为您要获取信息的空间、组织或帐户的标识。<br>缺省情况下，如果您未指定此参数，那么该命令使用您登录的资源的标识。</dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>（可选）设置开始日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*，例如 `2006-01-02`。<br>缺省值设置为 2 周前。</dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>（可选）设置结束日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*，例如 `2006-01-02`。<br>缺省值设置为当前日期。</dd>
  
  <dt>-t, --type, LOG_TYPE</dt>
  <dd>（可选）设置日志类型。<br>例如，*syslog* 是一种日志类型。<br>缺省值设置为星号 (*)。<br>可以指定多种日志类型并使用逗号分隔各个类型，例如 *log_type_1,log_type_2,log_type_3*。</dd>

</dl>


**返回值**

<dl>

    <dt>ID</dt>
    <dd>会话标识。</dd>
	
	<dt>Resource type</dt>
    <dd>资源标识。</dd>

    <dt>AccessTime</dt>
    <dd>指示最后一次使用会话时的时间戳记。</dd>

    <dt>CreateTime</dt>
    <dd>对应于创建会话时的日期和时间的时间戳记。</dd>
	
	<dt>Start</dt>
    <dd>指示用于过滤日志的第一天。</dd>

    <dt>End</dt>
    <dd>指示用于过滤日志的最后一天。</dd>

    <dt>类型</dt>
    <dd>通过会话下载的日志类型。</dd>

</dl>


**示例**

要创建包含 2017 年 11 月 13 日日志的会话，请运行以下命令：

```
bx logging session-create -s 2017-11-13 -e 2017-11-13
Creating session for xxxxx@yyy.com resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

ID                                     Space                                  CreateTime                       AccessTime                       Start        End          Type   
1ef776d1-4d25-4297-9693-882606c725c8   xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   2017-11-16T11:52:06.376125207Z   2017-11-16T11:52:06.376125207Z   2017-11-13   2017-11-13   ANY_TYPE   
Session: 1ef776d1-4d25-4297-9693-882606c725c8 is created
```
{: screen}


## bx logging session-delete 
{: #session_delete}

删除会话标识指定的会话。

```
bx session-delete [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] SESSION_ID
```
{: codeblock}

**参数**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>（可选）设置资源类型。有效值为：*space*、*account* 和 *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>（可选）将此字段设置为您要获取信息的空间、组织或帐户的标识。<br>缺省情况下，如果您未指定此参数，那么该命令使用您登录的资源的标识。</dd>
 
</dl>

**自变量**

<dl>
  <dt>SESSION_ID</dt>
  <dd>要删除的活动会话的标识。</dd>
</dl>

**示例**

要删除会话标识为 *cI6hvAa0KR_tyhjxZZz9Uw==* 的会话，请运行以下命令：

```
bx logging session-delete cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}



## bx logging sessions
{: #session_list}

列出活动会话及其标识。

```
bx logging sessions [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
```
{: codeblock}

**参数**

<dl>

  <dt>-r,--resource-type RESOURCE_TYPE</dt>
      <dd>（可选）设置资源类型。有效值为：*space*、*account* 和 *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
      <dd>（可选）将此字段设置为您要获取信息的空间、组织或帐户的标识。<br>缺省情况下，如果您未指定此参数，那么该命令使用您登录的资源的标识。</dd>
</dl>

**返回值**

<dl>	
    <dt>SESSION_ID</dt>
    <dd>活动会话的标识。</dd>
	   
    <dt>Resource ID</dt>
    <dd>会话有效的资源的标识。</dd>

    <dt>CreateTime</dt>
    <dd>对应于创建会话时的日期和时间的时间戳记。</dd>

    <dt>AccessTime</dt>
    <dd>指示最后一次使用会话的时间的时间戳记。</dd>
</dl>
 
**示例**

```
bx logging sessions
Listing sessions of resource: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ...

ID                                     Space                                  CreateTime                       AccessTime   
1ef776d1-4d25-4297-9693-882606c725c8   xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   2017-11-16T11:52:06.376125207Z   2017-11-16T11:52:06.376125207Z   
Listed the sessions of resource xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 
```
:{ screen}





## bx logging session-show
{: #session_show}

显示单个会话的状态。

```
bx logging session-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] SESSION_ID

```
{: codeblock}

**参数**

<dl>
   <dt>-r,--resource-type RESOURCE_TYPE</dt>
      <dd>（可选）设置资源类型。有效值为：*space*、*account* 和 *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
      <dd>（可选）将此字段设置为您要获取信息的空间、组织或帐户的标识。<br>缺省情况下，如果您未指定此参数，那么该命令使用您登录的资源的标识。</dd>
</dl>

**自变量**

<dl>
   <dt>SESSION_ID</dt>
   <dd>要获取其信息的活动会话的标识。</dd>
</dl>

**示例**

要显示会话标识为 *cI6hvAa0KR_tyhjxZZz9Uw==* 的会话的详细信息，请运行以下命令：

```
bx logging session-show cI6hvAa0KR_tyhjxZZz9Uw==
```
{: screen}


## bx logging log-show
{: #status}

返回有关在 {{site.data.keyword.Bluemix_notm}} 空间或帐户中收集的日志的信息。

```
bx logging log-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s, --start START_DATE] [-e, --end END_DATE] [-t, --type, LOG_TYPE] [-l, --list-type-detail]
```
{: codeblock}

* 当未指定资源类型时，命令会返回您登录的资源的详细信息。
* 如果指定资源类型，那么必须指定资源标识。
* 如果未指定开始日期和结束日期，该命令将仅报告存储在“日志收集”中的最近 2 周的日志的信息。

**参数**

<dl>
  <dt>-r,--resource-type RESOURCE_TYPE</dt>
  <dd>（可选）设置资源类型。有效值为：*space*、*account* 和 *org*
  </dd>
  
   <dt>-i,--resource-id RESOURCE_ID</dt>
  <dd>（可选）将此字段设置为您要获取信息的空间、组织或帐户的标识。<br>缺省情况下，如果您未指定此参数，那么该命令使用您登录的资源的标识。</dd>
  
  <dt>-s, --start START_DATE</dt>
  <dd>（可选）设置开始日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*，例如 `2006-01-02`。<br>缺省值设置为 2 周前。</dd>
  
  <dt>-e, --end END_DATE</dt>
  <dd>（可选）设置结束日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*，例如 `2006-01-02`。<br>缺省值设置为当前日期。</dd>
  
  <dt>-t, --type, LOG_TYPE</dt>
  <dd>（可选）设置日志类型。<br>例如，*syslog* 是一种日志类型。<br>缺省值设置为星号 (*)。<br>可以指定多种日志类型并使用逗号分隔各个类型，例如 *log_type_1,log_type_2,log_type_3*。</dd>
  
  <dt>-l, --list-type-detail</dt>
  <dd>（可选）设置此参数可分别列出每个日志类型。</dd>
</dl>


**示例**

```
bx logging log-show
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
 bx logging log-show -l
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
