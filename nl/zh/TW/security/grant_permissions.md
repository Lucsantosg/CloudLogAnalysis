---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---



{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 授與許可權
{: #grant_permissions}

在 {{site.data.keyword.Bluemix}} 中，您可以將一個以上的角色指派給使用者。這些角色定義針對該使用者啟用以使用 {{site.data.keyword.loganalysisshort}} 服務的作業。
{:shortdesc}



## 透過 {{site.data.keyword.Bluemix_notm}} 使用者介面將 IAM 原則指派給使用者
{: #grant_permissions_ui_account}

若要將檢視及管理帳戶日誌的許可權授與使用者，您必須新增該使用者的原則，以說明此使用者可在帳戶中使用 {{site.data.keyword.loganalysisshort}} 服務所執行的動作。只有帳戶擁有者才能將個別原則指派給使用者。

在 {{site.data.keyword.Bluemix_notm}} 中，完成下列步驟，以將使用 {{site.data.keyword.loganalysisshort}} 服務的許可權授與使用者：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。

    開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從功能表列中，按一下**管理 > 帳戶 > 使用者**。 

    *使用者* 視窗會顯示目前所選取帳戶的使用者及其電子郵件位址的清單。
	
3. 如果使用者是帳戶成員，請從清單中選取使用者名稱，或按一下*動作* 功能表中的**管理使用者**。

    如果使用者不是帳戶成員，請參閱[邀請使用者](/docs/iam/iamuserinv.html#iamuserinv)。

4. 在**存取原則**區段中，按一下**指派服務原則**，然後選取**指派資源的存取權**。

    即會開啟*將資源存取權指派給使用者* 視窗。

5. 輸入原則的相關資訊。下表列出可定義原則的必要欄位： 

    <table>
	  <caption>可配置 IAM 原則的欄位清單。</caption>
	  <tr>
	    <th>欄位</th>
		<th>值</th>
	  </tr>
	  <tr>
	    <td>服務</td>
		<td>*IBM Cloud Log Analysis*</td>
	  </tr>	  
	  <tr>
	    <td>地區</td>
		<td>您可以指定使用者將獲授與日誌使用存取權的地區。個別選取一個以上的地區，或選取**所有現行地區**以將存取權授與所有地區。</td>
	  </tr>
	  <tr>
	    <td>服務實例</td>
		<td>選取*所有服務實例*。</td>
	  </tr>
	  <tr>
	    <td>角色</td>
		<td>選取一個以上的 IAM 角色。<br>有效的角色為：*管理者*、*操作員*、*編輯者* 及*檢視者*。<br>如需每個角色所容許動作的相關資訊，請參閱 [IAM 角色](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles)。</td>
	  </tr>
     </table>
	
6. 按一下**指派原則**。
	
您配置的原則即適用於選取的地區。 

## 使用指令行將 IAM 原則指派給使用者
{: #grant_permissions_commandline}

若要將檢視及管理帳戶日誌的許可權授與使用者，您必須將 IAM 角色授與使用者。如需 IAM 角色以及透過角色啟用以使用 {{site.data.keyword.loganalysisshort}} 服務之作業的相關資訊，請參閱 [IAM 角色](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles)。

只有帳戶擁有者才能執行此作業。

請完成下列步驟，以使用指令行將檢視帳戶日誌存取權授與使用者：

1. 取得帳戶 ID。 

    執行下列指令，以取得帳戶 ID：

	```
	bx iam accounts
	```
    {: codeblock}	

	即會顯示帳戶及其 GUID 的清單。
	
	將計劃要將許可權授與使用者之帳戶的帳戶 ID 匯出至 Shell 變數（例如 `$acct_id`），例如：
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

2. 取得您要授與許可權之使用者的 {{site.data.keyword.Bluemix_notm}} ID。

    1. 顯示與帳戶相關聯的使用者。執行下列指令：
	
		```
		bx iam account-users
		```
		{: codeblock}
		
	2. 取得使用者的 GUID。**附註：**必須由您計劃要授與許可權的使用者完成此步驟。
	
	    例如，要求使用者執行下列指令來取得其使用者 ID：
		
		取得 IAM 記號。如需相關資訊，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 來取得 IAM 記號](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli)。

        從 IAM 記號中取得 IAM 記號前 2 個點之間的資料。將資料匯出至 Shell 變數（例如 `$user_data`）。 
		
	    ```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		例如，執行下列指令以取得使用者 ID。在此範例中，此指令使用 jq 將資訊解碼為 JSON 格式化文字：
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		此指令的執行輸出如下：
		
		```
		$ echo $user_data | base64 -d | jq
		{
		"iam_id": "IBMid-xxxxxxxxxx",
		"id": "IBMid-xxxxxxxxxx",
		"realmid": "IBMid",
		......
		}
		```
	    {: screen}
		
		將使用者 ID 傳送至帳戶擁有者。
		
	3. 將使用者 ID 匯出至 Shell 變數（例如 `$user_ibm_id`）。
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. 如果使用者還不是成員，請邀請使用者加入帳戶。如需相關資訊，請參閱[邀請使用者](/docs/iam/iamuserinv.html#iamuserinv)。

    例如，執行下列指令，以邀請使用者 xxx@yyy.com 加入帳戶 zzz@ggg.com：
	
	```
	bx iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. 建立原則檔案名稱。 

    例如，在美國南部地區中，使用下列範本來授與檢視許可權：
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-log-analysis",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	將原則檔案命名為：`policy.json`
	
5. 取得使用者 ID 的 IAM 記號。

    如需相關資訊，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 來取得 IAM 記號](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli)。

    將 IAM 記號匯出至 Shell 變數（例如 `$iam_token`），例如：
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. 將使用 {{site.data.keyword.loganalysisshort}} 服務的許可權授與使用者。 

   在美國南部地區中，執行下列 cURL 指令來授與許可權：
	
	```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	在英國地區中，執行下列 cURL 指令來授與許可權：
	
	```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	
在您將許可權授與使用者之後，使用者即可登入 {{site.data.keyword.Bluemix_notm}}，以及查看帳戶層次日誌。



## 使用 {{site.data.keyword.Bluemix_notm}} 使用者介面將檢視空間日誌許可權授與使用者
{: #grant_permissions_ui_space}

若要將檢視空間中日誌的許可權授與使用者，您必須將 Cloud Foundry 角色指派給使用者，以說明此使用者可在空間中使用 {{site.data.keyword.loganalysisshort}} 服務所執行的動作。 

請完成下列步驟，以將使用 {{site.data.keyword.loganalysisshort}} 服務的許可權授與使用者：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。

    開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從功能表列中，按一下**管理 > 帳戶 > 使用者**。 

    *使用者* 視窗會顯示目前所選取帳戶的使用者及其電子郵件位址的清單。
	
3. 如果使用者是帳戶成員，請從清單中選取使用者名稱，或按一下*動作* 功能表中的**管理使用者**。

    如果使用者不是帳戶成員，請參閱[邀請使用者](/docs/iam/iamuserinv.html#iamuserinv)。

4. 選取 **Cloud Foundry 存取**，然後選取組織。

    即會列出該組織中可用的空間清單。

5. 選擇一個空間。然後，從功能表動作中選取**編輯空間角色**。

6. 選取 1 個以上的空間角色。有效的角色為：*管理員*、*開發人員* 及*審核員*
	
7. 按一下**儲存角色**。




