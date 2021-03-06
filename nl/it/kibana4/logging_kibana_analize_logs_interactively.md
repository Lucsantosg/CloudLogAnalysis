---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, logging

subcollection: cloudloganalysis

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}

# Analisi dei log interattiva in Kibana
{:#kibana_analize_logs_interactively}

Nella pagina Rileva, puoi visualizzare e analizzare i tuoi log {{site.data.keyword.Bluemix}} interattivamente. Puoi definire le query di ricerca per filtrare i dati utilizzando il linguaggio di query Lucene. Per ogni query ricerca, puoi applicare i filtri per restringere le voci disponibili per l'analisi. Puoi salvare un ricerca per un riutilizzo futuro.
{:shortdesc}

In {{site.data.keyword.Bluemix_notm}}, per impostazione predefinita, la serie di dati visualizzata nella pagina Rileva quando avvii Kibana dalla IU {{site.data.keyword.Bluemix_notm}} è configurata per mostrare solo le voci per il contenitore o l'applicazione CF (Cloud Foundry) da cui hai avviato Kibana. 

La seguente tabella mostra la query predefinita per ogni risorsa quando avvii Kibana da {{site.data.keyword.Bluemix_notm}}:

| Risorsa | Query di ricerca predefinita Kibana |
|---------------|---------------|
| Applicazione CF   | `application_id:<app_GUID>`    |
| Singolo contenitore Docker | `instance:<instance_GUID>`    |
| Gruppo di contenitori con 2 istanze | `instance:<instance_GUID> OR instance:<instance_GUID>` |
{: caption="Tabella 1. Ricerche query predefinite" caption-side="top"}

**Nota:** 
* Ogni volta che avvii Kibana dalla IU {{site.data.keyword.Bluemix_notm}}, i dati che puoi visualizzare corrispondono alla query predefinita per impostazione predefinita e che si basa sul modello di indice.
* Nella pagina Rileva viene visualizzato un massimo di 500 voci, che corrisponde alle voci più recenti. Puoi modificare questo valore nella pagina Impostazioni.

Quando avvii Kibana da un browser, i dati visualizzati nella pagina Rileva includono tutti i dati di log disponibili nello spazio in cui hai eseguito l'accesso. La pagina non è limitata a contenitori o applicazioni specifici.

La pagina Rileva include un istogramma e una tabella che puoi personalizzare in modo da poter analizzare i dati interattivamente. 

Puoi eseguire ognuna delle seguenti attività per personalizzare la tabella nella pagina Rileva:

| Attività | Descrizione | 
|------|-------------|
| [Aggiungere una colonna di campo](/docs/services/CloudLogAnalysis/kibana4?topic=cloudloganalysis-kibana_analize_logs_interactively#kibana_discover_add_fields_to_table) | Aggiungere i campi per visualizzare i dati specifici necessari per l'analisi invece del messaggio completo. |
| [Riorganizzare una colonna di campo](/docs/services/CloudLogAnalysis/kibana4?topic=cloudloganalysis-kibana_analize_logs_interactively#kibana_discover_rearrange_fields_in_table) | Spostare la posizione di un campo nella tabella nella posizione che desideri. |
| [Visualizzare una voce](/docs/services/CloudLogAnalysis/kibana4?topic=cloudloganalysis-kibana_analize_logs_interactively#kibana_discover_view_entry_in_table) | Espandere una voce nella tabella per visualizzare i dettagli della voce analizzata per il campo o come JSON. |
| [Rimuovere una colonna di campo](/docs/services/CloudLogAnalysis/kibana4?topic=cloudloganalysis-kibana_analize_logs_interactively#kibana_discover_remove_fields_from_table) | Rimuovere un campo quando non è più necessario nella vista delle analisi. |
| [Ordinare le voci per il valore di un campo indicizzato](/docs/services/CloudLogAnalysis/kibana4?topic=cloudloganalysis-kibana_analize_logs_interactively#kibana_discover_sort_by_table) | Riordinare le voci per analisi più semplici. |
| [Aggiornare automaticamente i dati](/docs/services/CloudLogAnalysis/kibana4?topic=cloudloganalysis-kibana_analize_logs_interactively#kibana_discover_view_refresh_interval) | Aggiornare i dati visualizzati nella tabella con le ultime voci. Per impostazione predefinita, l'aggiornamento è **DISATTIVO**. |
{: caption="Tabella 2. Attività per personalizzare una tabella" caption-side="top"}

<br>

La seguente figura mostra un esempio di una tabella nella pagina Rileva:

![Pagina Rileva in Kibana](images/k4_discover_page.jpg "Pagina Rileva in Kibana")

Puoi definire altre ricerche. Quando definisci una nuova ricerca, i dati visualizzati nell'istogramma e nella tabella vengono automaticamente aggiornati.

Per definire una nuova ricerca, utilizza la query di ricerca predefinita come tuo punto di partenza e quindi rifinisci la ricerca eseguendo le seguente attività:

* Applica i filtri del campo per rifinire la serie di dati che puoi visualizzare. Puoi attivare/disattivare ogni filtro, bloccarlo nella pagina, abilitarlo o disabilitarlo se necessario e configurarlo per includere o escludere il valore. 

    **Suggerimento:** se non puoi trovare un campo nell'*Elenco campi* che ti aspetti di visualizzare o alcune delle lenti di ingrandimento per i campi elencati sono disabilitate nella pagina Rileva, ricarica l'elenco dei campi aggiornando il modello di indice nella pagina Rileva. 

    Ad esempio, se la tua applicazione CF ha più istanze, potresti voler analizzare i dati di un'istanza specifica. Puoi definire un filtro del campo per il valore dell'ID dell'istanza specifico che desideri analizzare. 
    
* Personalizza il *Selezionatore di tempo* per i dati basati sul tempo. Puoi definire un intervallo di tempo assoluto per una query, uno relativo o scegliere da una serie di valori predefiniti. 

Dopo aver configurato la ricerca che definisce la sottoserie di dati che desideri analizzare, puoi salvarla per un riutilizzo successivo.

Puoi eseguire ognuna delle seguenti attività con le ricerche che definisci nella pagina Rileva:

| Attività | Descrizione |
|------|-------------|
| Salvare una ricerca | Salvare la ricerca per un riutilizzo successivo.  |
| Eliminare una ricerca | Eliminare una ricerca quando non è più necessaria. |
| Esportare una ricerca | Esportare una ricerca per condividerla.  |
| Ricaricare una ricerca  | Caricare una ricerca esistente per analizzare nuovamente una serie di dati. |
| Aggiornare i dati di una ricerca | Configurare l'aggiornamento automatico dei dati visualizzati tramite la ricerca.  |
| Importare una ricerca | Importare una ricerca.  |
{: caption="Tabella 3. Attività per lavorare con le ricerche" caption-side="top"}

<br>

Puoi inoltre esaminare le statistiche nella pagina Rileva:
* Puoi visualizzare le statistiche per il campo. 
* Puoi visualizzare le statistiche nell'istogramma per `@timestamp` che hai configurato.

Per maggiori informazioni, vedi [Visualizzazione delle statistiche dei dati del campo](/docs/services/CloudLogAnalysis/kibana4?topic=cloudloganalysis-kibana_analize_logs_interactively#kibana_discover_view_fields_stats).

**Nota:** i dati visualizzati nella tabella e nell'istogramma sono statici. Per continuare a visualizzare le ultime voci, devi impostare un intervallo di aggiornamento. 


## Aggiunta di colonne di campo alla tabella
{: #kibana_discover_add_fields_to_table}

La tabella disponibile per analizzare i dati nella pagina Rileva, include i seguenti campi per impostazione predefinita:
* **time:** questo campo indica quando una voce è stata acquisita e registrata in {{site.data.keyword.Bluemix_notm}}.
* **_source:** questo campo include i dati originali della voce.

Puoi aggiungere una colonna di campo alla tabella scegliendo una delle seguenti opzioni:

* Aggiungi una colonna di campo dall'Elenco campi disponibile nella pagina.

    1. Nella pagina Rileva, identifica il campo nella sezione `Campi selezionati`.
    2. Passa con il mouse su un campo nell'Elenco campi.
    
        ![Aggiungi un campo dalla vista tabella](images/k4_add_field_column_hover.jpg "Aggiungi un campo dalla vista tabella")
    
    3. Per aggiungere un campo, fai clic su **Aggiungi**.
    
 * Aggiungi una colonna di campo dalla vista tabella di una voce espansa.

    1. Espandi una voce nella tabella.
    2. Nella vista Tabella, identifica il campo che desideri aggiungere.
    
        ![Aggiungi un campo dalla vista tabella](images/k4_add_field_column.jpg "Aggiungi un campo dalla vista tabella")
    
    3. Fai clic sull'icona **Attiva/disattiva colonna nella tabella** ![Attiva/disattiva colonna nella tabella](images/k4_toggle_field_icon.jpg).
    

**Nota:** quando aggiungi una colonna di campo alla tabella per la prima volta, la colonna di campo *_source* visualizzata nella tabella è nascosta. Il campo *_source* mostra il valore di ogni campo per ogni voce di log. Per visualizzare altri valori del campo per una voce di log nella tabella dopo aver aggiunto una colonna alla tabella, vedi la scheda vista tabella o la scheda JSON di ogni voce.

Ad esempio, se aggiungi il campo *application_id* alla tabella, la tabella cambia per presentarsi così:

![Visualizzazione della tabella dopo l'aggiunta di un nuovo campo](images/k4_add_field_filter_new_table_look.jpg "Visualizzazione della tabella dopo l'aggiunta di un nuovo campo")


## Aggiornamento automatico dei dati
{: #kibana_discover_view_refresh_interval}

Per impostazione predefinita, in {{site.data.keyword.Bluemix_notm}}, il periodo di *Aggiornamento automatico* è impostato su **DISATTIVO** e i dati che puoi visualizzare in Kibana corrispondono agli ultimi 15 minuti da quando hai avviato Kibana. I 15 minuti corrispondono al filtro temporale preconfigurato. Puoi scegliere di impostare un periodo di tempo differente. 

Completa la seguente procedura per impostare un periodo di *Aggiornamento automatico*:

1. Nella barra del menu della pagina Rileva, fai clic sul Selezionatore di tempo ![Selezionatore di tempo](images/k4_time_picker_icon.jpg "Selezionatore di tempo").

2. Seleziona il pulsante di aggiornamento automatico ![Pulsante di aggiornamento automatico](images/k4_auto_refresh_icon.jpg "Pulsante di aggiornamento automatico").

3. Scegli un intervallo di aggiornamento.

    ![Opzioni per impostare un tempo di aggiornamento automatico](images/k4_change_autorefresh.jpg "Opzioni per impostare un tempo di aggiornamento automatico")


Puoi mettere in pausa l'intervallo di aggiornamento facendo clic sul pulsante di pausa ![Pulsante di pausa](images/k4_auto_refresh_pause_icon.jpg "Pausa") 


## Identificazione dei dati visualizzati nella pagina Rileva
{: #k4_identify_data}

Quando utilizzi Kibana per analizzare i log {{site.data.keyword.Bluemix_notm}}, i dati che visualizzi dipendono da come avvii Kibana, dal modello di indice configurato e dai filtri e dalla query personalizzata che potresti aver applicato.

Considera le seguenti informazioni per identificare i dati disponibili nella tabella e nell'istogramma della pagina Rileva:

1. Controlla il modello dell'indice nella pagina Impostazioni.

    Il modello di indice definisce la query di ricerca applicata per impostazione predefinita per mostrare le voci nelle tue pagine Kibana. Per impostazione predefinita, il modello di indice è preconfigurato e impostato su tutti i dati disponibili in uno spazio. Ad esempio,

    * Se avvii Kibana dall'IU {{site.data.keyword.Bluemix_notm}}, dalla sezione *Log* delle pagine dell'IU di una risorsa specifica come un contenitore o un'applicazione CF (Cloud Foundry), il modello di indice applicato include tutte le voci disponibili nello spazio.
    
    * Se avvii Kibana da un browser, il modello dell'indice applicato include tutte le voci disponibili nello spazio visualizzato da Kibana in cui sei collegato.
        
2. Controlla la query nella pagina Rileva.  

    La query visualizzata nella pagina Rileva viene utilizzata per filtrare le voci disponibili per impostazione predefinita per l'analisi. Ad esempio:

    * Se immetti una stringa nella barra di ricerca, la query esegue la scansione di tutti i campi per tale stringa.
    
    * Se la query è impostata su `application_id:<GUID>` dove *GUID* è l'ID di un'applicazione CF, le voci che puoi visualizzare corrispondono a tutte le voci disponibili per tale applicazione CF nello spazio configurato nel modello di indice.
    
    * Se la query è impostata su `instance_id:<GUID>` dove *GUID* è l'ID di un'istanza del contenitore, le voci che puoi visualizzare corrispondono a tutte le voci disponibili per tale contenitore nello spazio configurato nel modello di indice.
    
    * Se la query è impostata su `instance_id:<GUID> AND instance_id:<GUID>` dove *GUID* è l'ID di un'istanza del contenitore, le voci che puoi visualizzare corrispondono a tutte le voci disponibili per tale gruppo di contenitori nello spazio configurato nel modello di indice.
   
    * Se la query è impostata su `*`, i dati sono una serie di tutte le voci disponibili nello spazio configurato nel modello di indice.
    
    * Se la query è impostata su `application_id:<GUID> AND message:"MY_search_text"` dove *GUID* è l'ID di un'applicazione CF e *My_search_text* è la stringa che desideri ricercare, le voci che puoi visualizzare corrispondono a tutte le voci che includono *My_search_text* nel campo del messaggio per tali voci dell'applicazione CF disponibili nello spazio configurato nel modello di indice.
    
3. Controlla i filtri del campo applicati alla tua query nella pagina Rileva.

    Puoi definire 0 o più filtri del campo per attivare le voci basate sul valore del campo. Ad esempio, se è abilitato un filtro del campo, le voci che puoi visualizzare corrispondono alla voci in cui il valore per tale campo corrisponde.
    

## Ordinare le voci per il valore di un campo indicizzato 
{: #kibana_discover_sort_by_table}

Puoi ordinare solo le voci nella tabella per i campi indicizzati.

Per trovare quali campi sono indicizzati, completa la seguente procedura:

1. Nella pagina Rileva, fai clic sull'icona Configura ![Icona Configura](images/k4_configure_icon.jpg "Icona Configura"). Viene visualizzata la sezione in cui puoi filtrare i campi nella sezione **Campi selezionati** della pagina.

    ![Sezione di configurazione per visualizzare i campi con specifici attributi](images/k4_reset_filters.jpg "Sezione di configurazione per visualizzare i campi con specifici attributi")
    
2. Per identificare i campi che vengono indicizzati, seleziona **Sì** per il campo di ricerca **Indicizzato**.

    ![Attributo indicizzato](images/k4_reset_filters_indexed_options.jpg "Attributo indicizzato")
    
 Viene visualizzato l'elenco dei campi indicizzati.
 
 ![Elenco di campi indicizzati](images/k4_list_indexed_fields.jpg "Elenco di campi indicizzati")
  	
 
Per ordinare le voci in una tabella per i valori di un campo indicizzato, completa la seguente procedura: 

1. Passa con il mouse sul nome del campo nella tabella per cui desideri ordinare i dati. Vengono visualizzati i vari pulsanti di azione.
2. Fai clic sul pulsante di ordinamento del campo per cui desideri ordinare i dati. Fai clic sull'icona di ordinamento del campo una seconda volta per invertire l'ordine di ordinamento.

**Nota:** quando ordini per un campo di tempo, per impostazione predefinita le voci sono ordinate in ordine cronologico inverso. Le voci più recenti vengono visualizzate per prime.


## Riorganizzazione delle colonne di campo nella tabella
{: #kibana_discover_rearrange_fields_in_table}

Puoi riorganizzare le colonne di campo nella tabella. Passa con il mouse sull'intestazione della colonna che desideri spostare e fai clic sul pulsante **Sposta colonna a sinistra** o **Sposta colonna a destra**.
<br>
![Sposta campo nella tabella](images/k4_add_field_filter_new_table_look.jpg "Sposta campo nella tabella")


## Ricaricamento dell'elenco dei campi
{: #kibana_discover_view_reload_fields}

Completa la seguente procedura per ricaricare l'elenco dei campi visualizzati in Kibana:

1. Seleziona la pagina Impostazioni.

    Quando selezioni la pagina Impostazioni, viene aperta la scheda *Indici*.
   
2. Seleziona il modello di indice per visualizzare tutti i campi e i tipi di core associati dei campi come registrato da Elasticsearch. 

3. Fai clic sul pulsante *Ricarica elenco campi* ![Ricarica elenco campi](images/k4_reload_field_list_icon.jpg "Ricarica elenco campi") per ricaricare i campi del modello di indice. 

L'elenco dei campi viene aggiornato.


## Rimozione delle colonne di campo dalla tabella
{: #kibana_discover_remove_fields_from_table}

Per rimuovere i campi dalla tabella, completa la seguente procedura:

1. Nella tabella, identifica il campo che desideri rimuovere dalla vista tabella.
2. Fai clic su **Rimuovi colonna**.
    
    ![Rimuovi un campo dalla vista tabella](images/k4_remove_field_column.jpg "Rimuovi un campo dalla vista tabella")


## Visualizzazione di una voce nella tabella
{: #kibana_discover_view_entry_in_table}

Per visualizzare i dati di una voce nella tabella, fai clic sul pulsante di espansione ![Icona pulsante di espansione](images/k4_expand_icon.jpg "Icona pulsante di espansione") della voce che desideri analizzare. 

![Tabella nella pagina Rileva in Kibana](images/k4_table_discover.jpg "Tabella nella pagina Rileva in Kibana") 	

Successivamente, scegli una delle seguenti opzioni per visualizzare i dati:

* Per visualizzare i dati in un formato tabella, fai clic su **Tabella**. Puoi visualizzare il valore di ogni campo disponibile per l'analisi in un formato tabella. Per ogni campo, puoi inoltre disporre di pulsanti di filtro e di un pulsante di attivazione.
* Per visualizzare i dati nel formato Json, fai clic su **JSON**.

## Visualizzazione delle statistiche dei dati del campo
{: #kibana_discover_view_fields_stats}

Nella pagina Rileva, puoi visualizzare le statistiche di ogni campo nell'*Elenco campi* e nell'*istogramma*. 

Puoi visualizzare le seguenti informazioni nell'Elenco Campi:
* Quante voci nella tabella contengono un campo particolare.
* Quali sono i primi 5 valori.
* Quale percentuale di voci contiene ogni valore.

Puoi visualizzare le seguenti informazioni nell'istogramma:
* Il numero di voci in un intervallo di tempo.

Per visualizzare le statistiche nell'istogramma, fai clic su una data/ora per visualizzare le statistiche per tale periodo. Ad esempio, 

![Visualizza le statistiche su un campo nell'istogramma](images/k4_see_stats_on_histogram.jpg "Visualizza le statistiche su un campo negli istogrammi")
   	
 	
Per visualizzare le statistiche di un campo nell'Elenco campi, fai clic sul nome. Ad esempio,

![Visualizza le statistiche su un campo nell'elenco Campi](images/k4_stats_field_list.jpg "Visualizza le statistiche su un campo nell'elenco Campi")


