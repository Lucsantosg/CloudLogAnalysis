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


# プランの変更
{: #change_plan}

{{site.data.keyword.loganalysisshort}} サービス・プランは、{{site.data.keyword.Bluemix_notm}} のサービス・ダッシュボードで変更することも、`cf update-service` コマンドを実行して変更することもできます。プランはいつでもアップグレードまたは削減することができます。
{:shortdesc}

## UI を使用したサービス・プランの変更
{: #change_plan_ui}

{{site.data.keyword.Bluemix_notm}} のサービス・ダッシュボードでサービス・プランを変更するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} にログインし、{{site.data.keyword.Bluemix_notm}} ダッシュボードから {{site.data.keyword.loganalysisshort}} サービスをクリックします。 
    
2. {{site.data.keyword.Bluemix_notm}} UI で**「プラン」**タブを選択します。

    現在のプランに関する情報が表示されます。
	
3. プランをアップグレードまたは削減するため、新しいプランを選択します。 

4. **「保存」**をクリックします。



## CLI を使用したサービス・プランの変更
{: #change_plan_cli}

Bluemix で CLI を介してサービス・プランを変更するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} 地域、組織、およびスペースにログインします。 

    例えば、米国南部地域にログインするには、以下のコマンドを実行します。
	
	```
cf login -a https://api.ng.bluemix.net
```
    {: codeblock}
	
2. `cf services` コマンドを実行して、現在のプランを確認し、スペースで使用可能なサービスのリストから {{site.data.keyword.loganalysisshort}} サービス名を取得します。 

    プランを変更する際、**name** フィールドの値を使用する必要があります。 

    以下に例を示します。
	
	```
	$ cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK
    
    name              service          plan      bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   premium                create succeeded
    ```
	{: screen}
    
3. プランをアップグレードまたは削減します。`cf update-service` コマンドを実行します。
    
	```
	cf update-service service_name [-p new_plan]
	```
	{: codeblock}
	
	各部分の説明: 
	
	* *service_name* は、サービスの名前です。`cf services` コマンドを実行して値を取得できます。
	* *new_plan* は、プランの名前です。
	
	次の表に、各種プランおよびサポートされている値を示します。
	
	<table>
	  <caption>表 1. プランのリスト</caption>
	  <tr>
	    <th>プラン</th>
	    <th>名前</th>
	  </tr>
	  <tr>
	    <td>ライト</td>
	    <td>lite</td>
	  </tr>
	  <tr>
	    <td>ログ収集</td>
	    <td>premium</td>
	  </tr>
	  <tr>
	    <td>ログ収集と 2 GB/日の検索</td>
	    <td>premiumsearch2</td>
	  </tr>
	  <tr>
	    <td>ログ収集と 5 GB/日の検索</td>
	    <td>premiumsearch5</td>
	  </tr>
	  <tr>
	    <td>ログ収集と 10 GB/日の検索</td>
	    <td>premiumsearch10</td>
	  </tr>
	</table>
	
	例えば、プランを削減して*ライト*・プランにするには、以下のコマンドを実行します。
	
	```
	cf update-service "Log Analysis-a4" -p lite
    Updating service instance Log Analysis-a4 as xxx@yyy.com...
    OK
	```
	{: screen}

4. 新規プランに変更されたことを検証します。`cf services` コマンドを実行します。

    ```
	cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service          plan   bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   lite                update succeeded
	```
	{: screen}






