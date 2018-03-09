---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# ログの削除
{: #deleting_logs}

Log Collection からログを削除するには、[bx cf logging delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status) コマンドを使用します。 
{:shortdesc}

* 特定期間内のログを削除できます。
* タイプ別にログを削除できます。 各ログ・ファイルのログ項目のタイプは 1 つであることに注意してください。
* スペースのログを削除したり、アカウント・ドメインのログを削除したりできます。


## 特定の期間のログの削除
{: #time_range}

以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、『[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)』を参照してください。
    
2. *status* コマンドを実行して、Log Collection 内にあるログを表示します。

    ```
    bx cf logging status
    ```
    {: codeblock}
    
    以下に例を示します。
    
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
	
3. 特定の日に保管されたログを削除します。

    ```
	bx cf logging delete -s StartDate -e EndDate
	```
	{: codeblock}
	
	ここで、
	
	* *-s* は、開始日を協定世界時 (UTC) YYYY-MM-DD で設定します。例えば、2006-01-02 です。
    * *-e* は、終了日を協定世界時 (UTC) YYYY-MM-DD で設定します。
    	
	例えば、2017 年 5 月 25 日のログを削除するには、以下のコマンドを実行します。
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25
	```
	{: screen}

	
## 特定期間のログ・タイプ別のログの削除
{: #time_range}

以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login) を参照してください。
    
2. *status* コマンドを実行して、Log Collection 内にあるログを表示します。

    ```
    bx cf logging status
    ```
    {: codeblock}
    
    以下に例を示します。
    
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
	
3. 特定の日に保管されたログを削除します。

    ```
	bx cf logging delete -s StartDate -e EndDate -t LogType
	```
	{: codeblock}
	
	ここで、
	
	* *-s* は、開始日を協定世界時 (UTC) YYYY-MM-DD で設定します。例えば、2006-01-02 です。
    * *-e* は、終了日を協定世界時 (UTC) YYYY-MM-DD で設定します。
	* *-t* は、ログ・タイプを設定します。
    	
	例えば、2017 年 5 月 25 日のタイプ linux_syslog のログを削除するには、以下のコマンドを実行します。
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
	```
	{: screen}

		
	
## 特定期間のログ・タイプ別のアカウント・ログの削除
{: #time_range}

以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login) を参照してください。
    
2. *status* コマンドを実行して、アカウント・レベルで Log Collection 内にあるログを表示します。

    ```
    bx cf logging status  -a
    ```
    {: codeblock}
    
    以下に例を示します。
    
    ```
    $ bx cf logging status -a
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. 特定の日に保管されたログを削除します。

    ```
	bx cf logging delete -s StartDate -e EndDate -t LogType -a
	```
	{: codeblock}
	
	ここで、
	
	* *-s* は、開始日を協定世界時 (UTC) YYYY-MM-DD で設定します。例えば、2006-01-02 です。
    * *-e* は、終了日を協定世界時 (UTC) YYYY-MM-DD で設定します。
	* *-t* は、ログ・タイプを設定します。
    	
	例えば、アカウント・レベルで Log Collection に保管された、2017 年 5 月 25 日のタイプ linux_syslog のログを削除するには、以下のコマンドを実行します。
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog -a
	```
	{: screen}
	












