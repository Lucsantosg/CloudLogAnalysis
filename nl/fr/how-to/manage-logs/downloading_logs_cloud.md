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

# Téléchargement des journaux
{: #downloading_logs}

Vous pouvez télécharger des journaux vers un fichier local ou diriger des données vers un autre programme. Les journaux sont téléchargés dans le contexte d'une session. Une session
spécifie les journaux à télécharger. Si le téléchargement des journaux est interrompu, la session reprend le téléchargement là où il s'est arrêté. Une fois le téléchargement terminé, vous
devez supprimer la session.
{:shortdesc}

Procédez comme suit pour télécharger dans un fichier journal les données de journal disponibles dans un espace :

## Etape 1 : Connexion à {{site.data.keyword.Bluemix_notm}}
{: #step1}

Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}} ?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

## Etape 2 : Identification des journaux disponibles
{: #step2}

1. Utilisez la commande `bx logging log-show` pour identifier les journaux disponibles pour les deux dernières semaines. Exécutez la commande suivante :

    ```
    bx logging log-show
    ```
    {: codeblock}
    
    Par exemple, l'exécution de cette commande génère la sortie suivante :
    
    ```
    bx logging log-show 
    Showing log status of resource: cedc73c5-1234-5678-abcd-378620d6fab5 ...

    Date         Size     Count   Searchable   Types   
    2017-11-16   794008   706     All          syslog, default   
	2017-11-17   794008   706     All          default   
    Logs of resource cedc73c5-1234-5678-abcd-378620d6fab5 is showed
    OK
    ```
    {: screen}

    **Remarque :** le service {{site.data.keyword.loganalysisshort}} est un service global qui utilise le temps universel coordonné (TUC). Les jours sont définis
en tant que jours TUC. Pour obtenir des journaux pour un jour à heure locale spécifique, il peut être nécessaire de télécharger plusieurs jours TUC.


## Etape 3 : Création d'une session
{: #step3}

Une session est requise pour définir l'étendue des données de journal disponibles pour un téléchargement et pour conserver le statut du téléchargement. 

Utilisez la commande [cf logging session-create](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#session_create) pour créer une session. Vous pouvez également spécifier une date
de début, une date de fin et des types de journaux lorsque vous créez une session :  

* Lorsque vous spécifiez la date de début et la date de fin, la session fournit un accès aux journaux entre ces dates incluses. 
* Lorsque vous spécifiez le type de journal (**-t**), la session fournit un accès à un type de journal particulier. Cette fonction est importante lorsque vous
gérez des journaux à grande échelle car vous pouvez étendre une session à un petit sous-ensemble de journaux qui vous intéresse.

Pour créer une session permettant de télécharger tous les journaux disponibles pour les deux dernières semaines, exécutez la commande suivante :

```
bx logging session-create 
```
{: codeblock}

La session renvoie les informations suivantes :

* La plage de dates à télécharger. La valeur par défaut est la date TUC en cours.
* Les types de journaux à télécharger. Par défaut, tous les types de journaux disponibles durant la période que vous spécifiez lorsque vous créez la session sont inclus. 
* Des informations indiquant si le compte entier doit être inclus, ou uniquement l'espace en cours. Par défaut, vous obtenez des journaux dans l'espace dans lequel vous êtes connecté.
* L'ID de session requis pour télécharger les journaux.

Exemple

```
$ bx logging session-create
Creating session for lopezdsr@uk.ibm.com resource: cedc73c5-6d55-4193-a9de-378620d6fab5 ...

ID                                     Space                                  CreateTime                       AccessTime                       Start        End          Type   
944aec4d-61f4-43d1-8f3b-c040195122da   12345678-1234-5678-abcd-378620d6fab5   2017-11-17T14:17:25.611542863Z   2017-11-17T14:17:25.611542863Z   2017-11-04   2017-11-17   ANY_TYPE   
Session: 944aec4d-61f4-43d1-8f3b-c040195122da is created
```
{: screen}

**Astuce :** pour afficher la liste des sessions actives, exécutez la commande [bx logging sessions](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#session_list).

## Etape 4 : Téléchargement des données de journal dans un fichier
{: #step4}

Pour télécharger les journaux qui sont spécifiés par les paramètres de session, exécutez la commande suivante :

```
bx logging log-download -o Log_File_Name Session_ID
```
{: codeblock}

où

* Log_File_Name est le nom du fichier de sortie.
* Session_ID est l'identificateur global unique de la session. Cette valeur est obtenue à l'étape précédente.

Exemple

```
bx logging log-download -o helloLogs.gz -jshdjsunelsssr4566722==
 160.00 KB / 380.33 KB [==============>------------------------]  42.07% 20.99 KB/s 10s
```
{: screen}

L'indicateur de progression se déplace de 0 à 100 % à mesure que les journaux se téléchargent.

**Remarque :** 

* Les données téléchargées sont au format JSON compressé. Si vous décompressez le fichier .gz et l'ouvrez, vous verrez les données au format JSON. 
* Le format JSON compressé est approprié pour l'ingestion par ElasticSearch ou Logstash. Si -o n'est pas fourni, les données sont directement transmises à la sortie standard (stdout) afin que vous puissiez
les diriger directement vers votre propre pile ELK.
* Vous pouvez également traiter les données avec un programme pouvant analyser JSON. 

## Etape 5 : Suppression de la session
{: #step5}

Une fois que le téléchargement est terminé, vous devez supprimer la session à l'aide de la commande [cf logging session delete](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#delete). 

Exécutez la commande suivante pour supprimer une session :

```
bx logging session-delete Session_ID
```
{: codeblock}

où Session_ID est l'identificateur global unique de la session créée à l'étape précédente.

Exemple

```
bx logging session-delete -jshdjsunelsssr4566722==
Deleting session: -jshdjsunelsssr4566722== of resource: 12345678-1234-5678-abcd-378620d6fab5 ...
Session: -jshdjsunelsssr4566722== is deleted

```
{: screen}



