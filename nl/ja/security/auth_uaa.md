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


# UAA トークンの取得
{: #auth_uaa}

{{site.data.keyword.loganalysisshort}} API を使用してログを管理するには、認証トークンを使用する必要があります。 {{site.data.keyword.loganalysisshort}} CLI を使用して UAA トークンを取得します。 トークンには有効期限があります。 
{:shortdesc}

		
## Log Analysis CLI (CF プラグイン) を使用した UAA トークンの取得
{: #uaa_cli}


許可トークンを取得するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} CLI をインストールします。

   詳しくは、『[{{site.data.keyword.Bluemix}} CLI のダウンロードとインストール](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)』を参照してください。
   
   CLI がインストールされている場合は、次のステップに進みます。
    
2. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、『[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)』を参照してください。
	
3. `bx cf oauth-token` コマンドを実行して、{{site.data.keyword.Bluemix_notm}} UAA トークンを取得します。

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	この出力は、そのスペースおよび組織でユーザー ID を認証するために使用する必要がある UAA トークンを返します。
	

**注:** トークンを使用する場合、API 呼び出しで渡すトークンの値から *Bearer* を削除してください。
