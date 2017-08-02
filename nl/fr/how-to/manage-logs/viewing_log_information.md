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

# Affichage des informations sur le journal
{: #viewing_log_status}

Utilisez la commande [cf logging status](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status) pour obtenir des informations sur les journaux qui sont collectés et stockés dans Collecte des journaux.
{:shortdesc}

## Obtention d'informations sur les journaux durant une période définie
{: #viewing_logs}

Utilisez la commande `cf logging status` pour voir la taille, le nombre, les types de journaux et pour voir s'ils sont disponibles ou non pour une analyse dans Kibana
pour les journaux qui sont stockés dans Log Collection. 

Utilisez la commande `cf logging status` avec les options **-s** pour définir la date de début et **-e** pour définir la date de fin. Par exemple :

* `cf logging status` fournit des informations sur les deux dernières semaines.
* `cf logging status -s 2017-05-03` fournit des informations du 3 mai 2017 à la date en cours.
* `cf logging status -s 2017-05-03 -e 2017-05-08` fournit des informations sur la période comprise entre le 3 mai 2017 et le 8 mai 2017. 

1. Connectez-vous à un espace, une organisation ou une région {{site.data.keyword.Bluemix_notm}}.  

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Exécutez la commande *status*.

    ```
    $ cf logging status
    ```
    {: codeblock}
    
    Par exemple
    
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


## Obtention d'informations sur un type de journal durant une période définie
{: #viewing_logs_by_log_type}

Pour obtenir des informations sur un type de journal durant une période définie, utilisez la commande `cf logging status` avec les options **-t** pour
spécifier le type de journal, **-s** pour définir la date de début et **-e** pour définir la date de fin. Par exemple

* `cf logging status -t syslog` fournit des informations sur les journaux de type *syslog* durant les deux dernières semaines.
* `cf logging status -s 2017-05-03 -t syslog` fournit des informations sur les journaux de type *syslog* du 3 mai 2017 à la date en cours.
* `cf logging status -s 2017-05-03 -e 2017-05-08 -t syslog` fournit des informations sur les journaux de type *syslog* du 3 mai 2017 au 8 mai 2017. 

1. Connectez-vous à un espace, une organisation ou une région {{site.data.keyword.Bluemix_notm}}.  

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Exécutez la commande *status*.

    ```
    $ cf logging status -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    où
    
    * *-s* est utilisé pour définir la date de début en UTC (Universal Coordinated Time) : *AAAA-MM-JJ*
    * *-e* est utilisé pour définir la date de fin en UTC (Universal Coordinated Time) : *AAAA-MM-JJ*
    * *-t* est utilisé pour définir le type de journal.
    
    Vous pouvez spécifier plusieurs types de journaux en séparant chaque type par une virgule, par exemple **log_type_1,log_type_2,log_type_3**. 
    
    Par exemple
    
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



## Obtention d'informations de compte sur les journaux
{: #viewing_logs_account}

Pour obtenir des informations sur les journaux durant une période définie pour le compte {{site.data.keyword.Bluemix_notm}}, utilisez la commande `cf logging
status` avec l'option **-a**. Vous pouvez également spécifier les options **-t** pour spécifier le type de journal, **-s**
pour définir la date de début et **-e** pour définir la date de fin. 

1. Connectez-vous à un espace, une organisation ou une région {{site.data.keyword.Bluemix_notm}}.  

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Exécutez la commande *status*.

    ```
    $ cf logging status -a -s YYYY-MM-DD -e YYYY-MM-DD -t *Log_Type*
    ```
    {: codeblock}
    
    où
    
    * *-a* est utilisé pour spécifier les informations sur le niveau de compte
    * *-s* est utilisé pour définir la date de début en UTC (Universal Coordinated Time) : *AAAA-MM-JJ*
    * *-e* est utilisé pour définir la date de fin en UTC (Universal Coordinated Time) : *AAAA-MM-JJ*
    * *-t* est utilisé pour définir le type de journal.
    

    Vous pouvez spécifier plusieurs types de journaux en séparant chaque type par une virgule, par exemple **log_type_1,log_type_2,log_type_3**. 
 
    Par exemple
    
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














