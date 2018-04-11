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


# IBM Cloud CLI の使用に関するよくある質問と回答
{: #cli_qa}

{{site.data.keyword.loganalysisshort}} サービスでの {{site.data.keyword.Bluemix}} CLI の使用に関する一般的な質問の回答を以下に示します。 
{:shortdesc}

* [{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)
* [{{site.data.keyword.Bluemix_notm}} CLI のインストール方法を教えてください](/docs/services/CloudLogAnalysis/qa/cli_qa.html#install_bmx_cli)
* [アカウントの GUID の取得方法を教えてください](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid)
* [組織の GUID の取得方法を教えてください](/docs/services/CloudLogAnalysis/qa/cli_qa.html#org_guid)
* [スペースの GUID の取得方法を教えてください](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid)

## IBM Cloud にログインするにはどうすればよいですか
{: #login}

{{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインするには、次のコマンドを実行します。

```
bx login -a Endpoint
```
{: codeblock}
	
ここで、*Endpoint* は、{{site.data.keyword.Bluemix_notm}} にログインするための URL です。 この URL は地域ごとに異なります。
	
<table>
    <caption>{{site.data.keyword.Bluemix_notm}} にアクセスするためのエンドポイントのリスト</caption>
	<tr>
	  <th>地域</th>
	  <th>URL</th>
	</tr>
	<tr>
	  <td>ドイツ</td>
	  <td>api.eu-de.bluemix.net</td>
	</tr>
	<tr>
	  <td>シドニー</td>
	  <td>api.au-syd.bluemix.net</td>
	</tr>
	<tr>
	  <td>米国南部</td>
	  <td>api.ng.bluemix.net</td>
	</tr>
	<tr>
	  <td>英国</td>
	  <td>api.eu-gb.bluemix.net</td>
	</tr>
</table>

例えば、米国南部地域にログインするには、次のコマンドを実行します。
	
```
bx login -a https://api.ng.bluemix.net
```
{: codeblock}

手順に従います。 

次に、組織およびスペースを設定します。 次のコマンドを実行します。

```
bx target -o OrgName -s SpaceName
```
{: codeblock}

各部分の説明:

* OrgName は、組織の名前です。
* SpaceName は、スペースの名前です。

	
	
## IBM Cloud CLI のインストール方法を教えてください
{: #install_bmx_cli}

『[{{site.data.keyword.Bluemix}} CLI のダウンロードとインストール](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)』を参照してください。



## アカウントの GUID の取得方法を教えてください
{: #account_guid}
	
アカウントの GUID を取得するには、以下の手順を実行します。
	
1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、『[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)』を参照してください。
	
2. `bx iam accounts` コマンドを実行して、アカウントの GUID を取得します。

    ```
	bx iam accounts
	```
	{: codeblock} 
	
	例えば、ユーザー xxx@yyy.com のすべてのアカウントを、対応する GUID と共に取得するには、以下のコマンドを実行します。
	
	```
	bx iam accounts
	Retrieving all accounts of xxx@yyy.com...
    OK
    Account GUID                       Name                               Type    State    Owner User ID   
    12345123451234512345123451234512   A Account                          TRIAL   ACTIVE   xxx@yyy.com   
    23456234562345622456234561234561   B Account                          TRIAL   ACTIVE   zzz@yyy.com   
	```
	{: screen}

	
## 組織の GUID の取得方法を教えてください
{: #org_guid}

組織の GUID を取得するには、以下の手順を実行します。
	
1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login) を参照してください。

2. `bx iam org` コマンドを実行して、組織の GUID を取得します。 

    ```
    bx iam org NAME --guid
    ```
    {: codeblock}
	
    ここで、NAME は {{site.data.keyword.Bluemix_notm}} 組織の名前です。
		
		
		
## スペースの GUID の取得方法を教えてください
{: #space_guid}
	
スペースの GUID を取得するには、以下の手順を実行します。
	
1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login) を参照してください。
	
2. `bx iam space` コマンドを実行して、スペースの GUID を取得します。 

    ```
    bx iam space NAME --guid
    ```
    {: codeblock}
	
    ここで、NAME は、{{site.data.keyword.Bluemix_notm}} スペースの名前です。 
	
    例えば、スペース *dev* の GUID を取得するには、以下のコマンドを実行します。
	
    ```
    bx iam space dev --guid
    e03afff1-3456-4af6-1234-59treg1b0abc
    ```
    {: screen}




		
		