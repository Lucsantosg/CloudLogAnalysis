---

copyright:
  years: 2017
lastupdated: "2017-07-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 查看日志信息
{: #viewing_log_status}

使用 [cf logging status](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status) 命令可获取有关在“日志收集”中收集并存储的日志的信息。
{:shortdesc}

## 获取有关日志在一段时间内的信息
{: #viewing_logs}

使用 `cf logging status` 命令可查看“日志收集”中存储的日志的大小、计数、日志类型以及这些日志是否可供在 Kibana 中进行分析。 

将 `cf logging status` 命令与 **-s**（用于设置开始日期）和 **-e** 选项（设置用于结束日期）一起使用。例如：

* `cf logging status` 提供最近 2 周的信息。
* `cf logging status -s 2017-05-03` 提供从 2017 年 5 月 3 日一直到当前日期的信息。
* `cf logging status -s 2017-05-03 -e 2017-05-08` 提供从 2017 年 5 月 3 日到 2017 年 5 月 8 日的信息。 

1. 登录到 {{site.data.keyword.Bluemix_notm}} 区域、组织和空间。 

    例如，要登录到美国南部区域，请运行以下命令：
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. 运行 *status* 命令。

    ```
    $ cf logging status
    ```
    {: codeblock}
    
    例如：
    
    ```
    $ cf logging status
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}


## 获取有关某个日志类型在一段时间内的信息
{: #viewing_logs_by_log_type}

要获取有关一段时间内某个日志类型的信息，请将 `cf logging status` 命令与 **-t**（用于指定日志类型）、**-s**（用于设置开始日期）和 **-e** 选项（用于设置结束日期）一起使用。例如：

* `cf logging status -t syslog` 提供有关类型为 *syslog* 的日志最近 2 周的信息。
* `cf logging status -s 2017-05-03 -t syslog` 提供有关类型为 *syslog* 的日志从 2017 年 5 月 3 日一直到当前日期的信息。
* `cf logging status -s 2017-05-03 -e 2017-05-08 -t syslog` 提供有关类型为 *syslog* 的日志从 2017 年 5 月 3 日到 2017 年 5 月 8 日的信息。 

1. 登录到 {{site.data.keyword.Bluemix_notm}} 区域、组织和空间。 

    例如，要登录到美国南部区域，请运行以下命令：
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. 运行 *status* 命令。

    ```
    $ cf logging status -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    其中
    
    * *-s* 用于设置开始日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*
    * *-e* 用于设置结束日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*
    * *-t* 用于设置日志类型。
    
    可以通过用逗号分隔各个类型来指定多种日志类型，例如 **log_type_1,log_type_2,log_type_3**。 
    
    例如：
    
    ```
    $ cf logging status -s 2017-05-24 -e 2017-05-25 -t log
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 |        log         |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}



## 获取有关日志的帐户信息
{: #viewing_logs_account}

要获取有关 {{site.data.keyword.Bluemix_notm}} 帐户上的日志在一段时间内的信息，请将 `cf logging status` 命令与 **-a** 选项一起使用。您还可以指定 **-t**（用于指定日志类型）、**-s**（用于设置开始日期）和 **-e** 选项（用于设置结束日期）。 

1. 登录到 {{site.data.keyword.Bluemix_notm}} 区域、组织和空间。 

    例如，要登录到美国南部区域，请运行以下命令：
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. 运行 *status* 命令。

    ```
    $ cf logging status -a -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    其中
    
    * *-a* 用于指定帐户级别信息。
    * *-s* 用于设置开始日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*
    * *-e* 用于设置结束日期，格式为全球标准时间 (UTC)：*YYYY-MM-DD*
    * *-t* 用于设置日志类型。
    

    可以通过用逗号分隔各个类型来指定多种日志类型，例如 **log_type_1,log_type_2,log_type_3**。 
 
    例如：
    
    ```
    $ cf logging status -s 2017-05-24 -e 2017-05-25 -t log -a
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 |        log         |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}














