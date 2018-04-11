---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 로깅 토큰 가져오기
{: #logging_token}

로그를 {{site.data.keyword.loganalysisshort}} 서비스로 보내기 위한 로깅 토큰을 가져오십시오.
{:shortdesc}


## {{site.data.keyword.loganalysisshort}} CLI를 사용하여 로그를 영역으로 보내는 로깅 토큰 가져오기 
{: #logging_token_la_cloud_cli}

로그를 {{site.data.keyword.loganalysisshort}} 서비스로 보내는 데 사용할 수 있는 로깅 토큰을 가져오려면 다음 단계를 완료하십시오. 

1. {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오. 

   자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 다운로드 및 설치](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)를 참조하십시오. 
   
   CLI가 설치되면 다음 단계로 계속 진행하십시오. 
    
2. {{site.data.keyword.Bluemix_notm}}의 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)을 참조하십시오.
	
3. 다음 명령을 실행하십시오.

    ```
	bx logging token-get
	```
	{: codeblock}

이 출력은 로깅 토큰을 리턴합니다.


## {{site.data.keyword.Bluemix_notm}} CLI를 사용하여 로그를 영역으로 보내는 로깅 토큰 가져오기
{: #logging_token_cloud_cli}

로그를 {{site.data.keyword.loganalysisshort}} 서비스로 보내는 데 사용할 수 있는 로깅 토큰을 가져오려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오.

   자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 다운로드 및 설치](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)를 참조하십시오.

   CLI가 설치되면 다음 단계로 계속 진행하십시오.

2. {{site.data.keyword.Bluemix_notm}}의 지역, 조직 및 영역에 로그인하십시오.

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)을 참조하십시오.

3. {{site.data.keyword.loganalysisshort}} 서비스가 프로비저닝된 영역에서 서비스 키를 작성하십시오. 다음 명령을 실행하십시오.

    영역에 있는 {{site.data.keyword.loganalysisshort}} 인스턴스의 이름을 얻기 위해 서비스를 나열하십시오.
	
    ```
	bx service list
	```
	{: codeblock}
	
	예:
	
	```
	bx service list
    Invoking 'cf services'...

    Getting services in org lopezdsr_org / space dev as xxx@yyyy...
    OK

    name              service          plan       bound apps   last operation
    Log Analysis-vg   ibmLogAnalysis   standard                create succeeded
    ```
	{: screen}
	
	키를 작성하십시오. servicename의 **name** 값을 사용하여 키 이름을 입력하십시오.
	
	```
	bx service key-create servicename KeyName
	```
	{: codeblock}
	
	예:
	
	```
	bx service key-create "Log Analysis-vg" mykey2
    Invoking 'cf create-service-key Log Analysis-vg mykey2'...

    Creating service key mykey2 for service instance Log Analysis-vg as xxx@yyyy...
    OK
    ```
	{: screen}
	
4. 로킹 토큰을 가져오십시오. 다음 명령을 실행하십시오.
	
	```
	bx service key-show name Keyname
	```
	{: codeblock}
	
	예:  
	
	```
	bx service key-show "Log Analysis-vg" "mykey2" 
    Invoking 'cf service-key Log Analysis-vg mykey2'...

    Getting key mykey2 for service instance Log Analysis-vg as xxx@yyyy...

    {
     "LOG_INGESTION_MTLJ_URL": "https://ingest-eu-fra.logging.bluemix.net:9091",
     "logging_token": "sdtghyrtfde4",
     "space_id": "12345678-avfg-erft-b1f2-2efrtgcb1744"
    }
    ```
	{: screen}
	
	로깅 토큰을 가져오기 위해 다음 명령을 실행할 수 있습니다. 
	
	```
	bx service key-show "Log Analysis-vg" "mykey2" | tail -n +4 | jq -r .logging_token
    sdtghyrtfde4
	```
	{: screen}

