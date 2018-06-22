---

copyright:
  years: 2017, 2018

lastupdated: "2018-04-20"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 合规性
{: #compliance}

[{{site.data.keyword.Bluemix}} 提供了根据 IBM 严格安全标准构建的云平台和服务。](/docs/security/compliance.html#compliance){{site.data.keyword.loganalysislong}} 服务是专为 {{site.data.keyword.Bluemix_notm}} 而构建的 DevOps 服务。
{:shortdesc}


## 一般数据保护法规

一般数据保护法规 (GDPR) 力图在整个欧盟范围内建立统一的数据保护法律框架，旨在让居民拿回对其个人数据的控制权，同时对在全球任意位置托管和“处理”数据的相关方实施严格的规则。该法规还引入了与欧盟境内和境外个人数据自由流动相关的规则。 

**免责声明**：{{site.data.keyword.loganalysisshort}} 服务存储并显示在 {{site.data.keyword.Bluemix_notm}} 帐户中运行的云资源的日志记录，以及可能从 {{site.data.keyword.Bluemix_notm}} 外部发送的日志的日志记录。个人信息 (PI) 不能包含在 {{site.data.keyword.loganalysisshort}} 中存储的任何日志条目中，因为这些数据可供您企业内的其他用户访问，也可供 {{site.data.keyword.IBM_notm}} 访问以支持云服务。

### 区域
{: #regions}

{{site.data.keyword.loganalysisshort}} 服务计划截至 2018 年 5 月 25 日，在此服务可用的 {{site.data.keyword.Bluemix_notm}} Public 区域中符合 GDPR。


### 数据保留
{: #data_retention}

{{site.data.keyword.loganalysisshort}} 服务包含 2 个可存储数据的数据存储库： 

* 日志搜索，用于托管可通过 Kibana 进行分析的日志数据。
* 日志收集，用于托管长期存储的日志数据。

根据 {{site.data.keyword.loganalysisshort}} 服务套餐，数据要么单独存储在“日志搜索”中，要么同时存储在“日志搜索”和“日志收集”中。标准套餐和轻量套餐仅在“日志搜索”中存储数据。其余套餐同时在“日志搜索”和“日志收集”中存储数据。

* 存储在“日志搜索”中的日志会保留 3 天。
* 除非您配置了保留时间策略或手动将日志删除，否则会保留在“日志收集”中存储的日志。缺省情况下，在“日志收集”中的日志会无限期保留。



### 数据删除
{: #data_deletion}

请考虑以下信息：

* 存储在“日志搜索”中的日志会在 3 天后删除。

* 对于“日志收集”中存储的日志，会在配置的保留时间策略中的天数后删除，或者可以手动删除这些日志。 

    可以配置日志保留时间策略，以定义希望日志在“日志收集”中保留的天数。[使用 {{site.data.keyword.Bluemix_notm}} 插件查看和配置日志保留时间策略](/docs/services/CloudLogAnalysis/how-to/manage-logs/configuring_retention_policy_cloud.html#configuring_retention_policy)。

    您可以使用[日志收集 API](https://console.bluemix.net/apidocs/948-ibm-cloud-log-collection-api?&language=node&env_id=ibm%3Ayp%3Aus-south#introduction){: new_window} 或[日志收集 CLI](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#log_analysis_cli){: new_window} 从“日志收集”中手动删除日志。 

    您可以使用 CLI 从“日志收集”中手动删除日志。有关更多信息，请参阅[使用 {{site.data.keyword.Bluemix_notm}} 插件运行 bx logging log-delete](/docs/services/CloudLogAnalysis/how-to/manage-logs/deleting_logs_cloud.html#deleting_logs)。


如果从付费套餐更改为标准套餐或轻量套餐，那么“日志收集”中的日志将在大约一天内删除。

您可以随时打开支持凭单，并请求从“日志搜索”和“日志收集”中删除所有数据。有关开具 IBM 支持凭单的信息，请参阅[联系支持人员](https://www.{DomainName}/docs/support/index.html#contacting-support)。



### 更多信息
{: #info}

要获取更多信息，请参阅：

[{{site.data.keyword.Bluemix_notm}} 安全合规性](/docs/security/compliance.html#compliance)

[GDPR - {{site.data.keyword.IBM_notm}} 官方页面](https://www.ibm.com/data-responsibility/gdpr/)



