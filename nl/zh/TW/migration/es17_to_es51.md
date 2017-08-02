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

# 將 ELK Stack 升級至 5.1 版之後的移轉考量 
{: #es17_to_es51}

在 {{site.data.keyword.Bluemix}} 中，ElasticSearch (ELK) Stack 已從 1.7 版升級至 2.3 版。提供了新增特性、可汲取日誌的 URL，以及在 Kibana 中分析日誌的新 URL。如需相關資訊，請參閱 [ElasticSearch 5.1 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html "外部鏈結圖示")。
{:shortdesc}

此特性不適用於搭配使用記載服務與 Kubernetes 叢集中所部署 Docker 容器的使用者。這些容器已使用 ELK Stack 2.3 版。

## 地區
{: #regions}

下列地區提供 ELK Stack 5.1 版：

* 美國南部


## 新增功能
{: #features}

1. 以不同的 URL 來使用日誌及度量值。

    在 ELK 1.7 中，會共用相同的 URL 來顯示及監視日誌和度量值。升級至 ELK 5.1 之後，您會有不同的 URL 來檢視日誌及度量值。如需相關資訊，請參閱[記載 URL](#logging)。
    
2. 支援 Kibana 5.1。 

    您可以從 {{site.data.keyword.Bluemix_notm}} 使用者介面啟動 Kibana，或直接從新的記載 URL 啟動 Kibana。如需相關資訊，請參閱[使用 Kibana 分析日誌](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana)。
    
    Kibana 3 已淘汰。您可以透過 [ELK 1.7 記載 URL](#logging) 來啟動 Kibana 3。每個地區的 URL 都不同。**附註：**您目前可以存取 Kibana 3 儀表板來進行比較，並可將 Kibana 3 儀表板移轉至 Kibana 5.1 儀表板。 
    
    如果您的 Kibana 儀表板以 ELK Stack 1.7 為建置基礎，則必須將它們移轉至 ELK 5.1 環境。
    
    如需 Kibana 5.1 的相關資訊，請參閱 [Kibana User Guide ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/5.1/index.html "外部鏈結圖示"){: new_window}。
    
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


## 記載 
{: #logging}

使用不同的 URL 將日誌傳送至 {{site.data.keyword.Bluemix_notm}}，以及在 Kibana 中分析資料。

下表列出「美國南部」地區的新 URL：

<table>
  <caption>「美國南部」地區的 URL</caption>
    <tr>
      <th>類型</th>
      <th>ELK 1.7 </th>
	  <th>ELK 5.1 </th>
    </tr>
  <tr>
    <td>用於汲取日誌的 URL</td>
    <td>logs.opvis.bluemix.net:9091</td>
	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>可分析日誌的 Kibana URL</td>
    <td>https://logmet.ng.bluemix.net</td>
	<td>https://logging.ng.bluemix.net</td>
  </tr>
</table>