## Log Analysis CLI(CF 플러그인)를 사용하여 로그를 영역으로 보내는 로깅 토큰 가져오기
{: #logging_token_cf_plugin}

로그를 {{site.data.keyword.loganalysisshort}} 서비스로 보내는 데 사용할 수 있는 로깅 토큰을 가져오려면 다음 단계를 완료하십시오. 

1. {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오. 

   자세한 정보는 [{{site.data.keyword.Bluemix}} CLI 다운로드 및 설치](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)를 참조하십시오.
   
   CLI가 설치되면 다음 단계로 계속 진행하십시오. 
    
2. {{site.data.keyword.Bluemix_notm}}의 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)을 참조하십시오.
	
3. 사용자가 인증 토큰을 얻은 영역의 GUID를 가져오십시오. 

   자세한 정보는 [영역의 GUID를 가져오는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid)을 참조하십시오.  
   
4. 로킹 토큰을 가져오십시오. 다음 명령을 실행하십시오.

    ```
    bx cf logging auth
    ```
    {: codeblock}

이 명령은 로그를 해당 ID로 보내는 데 필요한 *로깅 토큰* 및 *영역 ID*를 리턴합니다.	
	
## Log Analysis API를 사용하여 로그를 영역으로 보내는 로깅 토큰 가져오기
{: #logging_token_api}


로그를 {{site.data.keyword.loganalysisshort}} 서비스로 보내는 데 사용할 수 있는 로깅 토큰을 가져오려면 다음 단계를 완료하십시오. 

1. {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오. 

   자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 다운로드 및 설치](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)를 참조하십시오. 
   
   CLI가 설치되면 다음 단계로 계속 진행하십시오. 
    
2. {{site.data.keyword.Bluemix_notm}}의 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)을 참조하십시오.
	
3. [UAA 토큰](/docs/services/CloudLogAnalysis/security/auth_uaa.html#uaa_cli)을 가져오십시오.

    예를 들어 `bx cf oauth-token` 명령을 실행하여 UAA 토큰을 가져오십시오. 

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	이 출력은 해당 영역과 조직에서 사용자 ID를 인증하는 데 사용해야 하는 UAA 토큰을 리턴합니다.

4. 영역의 GUID을 가져오십시오.

   자세한 정보는 [영역 GUID를 가져오는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid)을 참조하십시오.
	
5. TOKEN 및 SPACEID 변수를 내보내십시오.

    * *TOKEN*은 이전 단계에서 가져온 bearer가 제외된 OAuth 토큰입니다.
	
	* *SPACEID*는 이전 단계에서 가져온 영역 GUID입니다.
		
	예:
	
	```
	export TOKEN="eyJhbGciOiJI....cGFzc3dvcmQiLCJjZiIsInVhYSIsIm9wZW5pZCJdfQ.JaoaVudG4jqjeXz6q3JQL_SJJfoIFvY8m-rGlxryWS8"
	export SPACEID="667fb895-abcd-defg-aaaa-cf4587341095"
	```
	{: screen}
	
6. 로깅 토큰을 가져오십시오. 다음 명령을 실행하십시오.

    ```
	curl -k -X GET  --header "X-Auth-Token: ${TOKEN}"  --header "X-Auth-Project-Id: s-${SPACEID}"  LOGGING_ENDPOINT/token
    ```
    {: codeblock}	
	
	여기서,
	* SPACEID는 서비스를 실행하는 영역의 GUID입니다.
	* TOKEN은 이전 단계에서 가져온 bearer 접두부가 없는 UAA 토큰입니다.
	* LOGGING_ENDPOINT는 조직과 영역을 사용할 수 있는 {{site.data.keyword.Bluemix_notm}} 지역의 {{site.data.keyword.loganalysisshort}} 엔드포인트입니다. LOGGING_ENDPOINT는 지역에 따라 다릅니다. 다른 엔드포인트의 URL을 보려면 [엔드포인트](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints)를 참조하십시오.
	
    이 명령은 로그를 해당 영역으로 보내는 데 사용해야 하는 로깅 토큰을 리턴합니다.
	
## Log Analysis API를 사용하여 로그를 계정 도메인으로 보내는 로깅 토큰 가져오기
{: #logging_acc_token_api}


로그를 {{site.data.keyword.loganalysisshort}} 서비스로 보내는 데 사용할 수 있는 로깅 토큰을 가져오려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오.

   자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 다운로드 및 설치](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)를 참조하십시오.

   CLI가 설치되면 다음 단계로 계속 진행하십시오.

2. {{site.data.keyword.Bluemix_notm}}의 지역, 조직 및 영역에 로그인하십시오.

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)을 참조하십시오.

3. [IAM 토큰](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli)을 가져오십시오.

    이 출력은 IAM 토큰을 리턴합니다.

4. 계정 GUID를 가져오십시오.

   자세한 정보는 [계정 GUID를 가져오는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid)을 참조하십시오.

5. TOKEN 및 AccountID 변수를 내보내십시오.

    * *TOKEN*은 이전 단계에서 가져온 bearer가 제외된 OAuth 토큰입니다.
	
	* *AccountID*는 이전 단게에서 가져온 계정 GUID입니다.
		
	예:
	
	```
	export TOKEN="eyJhbGciOiJI....cGFzc3dvcmQiLCJjZiIsInVhYSIsIm9wZW5pZCJdfQ.JaoaVudG4jqjeXz6q3JQL_SJJfoIFvY8m-rGlxryWS8"
	export AccountID="667fb8953456fg41095"
	```
	{: screen}
	
6. 로깅 토큰을 가져오십시오. 다음 명령을 실행하십시오.

    ```
	curl -k -X GET  --header "X-Auth-User-Token:iam ${TOKEN}"  --header "X-Auth-Project-Id: a-${AccountID}" -k  LOGGING_ENDPOINT/token
    ```
    {: codeblock}	
	
	여기서,
	* AccountID는 서비스를 실행하는 영역의 GUID입니다.
	* TOKEN은 이전 단계에서 가져온 bearer 접두부가 없는 IAM 토큰입니다.
	* LOGGING_ENDPOINT는 조직과 영역을 사용할 수 있는 {{site.data.keyword.Bluemix_notm}} 지역의 {{site.data.keyword.loganalysisshort}} 엔드포인트입니다. LOGGING_ENDPOINT는 지역에 따라 다릅니다. 다른 엔드포인트의 URL을 보려면 [엔드포인트](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints)를 참조하십시오.
	
    이 명령은 로그를 계정 도메인으로 보내는 데 사용해야 하는 로깅 토큰을 리턴합니다.
	
