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

# Lernprogramm 'Einführung'
{: #getting-started-with-cla}

In diesem Lernprogramm werden Sie schrittweise durch die Ausführung erweiterter Analysetasks mit dem {{site.data.keyword.loganalysislong}}-Service geführt. Sie erfahren, wie Sie Containerprotokolle für eine App, die in einem Kubernetes-Cluster bereitgestellt ist, durchsuchen und analysieren können.
{:shortdesc}

## Vorbereitende Schritte
{: #prereqs}

Erstellen Sie ein [{{site.data.keyword.Bluemix_notm}}-Konto](https://console.bluemix.net/registration/). Ihre Benutzer-ID muss ein Mitglied oder Eigner eines {{site.data.keyword.Bluemix_notm}}-Kontos mit Berechtigungen für die Erstellung von Kubernetes-Clustern, Bereitstellung von Anwendungen in Clustern und Abfragen der Protokolle in {{site.data.keyword.Bluemix_notm}} für die erweiterte Analyse in Kibana sein.

Öffnen Sie eine Terminalsitzung, von der aus Sie den Kubernetes-Cluster verwalten und Apps über die Befehlszeile bereitstellen können. Die Beispiele in diesem Lernprogramm sind für ein Ubuntu Linux-System ausgelegt.

[Installieren Sie das CLI-Plug-in](/docs/containers/cs_cli_install.html#cs_cli_install_steps) in Ihrer lokalen Umgebung, um den {{site.data.keyword.containershort}} über die Befehlszeile verwalten zu können.  



## Schritt 1: App in einem Kubernetes-Cluster bereitstellen
{: #step1}

1. [Erstellen Sie einen Kubernetes-Cluster](/docs/containers/cs_cluster.html#cs_cluster_ui).

2. [Konfigurieren Sie den Clusterkontext](/docs/containers/cs_cli_install.html#cs_cli_configure) in einem Linux-Terminal. Nachdem der Kontext festgelegt ist, können Sie den Kubernetes-Cluster verwalten und die Anwendung im Kubernetes-Cluster bereitstellen.

3. Stellen Sie eine Beispielapp im Kubernetes-Cluster bereit und führen Sie sie aus. [Führen Sie die Schritte für Lerneinheit 1 durch](/docs/containers/cs_tutorials.html#cs_apps_tutorial).

    Die App ist eine 'Hello World'-Node.js-App: 

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

    Wenn die App bereitgestellt ist, wird 'Log Collection' automatisch für alle Protokolleinträge aktiviert, die von der App an 'stdout' (Standardausgabe) und 'stderr' (Standardfehler) gesendet werden. 

    In dieser Beispielapp schreibt die App, wenn Sie sie in einem Browser testen, die folgende Nachricht an 'stdout': `Sample app is listening on port 8080.`

## Schritt 2: Zum Kibana-Dashboard navigieren
{: #step2}

Zum Anzeigen von Protokolldaten für einen Cluster müssen Sie in der öffentlichen Cloudregion, in der der Cluster erstellt wird, auf Kibana zugreifen. 

Beispiel: Navigieren Sie zum Starten von Kibana in der Region 'USA (Süden)' zur folgenden URL: 

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}

    
    
## Schritt 3: Protokolldaten in Kibana analysieren
{: #step3}

1. Auf der Seite **Discover** können Sie die angezeigten Ereignisse sehen. 

    Die Beispielanwendung 'Hello-World' generiert genau ein Ereignis.
    
    Im Abschnitt *Available fields* können Sie die Liste der Felder sehen, die verwendet werden können, um neue Abfragen zu definieren oder die Einträge zu filtern, die in der Tabelle auf dieser Seite aufgelistet sind.
    
    Die folgende Tabelle enthält die allgemeinen Felder, die zum Definieren neuer Suchabfragen verwendet werden können. Außerdem enthält die Tabelle Beispielwerte entsprechend dem Ereignis, das von der Beispielapp generiert wird:
    
     <table>
              <caption>Tabelle 2. Allgemeine Felder für Containerprotokolle </caption>
               <tr>
                <th align="center">Feld</th>
                <th align="center">Beschreibung</th>
                <th align="center">Beispiel</th>
              </tr>
              <tr>
                <td>*docker.container_id_str*</td>
                <td> Der Wert dieses Felds entspricht der GUID des Containers, der die App in einem Pod des Kubernetes-Clusters ausführt.</td>
                <td></td>
              </tr>
              <tr>
                <td>*ibm-containers.region_str*</td>
                <td>Der Wert dieses Felds entspricht der {{site.data.keyword.Bluemix_notm}}-Region, in der der Protokolleintrag erfasst wird.</td>
                <td>us-south</td>
              </tr>
              <tr>
                <td>*kubernetes.container_name_str*</td>
                <td>Der Wert dieses Felds informiert über den Namen des Containers.</td>
                <td>hello-world-deployment</td>
              </tr>
              <tr>
                <td>*kubernetes.host*</td>
                <td>Der Wert dieses Felds informiert über die öffentliche IP-Adresse, die zur Verfügung steht, um über das Internet auf die App zuzugreifen. </td>
                <td>169.47.218.231</td>
              </tr>
              <tr>
                <td>*kubernetes.labels.label_name*</td>
                <td>Die Felder 'Label' sind optional. Sie können 0 oder mehrere Bezeichnungen ("labels") haben. Jede Bezeichnung beginnt mit dem Präfix `kubernetes.labels.`, gefolgt von *label_name*. </td>
                <td>In der Beispielapp werden zwei Bezeichnungen angezeigt: <br>* *kubernetes.labels.pod-template-hash_str* = 3355293961 <br>* *kubernetes.labels.run_str* =	hello-world-deployment  </td>
              </tr>
              <tr>
                <td>*kubernetes.namespace_name_str*</td>
                <td>Der Wert dieses Felds informiert über den Kubernetes-Namensbereich, in dem der Pod ausgeführt wird. </td>
                <td>default</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_id_str*</td>
                <td>Der Wert dieses Felds entspricht der GUID des Pods, in dem der Container ausgeführt wird. </td>
                <td>d695f346-xxxx-xxxx-xxxx-aab0b50f7315</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_name_str*</td>
                <td>Der Wert dieses Felds informiert über den Namen des Pods.</td>
                <td>hello-world-deployment-3xxxxxxx1-xxxxx8</td>
              </tr>
              <tr>
                <td>*message*</td>
                <td>Dies ist die vollständige Nachricht, die von der Anwendung protokolliert wird.</td>
                <td>Sample app is listening on port 8080.</td>
              </tr>
        </table>
    
2. Auf der Seite **Discover** können Sie die Daten filtern.  

    In der Tabelle werden alle Einträge angezeigt, die für die Analyse verfügbar sind. Die aufgelisteten Einträge entsprechen der Suchabfrage, die in der Suchleiste angezeigt wird. Ein Stern (*) ist das Zeichen, das verwendet wird, um alle Einträge innerhalb des Zeitraums anzuzeigen, der für die Seite konfiguriert ist.  
    
    Um beispielsweise die Daten nach dem Kubernetes-Namensbereich zu filtern, ändern Sie die Abfrage in der Suchleiste. Fügen Sie einen Filter auf Grundlage des angepassten Felds *kubernetes.namespace_name_str* hinzu:
    
    1. Wählen Sie im Abschnitt *Verfügbare Felder* das Feld *kubernetes.namespace_name_str* aus. Eine Untergruppe der verfügbaren Werte für das Feld wird angezeigt.    
    
    2. Wählen Sie den Wert **default** aus. Dies ist der Namensbereich, in dem Sie im vorherigen Schritt die Beispielapp bereitgestellt haben.
    
        Nachdem Sie den Wert ausgewählt haben, wird ein Filter in der Suchleiste hinzugefügt und die Tabelle zeigt nur Einträge an, die mit den von Ihnen soeben ausgewählten Kriterien übereinstimmen.     
    
    Sie können das Bearbeitungssymbol des Filters auswählen, um den Namensbereich, nach dem Sie suchen, zu ändern.   
    
    Die folgende Abfrage wird angezeigt:
    
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
    
    Für die Suche nach Einträgen in einem anderen Namensbereich (z. B. *mynamespace1*) ändern Sie die Abfrage:
    
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
    
    Wenn keine Daten angezeigt werden, versuchen Sie, den Zeitfilter zu ändern. Weitere Informationen finden Sie unter [Zeitfilter festlegen](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
    

Weitere Informationen finden Sie unter [Protokolle in Kibana filtern](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).


## Nächste Schritte
{: #next_steps}

Als Nächstes werden Kibana-Dashboards erstellt. Weitere Informationen finden Sie unter [Protokolle in Kibana über ein Dashboard analysieren](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#analize_logs_dashboard).
                                                                                                                      

