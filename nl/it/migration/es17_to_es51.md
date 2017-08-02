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

# Considerazioni sulla migrazione dopo l'aggiornamento di ELK Stack alla versione 5.1 
{: #es17_to_es51}

In {{site.data.keyword.Bluemix}}, lo stack ElasticSearch (ELK) viene aggiornato dalla versione 1.7 alla 2.3. Sono disponibili nuove funzioni, URL per inserire i log e nuovi URL per analizzarli. Per ulteriori informazioni, vedi [ElasticSearch 5.1 ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html "Icona link esterno").
{:shortdesc}

Questa funzione non si applica agli utenti che utilizzano il servizio di registrazione con i contenitori Docker distribuiti in un cluster Kubernetes. Questi contenitori già utilizzano lo stack ELK versione 2.3.

## Regioni
{: #regions}

Lo stack ELK versione 5.1 è disponibile nelle seguenti regioni:

* Stati Uniti Sud


## Novità
{: #features}

1. Differenti URL da utilizzare con i log e le metriche.

    In ELK 1.7, lo stesso URL era condiviso per visualizzare e monitorare i log e le metriche. Con l'aggiornamento a ELK 5.1, disponi di URL separati per visualizzare i log e le metriche. Per maggiori informazioni, vedi [URL di registrazione](#logging).
    
2. Supporto per Kibana 5.1. 

    Puoi avviare Kibana dalla IU {{site.data.keyword.Bluemix_notm}} o direttamente dal nuovo URL di registrazione. Per maggiori informazioni, vedi [Analisi dei log con Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana).
    
    Kibana 3 è obsoleto. Puoi avviare Kibana 3 tramite l'[URL di registrazione ELK 1.7](#logging). Esistono diversi URL per regione. **Nota:** l'accesso ai dashboard Kibana 3 è al momento disponibile per il confronto e la migrazione dei tuoi dashboard Kibana 3 a 5.1. 
    
    Se disponi di dashboard Kibana creati con lo stack ELK 1.7, devi migrarli all'ambiente ELK 5.1.
    
    Per ulteriori informazioni su Kibana 5.1, vedi la [Kibana User Guide ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/kibana/5.1/index.html "Icona link esterno"){: new_window}.
    
3. Sono stati aggiunti dei suffissi basati sul tipo ai campi personalizzati.

    Puoi configurare i campi personalizzati come campi di ricerca Kibana. Ciascun campo disponibile in un messaggio viene analizzato al tipo di campo che corrisponde al suo valore. Ad esempio, ciascun campo nel seguente messaggio JSON: 

    ```
    {"field1":"string type",
        "field2":123,
        "field3":false,
        "field4":"4567"
    }
    ```
    {: screen}
    
    è disponibile come un campo che puoi utilizzare per attività di filtro e ricerca:

    * field1 viene analizzato come field1_str di tipo stringa.
    * field2 viene analizzato come field1_int di tipo numero intero.
    * field3 viene analizzato come field3_bool di tipo booleano.
    * field4 viene analizzato come field4_str di tipo stringa.
    
    Il messaggio JSON di esempio è un log che invii al servizio di registrazione. 

    **Nota:** questa funzione è disponibile solo in Elastic 5.1. Questa funzione non è disponibile in Elastic 1.7 per evitare l'interruzione dei dashboard Kibana3.


## Registrazione 
{: #logging}

Vengono utilizzati URL diversi per inviare i log in {{site.data.keyword.Bluemix_notm}} e per analizzare i dati in Kibana.

La seguente tabella elenca il nuovo URL per la regione Stati Uniti Sud:

<table>
  <caption>URL per la regione Stati Uniti Sud</caption>
    <tr>
      <th>Tipo</th>
      <th>ELK 1.7 </th>
	  <th>ELK 5.1 </th>
    </tr>
  <tr>
    <td>URL di inserimento per i log</td>
    <td>logs.opvis.bluemix.net:9091</td>
	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>URL Kibana per analizzare i log</td>
    <td>https://logmet.ng.bluemix.net</td>
	<td>https://logging.ng.bluemix.net</td>
  </tr>
</table>

