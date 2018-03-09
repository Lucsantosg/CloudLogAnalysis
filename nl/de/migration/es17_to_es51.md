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

# Hinweise zur Migration nach dem Upgrade des ElasticSearch-Stack auf Version 5.1 
{: #es17_to_es51}

In {{site.data.keyword.Bluemix}} wird der ELK-Stack (ElasticSearch) von Version 1.7 auf Version 2.3 aktualisiert. Es stehen neue Features, neue URLs für das Einpflegen von Protokollen sowie neue URLs zur Analyse von Protokollen in Kibana zur Verfügung. Weitere Informationen finden Sie unter [Elasticsearch 5.1 ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html).
{:shortdesc}

Dieses Feature gilt nicht für Benutzer, die den Protokollierungsservice mit Docker-Containern verwenden, die in einem Kubernetes-Cluster bereitgestellt sind. 

## Regionen
{: #regions}

Version 5.1 des Elastic-Stack ist in den folgenden Regionen verfügbar:

* Vereinigtes Königreich
* USA (Süden)
* Deutschland
* Sydney


## Neuerungen
{: #features}

1. Verschiedene URLs für Protokolle und Metriken

    In Elastic 1.7 wurde dieselbe URL verwendet, um Protokolle und Metriken anzuzeigen und zu überwachen. Mit dem Upgrade auf Elastic 5.1 erhalten Sie separate URLs für die Anzeige von Protokollen und Metriken. Weitere Informationen finden Sie unter [Protokollierungs-URLs](#logging).
    
2. Unterstützung für Kibana 5.1.

    Sie können Kibana über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder direkt über die neue Protokollierungs-URL starten. Weitere Informationen finden Sie unter [Zum Kibana-Dashboard navigieren](/docs/services/CloudLogAnalysis/kibana/launch.html#launch).
    
    Kibana 3 und Kibana 4 sind veraltet.
	
	**Hinweis:** Es gibt verschiedene URLs pro Region. Im Vereinigten Königreich können Sie derzeit auf Kibana 4-Dashboards zugreifen, sodass Sie einen Vergleich herstellen und Ihre Dashboards auf die Version Kibana 5.1 migrieren können. 
    
    Sie müssen Ihre Dashboards in die Elastic 5.1-Umgebung migrieren.
    
    Weitere Informationen zu Kibana 5.1 finden Sie in der Veröffentlichung [Kibana User Guide ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.
    
3. Angepassten Feldern wurden typbasierte Suffixe hinzugefügt.

    Sie können angepasste Felder als Kibana-Suchfelder konfigurieren. Jedes Feld, das in einer Nachricht verfügbar ist, wird in den Feldtyp analysiert, der mit dem Wert übereinstimmt. Beispiel: Jedes Feld in der folgenden JSON-Nachricht 

    ```
    {"field1":"string type",
     "field2":123,
     "field3":false,
     "field4":"4567"
     }
    ```
    {: screen}
    
    ist als Feld verfügbar, das Sie zum Filtern und Suchen verwenden können:

    * field1 wird als field1_str des Typs 'Zeichenfolge' analysiert.
    * field2 wird als field1_int des Typs 'Integer' analysiert.
    * field3 wird als field3_bool des Typs 'Boolesch' analysiert.
    * field4 wird als field4_str des Typs 'Zeichenfolge' analysiert.
    
    Die JSON-Beispielnachricht ist ein Protokoll, das Sie an den Protokollierungsservice gesendet haben. 

    **Hinweis:** Dieses Feature ist nur in Elastic 5.1 verfügbar. Das Feature ist nicht in Elastic 1.7 verfügbar, um zu vermeiden, dass Kibana 3-Dashboards unterbrochen werden.


## URLs protokollieren
{: #logging}

Es werden verschiedene URLs verwendet, um Protokolle an {{site.data.keyword.Bluemix_notm}} zu senden und um Daten in Kibana zu analysieren.

In der folgenden Tabelle werden URLs für die Region 'USA (Süden)' aufgeführt:

<table>
  <caption>Tabelle 1. URLs für die Region 'USA (Süden)'</caption>
    <tr>
      <th>Typ</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
    </tr>
  <tr>
    <td>Einpflege-URL für Protokolle</td>
    <td>logs.opvis.bluemix.net:9091</td>
  	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>Kibana-URL zur Analyse von Protokollen</td>
    <td>[https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net)</td>
	  <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
  </tr>
</table>

In der folgenden Tabelle werden URLs für die Region 'Vereinigtes Königreich' aufgeführt:

<table>
  <caption>Tabelle 2. URLs für die Region 'Vereinigtes Königreich'</caption>
  <tr>
     <th>Typ</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>Einpflege-URL für Protokolle</td>
	   <td>logs.eu-gb.opvis.bluemix.net:9091</td>
	   <td>ingest.logging.eu-gb.bluemix.net:9091</td>
  </tr>
  <tr>
     <td>Kibana-URL zur Analyse von Protokollen</td>
	 <td>[https://logmet.eu-gb.bluemix.net](https://logmet.eu-gb.bluemix.net)</td>
	 <td>[https://logging.eu-gb.bluemix.net](https://logging.eu-gb.bluemix.net)</td>
  </tr>
</table>

In der folgenden Tabelle werden URLs für die Region 'Frankfurt' aufgeführt:

<table>
  <caption>Tabelle 3. URLs für die Region 'Frankfurt'</caption>
  <tr>
     <th>Typ</th>
      <th>Elastic 2.3 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>Einpflege-URL für Protokolle</td>
	 <td>ingest.logging.eu-de.bluemix.net</td>
	 <td>ingest-eu-fra.logging.bluemix.net</td>
  </tr>
  <tr>
     <td>Kibana-URL zur Analyse von Protokollen</td>
	 <td>[https://logging.eu-de.bluemix.net](https://logging.eu-de.bluemix.net)</td>
	 <td>[https://logging.eu-fra.bluemix.net](https://logging.eu-fra.bluemix.net)</td>
  </tr>
</table>



