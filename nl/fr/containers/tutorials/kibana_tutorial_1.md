---

copyright:
  years: 2017

lastupdated: "2017-05-23"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Analyse dans Kibana des journaux d'une application déployée dans un cluster Kubernetes
{: #kibana_tutorial_1}

Familiarisez-vous avec Kibana. Découvrez comment rechercher et analyser des journaux de conteneurs pour une application déployée dans un cluster Kubernetes.
{:shortdesc}

**Remarque :** Pour suivre ce tutoriel, exécutez les tutoriels des différentes étapes associées.

## Prérequis
{: #prereq}

1. Etre membre ou propriétaire d'un compte Bluemix et disposer des autorisations de création de clusters Kubernetes, de déploiement d'applications dans des clusters, et d'interrogation des journaux {{site.data.keyword.Bluemix_notm}} pour analyse avancée dans Kibana.

2. Disposer d'une session de terminal depuis laquelle vous pouvez gérer le cluster Kubernetes et déployer des applications depuis la ligne de commande. Les exemples de ce tutoriel se réfèrent à un système Ubuntu Linux.

3. [Installez les plug-ins d'interface CLI](/docs/containers/cs_cli_install.html#cs_cli_install_steps) dans votre système Ubuntu pour gérer le service {{site.data.keyword.containershort}}  depuis la ligne de commande.  


## Etape 1 : Configuration et mise en route de Kubernetes dans Bluemix
{: #step1}

Procédez comme suit :

1. [Créez un cluster Kubernetes](/docs/containers/cs_cluster.html#cs_cluster_ui).

2. Configurez le contexte de cluster.  

    Par exemple, pour configurer le contexte dans un terminal Linux, exécutez les étapes décrites dans la rubrique [Configuration de l'interface CLI pour exécuter des commandes kubectl sur des clusters pour IBM Bluemix Container Service](/docs/containers/cs_cli_install.html#cs_cli_configure).

Une fois le contexte défini, vous pouvez gérer le cluster Kubernetes et déployer l'application dans ce cluster.

## Etape 2 : Déploiement d'une application dans le cluster Kubernetes
{: #step2}

Déployez et exécutez un exemple d'application dans le cluster Kubernetes. [Exécutez les tâches de la leçon 1](/docs/containers/cs_tutorials.html#cs_apps_tutorial).

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
{: screen}

Lorsque l'application est déployée, le collecte de journaux est automatiquement activée pour les entrées de journal envoyées par l'application vers les flux stdout (sortie standard) et stderr (erreur standard). 

Dans cet exemple d'application, lorsque vous testez votre application dans un navigateur, l'application consigne dans stdout le message suivant : `L'exemple d'application est à l'écoute sur le port 8080.`


## Etape 3 : Analyse des données de journal dans Kibana
{: #step3}

1. Lancez Kibana depuis un navigateur. 

    Pour analyser les données de journal pour un cluster, vous devez accéder à Kibana dans la région cloud Public où le cluster a été créé. 
    
    ```
	https://logging.ng.bluemix.net/ 
	```
	{: codeblock}
    
    Ensuite, à partir d'un navigateur, lancez l'URL pour ouvrir Kibana.
    
2. Sur la page **Discover**, examinez les événements qui sont affichés. 

    L'exemple d'application Hello-World génère un seul événement.
    
    ![Discover page in Kibana](images/sampleapp_2.gif "Discover page in Kibana")
    
    La section *Available fields* affiche une liste des zones que vous pouvez utiliser pour définir de nouvelles requêtes ou pour filtrer les entrées répertoriées dans le tableau qui est affiché sur la page.
    
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
                <td>Les zones de libellé sont facultatives. Vous pouvez ne pas les utiliser ou en utiliser plusieurs. Chaque libellé débute par le préfixe `kubernetes.labels.` suivi de *label_name*. </td>
                <td>Dans l'exemple d'application, vous pouvez observer deux libellés : <br>* *kubernetes.labels.pod-template-hash_str* = 3355293961 <br>* *kubernetes.labels.run_str* =	hello-world-deployment  </td>
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
    
    
    
3. Filtrez les données sur la page *Discover*.  

    Dans le tableau, vous pouvez observer toutes les entrées disponibles pour une analyse. Les entrées qui sont répertoriées correspondent à la requête de recherche qui est affichée dans la barre de recherche. Utilisez un astérisque (*) pour afficher toutes les entrées dans la période qui est configurée pour la page.

    Par exemple, pour filtrer les données par espace de nom Kubernetes, modifiez la requête de la barre de recherche. Ajoutez un filtre basé sur la zone personnalisée *kubernetes.namespace_name_str* :
    
    1. Dans la section **Available fields**, sélectionnez la zone *kubernetes.namespace_name_str*. Un sous-ensemble des valeurs disponibles pour la zone est affiché.    
    
    2. Sélectionnez la valeur **default**. Il s'agit de l'espace de nom où vous avez déployé dans une étape antérieure l'exemple d'application.
    
        Après avoir sélectionné la valeur, un filtre est ajouté à la barre de recherche et le tableau affiche uniquement les entrées qui correspondent aux critères que vous venez de sélectionner.     
    
    ![Filter for search for the default Kubernetes namespace](images/sampleapp_k4_1.gif "Filter for search for the default Kubernetes namespace")
    
    Vous pouvez sélectionner le symbole d'édition du filtre pour modifier le nom de l'espace de nom à rechercher.   
    
    ![Actions that are available for a filter](images/sampleapp_k4_1.gif "Actions that are available for a filter")
    
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
	{: screen}
    
    Pour rechercher des entrées dans un espace de nom différent comme *mynamespace1*, modifiez la requête :
    
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
	{: screen}
    
    Si vous ne voyez pas de données, essayez de changer le filtre temporel. Pour plus d'informations, voir [Définition d'un filtre temporel](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
    

Pour plus d'informations, voir [Filtrage des journaux dans Kibana](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).

