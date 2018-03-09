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

Use o comando [bx logging log-delete](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#delete) para excluir logs da Coleção de logs. 
{:shortdesc}

* É possível excluir logs dentro de um intervalo de tempo específico.
* É possível excluir logs por tipo. Observe que cada arquivo de log tem somente um tipo de entrada de log.
* É possível excluir logs para um espaço, para uma organização ou no domínio de contas.


## Excluindo todos os logs para um período de tempo específico
{: #time_range}

Conclua as etapas a seguir para excluir todos os logs que são armazenados em um domínio de espaço para um período de tempo específico:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Execute o comando a seguir para ver os logs que estão disponíveis na Coleção de logs.

    ```
    bx logging log-show
    ```
    {: codeblock}
    
    Por exemplo,
    
    ```
    $ bx logging log-show
    Showing log status of resource: 12345678-abcd-4193-aere-378620d6fab5 ...

    Date         Size       Count   Searchable          Types   
	2017-05-24   16         3020    None                default
	2017-05-25   1224       76115   All                 linux_syslog,log
    2017-05-26   19663113   17639   All                 default,linux_syslog  
    ```
    {: screen}
	
3. Exclua os logs que são armazenados em um dia específico.

    ```
	bx logging log-delete -s StartDate -e EndDate
	```
	{: codeblock}
	
	Em que
	
	* *-s* configura a data de início na Hora Universal Coordenada (UTC): AAAA-MM-DD, por exemplo, 2006-01-02.
    * *-e* configura a data de encerramento na Hora Universal Coordenada (UTC): AAAA-MM-DD
    	
	Por exemplo, para excluir os logs para 25 de maio de 2017, execute o comando a seguir:
	
	```
	bx logging log-delete -s 2017-05-25 -e 2017-05-25
	```
	{: screen}

	
## Excluindo logs por tipo de log para um período de tempo específico
{: #time_range}

Conclua as etapas a seguir para excluir os log por tipo de log que estão armazenados em um domínio de espaço para um período de tempo específico:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Execute o comando a seguir para ver os logs que estão disponíveis na Coleção de logs.

    ```
    bx logging log-show
    ```
    {: codeblock}
    
    Por exemplo,
    
    ```
    $ bx logging log-show
    Showing log status of resource: 12345678-1234-2edr-a9de-378620d6fab5 ...

    Tipos pesquisáveis de contagem de tamanho de data   
	2017-05-24   16         3020    None                default
	2017-05-25   1224       76115   All                 linux_syslog,log
    2017-05-26   19663113   17639   All                 default,linux_syslog  
    ```
    {: screen}
	
3. Exclua os logs que estão armazenados em um dia específico.

    ```
	bx logging log-delete -s StartDate -e EndDate -t LogType
	```
	{: codeblock}
	
	Em que
	
	* *-s* configura a data de início na Hora Universal Coordenada (UTC): AAAA-MM-DD, por exemplo, 2006-01-02.
    * *-e* configura a data de encerramento na Hora Universal Coordenada (UTC): AAAA-MM-DD
	* *-t* configura o tipo de log.
    	
	Por exemplo, para excluir os logs do tipo linux_syslog para 25 de maio de 2017, execute o comando a seguir:
	
	```
	bx logging log-delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
	```
	{: screen}

		
	
## Excluindo logs de contas por tipo de log para um período de tempo específico
{: #time_range}

Conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Obtenha o ID da conta.

    Para obter mais informações, veja [Como obter o GUID de uma conta](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Execute o comando a seguir para ver os logs que estão disponíveis na Coleção de logs no nível de conta.

    ```
    bx logging log-show  -r account -i AccountID
    ```
    {: codeblock}
    
    Por exemplo,
    
    ```
    $ bx logging log-show -r account -i 123456789123456789567c9c8de6dece -s 2017-05-24 -e 2017-05-25
	Showing log status of resource: 123456789123456789567c9c8de6dece ...

    Tipos pesquisáveis de contagem de tamanho de data   
	2017-05-24   16         3020    All                 default
	2017-05-25   2000       76115   All                 linux_syslog,log
    2017-05-26   195678     17639   All                 default,linux_syslog    
    Logs of resource 123456789123456789567c9c8de6dece is showed
    OK
    ```
    {: screen}
	
4. Exclua os logs que estão armazenados em um dia específico.

    ```
	bx logging log-delete -s StartDate -e EndDate -t LogType -r account -i AccountID
	```
	{: codeblock}
	
	Em que
	
	* *-s* configura a data de início na Hora Universal Coordenada (UTC): AAAA-MM-DD, por exemplo, 2006-01-02.
    * *-e* configura a data de encerramento na Hora Universal Coordenada (UTC): AAAA-MM-DD
	* *-t* configura o tipo de log.
    	
	Por exemplo, para excluir os logs do tipo linux_syslog para 25 de maio de 2017 que são armazenados em Coleção de logs no nível de conta, execute o comando a seguir:
	
	```
	bx logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog -r account -i 123456789123456789567c9c8de6dece
	```
	{: screen}
	












