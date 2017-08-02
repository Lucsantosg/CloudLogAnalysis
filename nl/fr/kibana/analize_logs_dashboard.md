---

copyright:
  years: 2017

lastupdated: "2017-07-19"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Analyses des journaux dans Kibana via un tableau de bord
{:#analize_logs_dashboard}

Utilisez la page *Dashboard* dans Kibana pour afficher des collections de visualisations regroupées en tableaux de bord. Utilisez les tableaux de bord pour analyser les données des journaux et comparer les résultats.
{:shortdesc}

Dans {{site.data.keyword.Bluemix}}, vous pouvez définit et personnaliser différents types de tableaux de bord pour visualiser et analyser les données. Le tableau suivant, par exemple, recense divers tableaux de bord courants :

| Type de tableau de bord | Description |
|-------------------|-------------|
| Tableau de bord d'application cf unique | Ce tableau de bord affiche des informations sur une application Cloud Foundry unique. |
| Tableau de bord de conteneur unique  | Ce tableau de bord affiche des informations sur un conteneur unique.  |
| Tableau de bord de groupe de conteneurs  | Ce tableau de bord affiche des informations sur un groupe de conteneurs spécifique.  |
| Tableau de bord multi-applications cf | Ce tableau de bord affiche des informations sur toutes les applications Cloud Foundry déployées dans le même espace {{site.data.keyword.Bluemix_notm}}.  | 
| Tableau de bord multi-conteneurs | Ce tableau de bord affiche des informations sur tous les conteneurs déployés dans le même espace {{site.data.keyword.Bluemix_notm}}.  |
| Tableau de bord d'espace | Ce tableau de bord affiche les données de consignation au journal disponibles dans un espace {{site.data.keyword.Bluemix_notm}}.  | 
{: caption="Tableau 1. Exemples de types de tableau de bord" caption-side="top"}

Pour visualiser les données dans un tableau de bord, vous devez configurer des panneaux. Kibana inclut différentes visualisations (telles que tableau, tendances et histogramme) que vous pouvez utiliser pour analyser les informations. Une visualisation est ajoutée à un tableau de bord sous forme de panneau. Vous pouvez ajouter, retirer et réorganiser des panneaux dans le tableau de bord. L'objectif de chaque panneau est différent. Certains panneaux sont organisés en lignes qui fournissent les résultats d'une ou de plusieurs requêtes. D'autres panneaux affichent des documents ou des informations personnalisées. Chaque panneau est basé sur une recherche. Le recherche définit le sous-ensemble de données qu'affiche le panneau. Par exemple, vous pouvez configurer un graphique à barres, un graphique circulaire ou un tableau pour visualiser les données et les analyser.  

Le tableau suivant répertorie différentes tâches que vous pouvez effectuer depuis la page Dashboard :

| Tâche | Informations sur la tâche |
|------|------------------|
| [Ajouter une visualisation](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#add_visualization) | Vous pouvez ajouter une visualisation ou une recherche existante à un tableau de bord.|
| [Créer un nouveau tableau de bord](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#new) | Vous pouvez créer plusieurs tableaux de bord. Chaque tableau de bord peut être conçu en vue d'inclure des recherches et des visualisations différentes, ainsi qu'un sous-ensemble distinct de données de journal.  |
| [Supprimer un tableau de bord](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#delete) | Vous pouvez supprimer les tableaux de bord superflus. |
| [Exporter un tableau de bord](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#export) | Vous pouvez exporter un tableau de bord sous forme de fichier JSON. |
| [Importer un tableau de bord](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#import) | Vous pouvez importer un tableau de bord depuis un fichier JSON. |
| [Charger un tableau de bord](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#reload) | Vous pouvez charger un tableau de bord pour mettre à jour les données, les modifier, ou les analyser. |
| [Sauvegarder un tableau de bord](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#save) | Vous pouvez sauvegarder un tableau de bord pour le réutiliser plus tard. |
{: caption="Tableau 2. Tâches de gestion de tableaux de bord" caption-side="top"}

Pour plus d'informations sur Kibana, reportez-vous au manuel [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.


## Ajout d'une nouvelle recherche ou visualisation
{: #add_visualization}

Pour ajouter une virtualisation ou une recherche existante, procédez comme suit :

1. Dans la barre d'outils de la page Dashboard, cliquez sur **Add**. 

    **Remarque **: vous pouvez ajouter des visualisations et des recherches. 

2. Sélectionnez l'onglet **Visualizations** pour ajouter une visualisation ou l'onglet **Searches** pour ajouter une recherche.

3. Cliquez sur la recherche ou la visualisation que vous désirez ajouter.

    Un panneau pour la recherche ou la visualisation concernée est ajouté au tableau de bord.

	
## Création d'un nouveau tableau de bord Kibana
{: #new}

Pour créer un nouveau tableau de bord, procédez comme suit :

1. Dans la barre d'outils de la page Dashboard, cliquez sur **Add**. 

2. Ajoutez une ou plusieurs recherches et visualisations. Pour plus d'informations, voir [Ajout d'une nouvelle recherche ou visualisation](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#add_visualization).

    Lorsque vous ajoutez une recherche ou une visualisation, un panneau est ajouté au tableau de bord.

3. Faites glisser un panneau et déposez-le à l'emplacement où vous désirez le positionner sur le tableau de bord.
 
4. Sauvegardez le tableau de bord pour une réutilisation ultérieure. Pour plus d'informations, voir [Sauvegarde d'un tableau de bord Kibana](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#save).


## Suppression d'un tableau de bord Kibana
{: #delete}

Pour supprimer un tableau de bord, procédez comme suit sur la page **Management** :

1. Sur la page **Management**, sélectionnez l'onglet **Advanced Objects**.

2. Dans l'onglet **Dashboards**, sélectionnez le tableau de bord que vous souhaitez supprimer.

3. Cliquez sur **Delete**.

## Exportation d'un tableau de bord Kibana
{: #export}

Pour exporter un tableau de bord en tant que fichier JSON, procédez comme suit sur la page **Management** :

1. Sur la page **Management**, sélectionnez l'onglet **Advanced Objects**.

2. Dans l'onglet **Dashboard**, sélectionnez le tableau de bord que vous désirez exporter.

3. Cliquez sur **Export**.

4. Sauvegardez le fichier.

## Importation d'un tableau de bord Kibana
{: #import}

Pour importer un tableau de bord en tant que fichier JSON, procédez comme suit sur la page **Management** :

1. Sur la page **Management**, sélectionnez l'onglet **Advanced Objects**.

2. Dans l'onglet **Dashboard**, sélectionnez **Import**.

3. Sélectionnez un fichier et cliquez sur **Open**.

Le tableau de bord est ajouté à la liste des tableaux de bord.

## Chargement d'un tableau de bord Kibana
{: #reload}

Pour charger un tableau de bord sauvegardé, procédez comme suit :

1. Dans la barre d'outils de la page Dashboard, cliquez sur **Open**.

2. Sélectionnez un tableau de bord dans la liste des tableaux de bord disponibles qui s'affiche sous la zone *Name*.

Vous pouvez également rechercher un tableau de bord dans la barre de recherche.

## Sauvegarde d'un tableau de bord Kibana
{: #save}

Procédez comme suit pour sauvegarder un tableau de bord Kibana après l'avoir personnalisé :

1. Dans la barre d'outils, cliquez sur **Save**.

2. Entrez un nom pour le tableau de bord.

    **Remarque :** le nom ne doit pas contenir d'espaces. 

3. Cliquez sur **Save**.




