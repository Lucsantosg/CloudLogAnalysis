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

# Remarques sur la migration après la mise à niveau de la pile ELK à la version 5.1 
{: #es17_to_es51}

Dans {{site.data.keyword.Bluemix}}, la pile ElasticSearch (ELK) est mise à niveau de la version 1.7 à la version 2.3. Les nouvelles fonctions, les URL pour l'ingestion des journaux
et les nouveaux URL pour l'analyse des journaux dans Kibana sont disponibles. Pour plus d'informations, voir
[ElasticSearch 5.1 ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html).
{:shortdesc}

Cette fonction ne s'applique pas aux utilisateurs qui utilisent le service de journalisation avec des conteneurs Docker déployés dans un cluster Kubernetes. Ces conteneurs utilisent
déjà la pile ELK de version 2.3.

## Régions
{: #regions}

La pile ELK de version 5.1 est disponible dans la région suivante :

* Sud des États-Unis


## Nouveautés
{: #features}

1. URL permettant de travailler avec les journaux et les métriques.

    Dans ELK 1.7, le même URL a été partagé pour afficher et contrôler des journaux et des métriques. Avec la mise à niveau à ELK 5.1, les journaux et les métriques sont affichés via des
URL distinctes. Pour plus d'informations, voir [URL de journalisation](#logging).
    
2. Prise en charge de Kibana 5.1. 

    Vous pouvez lancer Kibana à partir de l'interface utilisateur {{site.data.keyword.Bluemix_notm}} ou directement à partir de la nouvelle URL de journalisation. Pour plus
d'informations, voir [Analyse des journaux avec Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana).
    
    Kibana 3 est obsolète. Vous pouvez lancer Kibana 3 via l'[URL de journalisation d'ELK 1.7](#logging). Il existe différents URL pour chaque région. **Remarque
:** vous pouvez actuellement accéder aux tableaux de bord de Kibana 3 afin de pouvoir comparer vos tableaux de bord Kibana 3 à Kibana 5.1 et les faire migrer. 
    
    Si vos tableaux de bord Kibana reposent sur la pile ELK 1.7, vous devez les faire migrer vers l'environnement ELK 5.1.
    
    Pour plus d'informations sur Kibana 5.1, voir le [Guide d'utilisation de
Kibana![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.
    
3. Suffixes basés sur le type ajoutés aux zones personnalisées.

    Vous pouvez configurer des zones personnalisées en tant que zones de recherche Kibana. Chaque zone disponible dans un message est analysée en fonction du type de zone correspondant à sa valeur. Par exemple, chaque zone dans le message JSON suivant : 

    ```
    {"field1":"string type",
        "field2":123,
        "field3":false,
        "field4":"4567"
    }
    ```
    {: screen}
    
    est disponible en tant que zone que vous pouvez utiliser pour effectuer un filtrage et des recherches :

    * field1 est analysée en tant que field1_str de type string (chaîne).
    * field2 est analysée en tant que field1_int de type integer (entier).
    * field3 est analysée en tant que field3_bool de type boolean (booléen).
    * field4 est analysée en tant que field4_str de type string (chaîne).
    
    L'exemple de message JSON est un journal que vous envoyez au service de journalisation. 

    **Remarque :** cette fonction est uniquement disponible dans Elastic 5.1. Cette fonction n'est pas disponible dans Elastic 1.7 pour éviter de casser les tableaux de
bord Kibana3.


## Journalisation 
{: #logging}

Différentes URL sont utilisées pour envoyer des journaux dans {{site.data.keyword.Bluemix_notm}} et pour analyser les données dans Kibana.

Le tableau suivant indique la nouvelle URL que vous devez utiliser pour la région Sud des Etats-Unis :

<table>
  <caption>Adresses URL pour la région Sud des Etats-Unis</caption>
    <tr>
      <th>Type</th>
      <th>ELK 1.7 </th>
	  <th>ELK 5.1 </th>
    </tr>
  <tr>
    <td>URL d'ingestion pour les journaux</td>
    <td>logs.opvis.bluemix.net:9091</td>
	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>URL de Kibana pour l'analyse des journaux</td>
    <td>https://logmet.ng.bluemix.net</td>
	<td>https://logging.ng.bluemix.net</td>
  </tr>
</table>

