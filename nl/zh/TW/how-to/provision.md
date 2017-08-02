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


# 佈建 Log Analysis 服務
{: #provision}

您可以從 {{site.data.keyword.Bluemix}} 使用者介面或從指令行佈建 {{site.data.keyword.loganalysisshort}} 服務。
{:shortdesc}


## 從使用者介面佈建
{: #ui}

請完成下列步驟，以在 {{site.data.keyword.Bluemix_notm}} 中佈建 {{site.data.keyword.loganalysisshort}} 服務的實例：

1. 登入 {{site.data.keyword.Bluemix_notm}} 帳戶。

    {{site.data.keyword.Bluemix_notm}} 儀表板可以在下列網站找到：[http://bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net "外部鏈結圖示"){:new_window}。
    
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 按一下**型錄**。{{site.data.keyword.Bluemix_notm}} 上可用的服務清單隨即開啟。

3. 選取 **DevOps** 種類，以過濾所顯示的服務清單。

4. 按一下 **Log Analysis** 磚。

5. 選取服務方案。依預設，會設定**精簡**方案。

    如需服務方案的相關資訊，請參閱[服務方案](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)。
	
6. 按一下**建立**，以在所登入的 {{site.data.keyword.Bluemix_notm}} 空間中佈建 {{site.data.keyword.loganalysisshort}} 服務。
  
 

## 從 CLI 佈建
{: #cli}

請完成下列步驟，以透過指令行在 {{site.data.keyword.Bluemix_notm}} 中佈建 {{site.data.keyword.loganalysisshort}} 服務的實例：

1. 安裝 Cloud Foundry (CF) CLI。如果已安裝 CF CLI，請繼續進行下一步。

   如需相關資訊，請參閱[安裝 cf CLI ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "外部鏈結圖示"){: new_window}。 
    
2. 登入 {{site.data.keyword.Bluemix_notm}} 地區、組織及空間。 

    例如，若要登入「美國南部」地區，請執行下列指令：

    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    請遵循指示。輸入您的 {{site.data.keyword.Bluemix_notm}} 認證，選取組織及空間。
	
3. 執行 `cf create-service` 指令以佈建實例。

	```
	cf create-service service_name service_plan service_instance_name
	```
	{: codeblock}
	
	其中
	
	* service_name 是服務的名稱，亦即 **ibmLogAnalysis**。
	* service_plan 是服務方案名稱。如需方案的清單，請參閱[服務方案](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)。
	* service_instance_name 是您要用於所建立之新服務實例的名稱。
	
	如需 cf 指令的相關資訊，請參閱 [cf create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service)。

	例如，若要使用免費方案建立 {{site.data.keyword.loganalysisshort}} 服務的實例，請執行下列指令：
	
	```
	cf create-service ibmLogAnalysis lite my_logging_svc
	```
	{: codeblock}
	
4. 驗證已順利建立服務。執行下列指令：

	```	
	cf services
	```
	{: codeblock}
	
	執行指令的輸出如下所示：
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_logging_svc                ibmLogAnalysis               lite                                        create succeeded
	```
	{: screen}

	



