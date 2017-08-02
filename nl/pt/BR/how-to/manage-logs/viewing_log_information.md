---

copyright:
  years: 2017
lastupdated: "2017-07-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualizando informações de log
{: #viewing_log_status}

Use o comando [cf logging status](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status) para obter informações sobre os logs coletados e armazenados na Coleção de logs.
{:shortdesc}

## Obtendo informações sobre logs em um período de tempo
{: #viewing_logs}

Use o comando `cf logging status` para ver o tamanho, a contagem, os tipos de log e se os logs estão disponíveis ou não para análise no Kibana para logs armazenados na Coleção de logs. 

Use o comando `cf logging status` com as opções **-s** para configurar o dia de início e **-e** para configurar a data de encerramento. Por exemplo:

* `cf logging status` fornece informações das duas últimas semanas.
* `cf logging status -s 2017-05-03` fornece informações de 3 de maio de 2017 até a data atual.
* `cf logging status -s 2017-05-03 -e 2017-05-08` fornece informações entre 3 de maio de 2017 e 8 de maio de 2017. 

1. Efetue login em uma região, uma organização e um espaço do {{site.data.keyword.Bluemix_notm}}. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Execute o comando *status*.

    ```
    $ cf logging status
    ```
    {: codeblock}
    
    Por
exemplo,
    
    ```
    $ cf logging status
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}


## Obtendo informações sobre um tipo de log em um período de tempo
{: #viewing_logs_by_log_type}

Para obter informações sobre um tipo de log em um período de tempo, use o comando `cf logging status` com as opções **-t** para especificar o tipo de log, **-s** para configurar o dia de início e **-e** para configurar a data de encerramento. Por
exemplo,

* `cf logging status -t syslog` fornece informações sobre logs do tipo *syslog* para as duas últimas semanas.
* `cf logging status -s 2017-05-03 -t syslog` fornece informações sobre logs do tipo *syslog* de 3 de maio de 2017 até a data atual.
* `cf logging status -s 2017-05-03 -e 2017-05-08 -t syslog` fornece informações sobre logs do tipo *syslog* entre 3 de maio de 2017 e 8 de maio de 2017. 

1. Efetue login em uma região, uma organização e um espaço do {{site.data.keyword.Bluemix_notm}}. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Execute o comando *status*.

    ```
    $ cf logging status -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    em que
    
    * *-s* é usado para configurar a data de início em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-e* é usado para configurar a data de encerramento em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-t* é usado para configurar o tipo de log.
    
    É possível especificar múltiplos tipos de log separando cada tipo com uma vírgula, por exemplo, **log_type_1,log_type_2,log_type_3**. 
    
    Por
exemplo,
    
    ```
    $ cf logging status -s 2017-05-24 -e 2017-05-25 -t log
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 |        log         |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}



## Obtendo informações sobre logs de conta
{: #viewing_logs_account}

Para obter informações sobre logs em um período de tempo na conta do {{site.data.keyword.Bluemix_notm}}, use o comando `cf logging status` com a opção **-a**. Também é possível especificar as opções **-t** para especificar o tipo de log, **-s** para configurar o dia de início e **-e** para configurar a data de encerramento. 

1. Efetue login em uma região, uma organização e um espaço do {{site.data.keyword.Bluemix_notm}}. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Execute o comando *status*.

    ```
    $ cf logging status -a -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    em que
    
    * *-a* é usado para especificar informações de nível de conta
    * *-s* é usado para configurar a data de início em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-e* é usado para configurar a data de encerramento em Universal Coordinated Time (UTC): *AAAA-MM-DD*
    * *-t* é usado para configurar o tipo de log.
    

    É possível especificar múltiplos tipos de log separando cada tipo com uma vírgula, por exemplo, **log_type_1,log_type_2,log_type_3**. 
 
    Por
exemplo,
    
    ```
    $ cf logging status -s 2017-05-24 -e 2017-05-25 -t log -a
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 |        log         |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}














