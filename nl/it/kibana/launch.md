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


# Passaggio al dashboard Kibana
{: #launch}

Puoi avviare Kibana dal servizio {{site.data.keyword.loganalysisshort}}, dalla IU {{site.data.keyword.Bluemix}} o direttamente da un browser web.
{:shortdesc}

Per le applicazioni CF e i contenitori Docker distribuiti a un'infrastruttura cloud gestita da {{site.data.keyword.Bluemix_notm}}, puoi avviare Kibana da {{site.data.keyword.Bluemix_notm}} per visualizzare e analizzare i dati nel contesto nella risorsa da cui avvii Kibana. Ad esempio, puoi eseguire l'avvio ai log della tua specifica applicazione CF in Kibana, nel contesto di quella specifica applicazione.
    
Per tutte le risorse cloud come un contenitore Docker distribuito a un'infrastruttura Kubernetes, puoi avviare Kibana da un link browser diretto o dal dashboard del servizio {{site.data.keyword.loganalysisshort}} per visualizzare i dati di log aggregati dai servizi in uno spazio {{site.data.keyword.Bluemix_notm}} fornito. La query che viene utilizzata per filtrare i dati visualizzati nel dashboard richiama le voci di log per uno spazio nell'organizzazione
{{site.data.keyword.Bluemix_notm}}. Le informazioni di log visualizzate da Kibana includono i record per
tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso. 

La seguente tabella elenca alcune risorse cloud e i metodi di navigazione supportati per avviare Kibana:

<table>
<caption>Tabella 1. Elenco di risorse e metodi di navigazione supportati. </caption>
  <tr>
    <th>Risorsa</th>
	<th>Passaggio al dashboard Kibana dal dashboard del servizio {{site.data.keyword.loganalysisshort}}</th>
    <th>Passaggio al dashboard Kibana dal dashboard Bluemix</th>
    <th>Passaggio al dashboard Kibana da un browser web</th>
  </tr>
  <tr>
    <td>Applicazione CF</td>
	<td>Sì</td>
    <td>Sì</td>
    <td>Sì</td>
  </tr>  
  <tr>
    <td>Contenitore distribuito in un cluster Kubernetes</td>
	<td>Sì</td>
    <td>No</td>
    <td>Sì</td>
  </tr>  
  <tr>
    <td>Contenitore distribuito in un'infrastruttura cloud gestita da {{site.data.keyword.Bluemix_notm}}</td>
	<td>Sì</td>
    <td>Sì</td>
    <td>Sì</td>
  </tr>  
</table>

Per ulteriori informazioni sulle applicazioni Kibana, vedi la [ ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/kibana/5.1/index.html "Icona link esterno"){: new_window}.
    

##  Passaggio a Kibana dal dashboard del servizio Analisi di log
{: #launch_Kibana_from_log_analysis}

La query che viene utilizzata per filtrare i dati visualizzati in Kibana richiama le voci di log per tale spazio nell'organizzazione {{site.data.keyword.Bluemix_notm}}. 
	
Le informazioni di log visualizzate da Kibana includono i record per
tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso.

Completa la seguente procedura per avviare Kibana dal dashboard del servizio {{site.data.keyword.loganalysisshort}}:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul servizio {{site.data.keyword.loganalysisshort}} dal dashboard {{site.data.keyword.Bluemix_notm}}. 
    
2. Seleziona la scheda **Gestito** nella IU {{site.data.keyword.Bluemix_notm}}.

3. Fai clic su **AVVIA**. Viene aperto il dashboard Kibana.

Per impostazione predefinita, la pagina **Rileva** viene caricata con il modello di indice predefinito selezionato al momento dell'impostazione del filtro negli ultimi 15 minuti. 

Se la pagina Rileva non mostra alcuna voce di log, modifica il selezionatore di tempo. Per maggiori informazioni, vedi [Configurazione di un filtro temporale](filter_logs.html#set_time_filter).

	
	
##  Passaggio a Kibana da un browser web.
{: #launch_Kibana_from_browser}

La query che viene utilizzata per filtrare i dati visualizzati in Kibana richiama le voci di log per tale spazio nell'organizzazione {{site.data.keyword.Bluemix_notm}}. 
	
Le informazioni di log visualizzate da Kibana includono i record per
tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso.

Completa la seguente procedura per avviare Kibana da un browser:

1. Apri un browser Web e avvia Kibana. Accedi quindi all'interfaccia utente Kibana.
    
    Ad esempio, la seguente tabella elenca l'URL che devi utilizzare per avviare Kibana nella regione degli Stati uniti del sud:
      
    <table>
          <caption>Tabella 1. URL per avviare Kibana per regione</caption>
           <tr>
            <th>Regione</th>
            <th>URL</th>
          </tr>
          <tr>
            <td>Stati Uniti Sud</td>
            <td>https://logging.ng.bluemix.net/ </td>
          </tr>
    </table>
	
	Viene aperta la pagina Rileva in Kibana.
	
2. Seleziona il modello di indice per lo spazio {{site.data.keyword.Bluemix_notm}} da cui desideri visualizzare e analizzare i dati di log.

    1. Fai clic su **default-index**.
	
	2. Seleziona il modello di indice per lo spazio. Il formato del modello di indice è il seguente:
	
	    ```
	    [logstash-Space_ID-]YYYY.MM.DD 
	    ```
        {screen}
	
	    dove *Space_ID* è il GUID dello spazio {{site.data.keyword.Bluemix_notm}} in cui desideri visualizzare e analizzare i dati di log. 
	
Se la pagina Rileva non mostra alcuna voce di log, modifica il selezionatore di tempo. Per maggiori informazioni, vedi [Configurazione di un filtro temporale](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).


	
##  Passaggio a Kibana dal dashboard di una applicazione CF
{: #launch_Kibana_from_cf_app}

La query che viene utilizzata per filtrare i dati visualizzati in Kibana richiama le voci di log per l'applicazione CF {{site.data.keyword.Bluemix_notm}} da cui avvii Kibana.

Per visualizzare i log di un'applicazione Cloud Foundry in Kibana, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul contenitore o sul nome dell'applicazione dal dashboard {{site.data.keyword.Bluemix_notm}}. 
    
2. Apri la scheda di log nella IU {{site.data.keyword.Bluemix_notm}}.

    Per le applicazioni CF, fai clic su **Log** nella barra di navigazione. 
    Viene aperta la scheda dei log.  

3. Fai clic su **Vista avanzata**. Viene aperto il dashboard Kibana.

    Per impostazione predefinita, la pagina **Rileva** viene caricata con il modello di indice predefinito selezionato al momento dell'impostazione del filtro negli ultimi 30 secondi. La query di ricerca viene configurata per corrispondere a tutte le voci della tua applicazione CF.

    Se la pagina Rileva non mostra alcuna voce di log, modifica il selezionatore di tempo. Per maggiori informazioni, vedi [Configurazione di un filtro temporale](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).


##  Passaggio a Kibana dal dashboard di un contenitore
{: #launch_Kibana_for_containers}

Questo metodo si applica solo ai contenitori distribuiti nell'infrastruttura cloud gestita da {{site.data.keyword.Bluemix_notm}}.

La query che viene utilizzata per filtrare i dati visualizzati in Kibana richiama le voci di log per il contenitore da cui avvii Kibana.

Per visualizzare i log di un contenitore Docker in Kibana, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul contenitore dal dashboard {{site.data.keyword.Bluemix_notm}}. 
    
2. Apri la scheda di log nella IU {{site.data.keyword.Bluemix_notm}}.

    Per i contenitori distribuiti nell'infrastruttura cloud gestita da {{site.data.keyword.IBM_notm}}, seleziona **Monitoraggio e log** nella barra di navigazione e quindi fai clic sulla scheda **Registrazione**. 
    
    Viene aperta la scheda dei log.  

3. Fai clic su **Vista avanzata**. Viene aperto il dashboard Kibana.

    Per impostazione predefinita, la pagina **Rileva** viene caricata con il modello di indice predefinito selezionato al momento dell'impostazione del filtro negli ultimi 30 secondi. La query di ricerca viene configurata per corrispondere a tutte le voci del contenitore Docker.

    Se la pagina Rileva non mostra alcuna voce di log, modifica il selezionatore di tempo. Per maggiori informazioni, vedi [Configurazione di un filtro temporale](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).

	



