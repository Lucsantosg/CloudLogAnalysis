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

# Suppression de journaux
{: #deleting_logs}

Utilisez la commande
[bx cf
logging delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#status) pour supprimer des journaux de Log Collection. 
{:shortdesc}

* Vous pouvez supprimer des journaux dans un intervalle spécifique.
* Vous pouvez supprimer des journaux par type. Notez que chaque fichier
journal ne comporte qu'un seul type d'entrées de journal.
* Vous pouvez supprimer des journaux pour un espace, ou dans le domaine de compte.


## Suppression de journaux pour une période spécifique
{: #time_range}

Procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}} ?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Exécutez la commande *status* afin d'afficher les journaux qui sont disponibles dans Log Collection.

    ```
    bx cf logging status
    ```
    {: codeblock}
    
    Exemple :
    
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
	
3. Supprimez les journaux qui ont été stockés un jour spécifique.

    ```
	bx cf logging delete -s StartDate -e EndDate
	```
	{: codeblock}
	
	où
	
	* *-s* définit la date de début en temps universel coordonné (TUC) : AAAA-MM-JJ, par exemple 2006-01-02.
    * *-e* définit la date de fin en temps universel coordonné (TUC) : AAAA-MM-JJ.
    	
	Par exemple, pour supprimer les journaux du 25 mai 2017, exécutez la commande
suivante :
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25
	```
	{: screen}

	
## Suppression de journaux par type de journal pour une période spécifique :
{: #time_range}

Procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}} ?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Exécutez la commande *status* afin d'afficher les journaux qui sont disponibles dans Log Collection.

    ```
    bx cf logging status
    ```
    {: codeblock}
    
    Exemple :
    
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
	
3. Supprimez les journaux qui ont été stockés un jour spécifique.

    ```
	bx cf logging delete -s StartDate -e EndDate -t LogType
	```
	{: codeblock}
	
	où
	
	* *-s* définit la date de début en temps universel coordonné (TUC) : AAAA-MM-JJ, par exemple 2006-01-02.
    * *-e* définit la date de fin en temps universel coordonné (TUC) : AAAA-MM-JJ.	
	* *-t* définit le type de journal.
    	
	Par exemple, pour supprimer les journaux du type linux_syslog du 25 mai 2017, entrez la commande suivante :
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog
	```
	{: screen}

		
	
## Suppression de journaux de compte par type de journal pour une période spécifique
{: #time_range}

Procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}} ?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Exécutez la commande *status* afin d'afficher les journaux qui sont disponibles pour Log Collection au niveau du compte.

    ```
    bx cf logging status  -a
    ```
    {: codeblock}
    
    Exemple :
    
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
	
3. Supprimez les journaux qui ont été stockés un jour spécifique.

    ```
	bx cf logging delete -s StartDate -e EndDate -t LogType -a
	```
	{: codeblock}
	
	où
	
	* *-s* définit la date de début en temps universel coordonné (TUC) : AAAA-MM-JJ, par exemple 2006-01-02.
    * *-e* définit la date de fin en temps universel coordonné (TUC) : AAAA-MM-JJ.	
	* *-t* définit le type de journal.
    	
	Par exemple, afin de supprimer les journaux de type linux_syslog du 25 mai 2017 qui sont stockés dans Log Collection au niveau du compte, exécutez la commande suivante :
	
	```
	bx cf logging delete -s 2017-05-25 -e 2017-05-25 -t linux_syslog -a
	```
	{: screen}
	












