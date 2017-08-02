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


# Kibana 常見問題 (FAQ)
{: #faq_kibana}

以下是關於使用 {{site.data.keyword.Bluemix}} 記載功能的常見問題與解答。
{:shortdesc}

* [如果在 Kibana 的「探索」頁面中看不到資料，我該怎麼辦](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_no_data_discover_kibana)
* [如果發生鑑別異常狀況，我該怎麼辦](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_no_data_dashboard_kibana)
* [如何啟動 Kibana 3](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_kibana3)
* [為什麼我會在 Kibana「探索」頁面的欄位旁看到 ? 符號](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_kibana_question)
* [變更預設索引型樣時發生 403 錯誤](/docs/services/CloudLogAnalysis/qa/faq_kibana.html#error_403)

## 如果在 Kibana 的「探索」頁面中看不到資料，我該怎麼辦
{: #logging_qa_no_data_discover_kibana}

您在 Kibana 中看不到資料，可能會有以下幾種不同情境：

1. 啟動 Kibana 時，您在「探索」頁面中可能不會看到任何資料，並且收到下列訊息：**找不到任何結果**。 
2. 您可能正在 Kibana 的「探索」頁面中工作。不過，不久之後，當您嘗試在 Kibana 中執行作業時，收到下列訊息：**找不到任何結果**。

若要解決這個問題，請完成下列步驟：

1. 檢查「探索」頁面中設定的*時間選取器*，並增長時段。 

    **附註**：依預設，在 {{site.data.keyword.Bluemix_notm}} 中，*時間選取器* 設定為顯示過去 15 分鐘的資料。

    如需如何設定*時間選取器* 的相關資訊，請參閱[設定時間過濾器](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter)。
       
2. 按一下位於*探索* 頁面搜尋列中的放大鏡。頁面資料會根據預設搜尋查詢來重新整理。

    或者，您也可以設定*自動重新整理* 週期。

    **附註**：依預設，在 {{site.data.keyword.Bluemix_notm}} 中，*自動重新整理* 週期設定為**關閉**。
    
    如需如何啟用此功能的相關資訊，請參閱[自動重新整理資料](/docs/services/CloudLogAnalysis/kibana/analize_logs_interactively.html#discover_view_refresh_interval)。



## 如果發生鑑別異常狀況，我該怎麼辦
{: #logging_qa_no_data_dashboard_kibana}

如果您在「儀表板」頁面中，看不到視覺效果中顯示的資料，並收到錯誤訊息：**錯誤：授權異常狀況。**，請檢查您查看各視覺效果資料的許可權。

請考量下列資訊：您可以在「儀表板」頁面中配置一個以上的視覺效果。當「儀表板」頁面要求收集透過那些視覺效果顯示的資料時，針對所有視覺效果，只會發出一個要求。如果您沒有查看其中一項視覺效果資料的許可權，整個要求都會失敗。

若要解決這個問題，請完成下列步驟：

1. 識別您沒有許可權的視覺效果。

    1. 在*儀表板* 頁面中按一下視覺效果的*鉛筆* 圖示。該視覺效果會在*視覺化* 頁面中開啟。或者，您也可以在*視覺化* 頁面中，載入一個視覺效果。 
    2. 驗證您可以看到資料。
    
    重複這些步驟來處理每一個視覺效果。

2. 向您的雲端管理者要求查看那些視覺效果中之資料的存取權。

3. 建立新的「儀表板」頁面，其中排除您沒有許可權的視覺效果，但您有權查看造成問題之視覺效果中的資料。 

    如果您共用該「儀表板」，請勿刪除視覺效果，因為那樣會影響其他使用相同儀表板的團隊成員。

## 如何啟動 Kibana 3
{: #logging_qa_kibana3}

**附註：**Kibana 3 已淘汰。

您可以從瀏覽器啟動 Kibana 3。

請完成下列步驟，以從瀏覽器啟動 Kibana 3：

1. 開啟 [https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net) 以登入 Kibana 使用者介面。
    
2. 選取您想要用來分析日誌的 Kibana 版本。
    * 選取 **Kibana 4** 標籤，以使用 Kibana 4。「探索」頁面即會開啟。如需相關資訊，請參閱[在 Kibana 中以互動方式分析日誌](/docs/services/CloudLogAnalysis/qa/faq_kibana.html#logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)。
    * 選取 **Kibana 3** 標籤，以使用 Kibana 3。預設的 Kibana 儀表板即會開啟。如需使用 Kibana 3 來分析日誌的相關資訊，請參閱[在 Kibana 3 中分析日誌（已淘汰）](docs/monitor_log/kibana3/logging_view_kibana3.html#analyzing_logs_Kibana3)。如需自訂 Kibana 3 儀表板的相關資訊，請參閱[此部落格文章 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/ "外部鏈結圖示"){: new_window}。
     

## 為什麼我會在 Kibana「探索」頁面的欄位旁看到 ? 符號
{: #logging_qa_kibana_question}

當您在 Kibana 中開啟「探索」頁面時，可能會在可用欄位區段所列的欄位旁看到問號 `?`，而不是字元 `t`。當您重新載入欄位清單時，會分析欄位類型，並將問號 `?` 取代為字元 `t`。如需相關資訊，請參閱[重新載入欄位清單](/docs/services/CloudLogAnalysis/kibana/analize_logs_interactively.html#discover_view_reload_fields)。


## 變更預設索引型樣時發生 403 錯誤
{: #error_403}

無法變更預設索引型樣。 

如果您嘗試設定不同的索引型樣作為新的預設索引型樣，會發生下列錯誤：`Config: Error 403 Forbidden`


