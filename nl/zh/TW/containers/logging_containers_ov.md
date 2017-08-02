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


# IBM Bluemix Container Service 的記載功能
{: #logging_containers_ov}

您可以針對在 {{site.data.keyword.IBM}} 所管理雲端基礎架構中部署的 Docker 容器，以及在 Kubernetes 叢集中執行的 Docker 容器，來檢視、過濾及分析 Docker 容器的日誌。在 {{site.data.keyword.Bluemix_notm}} 或 Kubernetes 叢集中部署容器時，會自動啟用容器的記載功能。
{:shortdesc}

您可以使用搜索器，從容器外部監視及轉遞容器日誌。搜索器會將資料傳送至 {{site.data.keyword.Bluemix_notm}} 中的多方承租戶 Elasticsearch。



## 收集在 Kubernetes 叢集中執行之容器的日誌
{: #logging_containers_ov_logs_collected_kubernetes}

下圖顯示 {{site.data.keyword.containershort}} 記載功能的高階視圖：

![Kubernetes 叢集中所部署容器的高階元件概觀](images/containers_kube.gif "Kubernetes 叢集中所部署容器的高階元件概觀")

在 {{site.data.keyword.Bluemix_notm}} 中，當您在 Kubernetes 叢集中部署應用程式時，請考量下列資訊：

* 在 {{site.data.keyword.Bluemix_notm}} 帳戶中，您可以有一個以上的組織。 
* 每一個組織都可以有一個以上的 {{site.data.keyword.Bluemix_notm}} 空間。 
* 在組織中，您可以有一個以上的 Kubernetes 叢集。 
* 當您建立 Kubernetes 叢集時，會自動啟用日誌的收集。 
* Kubernetes 叢集與 {{site.data.keyword.Bluemix_notm}} 空間無關。不過，叢集及其資源的日誌資料都會與 {{site.data.keyword.Bluemix_notm}} 空間相關聯。
* 一旦部署 Pod，就會收集應用程式的日誌資料。
* 若要分析叢集的日誌資料，您必須存取叢集建立所在之「雲端公用」地區的 Kibana 儀表板。

在您建立叢集之前，必須透過 [{{site.data.keyword.Bluemix_notm}} 使用者介面](/docs/containers/cs_cluster.html#cs_cluster_ui)或[指令行](/docs/containers/cs_cluster.html#cs_cluster_cli)登入特定 {{site.data.keyword.Bluemix_notm}} 地區、帳戶、組織及空間。您所登入的空間就是收集叢集及其資源的記載資料的空間。

依預設，會收集任何容器處理程序列印到 stdout（標準輸出）及 stderr（標準錯誤）的資訊。將資訊傳送到 stdout 及 stderr 是公開容器資訊的標準 Docker 使用慣例。 

如果您將容器中所執行應用程式的日誌資料以 JSON 格式轉遞至 Docker 日誌收集程式，則可以在 Kibana 中使用 JSON 欄位來搜尋及分析日誌資料。如需相關資訊，請參閱[將自訂欄位配置為 Kibana 搜尋欄位](logging_containers_ov.html#send_data_in_json)。

**附註：**當您使用 Kubernetes 叢集時，名稱空間 *ibm-system* 及 *kube-system* 是保留的名稱空間。請不要在這些名稱空間中建立、刪除、修改或變更可用資源的許可權。這些名稱空間的日誌適用於 {{site.data.keyword.IBM_notm}}。


## 收集 Bluemix 所管理容器的日誌
{: #logging_containers_ov_logs_collected}

下圖顯示 {{site.data.keyword.containershort}} 記載功能的高階視圖：

![{{site.data.keyword.Bluemix_notm}} 所管理雲端基礎架構中所部署容器的高階元件概觀](images/container_bmx.gif "{{site.data.keyword.Bluemix_notm}} 所管理雲端基礎架構中所部署容器的高階元件概觀")

依預設，會收集 {{site.data.keyword.Bluemix_notm}} 所管理雲端基礎架構中所部署容器的下列日誌：

<table>
  <caption>表 2. 針對 Bluemix 所管理雲端基礎架構中所部署容器收集的日誌</caption>
  <tbody>
    <tr>
      <th align="center">日誌</th>
      <th align="center">說明</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> 依預設，Docker 訊息儲存在容器的 /var/log/messages 資料夾中。此日誌包括系統訊息。
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">此日誌是 Docker 日誌。<br> Docker 日誌檔未儲存為容器內部的檔案，但仍然會予以收集。依預設，會收集此日誌檔，因為它是標準 Docker 使用慣例，用來公開容器的 stdout（標準輸出）及 stderr（標準錯誤）資訊。會收集任何容器處理程序列印到 stdout 或 stderr 的資訊。
      </td>
     </tr>
  </tbody>
</table>

若要收集其他日誌，請在建立容器時，新增 **LOG_LOCATIONS** 環境變數，並包含日誌檔的路徑。您可以新增多個日誌檔，以逗點將其隔開。如需相關資訊，請參閱[收集容器中的非預設日誌資料](logging_containers_other_logs.html#logging_containers_collect_data)。


##  將自訂欄位配置為 Kibana 搜尋欄位 
{: #send_data_in_json}

依預設，會自動啟用容器的記載功能。Docker 日誌檔中的每個項目都會顯示在 Kibana 的 `message` 欄位中。如果您需要在 Kibana 中，使用屬於容器日誌項目一部分的特定欄位來過濾及分析資料，請配置應用程式以傳送有效的 JSON 格式化輸出。

請考量下列資訊：

* 針對 Kubernetes 叢集中所部署的容器，將訊息以 JSON 格式記載到 stdout（標準輸出）及 stderr（標準錯誤）。

    訊息中可用的每一個欄位都會剖析成符合值的欄位類型。例如，下列 JSON 訊息中的每一個欄位：
    
    ```
    {"field1":"string type",
        "field2":123,
        "field3":false,
        "field4":"4567"
    }
    ```
    
    可作為用於過濾及搜尋的欄位：
    
    * `field1` 剖析為 string 類型的 `field1_str`。
    * `field2` 剖析為 integer 類型的 `field1_int`。
    * `field3` 剖析為 boolean 類型的 `field3_bool`。
    * `field4` 剖析為 string 類型的 `field4_str`。
    
* 針對 {{site.data.keyword.Bluemix_notm}} 所管理雲端基礎架構中所部署的容器，完成下列步驟，以將容器日誌項目剖析為個別欄位：

    1. 將訊息記載至檔案。 
    2. 將日誌檔新增至來自容器可供分析的非預設日誌清單。如需相關資訊，請參閱[收集容器中的非預設日誌資料](logging_containers_other_logs.html#logging_containers_collect_data)。 
    
    以 STDOUT 形式將 JSON 日誌項目傳送至容器的 Docker 日誌檔時，不會將它們剖析為 JSON。 
    
    如果您將訊息記載至檔案，而且訊息判斷為有效的 JSON，則會剖析欄位，並為訊息中的每一個欄位建立新欄位。在 Kibana 中，只能過濾及排序 string 類型欄位值。

## 日誌汲取
{: #log_ingestion}

{{site.data.keyword.loganalysisshort}} 服務提供不同的方案。每一個方案都會定義您是否可以將日誌傳送至「日誌收集」。所有方案（不含*精簡* 方案）都可以將日誌傳送至「日誌收集」。如需方案的相關資訊，請參閱[服務方案](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)。

您可以使用「多方承租戶 Logstash 轉遞程式」，將日誌傳送至 {{site.data.keyword.loganalysisshort}}。如需相關資訊，請參閱[使用多方承租戶 Logstash 轉遞程式 (mt-logstash-forwarder) 傳送日誌資料](/docs/services/CloudLogAnalysis/how-to/send-data/send_data_mt.html#send_data_mt)。


## 日誌收集
{: #log_collection}

依預設，{{site.data.keyword.Bluemix_notm}} 會儲存最多 3 天的日誌資料：   

* 每個空間每天最多可儲存 500 MB 的資料。超過該 500 MB 上限的任何日誌都會被捨棄。上限配額會在每天凌晨 12:30（世界標準時間）重設。
* 可搜尋最多 3 天、最多 1.5 GB 的資料。達到 1.5 GB 資料或在 3 天之後，日誌資料就會輪替（先進先出）。

{{site.data.keyword.loganalysisshort}} 服務提供其他方案，讓您依所需將日誌儲存在「日誌收集」。如需每一個方案價格的相關資訊，請參閱[服務方案](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)。

您可以配置日誌保留原則，用來定義您要將日誌保留在「日誌收集」中的天數。如需相關資訊，請參閱[日誌保留原則](/docs/services/CloudLogAnalysis/log_analysis_ov.html#policies)。


## 日誌搜尋
{: #log_search}

依預設，在 {{site.data.keyword.Bluemix_notm}} 中，您可以使用 Kibana 每天最多搜尋 500 MB 的日誌。 

{{site.data.keyword.loganalysisshort}} 服務提供多個方案。每一個方案都有不同的日誌搜尋功能，例如，*日誌收集* 方案可讓您每天最多搜尋 1 GB 的資料。如需方案的相關資訊，請參閱[服務方案](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)。


## 檢視在 Kubernetes 叢集中執行之容器的容器日誌
{: #logging_containers_ov_methods_view_kube}

您可以使用下列任何一種方法，檢視 Kubernetes Pod 中之容器的最新日誌：

* 透過 Kubernetes 使用者介面來檢視日誌。針對每一個 Pod，您可以選取它，並存取其日誌。如需相關資訊，請參閱 [Web 使用者介面儀表板 ![（外部鏈結圖示）](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/ "外部鏈結圖示"){: new_window}。

* 使用 Kubernetes CLI 指令 [kubectl logs ![（外部鏈結圖示）](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://kubernetes-v1-4.github.io/docs/user-guide/kubectl/kubectl_logs/ "外部鏈結圖示"){: new_window}，來檢視日誌。 

若要檢視長期日誌，您可以使用 Kibana。請參閱[服務方案](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)以取得資料保留期間原則的相關資訊。



## 檢視 Bluemix 所管理容器的容器日誌
{: #logging_containers_ov_methods_view_bmx}

您可以使用下列任何一種方法，檢視 {{site.data.keyword.Bluemix_notm}} 所管理雲端基礎架構中部署之容器的最新日誌：

* 透過 {{site.data.keyword.Bluemix_notm}} 使用者介面來檢視日誌，以監視容器的最新活動。
    
    您可以透過每一個容器都有的**監視及日誌**標籤來檢視、過濾及分析日誌。如需相關資訊，請參閱[從 Bluemix 儀表板分析日誌](/docs/services/CloudLogAnalysis/logging_view_dashboard.html#analyzing_logs_bmx_ui)。
    
    
* 使用 {{site.data.keyword.containershort}} CLI 來檢視日誌。請使用指令，以程式設計方式管理日誌。
    
    您可以透過指令行介面，使用 **cf ic logs** 指令來檢視、過濾及分析日誌。如需相關資訊，請參閱[從指令行介面分析日誌](/docs/services/CloudLogAnalysis/logging_view_cli.html#analyzing_logs_cli)。


## 分析容器日誌
{: #logging_containers_ov_methods}

若要分析容器日誌資料，請使用 Kibana 來執行進階分析作業。您可以使用 Kibana（一種開放程式碼分析與視覺化平台），在各種圖形（例如圖表和表格）中監視、搜尋、分析及視覺化您的資料。如需相關資訊，請參閱[在 Kibana 中分析日誌](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana)。




## 指導教學：針對 Kubernetes 叢集中所部署的應用程式，在 Kibana 中分析日誌
{: #tutorial1}

若要瞭解如何使用 Kibana 來分析 Kubernetes 叢集中所部署容器的日誌，請參閱[指導教學：針對 Kubernetes 叢集中所部署的應用程式，在 Kibana 中分析日誌](/docs/services/CloudLogAnalysis/containers/tutorials/kibana_tutorial_1.html#kibana_tutorial_1)。


