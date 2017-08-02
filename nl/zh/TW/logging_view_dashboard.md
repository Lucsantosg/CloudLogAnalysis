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

# 在 Bluemix 使用者介面中分析日誌
{: #analyzing_logs_bmx_ui}

在 {{site.data.keyword.Bluemix}} 中，您可以透過每一個 Cloud Foundry 應用程式或 Docker 容器都有的日誌標籤來檢視、過濾及分析日誌（Cloud Foundry 應用程式或 Docker 容器在 {{site.data.keyword.IBM_notm}} 所管理基礎架構中執行）。
{:shortdesc}

##  導覽至 Cloud Foundry 應用程式的日誌
{: #launch_logs_tab_bmx_ui_cf}

若要查看 Cloud Foundry 應用程式的部署或運行環境日誌，請完成下列步驟：

1. 從「應用程式」儀表板，按一下 Cloud Foundry 應用程式的名稱。 
    
2. 從應用程式詳細資料頁面，按一下**日誌**。
    
    從**日誌**標籤，您可以檢視應用程式的最新日誌，或即時讀取日誌尾端的內容。此外，您還可以依元件（日誌類型）、依應用程式實例 ID 以及依錯誤來過濾日誌。
    
依預設，來自 {{site.data.keyword.Bluemix_notm}} 主控台可供分析的日誌包含過去 24 小時的資料。

**提示：**若要分析過去 24 小時之前的自訂期間的資料，請參閱[使用 Kibana 執行進階日誌分析](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana)。 





##  導覽至 Bluemix 中所管理 Docker 容器的日誌
{: #launch_logs_tab_bmx_ui_containers}

若要查看 {{site.data.keyword.IBM_notm}} 所管理雲端基礎架構中所部署 Docker 容器的部署或運行環境日誌，請完成下列步驟：

1. 從「應用程式」儀表板，按一下單一容器或容器群組。 
    
2. 從應用程式詳細資料頁面，按一下**監視及日誌**。

3. 選取**記載**標籤。
    
    從**記載**標籤，您可以檢視容器的最新日誌，或即時讀取日誌尾端的內容。 
	
	
	

## CF 應用程式日誌的日誌格式
{: #log_format_cf}

{{site.data.keyword.Bluemix_notm}} Cloud Foundry 應用程式的日誌會以固定格式顯示，與下列型樣類似：

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>/<var class="keyword varname">message</var>/<var class="keyword varname">timestamp</var></code>

每個日誌項目都包含下列欄位：

| 欄位 | 說明 |
|-------|-------------|
| 時間戳記 | 日誌陳述文字的時間。時間戳記最多定義到毫秒。|
| 元件 | 產生日誌的元件。如需不同元件的清單，請參閱 [CF 應用程式的日誌來源](cfapps/logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)。<br> 每一個元件類型後面都接著一個斜線，以及一個指出應用程式實例用的數字。數字 0 配置給第一個實例，數字 1 配置給第二個實例，依此類推。|
| 訊息 | 元件所發出的訊息。訊息會視環境定義而改變。|
{: caption="表 1. CF 應用程式日誌項目欄位" caption-side="top"}


## 容器日誌的日誌格式
{: #log_format_containers}

容器的日誌會以固定格式顯示，與下列型樣類似：

<code><var class="keyword varname">timestamp</var>/<var class="keyword varname">machine</var>/<var class="keyword varname">message</var>  </code>

每個日誌項目都包含下列欄位：

| 欄位 | 說明 |
|-------|-------------|
| 日期/時間 | 日誌陳述文字的時間。時間戳記定義以毫秒為單位。|
| 機器 | 容器執行所在的主機名稱。|
| 訊息 | 發出的訊息。訊息會視環境定義而改變。|
{: caption="表 2. Docker 容器日誌項目欄位" caption-side="top"}

