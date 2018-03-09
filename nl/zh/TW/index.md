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

# 入門指導教學
{: #getting-started-with-cla}

使用此指導教學，瞭解如何在 {{site.data.keyword.Bluemix}} 中開始使用 {{site.data.keyword.loganalysislong}} 服務。
{:shortdesc}

## 目標
{: #objectives}

* 在空間中佈建 {{site.data.keyword.loganalysislong}} 服務。
* 設定指令行以管理日誌。
* 設定使用者檢視空間中日誌的許可權。
* 啟動 Kibana，其為您可用來檢視日誌的開放程式碼工具。


## 開始之前
{: #prereqs}

您的使用者 ID 必須是 {{site.data.keyword.Bluemix_notm}} 帳戶的成員或擁有者。若要取得 {{site.data.keyword.Bluemix_notm}} 使用者 ID，請移至：[登錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/registration/){:new_window}

此指導教學提供在美國南部地區中佈建及使用 {{site.data.keyword.loganalysisshort}} 服務的指示。


## 步驟 1：佈建 {{site.data.keyword.loganalysisshort}} 服務
{: #step1}

**附註：**您可以在 Cloud Foundry (CF) 空間中佈建 {{site.data.keyword.loganalysisshort}} 服務實例。一個空間只需要一個服務實例。您無法在帳戶層次佈建 {{site.data.keyword.loganalysisshort}} 服務。 

請完成下列步驟，以在 {{site.data.keyword.Bluemix_notm}} 中佈建 {{site.data.keyword.loganalysisshort}} 服務的實例：

1. 登入 {{site.data.keyword.Bluemix_notm}}：[http://bluemix.net ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}。  

2. 選取您要佈建 {{site.data.keyword.loganalysisshort}} 服務的地區、組織及空間。  

3. 按一下**型錄**。{{site.data.keyword.Bluemix_notm}} 上可用的服務清單隨即開啟。

4. 選取 **DevOps** 種類，以過濾所顯示的服務清單。

5. 按一下 **Log Analysis** 磚。

6. 選取服務方案。依預設，會設定**精簡**方案。

    如需服務方案的相關資訊，請參閱[服務方案](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)。
	
7. 按一下**建立**，以在所登入的 {{site.data.keyword.Bluemix_notm}} 空間中佈建 {{site.data.keyword.loganalysisshort}} 服務。




## 步驟 2：[選用] 變更 {{site.data.keyword.loganalysisshort}} 服務的服務方案。
{: #step2}

如果您需要更多的搜尋配額、長期儲存日誌或兩者，則可以透過 {{site.data.keyword.Bluemix_notm}} 使用者介面，或執行 `bx cf update-service` 指令以啟用這些特性，來變更 {{site.data.keyword.loganalysisshort}} 服務實例方案。 

您隨時可以升級或降低服務方案。

如需相關資訊，請參閱 [{{site.data.keyword.loganalysisshort}} 服務方案](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)。

**附註：**將方案變更為付款方案有其成本。

若要在 {{site.data.keyword.Bluemix_notm}} 使用者介面中變更服務方案，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}：[http://bluemix.net ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}。  

2. 選取可使用 {{site.data.keyword.loganalysisshort}} 服務的地區、組織及空間。  

3. 從 {{site.data.keyword.Bluemix_notm}} *儀表板* 中，按一下 {{site.data.keyword.loganalysisshort}} 服務實例。 
    
4. 在 {{site.data.keyword.loganalysisshort}} 儀表板中，選取**方案**標籤。

    即會顯示現行方案的相關資訊。
	
5. 選取新方案以升級或降低您的方案。 

6. 按一下**儲存**。



## 步驟 3：設定本端環境使用 {{site.data.keyword.loganalysisshort}} 服務
{: #step3}


{{site.data.keyword.loganalysisshort}} 服務包括指令行介面 (CLI)，可用來管理「日誌收集」（長期儲存元件）中所儲存的日誌。 

您可以使用 {{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}} 外掛程式來檢視日誌的狀態、下載日誌，以及配置日誌保留原則。 

CLI 提供不同類型的說明：瞭解 CLI 及所支援指令的一般說明、瞭解如何使用指令的指令說明，或瞭解如何使用指令之次指令的次指令說明。


若要從 {{site.data.keyword.Bluemix_notm}} 儲存庫中安裝 {{site.data.keyword.loganalysisshort}} CLI，請完成下列步驟：

1. 安裝 {{site.data.keyword.Bluemix_notm}} CLI。

   如需相關資訊，請參閱[安裝 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)。

2. 安裝 {{site.data.keyword.loganalysisshort}} 外掛程式。執行下列指令：

    ```
    bx plugin install logging-cli -r Bluemix
    ```
    {: codeblock}
 
3. 驗證已安裝 {{site.data.keyword.loganalysisshort}} 外掛程式。
  
    例如，執行下列指令，以查看已安裝的外掛程式清單：
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    輸出如下所示：
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}




## 步驟 4：設定使用者檢視日誌的許可權。
{: #step4}

若要控制容許使用者執行的 {{site.data.keyword.loganalysisshort}} 動作，您可以將角色及原則指派給使用者。 

{{site.data.keyword.Bluemix_notm}} 中有兩種類型的安全許可權可控制使用者在使用 {{site.data.keyword.loganalysisshort}} 服務時可執行的動作：

* Cloud Foundry (CF) 角色：您可以將 CF 角色授與使用者，而 CF 角色定義使用者必須要有才能檢視空間中日誌的許可權。
* IAM 角色：您可以將 IAM 原則授與使用者，而 IAM 原則定義使用者必須要有才能檢視帳戶網域中日誌的許可權，以及使用者必須要有才能管理「日誌收集」中所儲存日誌的許可權。 


請完成下列步驟，以將檢視空間中日誌的許可權授與使用者：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。

    開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://bluemix.net ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從功能表列中，按一下**管理 > 帳戶 > 使用者**。 

    *使用者* 視窗會顯示目前所選取帳戶的使用者及其電子郵件位址的清單。
	
3. 如果使用者是帳戶成員，請從清單中選取使用者名稱，或按一下*動作* 功能表中的**管理使用者**。

    如果使用者不是帳戶成員，請參閱[邀請使用者](/docs/iam/iamuserinv.html#iamuserinv)。

4. 選取 **Cloud Foundry 存取**，然後選取組織。

    即會列出該組織中可用的空間清單。

5. 選擇已佈建 {{site.data.keyword.loganalysisshort}} 服務的空間。然後，從功能表動作中選取**編輯空間角色**。

6. 選取*審核員*。 

    您可以選取 1 個以上的空間角色。所有下列角色都容許使用者檢視日誌：*管理員*、*開發人員* 及*審核員*
	
7. 按一下**儲存角色**。


如需相關資訊，請參閱[授與許可權](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account)。



## 步驟 5：啟動 Kibana
{: #step5}

若要檢視及分析日誌資料，您必須存取可使用日誌資料的「雲端公用」地區中的 Kibana。 


若要在美國南部地區中啟動 Kibana，請開啟 Web 瀏覽器，然後輸入下列 URL：

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}


如需如何在其他地區中啟動 Kibana 的相關資訊，請參閱[從 Web 瀏覽器導覽至 Kibana](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser)。

**附註：**當您啟動 Kibana 時，如果所收到的訊息指出*載送記號無效*，則請檢查您在空間中的許可權。此訊息指出您的使用者 ID 沒有查看日誌的許可權。
    

## 後續步驟 
{: #next_steps}

產生日誌。請嘗試下列任何指導教學：

* [針對 Kubernetes 叢集中所部署的應用程式，在 Kibana 中分析日誌](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs){:new_window} 

    此指導教學示範讓下列完整情境運作所需的步驟：佈建叢集、在 {{site.data.keyword.Bluemix_notm}} 中配置叢集以將日誌傳送至 {{site.data.keyword.loganalysisshort}} 服務、在叢集中部署應用程式，以及使用 Kibana 來檢視及過濾該叢集的容器日誌。     
    
* [在 Kibana 中分析 Cloud Foundry 應用程式的日誌](/docs/tutorials/application-log-analysis.html#generate-access-and-analyze-application-logs){:new_window}                                                                                                            

    此指導教學示範讓下列完整情境運作所需的步驟：部署 Python Cloud Foundry 應用程式、產生不同類型的日誌，以及使用 Kibana 來檢視、搜尋及分析 CF 日誌。
   








