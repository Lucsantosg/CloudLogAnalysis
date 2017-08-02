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

# Téléchargement des journaux
{: #downloading_logs}

Vous pouvez télécharger des journaux vers un fichier local ou diriger des données vers un autre programme. Les journaux sont téléchargés dans le contexte d'une session. Une session
spécifie les journaux à télécharger. Si le téléchargement des journaux est interrompu, la session reprend le téléchargement là où il s'est arrêté. Une fois le téléchargement terminé, vous
devez supprimer la session.
{:shortdesc}

Procédez comme suit pour télécharger les données de journal disponibles dans un espace {{site.data.keyword.Bluemix_notm}} vers un fichier local :

Avant de commencer, connectez-vous à un espace, à une organisation ou à une région {{site.data.keyword.Bluemix_notm}}. 

Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
```
cf login -a https://api.ng.bluemix.net
```
{: codeblock}

## Etape 1 : identifiez les journaux disponibles
{: #step1}

1. Utilisez la commande `cf logging status` pour voir quels journaux sont disponibles pour les 2 dernières semaines. Exécutez la commande suivante :

    ```
    $ cf logging status
    ```
    {: codeblock}
    
    Par exemple, l'exécution de cette commande génère la sortie suivante :
    
    ```
    +------------+--------+-------+--------------------+------------+
    |    DATE    |  COUNT | SIZE  |       TYPES        | SEARCHABLE |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-24 |    16  | 3020  |        log         |   None     |
    +------------+--------+-------+--------------------+------------+
    | 2017-05-25 |   1224 | 76115 | linux_syslog,log   |    All     |
    +------------+--------+-------+--------------------+------------+
    ```
    {: screen}

    **Remarque :** le service {{site.data.keyword.loganalysisshort}} est un service global qui utilise UTC (Coordinated Universal Time). Les jours sont définis
en tant que jours UTC. Pour obtenir des journaux pour un jour à heure locale spécifique, il est possible qu'il soit nécessaire de télécharger plusieurs jours UTC.


## Etape 2 : créez une session
{: #step2}

Une session est requise pour définir l'étendue des données de journal disponibles pour un téléchargement et pour conserver l'état du téléchargement. 

Utilisez la commande [cf logging session create](/docs/services/CloudLogAnalysis/reference/logging_cli.html#session_create) pour créer une session. Vous pouvez également spécifier une date
de début, une date de fin et des types de journaux lorsque vous créez une session :  

* Lorsque vous spécifiez la date de début et la date de fin, la session fournit un accès aux journaux entre ces dates incluses. 
* Lorsque vous spécifiez le type de journal (**-t**), la session fournit un accès à un type de journal particulier. Cette fonction est importante lorsque vous
gérez des journaux à grande échelle car vous pouvez étendre une session à un petit sous-ensemble de journaux qui vous intéresse.

Pour créer une session utilisée pour télécharger des journaux de type *log*, exécutez la commande suivante :

```
cf logging session create -t log
```
{: codeblock}

La session renvoie les informations suivantes :

* La plage de dates à télécharger. La valeur par défaut est la date UTC en cours.
* Les types de journaux à télécharger. Par défaut, tous les types de journaux disponibles durant la période que vous spécifiez lorsque vous créez la session sont inclus. 
* Des informations indiquant si le compte entier doit être inclus, ou uniquement l'espace en cours. Par défaut, vous obtenez des journaux dans l'espace dans lequel vous êtes connecté.
* L'ID de session requis pour télécharger les journaux.

Par exemple

```
$ cf logging session create -t log     
+--------------+--------------------------------------+
|     NAME     |                VALUE                 |
+--------------+--------------------------------------+
| Access-Time  | 2017-05-25T18:04:21.743792338Z       |
| Create-Time  | 2017-05-25T18:04:21.743792338Z       |
| Date-Range   | {                                    |
|              |  "End": "2017-05-25T00:00:00Z",      |
|              |  "Start": "2017-05-25T00:00:00Z"     |
|              | }                                    |
| Id           | -jshdjsunelsssr4566722==             |
| Space        | fdgrghg3-b090-4567-vvfg-afbc436902a3 |
| Type-Account | {                                    |
|              |  "Type": "log"                       |
|              | }                                    |
| Username     | xxx@yyy.com                          |
+--------------+--------------------------------------+
```
{: screen}

**Astuce :** pour afficher une liste des sessions actives, exécutez la commande [cf logging session list](/docs/services/CloudLogAnalysis/reference/logging_cli.html#session_list).

## Etape 3 : téléchargez les données de journal vers un fichier
{: #step3}

Pour télécharger les journaux qui sont spécifiés par les paramètres de session, exécutez la commande suivante :

```
cf logging download -o Log_File_Name Session_ID
```
{: codeblock}

où

* Log_File_Name est le nom du fichier de sortie.
* Session_ID est l'identificateur global unique de la session. Cette valeur est obtenue à l'étape précédente.

Par exemple

```
cf logging download -o helloLogs.gz -jshdjsunelsssr4566722==
 160.00 KB / 380.33 KB [==============>------------------------]  42.07% 20.99 KB/s 10s
```
{: screen}

L'indicateur de progression se déplace de 0 à 100% à mesure que les journaux se téléchargent.

**Remarque :** 

* Le format des données téléchargées est compressé JSON. Si vous décompressez le fichier .gz et l'ouvrez, vous verrez les données au format JSON. 
* Le format JSON compressé est approprié pour l'ingestion par ElasticSearch ou Logstash. Si -o n'est pas fourni, les données sont directement transférées à stdout afin que vous puissiez
les diriger directement vers votre propre pile ELK.
* Vous pouvez également traiter les données avec un programme pouvant analyser JSON. 

## Etape 4 : supprimez la session

Une fois que le téléchargement est terminé, vous devez supprimer la session à l'aide de la commande [cf logging session delete](/docs/services/CloudLogAnalysis/reference/logging_cli.html#session_delete). 

Exécutez la commande suivante pour supprimer une session :

```
cf logging session delete Session_ID
```
{: codeblock}

où Session_ID est l'identificateur global unique de la session créée à l'étape précédente.

Par exemple

```
cf logging session delete -jshdjsunelsssr4566722==
+---------+------------------------+
|  NAME   |         VALUE          |
+---------+------------------------+
| Message | Delete session success |
+---------+------------------------+
```
{: screen}




