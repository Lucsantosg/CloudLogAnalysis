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

# Supresión de registros
{: #deleting_logs}

Utilice el mandato [bx logging log-delete](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#delete) para suprimir los registros de la recopilación de registros. 
{:shortdesc}

* Puede suprimir los registros comprendidos en un determinado intervalo de tiempo.
* Puede suprimir registros por tipo. Tenga en cuenta que cada archivo de registro solo tiene un tipo de entradas de registro.
* Puede suprimir registros correspondientes a un espacio, a una organización o a un dominio de la cuenta.


## Supresión de todos los registros correspondientes a un determinado periodo de tiempo
{: #time_range}

Siga estos pasos para suprimir todos los registros almacenados en un dominio del espacio correspondientes a un determinado periodo de tiempo:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Ejecute el siguiente mandato para ver los registros disponibles en la recopilación de registros.

    ```
    bx logging log-show
    ```
    {: codeblock}
    
    Por ejemplo,
    
    ```
    $ bx logging log-show
    Showing log status of resource: 12345678-abcd-4193-aere-378620d6fab5 ...

    Date         Size       Count   Searchable          Types
	2017-05-24   16         3020    None                default
	2017-05-25   1224       76115   All                 linux_syslog,log
    2017-05-26   19663113   17639   All                 default,linux_syslog  
    ```
    {: screen}
	
3. Suprima los registros almacenados en un día específico.

    ```
	bx logging log-delete -s StartDate -e EndDate
	```
	{: codeblock}
	
	donde
	
	* *-s* define la fecha inicial en hora universal coordinada (UTC): AAAA-MM-DD, por ejemplo 2006-01-02.
    * *-e* define la fecha final en hora universal coordinada (UTC): AAAA-MM-DD
    	
	Por ejemplo, para suprimir los registros correspondientes al 25 de mayo de 2017, ejecute el mandato siguiente:
	
	```
	bx logging log-delete -s 2017-05-25 -e 2017-05-25
	```
	{: screen}

	
## Supresión de registros por tipo de registro correspondientes a un determinado periodo de tiempo
{: #time_range}

Siga los pasos siguientes para suprimir registros por tipo de registro almacenados en un dominio del espacio correspondientes a un determinado periodo de tiempo:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Ejecute el siguiente mandato para ver los registros disponibles en la recopilación de registros.

    ```
    bx logging log-show
    ```
    {: codeblock}
    
    Por ejemplo,
    
    ```
    $ bx logging log-show
    Showing log status of resource: 12345678-1234-2edr-a9de-378620d6fab5 ...

    Date         Size       Count   Searchable          Types   
	2017-05-24   16         3020    None                default
	2017-05-25   1224       76115   All                 linux_syslog,log
    2017-05-26   19663113   17639   All                 default,linux_syslog  
    ```
    {: screen}
	
3. Suprima los registros almacenados en un día específico.

    ```
	bx logging log-delete -s StartDate -e EndDate -t LogType
	```
	{: codeblock}
	
	donde
	
	* *-s* define la fecha inicial en hora universal coordinada (UTC): AAAA-MM-DD, por ejemplo 2006-01-02.
    * *-e* define la fecha final en hora universal coordinada (UTC): AAAA-MM-DD
    * *-t* define el tipo de registro.
    	
	Por ejemplo, para suprimir los registros de tipo linux_syslog correspondientes al 25 de mayo de 2017, ejecute el mandato siguiente:
	
	```
	bx logging log-delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
	```
	{: screen}

		
	
## Supresión de registros de la cuenta por tipo de registro correspondientes a un determinado periodo de tiempo
{: #time_range}

Siga estos pasos:

1. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Obtenga el ID de cuenta.

    Para obtener más información, consulte [Cómo se obtiene el GUID de una cuenta](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Ejecute el siguiente mandato para ver los registros disponibles en la recopilación de registros a nivel de cuenta.

    ```
    bx logging log-show  -r account -i AccountID
    ```
    {: codeblock}
    
    Por ejemplo,
    
    ```
    $ bx logging log-show -r account -i 123456789123456789567c9c8de6dece -s 2017-05-24 -e 2017-05-25
	Showing log status of resource: 123456789123456789567c9c8de6dece ...

    Date         Size       Count   Searchable          Types   
	2017-05-24   16         3020    All                 default
	2017-05-25   2000       76115   All                 linux_syslog,log
    2017-05-26   195678     17639   All                 default,linux_syslog    
    Logs of resource 123456789123456789567c9c8de6dece is showed
    OK
    ```
    {: screen}
	
4. Suprima los registros almacenados en un día específico.

    ```
	bx logging log-delete -s StartDate -e EndDate -t LogType -r account -i AccountID
	```
	{: codeblock}
	
	donde
	
	* *-s* define la fecha inicial en hora universal coordinada (UTC): AAAA-MM-DD, por ejemplo 2006-01-02.
    * *-e* define la fecha final en hora universal coordinada (UTC): AAAA-MM-DD
    * *-t* define el tipo de registro.
    	
	Por ejemplo, para suprimir los registros de tipo linux_syslog correspondientes al 25 de mayo de 2017 almacenados en la recopilación de registros a nivel de cuenta, ejecute el mandato siguiente:
	
	```
	bx logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog -r account -i 123456789123456789567c9c8de6dece
	```
	{: screen}
	












