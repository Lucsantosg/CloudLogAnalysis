---

copyright:
  years: 2017, 2018

lastupdated: "2018-07-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 取得 UAA 記號
{: #auth_uaa}

若要使用 {{site.data.keyword.loganalysisshort}} API 來管理空間網域中的可用日誌，您必須使用鑑別記號。
{:shortdesc}

		
## 取得 UAA 記號
{: #uaa_cli}


若要取得授權記號，請完成下列步驟：

1. 安裝 {{site.data.keyword.Bluemix_notm}} CLI。

   如需相關資訊，請參閱[下載並安裝 {{site.data.keyword.Bluemix}} CLI](/docs/cli/index.html#overview)。
   
   如果已安裝 CLI，請繼續進行下一步。
    
2. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)。
	
3. 執行 `ibmcloud iam oauth-token` 指令來取得 {{site.data.keyword.Bluemix_notm}} UAA 記號。

    ```
	ibmcloud iam oauth-token
	```
	{: codeblock}
	
	此輸出會傳回必要的 UAA 記號，以用來在該空間及組織中鑑別使用者 ID。
	


	

**附註：**當您使用記號時，請從您傳入 API 呼叫的記號值中移除 *Bearer*。
