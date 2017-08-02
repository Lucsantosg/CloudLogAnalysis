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

# Visualización de la información de registro
{: #viewing_log_status}

Utilice el mandato [cf logging status](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status) para obtener información sobre los registros que se recopilan y almacenan en el componente de recopilación de registros.
{:shortdesc}

## Obtención de información sobre los registros durante un periodo de tiempo
{: #viewing_logs}

Utilice el mandato `cf logging status` para ver el tamaño, recuento, tipos de registros y si los registros están o no disponibles para su análisis en Kibana para los registros que se almacenan en el componente de recopilación de registros. 

Utilice el mandato `cf logging status` con las opciones **-s** para definir la fecha inicial y **-e** para definir la fecha final. Por ejemplo:

* `cf logging status` ofrece información correspondiente a las 2 últimas semanas.
* `cf logging status -s 2017-05-03` ofrece información comprendida entre el 3 de mayo de 2017 y el día de hoy.
* `cf logging status -s 2017-05-03 -e 2017-05-08` ofrece información comprendida entre el 3 de mayo de 2017 y el 8 de mayo de 2017. 

1. Inicie la sesión en una región, organización y espacio de {{site.data.keyword.Bluemix_notm}}. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Ejecute el mandato *status*.

    ```
    $ cf logging status
    ```
    {: codeblock}
    
    Por ejemplo,
    
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


## Obtención de información sobre un tipo de registro durante un periodo de tiempo
{: #viewing_logs_by_log_type}

Para obtener información sobre un tipo de registro durante un periodo de tiempo, utilice el mandato `cf logging status` con las opciones **-t** para especificar el tipo de registro, **-s** para definir la fecha inicial y **-e** para definir la fecha final. Por ejemplo,

* `cf logging status -t syslog` proporciona información sobre los registros de tipo *syslog* durante las 2 últimas semanas.
* `cf logging status -s 2017-05-03 -t syslog` proporciona información sobre los registros de tipo *syslog* comprendido entre el 3 de mayo de 2017 y el día de hoy.
* `cf logging status -s 2017-05-03 -e 2017-05-08 -t syslog` proporciona información sobre los registros de tipo *syslog* entre el 3 de mayo de 2017 y el 8 de mayo de 2017. 

1. Inicie la sesión en una región, organización y espacio de {{site.data.keyword.Bluemix_notm}}. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Ejecute el mandato *status*.

    ```
    $ cf logging status -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    donde
    
    * *-s* se utiliza para definir la fecha inicial en hora universal coordinada (UTC): *AAAA-MM-DD*
    * *-e* se utiliza para definir la fecha final en hora universal coordinada (UTC): *AAAA-MM-DD*
    * *-t* se utiliza para definir el tipo de registro.
    
    Puede especificar varios tipos de registro separando cada tipo con una coma, por ejemplo **log_type_1,log_type_2,log_type_3**. 
    
    Por ejemplo,
    
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



## Obtención de información de cuenta sobre los registros
{: #viewing_logs_account}

Para obtener información sobre los registros durante un periodo de tiempo de la cuenta de {{site.data.keyword.Bluemix_notm}}, utilice el mandato `cf logging status` con la opción **-a**. También puede especificar las opciones **-t** para especificar el tipo de registro, **-s** para definir la fecha inicial y **-e** para definir la fecha final. 

1. Inicie la sesión en una región, organización y espacio de {{site.data.keyword.Bluemix_notm}}. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Ejecute el mandato *status*.

    ```
    $ cf logging status -a -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    donde
    
    * *-a* se utiliza para especificar información de nivel de cuenta
    * *-s* se utiliza para definir la fecha inicial en hora universal coordinada (UTC): *AAAA-MM-DD*
    * *-e* se utiliza para definir la fecha final en hora universal coordinada (UTC): *AAAA-MM-DD*
    * *-t* se utiliza para definir el tipo de registro.
    

    Puede especificar varios tipos de registro separando cada tipo con una coma, por ejemplo **log_type_1,log_type_2,log_type_3**. 
 
    Por ejemplo,
    
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














