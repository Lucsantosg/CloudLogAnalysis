---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 啟用自動收集叢集日誌
{: #containers_kube_other_logs}

若要能夠在 {{site.data.keyword.loganalysisshort}} 服務中檢視及分析叢集日誌，您必須配置叢集，以將這些日誌轉遞至 {{site.data.keyword.loganalysisshort}} 服務。
{:shortdesc}

## 步驟 1：檢查許可權
{: step1}

只有使用者具有含叢集管理許可權之 {{site.data.keyword.containershort}} 的 IAM 原則時，才能啟用此特性。需要下列任何角色：*管理者*、*操作員*

若要檢查使用者 ID 已指派可管理叢集的 IAM 原則，請完成下列步驟：

**附註：**只有帳戶擁有者或具有原則指派許可權的使用者才能執行此步驟。

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從功能表列中，按一下**管理 > 帳戶 > 使用者**。*使用者* 視窗會顯示目前所選取帳戶的使用者及其電子郵件位址的清單。
	
3. 選取使用者 ID，並驗證使用者 ID 的原則具有 {{site.data.keyword.containershort}} 的*檢視者* 許可權。




## 步驟 2：設定叢集環境定義。
{: #step2}

請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)。
    
2. 起始設定 {{site.data.keyword.loganalysisshort}} 服務外掛程式。

	```
	bx cs init
	```
	{: codeblock}

3. 將終端機環境定義設為叢集。
    
	```
	bx cs cluster-config ClusterName
	```
	{: codeblock}

    此指令的執行輸出所提供的指令，就是您必須在終端機中執行以設定配置檔路徑的指令。例如，針對名為 *MyCluster* 的叢集：

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

4. 複製並貼上指令以在終端機中設定環境變數，然後按 **Enter** 鍵。



## 步驟 3：配置叢集
{: step3}

您可以選擇要轉遞至 {{site.data.keyword.loganalysisshort}} 服務的叢集日誌。 

* 若要啟用 stdout 及 stderr 的自動日誌收集及轉遞，請參閱[啟用容器日誌的自動日誌收集及轉遞](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#containers)。
* 若要啟用應用程式日誌的自動日誌收集及轉遞，請參閱[啟用應用程式日誌的自動日誌收集及轉遞](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#apps)。
* 若要啟用工作者日誌的自動日誌收集及轉遞，請參閱[啟用工作者日誌的自動日誌收集及轉遞](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#workers)。
* 若要啟用 Kubernetes 系統元件日誌的自動日誌收集及轉遞，請參閱[啟用 Kubernetes 系統元件日誌的自動日誌收集及轉遞](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#system)。
* 若要啟用 Kubernetes Ingress 控制器日誌的自動日誌收集及轉遞，請參閱[啟用 Kubernetes Ingress 控制器日誌的自動日誌收集及轉遞](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#controller)。



## 步驟 4：設定 {{site.data.keyword.containershort_notm}} 金鑰擁有者的許可權
{: #step4}

當您將日誌轉遞至空間時，也必須將 Cloud Foundry (CF) 許可權授與組織及空間中的 {{site.data.keyword.containershort}} 金鑰擁有者。金鑰擁有者需要組織的 *orgManager* 角色，以及空間的 *SpaceManager* 及 *Developer*。

請完成下列步驟：

1. 識別帳戶中為 {{site.data.keyword.containershort}} 金鑰擁有者的使用者。從終端機中，執行下列指令：

    ```
    bx cs api-key-info ClusterName
    ```
    {: codeblock}
    
    其中 *ClusterName* 是叢集的名稱。
    
2. 驗證識別為 {{site.data.keyword.containershort}} 金鑰擁有者的使用者具有組織的 *orgManager* 角色，以及空間的 *SpaceManager* 及 *Developer*。

    登入 {{site.data.keyword.Bluemix_notm}} 主控台。開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}。使用您的使用者 ID 及密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

    從功能表列中，按一下**管理 > 帳戶 > 使用者**。*使用者* 視窗會顯示目前所選取帳戶的使用者及其電子郵件位址的清單。
	
    選取使用者的 ID，並驗證使用者具有組織的 *orgManager* 角色，以及空間的 *SpaceManager* 及 *Developer*。
 
3. 如果使用者沒有正確的許可權，請完成下列步驟：

    1. 將下列許可權授與使用者：組織的 *orgManager* 角色，以及空間的 *SpaceManager* 及 *Developer*。如需相關資訊，請參閱[使用 IBM Cloud 使用者介面將檢視空間日誌許可權授與使用者](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_space)。
    
    2. 重新整理記載配置。執行下列指令：
    
        ```
        bx cs logging-config-refresh ClusterName
        ```
        {: codeblock}
        
        其中 *ClusterName* 是叢集的名稱。
  




## 啟用容器日誌的自動日誌收集及轉遞 
{: #containers}

執行下列指令，以將 *stdout* 及 *stderr* 日誌檔傳送至 {{site.data.keyword.loganalysisshort}} 服務：

```
bx cs logging-config-create ClusterName --logsource container --namespace '*' --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

其中 

* *ClusterName* 是叢集的名稱。
* *EndPoint* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在地區中的記載服務 URL。如需端點清單，請參閱[端點](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)。
* *OrgName* 是可使用空間的組織名稱。
* *SpaceName* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在空間的名稱。


例如，若要建立記載配置以將 stdout 及 stderr 日誌轉遞至德國地區的帳戶網域，請執行下列指令：

```
bx cs logging-config-create MyCluster --logsource container --type ibm --namespace '*' --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}

若要建立記載配置以將 stdout 及 stderr 日誌轉遞至德國地區的空間網域，請執行下列指令：

```
bx cs logging-config-create MyCluster --logsource container --type ibm --namespace '*' --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org MyOrg --space MySpace
```
{: screen}



## 啟用應用程式日誌的自動日誌收集及轉遞 
{: #apps}

執行下列指令，以將 */var/log/apps/**/.log* 及 */var/log/apps/*/.err* 日誌檔傳送至 {{site.data.keyword.loganalysisshort}} 服務：

```
bx cs logging-config-create ClusterName --logsource application --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

其中 

* *ClusterName* 是叢集的名稱。
* *EndPoint* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在地區中的記載服務 URL。如需端點清單，請參閱[端點](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)。
* *OrgName* 是可使用空間的組織名稱。
* *SpaceName* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在空間的名稱。


例如，若要建立記載配置以將應用程式日誌轉遞至德國地區的空間網域，請執行下列指令：

```
bx cs logging-config-create MyCluster --logsource application --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org MyOrg --space MySpace
```
{: screen}

例如，若要建立記載配置以將應用程式日誌轉遞至德國地區的帳戶網域，請執行下列指令：

```
bx cs logging-config-create MyCluster --logsource application --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}



## 啟用工作者日誌的自動日誌收集及轉遞 
{: #workers}


執行下列指令，以將 */var/log/syslog* 及 */var/log/auth.log* 日誌檔傳送至 {{site.data.keyword.loganalysisshort}} 服務：

```
bx cs logging-config-create ClusterName --logsource worker --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

其中 

* *ClusterName* 是叢集的名稱。
* *EndPoint* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在地區中的記載服務 URL。如需端點清單，請參閱[端點](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)。
* *OrgName* 是可使用空間的組織名稱。
* *SpaceName* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在空間的名稱。



例如，若要建立記載配置以將工作者日誌轉遞至德國地區的空間網域，請執行下列指令：

```
bx cs logging-config-create MyCluster --logsource worker  --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org OrgName --space SpaceName 
```
{: screen}

例如，若要建立記載配置以將工作者日誌轉遞至德國地區的帳戶網域，請執行下列指令：

```
bx cs logging-config-create MyCluster --logsource worker  --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}



## 啟用 Kubernetes 系統元件日誌的自動日誌收集及轉遞
{: #system}

執行下列指令，以將 */var/log/kubelet.log* 及 */var/log/kube-proxy.log* 日誌檔傳送至 {{site.data.keyword.loganalysisshort}} 服務：

```
bx cs logging-config-create ClusterName --logsource kubernetes --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

其中 

* *ClusterName* 是叢集的名稱。
* *EndPoint* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在地區中的記載服務 URL。如需端點清單，請參閱[端點](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)。
* *OrgName* 是可使用空間的組織名稱。
* *SpaceName* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在空間的名稱。



例如，若要建立記載配置以將 Kubernetes 系統元件日誌轉遞至德國地區的空間網域，請執行下列指令：

```
bx cs logging-config-create MyCluster --logsource kubernetes --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org OrgName --space SpaceName 
```
{: screen}

例如，若要建立記載配置以將 Kubernetes 系統元件日誌轉遞至德國地區的帳戶網域，請執行下列指令：

```
bx cs logging-config-create MyCluster --logsource kubernetes --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}



## 啟用 Kubernetes Ingress 控制器日誌的自動日誌收集及轉遞
{: #controller}

執行下列指令，以將 */var/log/alb/ids/.log*、*/var/log/alb/ids/.err*、*/var/log/alb/customerlogs/.log* 及 /var/log/alb/customerlogs/.err* 日誌檔傳送至 {{site.data.keyword.loganalysisshort}} 服務：

```
bx cs logging-config-create ClusterName --logsource ingress --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName s
```
{: codeblock}

其中 

* *ClusterName* 是叢集的名稱。
* *EndPoint* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在地區中的記載服務 URL。如需端點清單，請參閱[端點](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)。
* *OrgName* 是可使用空間的組織名稱。
* *SpaceName* 是 {{site.data.keyword.loganalysisshort}} 服務佈建所在空間的名稱。



例如，若要建立記載配置以將 Ingress 控制器日誌轉遞至德國地區的空間網域，請執行下列指令：

```
bx cs logging-config-create MyLoggingDemoCluster --logsource ingress --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org OrgName --space SpaceName 
```
{: screen}

例如，若要建立記載配置以將 Ingress 控制器日誌轉遞至德國地區的帳戶網域，請執行下列指令：

```
bx cs logging-config-create MyLoggingDemoCluster --logsource ingress --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091  
```
{: screen}



