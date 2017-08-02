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


# Log Analysis サービスのプロビジョン
{: #provision}

{{site.data.keyword.loganalysisshort}} サービスは、{{site.data.keyword.Bluemix}} UI かコマンド・ラインからプロビジョンできます。
{:shortdesc}


## UI からのプロビジョン
{: #ui}

{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.loganalysisshort}} サービスのインスタンスをプロビジョンするには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} アカウントにログインします。

    {{site.data.keyword.Bluemix_notm}} ダッシュボードは、[http://bluemix.net ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net "外部リンク・アイコン"){:new_window} にあります。
    
	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. **「カタログ」**をクリックします。{{site.data.keyword.Bluemix_notm}} で使用可能なサービスのリストが開きます。

3. **「DevOps」**カテゴリーを選択して、表示されたサービスのリストをフィルタリングします。

4. **「Log Analysis」**タイルをクリックします。

5. サービス・プランを選択します。デフォルトでは、**「ライト」**プランが設定されています。

    サービス・プランについて詳しくは、『[サービス・プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)』を参照してください。
	
6. **「作成」**をクリックして、ログインしている {{site.data.keyword.Bluemix_notm}} スペースで {{site.data.keyword.loganalysisshort}} サービスをプロビジョンします。
  
 

## CLI からのプロビジョン
{: #cli}

{{site.data.keyword.Bluemix_notm}} でコマンド・ラインを使用して {{site.data.keyword.loganalysisshort}} サービスのインスタンスをプロビジョンするには、以下のステップを実行します。

1. Cloud Foundry (CF) CLI をインストールします。CF CLI がインストールされている場合は、次のステップに進みます。

   詳しくは、『[Installing the cf CLI ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "外部リンク・アイコン"){: new_window}』を参照してください。 
    
2. {{site.data.keyword.Bluemix_notm}} 地域、組織、およびスペースにログインします。 

    例えば、米国南部地域にログインするには、以下のコマンドを実行します。

    ```
cf login -a https://api.ng.bluemix.net
```
    {: codeblock}

    手順に従います。{{site.data.keyword.Bluemix_notm}} の資格情報を入力し、組織とスペースを選択します。
	
3. `cf create-service` コマンドを実行して、インスタンスをプロビジョンします。

    ```
	cf create-service service_name service_plan service_instance_name
	```
	{: codeblock}

    各部分の説明:
	
	* service_name はサービスの名前 (「ibmLogAnalysis」) です。
	* service_plan はサービス・プラン名です。プランのリストについては、[サービス・プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans) を参照してください。
	* service_instance_name は、作成する新規サービス・インスタンスに使用する名前です。
	cf コマンドについて詳しくは、[cf create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service) を参照してください。

	例えば、無料プランで {{site.data.keyword.loganalysisshort}} サービスのインスタンスを作成するには、以下のコマンドを実行します。
	
	```
	cf create-service ibmLogAnalysis lite my_logging_svc
	```
	{: codeblock}

    4. サービスが正常に作成されたことを確認します。次のコマンドを実行します。

    ```	
	cf services
	```
	{: codeblock}

    このコマンドの実行による出力は以下のようになります。
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_logging_svc                ibmLogAnalysis               lite                                        create succeeded
	```
	    {: screen}
	
    



