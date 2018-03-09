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

# 將 Elastic Stack 升級至 5.1 版之後的移轉考量 
{: #es17_to_es51}

在 {{site.data.keyword.Bluemix}} 中，ElasticSearch (ELK) Stack 已從 1.7 版升級至 5.1 版。提供新增特性、可汲取日誌的新 URL，以及在 Kibana 中分析日誌的新 URL。如需相關資訊，請參閱 [ElasticSearch 5.1 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html)。
{:shortdesc}

此特性不適用於搭配使用記載服務與 Kubernetes 叢集中所部署 Docker 容器的使用者。 

## 地區
{: #regions}

下列地區提供 Elastic 5.1 版：

* 英國
* 美國南部
* 德國
* 雪梨


## 新增功能
{: #features}

1. 以不同的 URL 來使用日誌及度量值。

    在 Elastic 1.7 中，會共用相同的 URL 來顯示及監視日誌和度量值。升級至 Elastic 5.1 之後，您會有不同的 URL 來檢視日誌及度量值。如需相關資訊，請參閱[記載 URL](#logging)。
    
2. Kibana 5.1 支援。

    您可以從 {{site.data.keyword.Bluemix_notm}} 使用者介面啟動 Kibana，或直接從新的記載 URL 啟動 Kibana。如需相關資訊，請參閱[導覽至 Kibana 儀表板](/docs/services/CloudLogAnalysis/kibana/launch.html#launch)。
    
    Kibana 3 及 Kibana 4 已淘汰。
	
	**附註：**每個地區的 URL 都不同。您目前可以在英國存取 Kibana 4 儀表板來進行比較，並可以將儀表板移轉至 Kibana 5.1 儀表板。 
    
    您必須將儀表板移轉至 Elastic 5.1 環境。
    
    如需 Kibana 5.1 的相關資訊，請參閱 [Kibana User Guide ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}。
    
3. 已在自訂欄位新增以類型為基礎的字尾。

    您可以將自訂欄位配置為 Kibana 搜尋欄位。訊息中可用的每一個欄位都會剖析成符合值的欄位類型。例如，下列 JSON 訊息中的每一個欄位： 

    ```
    {"field1":"string type",
     "field2":123,
     "field3":false,
     "field4":"4567"
     }
    ```
    {: screen}
    
    可作為用於過濾及搜尋的欄位：

    * field1 剖析為 string 類型的 field1_str。
    * field2 剖析為 integer 類型的 field1_int。
    * field3 剖析為 boolean 類型的 field3_bool。
    * field4 剖析為 string 類型的 field4_str。
    
    範例 JSON 訊息是您已傳送至記載服務的日誌。 

    **附註：**只有 Elastic 5.1 才提供此特性。Elastic 1.7 未提供此特性，以避免破壞 Kibana3 儀表板。


## 記載 URL
{: #logging}

使用不同的 URL 將日誌傳送至 {{site.data.keyword.Bluemix_notm}}，以及在 Kibana 中分析資料。

下表列出美國南部地區的 URL：

<table>
  <caption>表 1. 美國南部地區的 URL</caption>
    <tr>
      <th>類型</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
    </tr>
  <tr>
    <td>用於汲取日誌的 URL</td>
    <td>logs.opvis.bluemix.net:9091</td>
  	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>可分析日誌的 Kibana URL</td>
    <td>[https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net)</td>
	  <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
  </tr>
</table>

下表列出英國地區的 URL：

<table>
  <caption>表 2. 英國地區的 URL</caption>
  <tr>
     <th>類型</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>用於汲取日誌的 URL</td>
	   <td>logs.eu-gb.opvis.bluemix.net:9091</td>
	   <td>ingest.logging.eu-gb.bluemix.net:9091</td>
  </tr>
  <tr>
     <td>可分析日誌的 Kibana URL</td>
	 <td>[https://logmet.eu-gb.bluemix.net](https://logmet.eu-gb.bluemix.net)</td>
	 <td>[https://logging.eu-gb.bluemix.net](https://logging.eu-gb.bluemix.net)</td>
  </tr>
</table>

下表列出法蘭克福地區的 URL：

<table>
  <caption>表 3. 法蘭克福地區的 URL</caption>
  <tr>
     <th>類型</th>
      <th>Elastic 2.3 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>用於汲取日誌的 URL</td>
	 <td>ingest.logging.eu-de.bluemix.net</td>
	 <td>ingest-eu-fra.logging.bluemix.net</td>
  </tr>
  <tr>
     <td>可分析日誌的 Kibana URL</td>
	 <td>[https://logging.eu-de.bluemix.net](https://logging.eu-de.bluemix.net)</td>
	 <td>[https://logging.eu-fra.bluemix.net](https://logging.eu-fra.bluemix.net)</td>
  </tr>
</table>



