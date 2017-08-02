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

# Erweiterte Protokollanalyse mit Kibana
{:#analyzing_logs_Kibana}

In {{site.data.keyword.Bluemix}} können Sie Kibana 5.1, eine quelloffene Analyse- und Visualisierungsplattform, dazu verwenden, Ihre Daten in einer Reihe von Darstellungsarten, wie zum Beispiel Diagrammen und Tabellen, zu überwachen, zu durchsuchen, zu analysieren und zu visualisieren. Verwenden Sie Kibana für erweiterte Analysetasks.
{:shortdesc}

Kibana ist eine browserbasierte Schnittstelle, in der Sie die Daten interaktiv analysieren und Dashboards anpassen können, die Sie dann verwenden können, um Protokolldaten zu analysieren und erweiterte Management-Tasks durchzuführen. Weitere Informationen finden Sie in der Veröffentlichung [Kibana User Guide ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.elastic.co/guide/en/kibana/5.1/index.html "Symbol für externen Link"){: new_window}.

Die Daten, die auf einer Kibana-Seite angezeigt werden, werden durch eine Suche beschränkt. Das Standarddataset wird durch das vorkonfigurierte Indexmuster (Index Pattern) definiert. Zum Filtern der Informationen können Sie neue Suchabfragen hinzufügen und Filter auf das Standarddataset anwenden. Sie können die Suche zur späteren Verwendung speichern. 

Kibana enthält verschiedene Seiten, die Sie zur Analyse Ihrer Protokolle nutzen können:

| Kibana-Seite | Beschreibung |
|-------------|-------------|
| Discover | Auf dieser Seite können Sie Suchen definieren und Ihre Protokolle interaktiv über eine Tabelle und ein Histogramm analysieren. |
| Visualize | Auf dieser Seite können Sie Visualisierungen wie Diagramme und Tabellen erstellen, mit denen Sie Ihre Protokolldaten analysieren und Ergebnisse vergleichen können.  |
| Dashboard | Auf dieser Seite können Sie Ihre Protokolle mithilfe von gespeicherten Visualisierungen und Suchen analysieren.  |
{: caption="Tabelle 1. Kibana-Seiten" caption-side="top"}

**Hinweis:** Sie können nur einen vollständigen Tag gleichzeitig auf der Seite 'Visualize' oder der Seite 'Dashboard' analysieren, obwohl Sie sieben Tage zurückgehen können. Protokolldaten werden standardmäßig drei Tage lang gespeichert. 

| Kibana-Seite | Informationen zum Zeitraum |
|-------------|-------------------------|
| Discover | Datenanalyse über maximal drei Tage. |
| Visualize | Datenanalyse über einen Zeitraum von 24 Stunden. <br> Sie können Protokolldaten für einen angepassten Zeitraum filtern, der nach 24 Stunden abläuft.  |
| Dashboard | Datenanalyse über einen Zeitraum von 24 Stunden. <br> Sie können Protokolldaten für einen angepassten Zeitraum filtern, der nach 24 Stunden abläuft. <br> Der Zeitraum, den Sie über das Zeitauswahlfeld festlegen, wird auf alle Visualisierungen angewendet, die im Dashboard enthalten sind. |
{: caption="Tabelle 2. Informationen zum Zeitraum" caption-side="top"}

Sie können Kibana zum Beispiel wie folgt zum Anzeigen von Informationen zu einer CF-App oder zu einem Container in Ihrem Bereich auf den verschiedenen Seiten verwenden:

## Zum Kibana-Dashboard navigieren
{: #launch_Kibana}

Sie können Kibana auf eine der folgenden Arten starten:

* Über das {{site.data.keyword.loganalysisshort}}-Service-Dashboard

    Sie können Kibana so starten, dass die Daten, die angezeigt werden, Protokolle aus Services in einem angegebenen {{site.data.keyword.Bluemix_notm}}-Bereich aggregieren.
	
	Weitere Informationen finden Sie unter [Vom Dashboard des Log Analysis-Service zu Kibana navigieren](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_log_analysis). 

* Über {{site.data.keyword.Bluemix_notm}}

    Sie können Ihre spezifischen CF-App-Protokolle in Kibana im Kontext dieser spezifischen App starten. Weitere Informationen finden Sie unter [Vom Dashboard einer CF-App zu Kibana navigieren](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_cf_app). 
    
    Sie können Ihre spezifischen Docker-Containerprotokolle in Kibana im Kontext dieser spezifischen Container starten. Dieses Feature gilt nur für Container, die in der {{site.data.keyword.Bluemix_notm}}-verwalteten Cloudinfrastruktur bereitgestellt sind. Weitere Informationen finden Sie unter [Vom Dashboard eines Containers zu Kibana navigieren](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_for_containers). 
    
    Für CF-Apps ruft die Abfrage, die zum Filtern der für die Analyse in Kibana verfügbaren Daten verwendet wird, Protokolleinträge für die Cloud Foundry-Anwendung ab. Die Protokollinformationen, die standardmäßig in Kibana angezeigt werden, beziehen sich sämtlich auf eine einzelne Cloud Foundry-Anwendung und alle zugehörigen Instanzen. 
    
    Für Container ruft die Abfrage, die zum Filtern der für die Analyse in Kibana verfügbaren Daten verwendet wird, Protokolleinträge für alle Instanzen des Containers ab. Die Protokollinformationen, die standardmäßig in Kibana angezeigt werden, beziehen sich sämtlich auf einen einzelnen Container oder eine Containergruppe und alle zugehörigen Instanzen. 
    
    

* Über einen direkten Browser-Link

    Sie können Kibana so starten, dass die Daten, die angezeigt werden, Protokolle aus Services in einem angegebenen {{site.data.keyword.Bluemix_notm}}-Bereich aggregieren.
    
    Die Abfrage, durch die die Daten gefiltert werden, die im Dashboard angezeigt werden, ruft Protokolleinträge für einen Bereich in der {{site.data.keyword.Bluemix_notm}}-Organisation ab. Die Protokollinformationen, die in Kibana angezeigt werden, umfassen Einträge für alle Ressourcen, die innerhalb des Bereichs der {{site.data.keyword.Bluemix_notm}}-Organisation bereitgestellt sind, an der Sie angemeldet sind. 
    
    Weitere Informationen finden Sie unter [Zum Bluemix-Dashboard über einen Web-Browser navigieren](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser).
    
    

## Daten interaktiv analysieren
{: #analyze_discover}

Auf der Seite 'Discover' können Sie neue Suchabfragen definieren und Filter auf einzelne Abfragen anwenden. Die Protokolldaten werden in einer Tabelle und einem Histogramm angezeigt. Mit diesen Visualisierungen können Sie die Daten interaktiv analysieren. Weitere Informationen finden Sie unter [Protokolle in Kibana interaktiv analysieren](analize_logs_interactively.html#analize_logs_interactively).

Sie können Filter für Protokollfelder wie zum Beispiel 'message_type' und 'instance_ID' konfigurieren und einen Zeitraum festlegen. Sie können diese Filter dynamisch aktivieren oder inaktivieren. In der Tabelle und im Histogramm werden die Protokolleinträge angezeigt, die den Abfrage- und Filterkriterien entsprechen, die Sie aktivieren. Weitere Informationen finden Sie unter [Protokolle in Kibana filtern](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs).

## Daten mit einer Visualisierung analysieren
{: #analyze_visualize}
    
Auf der Seite 'Visualize' können Sie neue Suchabfragen und Visualisierungen definieren. Sie haben außerdem die Möglichkeit, gespeicherte Visualisierungen zu öffnen oder eine Visualisierung zu speichern.

Zur Analyse der Daten können Sie Visualisierungen auf der Basis einer vorhandenen Suche oder einer neuen Suche erstellen. Kibana enthält verschiedene Typen von Visualisierungen, wie zum Beispiel Tabellen, Trends und Histogramme, die Sie zur Analyse der Informationen verwenden können. Der Zweck jeder Visualisierung variiert. Einige Visualisierungen zeigen zeilenweise die Ergebnisse einer oder mehrerer Abfragen. Andere Visualisierungen enthalten Dokumente oder angepasste Informationen. Die Daten in einer Visualisierung können fest sein oder sich ändern, wenn eine Suchabfrage aktualisiert wird. Sie können die Visualisierung in eine Webseite einbetten oder zur gemeinsame Nutzung verfügbar machen. 

Weitere Informationen finden Sie unter [Protokolle mit Visualisierungen analysieren](/docs/services/CloudLogAnalysis/kibana/kibana_visualizations.html#kibana_visualizations).

## Daten in einem Dashboard analysieren
{: #analyze_dashboard}

Auf der Seite 'Dashboard' können Sie mehrere Visualisierungen und Suchen gleichzeitig anpassen, speichern und zur gemeinsamen Nutzung verfügbar machen. 

Sie können Visualisierungen im Dashboard hinzufügen, entfernen und neu anordnen. Weitere Informationen finden Sie unter [Protokolle in Kibana über ein Dashboard analysieren](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#analize_logs_dashboard).
    
Nach der Anpassung eines Kibana-Dashboards können Sie die Daten in den Visualisierungen analysieren und zur künftigen Wiederverwendung speichern. Weitere Informationen finden Sie unter [Kibana-Dashboard speichern](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#save).

In Kibana finden Sie darüber hinaus eine Seite **Management**, über die Sie Kibana konfigurieren sowie Suchen, Visualisierungen und Dashboards speichern, löschen, exportieren und importieren können.


