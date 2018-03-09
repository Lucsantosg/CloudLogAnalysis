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


# 検索割り当て量および日次使用量の計算
{: #quota}

{{site.data.keyword.loganalysisshort}} サービスのログ・ドメインの割り当て量および現在の日次使用量を取得するために、cURL コマンドを実行できます。 
{:shortdesc}


## アカウントの検索割り当て量および日次使用量の計算
{: #account}

以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} にログインします。 

    詳しくは、『[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)』を参照してください。

2. アカウントの ID を取得します。 次のコマンドを実行します。

    ```
	bx iam accounts
	```
    {: codeblock}	

	アカウントとその GUID のリストが表示されます。
	
	アカウント ID をシェル変数にエクスポートします。 以下に例を示します。
	
	```
	export AccountID="1234567891234567812341234123412"
	```
	{: screen}

3. UAA トークンを取得します。 

    詳しくは、[UAA トークンの取得](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa) を参照してください。

    UAA トークンをシェル変数にエクスポートします。 「Bearer」を含めないでください。 以下に例を示します。
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. ドメインの割り当て量と現在の使用量を取得します。 次のコマンドを実行します。

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	ここで、*ENDPOINT* は地域ごとに異なります。 地域ごとのエンドポイントのリストを取得については、[ロギング・エンドポイント](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints) を参照してください。
	
	例えば、米国南部地域のアカウントの割り当て量を取得するには、次の cURL コマンドを実行します。
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	結果には、日次の割り当て量および使用量についての情報が含まれます。
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

   {
      "usage": {
        "dailyallotment": 524288000,
        "current": 2115811531
       }
    }
    ```
    {: screen}

	
## スペースの検索割り当て量および日次使用量の計算
{: #space}

以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} にログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login) を参照してください。

2. スペースの ID を取得します。

    詳しくは、[スペースの GUID の取得方法を教えてください](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid) を参照してください。
	
	スペース ID をシェル変数にエクスポートします。 以下に例を示します。
	
	```
	export SpaceID="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

3. UAA トークンを取得します。 

    詳しくは、[UAA トークンの取得](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa) を参照してください。

    UAA トークンをシェル変数にエクスポートします。 「Bearer」を含めないでください。 以下に例を示します。
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. ドメインの割り当て量と現在の使用量を取得します。 次のコマンドを実行します。

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	ここで、*ENDPOINT* は地域ごとに異なります。 地域ごとのエンドポイントのリストを取得については、[ロギング・エンドポイント](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints) を参照してください。

    例えば、米国南部地域のスペース・ドメインの割り当て量および使用量を取得するには、以下の cURL コマンドを実行します。
	
    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	結果には、日次の割り当て量および使用量についての情報が含まれます。
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

   {
      "usage": {
        "dailyallotment": 524288000,
        "current": 2115811531
       }
    }
    ```
    {: screen}



