---

copyright:
  years: 2017

lastupdated: "2017-05-23"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Protokolle in Kibana für eine App analysieren, die in einem Kubernetes-Cluster bereitgestellt ist
{: #kibana_tutorial_1}

Führen Sie erste Schritte mit Kibana aus. Hier erfahren Sie, wie Sie Containerprotokolle für eine App, die in einem Kubernetes-Cluster bereitgestellt ist, durchsuchen und analysieren können.
{:shortdesc}

**Hinweis:** Zur vollständigen Durchführung dieses Lernprogramms müssen Sie auch alle Lernprogramme ausführen, die mit den einzelnen Schritten verknüpft sind.

## Voraussetzungen
{: #prereq}

1. Werden Sie Mitglied oder Eigner eines Bluemix-Kontos mit Berechtigungen für das Erstellen von Kubernetes-Clustern, das Bereitstellen von Anwendungen in Clustern und das Abfragen der Protokolle in {{site.data.keyword.Bluemix_notm}} für die erweiterte Analyse in Kibana. 

2. Führen Sie eine Terminalsitzung durch, von der aus Sie den Kubernetes-Cluster verwalten und Apps über die Befehlszeile bereitstellen können. Die Beispiele in diesem Lernprogramm sind für ein Ubuntu Linux-System ausgelegt.

3. [Installieren Sie das CLI-Plug-in](/docs/containers/cs_cli_install.html#cs_cli_install_steps) in Ihrem Ubuntu-System, um den {{site.data.keyword.containershort}} über die Befehlszeile verwalten zu können.  


## Schritt 1: Kubernetes in Bluemix betriebsbereit machen
{: #step1}

Führen Sie die folgenden Schritte aus:

1. [Erstellen Sie einen Kubernetes-Cluster](/docs/containers/cs_cluster.html#cs_cluster_ui).

2. Konfigurieren Sie den Cluster-Kontext.  

    Beispiel: Führen Sie zum Konfigurieren des Kontextes in einem Linux-Terminal die Schritte in [CLI (Befehlszeilenschnittstelle) zur Ausführung mit kubectl für Cluster für IBM Bluemix Container Service konfigurieren](/docs/containers/cs_cli_install.html#cs_cli_configure) aus. 

Nachdem der Kontext festgelegt ist, können Sie den Kubernetes-Cluster verwalten und die Anwendung im Kubernetes-Cluster bereitstellen.

## Schritt 2: App im Kubernetes-Cluster bereitstellen
{: #step2}

Stellen Sie eine Beispielapp im Kubernetes-Cluster bereit und führen Sie sie aus. [Führen Sie die Schritte für Lerneinheit 1 durch](/docs/containers/cs_tutorials.html#cs_apps_tutorial).

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
{: screen}

Wenn die App bereitgestellt ist, wird die Protokollerfassung automatisch für alle Protokolleinträge aktiviert, die von der App an 'stdout' (Standardausgabe) und 'stderr' (Standardfehler) gesendet werden. 

In dieser Beispielapp schreibt die App, wenn Sie sie in einem Browser testen, die folgende Nachricht an 'stdout': `Sample app is listening on port 8080.`


## Schritt 3: Protokolldaten in Kibana analysieren
{: #step3}

1. Starten Sie Kibana über einen Browser. 

    Zum Anzeigen von Protokolldaten für einen Cluster müssen Sie in der öffentlichen Cloudregion, in der der Cluster erstellt wird, auf Kibana zugreifen. 
    
    ```
	https://logging.ng.bluemix.net/ 
	```
	{: codeblock}
    
    Anschließend starten Sie über einen Browser die URL, um Kibana zu öffnen.
    
2. Auf der Seite **Discover** können Sie die angezeigten Ereignisse sehen. 

    Die Beispielanwendung 'Hello-World' generiert genau ein Ereignis.
    
    ![Discover-Seite in Kibana](images/sampleapp_2.gif "Discover page in Kibana")
    
    Im Abschnitt *Available fields* können Sie die Liste der Felder sehen, die verwendet werden können, um neue Abfragen zu definieren oder die Einträge zu filtern, die in der Tabelle auf dieser Seite aufgelistet sind.
    
    Die folgende Tabelle enthält die allgemeinen Felder, der zum Definieren neuer Suchabfragen verwendet werden können. Außerdem enthält die Tabelle Beispielwerte entsprechend dem Ereignis, das von der Beispielapp generiert wird:
    
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
    
    
    
3. Filtern von Daten auf der Seite *Discover*.  

    In der Tabelle werden alle Einträge angezeigt, die für die Analyse verfügbar sind. Die aufgelisteten Einträge entsprechen der Suchabfrage, die in der Suchleiste angezeigt wird. Verwenden Sie einen Stern (*), um alle Einträge im Zeitraum anzuzeigen, die für die Seite konfiguriert sind.
    Um beispielsweise die Daten nach dem Kubernetes-Namensbereich zu filtern, ändern Sie die Abfrage in der Suchleiste. Fügen Sie einen Filter auf Grundlage des angepassten Felds *kubernetes.namespace_name_str* hinzu:
    
    1. Wählen Sie im Abschnitt **Available fields** das Feld *kubernetes.namespace_name_str* aus. Eine Untergruppe der verfügbaren Werte für das Feld wird angezeigt.    
    
    2. Wählen Sie den Standardwert aus. Dies ist der Namensbereich, in dem Sie im vorherigen Schritt die Beispielapp bereitgestellt haben.
    
        Nachdem Sie den Wert ausgewählt haben, wird ein Filter in der Suchleiste hinzugefügt und die Tabelle zeigt nur Einträge an, die mit den von Ihnen soeben ausgewählten Kriterien übereinstimmen.     
    
    ![Filter für Suche für den Standard-Kubernetes-Namensbereich](images/sampleapp_k4_1.gif "Filter für Suche für den Standard-Kubernetes-Namensbereich")
    
    Sie können das Bearbeitungssymbol des Filters auswählen, um den Namensbereich, nach dem Sie suchen, zu ändern.   
    
    ![Aktionen, die für einen Filter verfügbar sind](images/sampleapp_k4_1.gif "Aktionen, die für einen Filter verfügbar sind")
    
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
	{: screen}
    
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
	{: screen}
    
    Wenn keine Daten angezeigt werden, versuchen Sie, den Zeitfilter zu ändern. Weitere Informationen finden Sie unter [Zeitfilter festlegen](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
    

Weitere Informationen finden Sie unter [Protokolle in Kibana filtern](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).

