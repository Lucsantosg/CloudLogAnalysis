---

copyright:
  years: 2017

lastupdated: "2017-05-23"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Analizza i log in Kibana per un'applicazione distribuita in un cluster Kubernetes
{: #kibana_tutorial_1}

Inizia a lavorare con Kibana. Impara come eseguire ricerche nei log del contenitore e come analizzarli per un'applicazione distribuita in un cluster Kubernetes.
{:shortdesc}

**Nota:** per completare questa esercitazione, completa le esercitazioni che sono collegate dai diversi passi.

## Prerequisiti
{: #prereq}

1. Essere un membro o un proprietario di un account Bluemix con autorizzazioni per creare i cluster Kubernetes, distribuire le applicazioni nei cluster ed eseguire query dei log in {{site.data.keyword.Bluemix_notm}} per l'analisi avanzata in Kibana. 

2. Avere una sessione terminale dalla quale poter gestire il cluster Kubernetes e distribuire le applicazioni dalla riga di comando. Gli esempi in questa esercitazione vengono forniti per un sistema Linux Ubuntu.

3. [Installa i plugin CLI](/docs/containers/cs_cli_install.html#cs_cli_install_steps) nel tuo sistema Ubuntu per gestire {{site.data.keyword.containershort}} dalla riga di comando. 


## Passo 1: diventa operativo con Kubernetes in Bluemix
{: #step1}

Completa la seguente procedura:

1. [Crea un cluster Kubernetes](/docs/containers/cs_cluster.html#cs_cluster_ui).

2. Configura il contesto del cluster. 

    Ad esempio, per configurare il contesto in un terminale Linux, completa la procedura in [Configurazione della CLI per eseguire i comandi kubectl sui cluster per il servizio IBM Bluemix Container](/docs/containers/cs_cli_install.html#cs_cli_configure).

Dopo che il contesto è stato impostato, puoi gestire il cluster Kubernetes e distribuire l'applicazione nel cluster Kubernetes.

## Passo 2: distribuisci un'applicazione nel cluster Kubernetes
{: #step2}

Distribuisci ed esegui un'applicazione di esempio nel cluster Kubernetes. [Completa la procedura per la lezione 1](/docs/containers/cs_tutorials.html#cs_apps_tutorial).

L'applicazione è un'applicazione Node.js Hello World:

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

Quando l'applicazione viene distribuita, la raccolta dei log viene abilitata automaticamente per qualsiasi voce di log che viene inviata dall'applicazione a stdout (output standard) e stderr (errore standard). 

In questa applicazione di esempio, quando verifichi la tua applicazione in un browser, l'applicazione scrive in stdout il seguente messaggio: `L'applicazione di esempio è in ascolto sulla porta 8080.`


## Passo 3: analizza i dati di log in Kibana
{: #step3}

1. Avvia Kibana da un browser. 

    Per analizzare i dati di log per un cluster, devi accedere a Kibana nella regione di cloud pubblico dove viene creato il cluster. 
    
    ```
	https://logging.ng.bluemix.net/ 
	```
	{: codeblock}
    
    Quindi, da un browser, avvia l'URL per aprire Kibana.
    
2. Nella pagina **Rileva**, guarda gli eventi visualizzati. 

    L'applicazione Hello-World di esempio genera un singolo evento.
    
    ![Pagina Rileva in Kibana](images/sampleapp_2.gif "Pagina Rileva in Kibana")
    
    Nella sezione *Campi disponibili*, puoi vedere l'elenco di campi che puoi utilizzare per definire nuove query o filtrare le voci elencate nella tabella visualizzata nella pagina.
    
    La seguente tabella elenca i campi comuni che puoi usare per definire le nuove query di ricerca. La tabella include anche dei valori di esempio che corrispondono all'evento generato dall'applicazione di esempio:
    
     <table>
              <caption>Tabella 2. Campi comuni per i log del contenitore </caption>
               <tr>
                <th align="center">Campo</th>
                <th align="center">Descrizione</th>
                <th align="center">Esempio</th>
              </tr>
              <tr>
                <td>*docker.container_id_str*</td>
                <td> Il valore di questo campo corrisponde al GUID del contenitore che esegue l'applicazione in un pod del cluster Kubernetes.</td>
                <td></td>
              </tr>
              <tr>
                <td>*ibm-containers.region_str*</td>
                <td>l valore di questo campo corrisponde alla regione {{site.data.keyword.Bluemix_notm}} dove viene raccolta la voce di log.</td>
                <td>us-south</td>
              </tr>
              <tr>
                <td>*kubernetes.container_name_str*</td>
                <td>Il valore di questo campo fornisce informazioni sul nome del contenitore.</td>
                <td>hello-world-deployment</td>
              </tr>
              <tr>
                <td>*kubernetes.host*</td>
                <td>Il valore di questo campo fornisce informazioni sull'IP pubblico disponibile per accedere all'applicazione da Internet. </td>
                <td>169.47.218.231</td>
              </tr>
              <tr>
                <td>*kubernetes.labels.label_name*</td>
                <td>I campi di etichetta sono facoltativi. Puoi avere 0 o più etichette. Ciascuna etichetta inizia con il prefisso `kubernetes.labels.` seguito da *label_name*. </td>
                <td>Nell'applicazione di esempio, puoi vedere due etichette: <br>* *kubernetes.labels.pod-template-hash_str* = 3355293961 <br>* *kubernetes.labels.run_str* =	hello-world-deployment  </td>
              </tr>
              <tr>
                <td>*kubernetes.namespace_name_str*</td>
                <td>Il valore di questo campo indica lo spazio dei nomi Kubernetes dove è in esecuzione il pod. </td>
                <td>default</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_id_str*</td>
                <td>Il valore di questo campo corrisponde al GUI del pod dove viene eseguito il contenitore. </td>
                <td>d695f346-xxxx-xxxx-xxxx-aab0b50f7315</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_name_str*</td>
                <td>Il valore di questo campo indica il nome del pod.</td>
                <td>hello-world-deployment-3xxxxxxx1-xxxxx8</td>
              </tr>
              <tr>
                <td>*message*</td>
                <td>Questo è il messaggio completo registrato dall'applicazione.</td>
                <td>L'applicazione di esempio è in ascolto sulla porta 8080.</td>
              </tr>
        </table>
    
    
    
3. Filtra i dati nella pagina *Rileva*.  

    Nella tabella, puoi vedere tutte le voci che sono disponibili per l'analisi. Le voci elencate corrispondono alla query di ricerca visualizzata nella barra *Ricerca*. Utilizza un asterisco (*) per visualizzare tutte le voci nel periodo di tempo configurato per la pagina.

    Ad esempio, per filtrare i dati in base allo spazio dei nomi Kubernetes, modifica la query della barra *Ricerca*. Aggiungi un filtro basato sul campo personalizzato *kubernetes.namespace_name_str*:
    
    1. Nella sezione **Campi disponibili**, seleziona il campo *kubernetes.namespace_name_str*. Viene visualizzato un sottoinsieme dei valori disponibili per il campo.    
    
    2. Seleziona il valore **default**. Questo è lo spazio dei nomi dove hai distribuito in un passo precedente l'applicazione di esempio.
    
        Dopo che hai selezionato il valore, alla *Barra di ricerca* viene aggiunto un filtro e la tabella visualizza solo le voci che corrispondono ai criteri che hai appena selezionato.     
    
    ![Filtro per la ricerca per lo spazio dei nomi Kubernetes predefinito](images/sampleapp_k4_1.gif "Filtro per la ricerca per lo spazio dei nomi Kubernetes predefinito")
    
    Puoi selezionare il simbolo di modifica del filtro per modificare il nome dello spazio dei nomi che cerchi.   
    
    ![Azioni disponibili per un filtro](images/sampleapp_k4_1.gif "Azioni disponibili per un filtro")
    
    Viene visualizzata la seguente query:
    
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
    
    Per cercare le voci in uno spazio dei nomi differente come *mynamespace1*, modifica la query:
    
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
    
    Se non riesci a vedere alcun dato, prova a modificare il filtro temporale. Per maggiori informazioni, vedi [Configurazione di un filtro temporale](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
    

Per maggiori informazioni, vedi [Filtro dei log in Kibana](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).

