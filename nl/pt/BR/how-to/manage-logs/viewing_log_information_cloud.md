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

# Visualizando informações de log
{: #viewing_log_status}

Use o comando [bx logging log-show](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#status) para obter informações sobre os logs que são coletados e armazenados em Coleção de logs. É possível obter informações sobre o tamanho, o número de registros, os tipos de log e se os logs estão disponíveis ou não para análise no Kibana.
{:shortdesc}

## Obtendo informações sobre logs em um período de tempo
{: #viewing_logs}

Use `bx logging log-show` com as opções **-s** para configurar o dia de início e **-e** para configurar a data de encerramento. Por exemplo:

* `bx logging log-show` fornece informações para as últimas 2 semanas.
* `bx logging log-show -s 2017-05-03` fornece informações de 3 de maio de 2017 até a data atual.
* `bx logging log-show -s 2017-05-03 -e 2017-05-08` fornece informações entre 3 de maio de 2017 e 8 de maio de 2017. 

Conclua as etapas a seguir para obter informações sobre os logs que são armazenados em um espaço:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Execute o comando a seguir:

    ```
    bx logging log-show
    ```
    {: codeblock}
    
    Por exemplo,
    
    ```
    $ bx logging log-show -s 2017-11-17 -e 2017-11-17
    Showing log status of resource: cedc73c5-1234-5678-abcd-378620d6fab5 ...

    Date         Size     Count   Searchable   Types   
    2017-11-17   794008   706     All          default   
    Logs of resource cedc73c5-1234-5678-abcd-378620d6fab5 is showed
    OK
    ```
    {: screen}


## Obtendo informações sobre um tipo de log em um período de tempo
{: #viewing_logs_by_log_type}

Para obter informações sobre um tipo de log durante um período de tempo, use o comando `bx logging log-show` com as opções **-t** para especificar o tipo de log, **-s** para configurar o dia de início e **-e** para configurar a data de encerramento. Por exemplo,

* `bx logging log-show -t syslog` fornece informações sobre logs do tipo *syslog* para as últimas 2 semanas.
* `bx logging log-show -s 2017-05-03 -t syslog` fornece informações sobre logs do tipo *syslog* de 3 de maio de 2017 até a data atual.
* `bx logging log-show -s 2017-05-03 -e 2017-05-08 -t syslog` fornece informações sobre logs do tipo *syslog* entre 3 de maio de 2017 e 8 de maio de 2017. 

Conclua as etapas a seguir para obter informações sobre um tipo de log durante um período de tempo:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Execute o comando a seguir:

    ```
    bx logging log-show -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    Em que
    
    * *-s* é usado para configurar a data de início em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-e* é usado para configurar a data de encerramento em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-t* é usado para configurar o tipo de log.
    
    É possível especificar múltiplos tipos de log separando cada tipo com uma vírgula, por exemplo, **log_type_1,log_type_2,log_type_3**. 
    
    Por exemplo,
    
    ```
    $ bx logging log-show -s 2017-05-24 -e 2017-05-25 -t syslog
    Showing log status of resource: cedc73c5-1234-5678-abcd-378620d6fab5 ...

    Date         Size     Count   Searchable   Types   
    2017-11-17   794008   706     All          syslog   
    Logs of resource cedc73c5-1234-5678-abcd-378620d6fab5 is showed
    OK
    ```
    {: screen}



## Obtendo informações sobre logs no nível de conta
{: #viewing_logs_account}

Para obter informações sobre logs que estão disponíveis no nível de conta durante um período de tempo, use o comando `bx logging log-show` com a opção **-r account** e **-i** para configurar o ID da conta. Também é possível especificar as opções **-t** para especificar o tipo de log, **-s** para configurar o dia de início e **-e** para configurar a data de encerramento. 

Conclua as etapas a seguir para obter dados da conta sobre logs:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Obtenha o ID da conta.

    Para obter mais informações, veja [Como obter o GUID de uma conta](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Execute o comando a seguir:

    ```
    bx logging log-show -r account -i AccountID -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    Em que
    
    * *-r account* é usado para configurar o domínio no qual você deseja obter informações sobre os logs.
    * *-i AccountID* é usado para configurar o ID da conta.
    * *-s* é usado para configurar a data de início em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-e* é usado para configurar a data de encerramento em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-t* é usado para configurar o tipo de log.
    

    É possível especificar múltiplos tipos de log separando cada tipo com uma vírgula, por exemplo, **log_type_1,log_type_2,log_type_3**. 
 
    Por exemplo, para mostrar informações sobre os logs que são armazenados para 17 de novembro de 2017 no domínio de contas para a conta *123456789123456789567c9c8de6dece*, execute o comando a seguir:
    
    ```
    $ bx logging log-show -r account -i 123456789123456789567c9c8de6dece -s 2017-05-24 -e 2017-05-25
	Showing log status of resource: 123456789123456789567c9c8de6dece ...

    Date         Size      Count   Searchable   Types   
	2017-11-17   794008    200     All          syslog  
    Logs of resource 123456789123456789567c9c8de6dece is showed
    OK
    ```
    {: screen}


## Obtendo informações sobre logs no nível de organização
{: #viewing_logs_account}

Para obter informações sobre logs que estão disponíveis no nível de organização durante um período de tempo, use o comando `bx logging log-show` com a opção **-r org** e **-i** para configurar o ID da organização. Também é possível especificar as opções **-t** para especificar o tipo de log, **-s** para configurar o dia de início e **-e** para configurar a data de encerramento. 

Conclua as etapas a seguir para obter dados da conta sobre logs:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Obtenha o ID da conta.

    Para obter mais informações, veja [Como obter o GUID de uma organização](/docs/services/CloudLogAnalysis/qa/cli_qa.html#org_guid).
    
3. Execute o comando a seguir:

    ```
    bx logging log-show -r org -i OrgID -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    Em que
    
    * *-r org* é usado para configurar o domínio no qual você deseja obter informações sobre os logs.
    * *-i OrgID* é usado para configurar o ID da organização.
    * *-s* é usado para configurar a data de início em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-e* é usado para configurar a data de encerramento em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-t* é usado para configurar o tipo de log.
    

    É possível especificar múltiplos tipos de log separando cada tipo com uma vírgula, por exemplo, **log_type_1,log_type_2,log_type_3**. 
 
    Por exemplo, para mostrar informações sobre os logs armazenados em 17 de novembro de 2017 no domínio de organização para a organização com o ID *abcd56789123456789567c9c8de6dece*, execute o comando a seguir:
    
    ```
    $ bx logging log-show -r org -i abcd56789123456789567c9c8de6dece -s 2017-05-24 -e 2017-05-25
	Showing log status of resource: abcd56789123456789567c9c8de6dece ...

    Date         Size      Count   Searchable   Types   
	2017-11-17   794008    200     All          syslog  
    Logs of resource abcd56789123456789567c9c8de6dece is showed
    OK
    ```
    {: screen}








