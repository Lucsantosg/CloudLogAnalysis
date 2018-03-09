---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Remarques sur la migration après la mise à niveau d'Elastic Stack vers la version 5.1 
{: #es17_to_es51}

Dans {{site.data.keyword.Bluemix}}, la pile ElasticSearch (ELK) est mise à niveau de la version 1.7 vers la version 5.1. De nouvelles fonctions, de nouvelles URL pour ingérer les journaux et de nouvelles URL pour analyser les journaux dans Kibana sont disponibles. Pour plus d'informations, voir
[ElasticSearch 5.1 ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html).
{:shortdesc}

Cette fonction ne s'applique pas aux utilisateurs qui utilisent le service de journalisation avec des conteneurs Docker déployés dans un cluster Kubernetes. 

## Régions
{: #regions}

Elastic version 5.1 est disponible dans la région suivante :

* Royaume-Uni
* Sud des Etats-Unis
* Allemagne
* Sydney


## Nouveautés
{: #features}

1. URL permettant d'utiliser des journaux et des mesures.

    Dans Elastic 1.7, la même URL était partagée pour afficher et surveiller des journaux et des mesures. Avec la mise à niveau vers Elastic 5.1, vous disposez d'URL distinctes pour l'affichage des journaux et des mesures. Pour plus d'informations, voir [URL de journalisation](#logging).
    
2. Prise en charge pour Kibana 5.1.

    Vous pouvez lancer Kibana à partir de l'interface utilisateur {{site.data.keyword.Bluemix_notm}} ou directement à partir de la nouvelle URL de journalisation. Pour plus d'informations, voir [Accès au tableau de bord Kibana](/docs/services/CloudLogAnalysis/kibana/launch.html#launch).
    
    Kibana 3 et Kibana 4 ont été dépréciés. 
	
	**Remarque :** les URL sont différentes selon les régions. L'accès aux tableaux de bord Kibana 4 est actuellement disponible au Royaume-Uni pour que vous puissiez comparer vos tableaux de bord avec ceux de Kibana 5.1 et les migrer.  
    
    Vous devez migrer vos tableaux de bord dans l'environnement Elastic 5.1. 
    
    Pour plus d'informations sur Kibana 5.1, voir le manuel [Kibana User Guide ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.
    
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


## URL de journalisation
{: #logging}

Différentes URL sont utilisées pour envoyer des journaux dans {{site.data.keyword.Bluemix_notm}} et pour analyser des données dans Kibana.

Le tableau suivant répertorie les URL pour la région Sud des Etats-Unis :

<table>
  <caption>Tableau 1. URL pour la région Sud des Etats-Unis</caption>
    <tr>
      <th>Type</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
    </tr>
  <tr>
    <td>URL d'ingestion pour les journaux</td>
    <td>logs.opvis.bluemix.net:9091</td>
  	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>URL de Kibana pour l'analyse des journaux</td>
    <td>[https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net)</td>
	  <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
  </tr>
</table>

Le tableau suivant répertorie les URL pour la région Royaume-Uni :

<table>
  <caption>Tableau 2. URL pour la région Royaume-Uni</caption>
  <tr>
     <th>Type</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>URL d'ingestion pour les journaux</td>
	   <td>logs.eu-gb.opvis.bluemix.net:9091</td>
	   <td>ingest.logging.eu-gb.bluemix.net:9091</td>
  </tr>
  <tr>
     <td>URL de Kibana pour l'analyse des journaux</td>
	 <td>[https://logmet.eu-gb.bluemix.net](https://logmet.eu-gb.bluemix.net)</td>
	 <td>[https://logging.eu-gb.bluemix.net](https://logging.eu-gb.bluemix.net)</td>
  </tr>
</table>

Le tableau suivant répertorie les URL pour la région Francfort :

<table>
  <caption>Tableau 3. URL pour la région Francfort</caption>
  <tr>
     <th>Type</th>
      <th>Elastic 2.3 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>URL d'ingestion pour les journaux</td>
	 <td>ingest.logging.eu-de.bluemix.net</td>
	 <td>ingest-eu-fra.logging.bluemix.net</td>
  </tr>
  <tr>
     <td>URL de Kibana pour l'analyse des journaux</td>
	 <td>[https://logging.eu-de.bluemix.net](https://logging.eu-de.bluemix.net)</td>
	 <td>[https://logging.eu-fra.bluemix.net](https://logging.eu-fra.bluemix.net)</td>
  </tr>
</table>



