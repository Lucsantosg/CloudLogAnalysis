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


# 變更方案
{: #change_plan}

您可以在 {{site.data.keyword.Bluemix_notm}} 的服務「儀表板」中變更 {{site.data.keyword.loganalysisshort}} 服務方案，或是透過執行 `cf update-service` 指令來變更。您隨時可以升級或降低方案。
{:shortdesc}

## 透過使用者介面變更服務方案
{: #change_plan_ui}

若要在 {{site.data.keyword.Bluemix_notm}} 的服務儀表板中變更服務方案，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從 {{site.data.keyword.Bluemix_notm}} 儀表板按一下 {{site.data.keyword.loganalysisshort}} 服務。 
    
2. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，選取**方案**標籤。

    即會顯示現行方案的相關資訊。
	
3. 選取新方案以升級或降低您的方案。 

4. 按一下**儲存**。



## 透過 CLI 變更服務方案
{: #change_plan_cli}

若要在 Bluemix 中透過 CLI 變更服務方案，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 地區、組織及空間。 

    例如，若要登入「美國南部」地區，請執行下列指令：
	
	```
    cf login -a https://api.ng.bluemix.net
	```
    {: codeblock}
	
2. 執行 `cf services` 指令來檢查現行方案，以及從空間中的可用服務清單，取得 {{site.data.keyword.loganalysisshort}} 服務名稱。 

    **name** 欄位的值就是您必須用來變更方案的值。 

    例如，
	
	```
	$ cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK
    
    name              service          plan      bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   premium                create succeeded
	```
	{: screen}
    
3. 升級或降低您的方案。執行 `cf update-service` 指令。
    
	```
	cf update-service service_name [-p new_plan]
	```
	{: codeblock}
	
	其中 
	
	* *service_name* 是服務的名稱。您可以執行 `cf services` 指令來取得值。
	* *new_plan* 是方案的名稱。
	
	下表列出不同的方案及其支援的值：
	
	<table>
	  <caption>表 1. 方案清單。</caption>
	  <tr>
	    <th>方案</th>
	    <th>名稱</th>
	  </tr>
	  <tr>
	    <td>精簡</td>
	    <td>lite</td>
	  </tr>
	  <tr>
	    <td>日誌收集</td>
	    <td>premium</td>
	  </tr>
	  <tr>
	    <td>日誌收集，每天搜尋 2 GB</td>
	    <td>premiumsearch2</td>
	  </tr>
	  <tr>
	    <td>日誌收集，每天搜尋 5 GB</td>
	    <td>premiumsearch5</td>
	  </tr>
	  <tr>
	    <td>日誌收集，每天搜尋 10 GB</td>
	    <td>premiumsearch10</td>
	  </tr>
	</table>
	
	例如，若要將您的方案降低為*精簡* 方案，請執行下列指令：
	
	```
	cf update-service "Log Analysis-a4" -p lite
    Updating service instance Log Analysis-a4 as xxx@yyy.com...
    OK
	```
	{: screen}

4. 驗證已變更新方案。執行 `cf services` 指令。

	```
	cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service          plan   bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   lite                update succeeded
	```
	{: screen}






