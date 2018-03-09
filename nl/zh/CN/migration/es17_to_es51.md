---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 将 Elastic 堆栈升级到 V5.1 后的迁移注意事项 
{: #es17_to_es51}

在 {{site.data.keyword.Bluemix}} 中，ElasticSearch (ELK) 堆栈已从 V1.7 升级到 V5.1。提供了新的功能、用于获取日志的新 URL 以及用于在 Kibana 中分析日志的新 URL。有关更多信息，请参阅 [ElasticSearch 5.1 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html)。
{:shortdesc}

此功能不适用于将日志记录服务用于在 Kubernetes 集群中部署的 Docker 容器的用户。 

## 区域
{: #regions}

Elastic V5.1 在以下区域中可用：

* 英国
* 美国南部
* 德国
* 悉尼


## 新增功能
{: #features}

1. 有不同的 URL 用于处理日志和度量值。

    在 Elastic 1.7 中，会共享同一 URL 来显示并监视日志和度量值。升级到 Elastic 5.1 后，有不同的 URL 用于查看日志和度量值。有关更多信息，请参阅[日志记录 URL](#logging)。
    
2. 对 Kibana 5.1 的支持。

    可以通过 {{site.data.keyword.Bluemix_notm}} UI 或直接通过新的日志记录 URL 启动 Kibana。
有关更多信息，请参阅[导航至 Kibana 仪表板](/docs/services/CloudLogAnalysis/kibana/launch.html#launch)。
    
    Kibana 3 和 Kibana 4 已弃用。
	
	**注：**每个区域具有不同的 URL。目前，可访问英国可用的 Kibana 4 仪表板来比较您的仪表板和 Kibana 5.1 仪表板，并迁移到 Kibana 5.1 仪表板。 
    
    必须将您的仪表板迁移到 Elastic 5.1 环境。
    
    有关 Kibana 5.1 的更多信息，请参阅 [Kibana User Guide ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}。
    
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
    
    可供您用于过滤和搜索的字段：

    * field1 解析为字符串类型的 field1_str。
    * field2 解析为整数类型的 field1_int。
    * field3 解析为布尔类型的 field3_bool。
    * field4 解析为字符串类型的 field4_str。
    
    样本 JSON 消息是发送到日志记录服务的日志。 

    **注**：此功能仅在 Elastic 5.1 中可用。此功能在 Elastic 1.7 中不可用，以避免中断 Kibana 3 仪表板。


## 日志记录 URL
{: #logging}

将日志发送到 {{site.data.keyword.Bluemix_notm}} 中以及在 Kibana 中分析数据将使用不同的 URL。

下表列出了美国南部区域的 URL：

<table>
  <caption>表 1. 美国南部区域的 URL</caption>
    <tr>
      <th>类型</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
    </tr>
  <tr>
    <td>用于获取日志的 URL</td>
    <td>logs.opvis.bluemix.net:9091</td>
  	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>用于分析日志的 Kibana URL</td>
    <td>[https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net)</td>
	  <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
  </tr>
</table>

下表列出了英国区域的 URL：

<table>
  <caption>表 2. 英国区域的 URL</caption>
  <tr>
     <th>类型</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>用于获取日志的 URL</td>
	   <td>logs.eu-gb.opvis.bluemix.net:9091</td>
	   <td>ingest.logging.eu-gb.bluemix.net:9091</td>
  </tr>
  <tr>
     <td>用于分析日志的 Kibana URL</td>
	 <td>[https://logmet.eu-gb.bluemix.net](https://logmet.eu-gb.bluemix.net)</td>
	 <td>[https://logging.eu-gb.bluemix.net](https://logging.eu-gb.bluemix.net)</td>
  </tr>
</table>

下表列出了法兰克福区域的 URL：

<table>
  <caption>表 3. 法兰克福区域的 URL</caption>
  <tr>
     <th>类型</th>
      <th>Elastic 2.3 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>用于获取日志的 URL</td>
	 <td>ingest.logging.eu-de.bluemix.net</td>
	 <td>ingest-eu-fra.logging.bluemix.net</td>
  </tr>
  <tr>
     <td>用于分析日志的 Kibana URL</td>
	 <td>[https://logging.eu-de.bluemix.net](https://logging.eu-de.bluemix.net)</td>
	 <td>[https://logging.eu-fra.bluemix.net](https://logging.eu-fra.bluemix.net)</td>
  </tr>
</table>



