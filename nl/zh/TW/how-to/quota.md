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


# 計算搜尋配額及每日用量
{: #quota}

若要取得 {{site.data.keyword.loganalysisshort}} 服務之日誌網域的配額及現行每日用量，您可以執行 cURL 指令。
{:shortdesc}


## 計算帳戶的搜尋配額及每日用量
{: #account}

請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)。

2. 取得帳戶的 ID。執行下列指令：

	```
	bx iam accounts
	```
    {: codeblock}	

	即會顯示帳戶及其 GUID 的清單。
	
	將帳戶 ID 匯出至 Shell 變數。例如：
	
	```
	export AccountID="1234567891234567812341234123412"
	```
	{: screen}

3. 取得 UAA 記號。 

    如需相關資訊，請參閱[取得 UAA 記號](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa)。

    將 UAA 記號匯出至 Shell 變數。請不要包括 `Bearer`。例如：
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. 取得網域的配額及現行用量。執行下列指令：

	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	其中，每個地區的 *ENDPOINT* 都不同。如需每個地區的端點清單，請參閱[記載端點](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints)。
	
	例如，執行 cURL 指令，以取得美國南部地區中帳戶的配額：
	
	```
curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	此結果會包括每日配額及用量的相關資訊。
	
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

	
## 計算空間的搜尋配額及每日用量
{: #space}

請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)。

2. 取得空間的 ID。

    如需相關資訊，請參閱[如何取得空間的 GUID](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid)。
	
	將空間 ID 匯出至 Shell 變數。例如：
	
	```
	export SpaceID="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

3. 取得 UAA 記號。 

    如需相關資訊，請參閱[取得 UAA 記號](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa)。

    將 UAA 記號匯出至 Shell 變數。請不要包括 `Bearer`。例如：
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. 取得網域的配額及現行用量。執行下列指令：

	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	其中，每個地區的 *ENDPOINT* 都不同。如需每個地區的端點清單，請參閱[記載端點](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints)。

    例如，執行下列 cURL 指令，以取得美國南部地區中空間網域的配額及用量：
	
	```
curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	此結果會包括每日配額及用量的相關資訊。
	
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



