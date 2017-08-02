---

copyright:
  years: 2017

lastupdated: "2017-07-19"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 導覽至 Kibana 儀表板
{: #launch}

您可以從 {{site.data.keyword.loganalysisshort}} 服務或 {{site.data.keyword.Bluemix}} 使用者介面啟動 Kibana，或直接從 Web 瀏覽器啟動 Kibana。
{:shortdesc}

若為 CF 應用程式，以及 {{site.data.keyword.Bluemix_notm}} 所管理雲端基礎架構中部署的 Docker 容器，您可以從 {{site.data.keyword.Bluemix_notm}} 啟動 Kibana，以根據啟動 Kibana 所用之資源的環境定義來檢視及分析資料。例如，在 Kibana 中，您可以在特定 CF 應用程式的環境定義中，啟動至該特定應用程式的日誌。
    
若為任何雲端資源（例如 Kubernetes 基礎架構中部署的 Docker 容器），您可以從直接瀏覽器鏈結或從 {{site.data.keyword.loganalysisshort}} 服務儀表板啟動 Kibana，以查看所提供 {{site.data.keyword.Bluemix_notm}} 空間內服務的聚集日誌資料。用來過濾儀表板顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中某個空間的日誌項目。Kibana 顯示的日誌資訊，包括部署在 {{site.data.keyword.Bluemix_notm}} 組織中您登入之空間內的所有資源記錄。 

下表列出啟動 Kibana 的一些雲端資源及支援的導覽方法：

<table>
<caption>表 1. 資源及所支援導覽方法的清單。</caption>
  <tr>
    <th>資源</th>
	<th>從 {{site.data.keyword.loganalysisshort}} 服務儀表板導覽至 Kibana 儀表板</th>
    <th>從 Bluemix 儀表板導覽至 Kibana 儀表板</th>
    <th>從 Web 瀏覽器導覽至 Kibana 儀表板</th>
  </tr>
  <tr>
    <td>CF 應用程式</td>
	<td>是</td>
    <td>是</td>
    <td>是</td>
  </tr>  
  <tr>
    <td>Kubernetes 叢集中部署的容器</td>
	<td>是</td>
    <td>否</td>
    <td>是</td>
  </tr>  
  <tr>
    <td>{{site.data.keyword.Bluemix_notm}} 所管理雲端基礎架構中部署的容器</td>
	<td>是</td>
    <td>是</td>
    <td>是</td>
  </tr>  
</table>

如需 Kibana 的相關資訊，請參閱 [Kibana User Guide ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/5.1/index.html "外部鏈結圖示"){: new_window}。
    

##  從 Log Analysis 服務的儀表板導覽至 Kibana
{: #launch_Kibana_from_log_analysis}

用來過濾 Kibana 顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中該空間的日誌項目。 
	
Kibana 顯示的日誌資訊，包括部署在 {{site.data.keyword.Bluemix_notm}} 組織中您登入空間內之所有資源的記錄。

請完成下列步驟，以從 {{site.data.keyword.loganalysisshort}} 服務的儀表板中啟動 Kibana：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從 {{site.data.keyword.Bluemix_notm}} 儀表板按一下 {{site.data.keyword.loganalysisshort}} 服務。 
    
2. 選取 {{site.data.keyword.Bluemix_notm}} 使用者介面中的**受管理**標籤。

3. 按一下**啟動**。即會開啟 Kibana 儀表板。

依預設，**探索**頁面會載入，並選取預設索引型樣，且時間過濾器設為過去 15 分鐘。 

如果「探索」頁面未顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](filter_logs.html#set_time_filter)。

	
	
##  從 Web 瀏覽器導覽至 Kibana
{: #launch_Kibana_from_browser}

用來過濾 Kibana 顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中該空間的日誌項目。 
	
Kibana 顯示的日誌資訊，包括部署在 {{site.data.keyword.Bluemix_notm}} 組織中您登入空間內之所有資源的記錄。

請完成下列步驟，以從瀏覽器啟動 Kibana：

1. 開啟 Web 瀏覽器，並啟動 Kibana。然後，登入 Kibana 使用者介面。
    
    例如，下表列出在美國南部地區啟動 Kibana 時必須使用的 URL：
      
    <table>
          <caption>表 1. 每個地區用來啟動 Kibana 的 URL</caption>
           <tr>
            <th>地區</th>
            <th>URL</th>
          </tr>
          <tr>
            <td>美國南部</td>
            <td>https://logging.ng.bluemix.net/ </td>
          </tr>
    </table>
	
	即會開啟 Kibana 中的「探索」頁面。
	
2. 選取您要在其中檢視及分析日誌資料之 {{site.data.keyword.Bluemix_notm}} 空間的索引型樣。

    1. 按一下 **default-index**。
	
	2. 選取空間的索引型樣。索引型樣的格式如下：
	
	    ```
	    [logstash-Space_ID-]YYYY.MM.DD 
	    ```
        {screen}
	
	    其中，*Space_ID* 是您要在其中檢視及分析日誌資料之 {{site.data.keyword.Bluemix_notm}} 空間的 GUID。 
	
如果「探索」頁面未顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter)。


	
##  從 CF 應用程式的儀表板導覽至 Kibana
{: #launch_Kibana_from_cf_app}

用來過濾 Kibana 顯示資料的查詢，會擷取 Kibana 啟動所在之 {{site.data.keyword.Bluemix_notm}} CF 應用程式的日誌項目。

若要在 Kibana 中查看 Cloud Foundry 應用程式的日誌，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從 {{site.data.keyword.Bluemix_notm}} 儀表板按一下應用程式名稱或容器。 
    
2. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，開啟「日誌」標籤。

    若為 CF 應用程式，請按一下導覽列中的**日誌**。
    即會開啟「日誌」標籤。  

3. 按一下**進階視圖**。即會開啟 Kibana 儀表板。

    依預設，**探索**頁面會載入，並選取預設索引型樣，且時間過濾器設為過去 30 秒。搜尋查詢設為符合 CF 應用程式的所有項目。

    如果「探索」頁面未顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter)。


##  從容器的儀表板導覽至 Kibana
{: #launch_Kibana_for_containers}

此方法只適用於 {{site.data.keyword.Bluemix_notm}} 所管理雲端基礎架構中部署的容器。

用來過濾 Kibana 顯示資料的查詢，會擷取 Kibana 啟動所在之容器的日誌項目。

若要在 Kibana 中查看 Docker 容器的日誌，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從 {{site.data.keyword.Bluemix_notm}} 儀表板按一下容器。 
    
2. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，開啟「日誌」標籤。

    針對 {{site.data.keyword.IBM_notm}} 所管理雲端基礎架構中所部署的容器，選取導覽列中的**監視及日誌**，然後按一下**記載**標籤。 
    
    即會開啟「日誌」標籤。  

3. 按一下**進階視圖**。即會開啟 Kibana 儀表板。

    依預設，**探索**頁面會載入，並選取預設索引型樣，且時間過濾器設為過去 30 秒。搜尋查詢設為符合 Docker 容器的所有項目。

    如果「探索」頁面未顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter)。

	



