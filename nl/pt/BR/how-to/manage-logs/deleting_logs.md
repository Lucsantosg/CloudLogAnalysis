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

# Excluindo logs
{: #deleting_logs}

Use o comando [bx cf logging delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status) para excluir logs da Coleção de logs. 
{:shortdesc}

* É possível excluir logs dentro de um intervalo de tempo específico.
* É possível excluir logs por tipo. Observe que cada arquivo de log tem somente um tipo de entrada de log.
* É possível excluir logs para um espaço ou no domínio de contas.


## Excluindo logs para um período de tempo específico
{: #time_range}

Conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Execute o comando *status* para ver os logs que estão disponíveis em Coleção de logs.

    ```
    bx cf logging status
    ```
    {: codeblock}
    
    Por exemplo,
    
    ```
    $ bx cf logging status +------------+--------+-------+--------------------+------------+ | DATE | COUNT | SIZE | TYPES | SEARCHABLE | +------------+--------+-------+--------------------+------------+ | 2017-05-24 | 16 | 3020 | log | None | +------------+--------+-------+--------------------+------------+ | 2017-05-25 | 1224 | 76115 | linux_syslog,log | All | +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. Exclua os logs que são armazenados em um dia específico.

    ```
	bx cf logging delete -s StartDate -e EndDate
	```
	{: codeblock}
	
	Em que
	
	* *-s* configura a data de início na Hora Universal Coordenada (UTC): AAAA-MM-DD, por exemplo, 2006-01-02.
    * *-e* configura a data de encerramento na Hora Universal Coordenada (UTC): AAAA-MM-DD
    	
	Por exemplo, para excluir os logs para 25 de maio de 2017, execute o comando a seguir:
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25
	```
	{: screen}

	
## Excluindo logs por tipo de log para um período de tempo específico
{: #time_range}

Conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Execute o comando *status* para ver os logs que estão disponíveis em Coleção de logs.

    ```
    bx cf logging status
    ```
    {: codeblock}
    
    Por exemplo,
    
    ```
    $ bx cf logging status
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   Nenhuma     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    Todos     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. Exclua os logs que são armazenados em um dia específico.

    ```
	bx cf logging delete -s StartDate -e EndDate -t LogType
	```
	{: codeblock}
	
	Em que
	
	* *-s* configura a data de início na Hora Universal Coordenada (UTC): AAAA-MM-DD, por exemplo, 2006-01-02.
    * *-e* configura a data de encerramento na Hora Universal Coordenada (UTC): AAAA-MM-DD
 * *-t* configura o tipo de log.
    	
	Por exemplo, para excluir os logs do tipo linux_syslog para 25 de maio de 2017, execute o comando a seguir:
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
	```
	{: screen}

		
	
## Excluindo logs de contas por tipo de log para um período de tempo específico
{: #time_range}

Conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Execute o comando *status* para ver os logs que estão disponíveis em Coleção de logs no nível de conta.

    ```
    bx cf logging status  -a
    ```
    {: codeblock}
    
    Por exemplo,
    
    ```
    $ bx cf logging status -a
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   Nenhuma     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    Todos     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}
	
3. Exclua os logs que são armazenados em um dia específico.

    ```
	bx cf logging delete -s StartDate -e EndDate -t LogType -a
	```
	{: codeblock}
	
	Em que
	
	* *-s* configura a data de início na Hora Universal Coordenada (UTC): AAAA-MM-DD, por exemplo, 2006-01-02.
    * *-e* configura a data de encerramento na Hora Universal Coordenada (UTC): AAAA-MM-DD
 * *-t* configura o tipo de log.
    	
	Por exemplo, para excluir os logs do tipo linux_syslog para 25 de maio de 2017 que são armazenados em Coleção de logs no nível de conta, execute o comando a seguir:
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog -a
	```
	{: screen}
	












