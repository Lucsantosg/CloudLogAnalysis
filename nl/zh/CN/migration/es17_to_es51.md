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

# 将 ELK 堆栈升级到 V5.1 后的迁移注意事项 
{: #es17_to_es51}

在 {{site.data.keyword.Bluemix}} 中，ElasticSearch (ELK) 堆栈已从 V1.7 升级到 V2.3。提供了新的功能、用于获取日志的 URL 以及用于在 Kibana 中分析日志的新 URL。有关更多信息，请参阅 [ElasticSearch 5.1 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html "外部链接图标")。
{:shortdesc}

此功能不适用于将日志记录服务用于在 Kubernetes 集群中部署的 Docker 容器的用户。这些容器已经使用 ELK 堆栈 V2.3。

## 区域
{: #regions}

ELK 堆栈 V5.1 在以下区域中可用：

* 美国南部


## 新增功能
{: #features}

1. 有不同的 URL 用于处理日志和度量值。

    在 ELK 1.7 中，会共享同一 URL 来显示并监视日志和度量值。升级到 ELK 5.1 后，有不同的 URL 用于查看日志和度量值。有关更多信息，请参阅[日志记录 URL](#logging)。
    
2. 对 Kibana 5.1 的支持。 

    可以通过 {{site.data.keyword.Bluemix_notm}} UI 或直接通过新的日志记录 URL 启动 Kibana。
有关更多信息，请参阅[使用 Kibana 分析日志](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana)。
    
    但不推荐使用 Kibana 3。可以通过 [ELK 1.7 日志记录 URL](#logging) 启动 Kibana 3。每个区域有不同的 URL。**注**：目前，您可访问 Kibana 3 仪表板来比较 Kibana 3 仪表板和 Kibana 5.1 仪表板，并从 Kibana 3 仪表板迁移到 Kibana 5.1 仪表板。 
    
    如果您的 Kibana 仪表板是基于 ELK 1.7 堆栈构建的，那么必须将其迁移到 ELK 5.1 环境。
    
    有关 Kibana 5.1 的更多信息，请参阅 [Kibana User Guide ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/kibana/5.1/index.html "外部链接图标"){: new_window}。
    
3. 向定制字段添加了基于类型的后缀。

    可以将定制字段配置为 Kibana 搜索字段。消息中可用的每个字段都会解析为与值相匹配的字段类型。例如，以下 JSON 消息中的每个字段： 

    ```
    {"field1":"string type",
        "field2":123,
        "field3":false,
        "field4":"4567"
    }
    ```
    {: screen}
    
    可用作您可用于过滤和搜索的字段：

    * field1 解析为字符串类型的 field1_str。
    * field2 解析为整数类型的 field1_int。
    * field3 解析为布尔类型的 field3_bool。
    * field4 解析为字符串类型的 field4_str。
    
    样本 JSON 消息是发送到日志记录服务的日志。 

    **注**：此功能仅在 Elastic 5.1 中可用。此功能在 Elastic 1.7 中不可用，以避免中断 Kibana 3 仪表板。


## 日志记录 
{: #logging}

将日志发送到 {{site.data.keyword.Bluemix_notm}} 中以及在 Kibana 中分析数据将使用不同的 URL。

下表列出了美国南部区域的新 URL：

<table>
  <caption>美国南部区域的 URL</caption>
    <tr>
      <th>类型</th>
      <th>ELK 1.7</th>
	  <th>ELK 5.1</th>
    </tr>
  <tr>
    <td>用于获取日志的 URL</td>
    <td>logs.opvis.bluemix.net:9091</td>
	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>用于分析日志的 Kibana URL</td>
    <td>https://logmet.ng.bluemix.net</td>
	<td>https://logging.ng.bluemix.net</td>
  </tr>
</table>

