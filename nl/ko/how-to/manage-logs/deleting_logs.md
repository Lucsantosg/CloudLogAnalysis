---

copyright:
  years: 2017, 2018

lastupdated: "2018-04-19"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 로그 삭제
{: #deleting_logs}

[bx cf logging delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status) 명령을 사용하여 로그 콜렉션에서 로그를 삭제합니다. 
{:shortdesc}

* 특정 시간 범위 내의 로그를 삭제할 수 있습니다.
* 유형별 로그를 삭제할 수 있습니다. 각 로그 파일에는 한 유형의 로그 항목만 있습니다.
* 영역 또는 계정 도메인에 대한 로그를 삭제할 수 있습니다.


## 특정 기간의 로그 삭제
{: #fix_period}

다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}}의 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)을 참조하십시오.
    
2. *status* 명령을 실행하여 로그 콜렉션에서 사용할 수 있는 로그를 확인하십시오.

    ```
    bx cf logging status
    ```
    {: codeblock}
    
    예:
    
    ```
    $ bx cf logging status
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. 특정일에 저장된 로그를 삭제하십시오.

    ```
	bx cf logging delete -s StartDate -e EndDate
	```
	{: codeblock}
	
	여기서,
	
	* *-s*는 시작 날짜를 협정 세계시(UTC): YYYY-MM-DD로 설정합니다. 예: 2006-01-02.
    * *-e*는 종료 날짜를 협정 세계시(UTC): YYYY-MM-DD로 설정합니다.
    	
	예를 들어 2017년 5월 25일의 로그를 삭제하려면 다음 명령을 실행하십시오.
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25
	```
	{: screen}

	
## 특정 기간 동안의 로그 유형별 로그 삭제
{: #log_type}

다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}}의 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)을 참조하십시오.
    
2. *status* 명령을 실행하여 로그 콜렉션에서 사용할 수 있는 로그를 확인하십시오.

    ```
    bx cf logging status
    ```
    {: codeblock}
    
    예:
    
    ```
    $ bx cf logging status
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   없음     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. 특정일에 저장된 로그를 삭제하십시오.

    ```
	bx cf logging delete -s StartDate -e EndDate -t LogType
	```
	{: codeblock}
	
	여기서,
	
	* *-s*는 시작 날짜를 협정 세계시(UTC): YYYY-MM-DD로 설정합니다. 예: 2006-01-02.
    * *-e*는 종료 날짜를 협정 세계시(UTC): YYYY-MM-DD로 설정합니다.
	* *-t*는 로그 유형을 설정합니다.
    	
	예를 들어 2017년 5월 25일에 생성된 linux_syslog 유형의 로그를 삭제하려면 다음 명령을 실행하십시오.
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
	```
	{: screen}

		
	
## 특정 기간 동안의 로그 유형별 계정 로그 삭제
{: #acc_log_type}

다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}}의 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)을 참조하십시오.
    
2. *status* 명령을 실행하여 로그 콜렉션에서 계정 레벨로 사용할 수 있는 로그를 확인하십시오.

    ```
    bx cf logging status  -a
    ```
    {: codeblock}
    
    예:
    
    ```
    $ bx cf logging status -a
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   없음     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. 특정일에 저장된 로그를 삭제하십시오.

    ```
	bx cf logging delete -s StartDate -e EndDate -t LogType -a
	```
	{: codeblock}
	
	여기서,
	
	* *-s*는 시작 날짜를 협정 세계시(UTC): YYYY-MM-DD로 설정합니다. 예: 2006-01-02.
    * *-e*는 종료 날짜를 협정 세계시(UTC): YYYY-MM-DD로 설정합니다.
	* *-t*는 로그 유형을 설정합니다.
    	
	예를 들어 2017년 5월 25일에 로그 콜렉션에서 계정 레벨로 저장된 linux_syslog 유형의 로그를 삭제하려면 다음 명령을 실행하십시오.
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog -a
	```
	{: screen}
	












