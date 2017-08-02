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

# Tutoriel Initiation
{: #getting-started-with-cla}

Dans ce didacticiel d'initiation, nous vous guidons à travers les étapes nécessaires pour exécuter des tâches analytiques avancées à l'aide du service
{{site.data.keyword.loganalysislong}}. Découvrez comment rechercher et analyser des journaux de conteneurs pour une application déployée dans un cluster Kubernetes.
{:shortdesc}

## Avant de commencer
{: #prereqs}

Créez un compte [{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/). Votre ID d'utilisateur doit être membre ou propriétaire d'un
compte {{site.data.keyword.Bluemix_notm}} autorisé à créer des clusters Kubernetes, à déployer des applications dans des clusters et à interroger des journaux dans
{{site.data.keyword.Bluemix_notm}} pour une analyse avancée dans Kibana.

Ouvrez une session de terminal à partir de laquelle vous pouvez gérer le cluster Kubernetes et déployer des applications à partir de la ligne de commande. Les exemples de ce tutoriel se réfèrent à un système Ubuntu Linux.

[Installez les plug-ins d'interface CLI](/docs/containers/cs_cli_install.html#cs_cli_install_steps) dans votre environnement local pour gérer le service {{site.data.keyword.containershort}} depuis la ligne de commande.  



## Etape 1 : déployez une application dans un cluster Kubernetes
{: #step1}

1. [Créez un cluster Kubernetes](/docs/containers/cs_cluster.html#cs_cluster_ui).

2. [Configurez le contexte de cluster](/docs/containers/cs_cli_install.html#cs_cli_configure) dans un terminal Linux. Une fois le contexte défini, vous pouvez gérer le cluster Kubernetes et déployer l'application dans ce cluster.

3. Déployez et exécutez un exemple d'application dans le cluster Kubernetes. [Exécutez les tâches de la leçon 1](/docs/containers/cs_tutorials.html#cs_apps_tutorial).

    L'application est une application Hello World Node.js :

    ```
    var express = require('express')
var app = express()

    app.get('/', function(req, res) {
      res.send('Hello world! Your app is up and running in a cluster!\n')
    })
    app.listen(8080, function() {
      console.log('Sample app is listening on port 8080.')
    })
    ```
	{: codeblock}

    Lorsque l'application est déployée, le collecte de journaux est automatiquement activée pour les entrées de journal envoyées par l'application vers les flux stdout (sortie standard) et stderr (erreur standard). 

    Dans cet exemple d'application, lorsque vous testez votre application dans un navigateur, l'application écrit le message suivant dans stdout: `Sample app is listening on port
8080.`

## Etape 2 : accédez au tableau de bord Kibana
{: #step2}

Pour analyser les données de journal pour un cluster, vous devez accéder à Kibana dans la région cloud Public où le cluster a été créé. 

Par exemple, pour lancer Kibana dans la région du sud des États-Unis, accédez à l'URL suivante :

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}

    
    
## Etape 3 : Analyse des données de journal dans Kibana
{: #step3}

1. Sur la page **Discover**, examinez les événements qui sont affichés. 

    L'exemple d'application Hello-World génère un seul événement.
    
    La section Available fields affiche une liste des zones que vous pouvez utiliser pour définir des nouvelles requêtes ou pour filtrer les entrées répertoriées dans le tableau affiché
sur la page.
    
    Le tableau suivant répertorie les zones communes que vous pouvez utiliser pour définir de nouvelles requêtes de recherche. Il comprend également des exemples de valeurs correspondant à l'événement généré par l'exemple d'application :
    
     <table>
              <caption>Tableau 2. Zones communes aux journaux de conteneurs </caption>
               <tr>
                <th align="center">Zone</th>
                <th align="center">Description</th>
                <th align="center">Exemple</th>
              </tr>
              <tr>
                <td>*docker.container_id_str*</td>
                <td> La valeur de cette zone correspond à l'identificateur global unique du conteneur qui exécute l'application dans une nacelle du cluster Kubernetes.</td>
                <td></td>
              </tr>
              <tr>
                <td>*ibm-containers.region_str*</td>
                <td>La valeur de cette zone correspond à la région {{site.data.keyword.Bluemix_notm}} où l'entrée de journal est collectée.</td>
                <td>us-south</td>
              </tr>
              <tr>
                <td>*kubernetes.container_name_str*</td>
                <td>La valeur de cette zone indique le nom du conteneur.</td>
                <td>hello-world-deployment</td>
              </tr>
              <tr>
                <td>*kubernetes.host*</td>
                <td>La valeur de cette zone indique l'adresse IP publique disponible pour accès à l'application depuis Internet. </td>
                <td>169.47.218.231</td>
              </tr>
              <tr>
                <td>*kubernetes.labels.label_name*</td>
                <td>Les zones de libellé sont facultatives. Vous pouvez ne pas les utiliser ou en utiliser plusieurs. Chaque libellé débute par le préfixe `kubernetes.labels.`, suivi du *label_name* (nom du libellé). </td>
                <td>Dans l'exemple d'application, vous pouvez observer 2 libellés : <br>* *kubernetes.labels.pod-template-hash_str* = 3355293961 <br>* *kubernetes.labels.run_str* =	hello-world-deployment  </td>
              </tr>
              <tr>
                <td>*kubernetes.namespace_name_str*</td>
                <td>La valeur de cette zone indique l'espace de nom Kubernetes sous lequel la nacelle s'exécute. </td>
                <td>défaut</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_id_str*</td>
                <td>La valeur de cette zone correspond à l'identificateur global unique de la nacelle dans laquelle le conteneur s'exécute. </td>
                <td>d695f346-xxxx-xxxx-xxxx-aab0b50f7315</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_name_str*</td>
                <td>La valeur de cette zone indique le nom de la capsule.</td>
                <td>hello-world-deployment-3xxxxxxx1-xxxxx8</td>
              </tr>
              <tr>
                <td>*message*</td>
                <td>Message complet consigné par l'application.</td>
                <td>L'exemple d'application est à l'écoute sur le port 8080.</td>
              </tr>
        </table>
    
2. Filtrez les données sur la page **Discover**.  

    Dans le tableau, vous pouvez observer toutes les entrées disponibles pour une analyse. Les entrées répertoriées correspondent à la requête de recherche affichée dans la barre de
recherche. L'astérisque (*) est utilisé pour afficher toutes les entrées comprises dans la période qui est configurée pour la page.

     
    
    Par exemple, pour filtrer les données par espace de nom Kubernetes, modifiez la requête de la barre de recherche. Ajoutez un filtre basé sur la zone personnalisée *kubernetes.namespace_name_str*:
    
    1. Dans la section *Zones disponibles*, sélectionnez la zone *kubernetes.namespace_name_str*. Un sous-ensemble des valeurs disponibles pour la zone est affiché.    
    
    2. Sélectionnez la valeur **default**. Il s'agit de l'espace de nom où vous avez déployé dans une étape antérieure l'exemple d'application.
    
        Après avoir sélectionné la valeur, un filtre est ajouté à la barre de recherche et le tableau affiche uniquement les entrées qui correspondent aux critères que vous venez de
sélectionner.     
    
    Vous pouvez sélectionner le symbole d'édition du filtre pour modifier le nom de l'espace de nom à rechercher.   
    
    La requête suivante est affichée :
    
    ```
	{
    "query": {
          "match": {
            "kubernetes.namespace_name_str": {
              "query": "default",
              "type": "phrase"
            }
          }
        }
    }
    ```
	{: codeblock}
    
    Pour rechercher des entrées dans un espace de nom différent (par exemple, *mynamespace1*), modifiez comme suit la requête :
    
    ```
	{
    "query": {
          "match": {
            "kubernetes.namespace_name_str": {
              "query": "mynamespace1",
              "type": "phrase"
            }
          }
        }
    }
    ```
	{: codeblock}
    
    Si vous ne voyez pas de données, essayez de changer le filtre temporel. Pour plus d'informations, voir [Définition d'un filtre temporel](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
    

Pour plus d'informations, voir [Filtrage des journaux dans Kibana](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).


## Etapes suivantes
{: #next_steps}

Ensuite, créez des tableaux de bord Kibana. Pour plus d'informations, voir [Analyse des journaux dans Kibana via un tableau de bord](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#analize_logs_dashboard).
                                                                                                                      

