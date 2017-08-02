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

# Protokolle in der Bluemix-Benutzerschnittstelle analysieren
{: #analyzing_logs_bmx_ui}

In {{site.data.keyword.Bluemix}} können Sie Protokolle über die Registerkarte 'Protokolle' anzeigen, filtern und analysieren, die für jede Cloud Foundry-App und jeden Docker-Container verfügbar ist, die/der in der von {{site.data.keyword.IBM_notm}} verwalteten Infrastruktur ausgeführt wird.
{:shortdesc}

##  Zu den Protokollen einer Cloud Foundry-App navigieren
{: #launch_logs_tab_bmx_ui_cf}

Führen Sie die folgenden Schritte aus, um die Bereitstellungs- oder Laufzeitprotokolle einer Cloud Foundry-App anzuzeigen:

1. Klicken Sie im Dashboard 'Apps' auf den Namen Ihrer Cloud Foundry-App. 
    
2. Klicken Sie auf der Seite 'App-Details' auf **Protokolle**.
    
    Auf der Registerkarte **Protokolle** können Sie die neuesten Protokolle für Ihre App anzeigen oder die Protokolle per Tailing in Echtzeit verfolgen. Darüber hinaus können Sie Protokolle nach Komponente (Protokolltyp), nach App-Instanz-ID und nach Fehler filtern.
    
Standardmäßig enthalten die Protokolle, die für die Analyse über die {{site.data.keyword.Bluemix_notm}}-Konsole zur Verfügung stehen, Daten für die letzten 24 Stunden.

**Tipp:** Informationen zur Analyse von Daten für einen angepassten Zeitraum, der den letzten 24 Stunden vorausgeht, finden Sie unter [Erweiterte Protokollanalyse mit Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana). 





##  Zu den Protokollen eines Docker-Containers navigieren, der in Bluemix verwaltet wird
{: #launch_logs_tab_bmx_ui_containers}

Führen Sie die folgenden Schritte aus, um die Bereitstellungs- oder Laufzeitprotokolle eines Docker-Containers anzuzeigen, der in der {{site.data.keyword.IBM_notm}}-verwalteten Cloudinfrastruktur bereitgestellt ist:

1. Klicken Sie im Dashboard 'Apps' auf einen einzelnen Container oder eine Containergruppe. 
    
2. Klicken Sie auf der Seite 'App-Details' auf **Überwachung und Protokolle**.

3. Wählen Sie die Registerkarte **Protokollierung** aus.
    
    Auf der Registerkarte **Protokollierung** können Sie die neuesten Protokolle für Ihren Container anzeigen oder die Protokolle per Tailing in Echtzeit verfolgen. 
	
	
	

## Protokollformat für CF-App-Protokolle
{: #log_format_cf}

Die Protokolle für {{site.data.keyword.Bluemix_notm}}-Cloud Foundry-Apps werden in einem festen Format angezeigt, ähnlich dem folgenden Muster:

<code><var class="keyword varname">Komponente</var>/<var class="keyword varname">Instanz-ID</var>/<var class="keyword varname">Nachricht</var>/<var class="keyword varname">Zeitmarke</var></code>

Jeder Protokolleintrag enthält die folgenden Felder:

| Feld | Beschreibung |
|-------|-------------|
| Zeitmarke | Die Zeit der Protokollanweisung. Die Zeitmarke wird millisekundengenau definiert. |
| Komponente | Die Komponente, die das Protokoll erstellt. Eine Liste der verschiedenen Komponenten finden Sie unter [Protokollquellen für CF-Apps](cfapps/logging_cf_apps.html#logging_bluemix_cf_apps_log_sources). <br> Auf jeden Komponententyp folgt ein Schrägstrich und eine Ziffer, die die Anwendungsinstanz angibt. Die Ziffer 0 ist der ersten Instanz zugeordnet, die Ziffer 1 der zweiten Instanz usw. |
| Nachricht | Die Nachricht, die von der Komponente ausgegeben wird. Die Nachricht variiert abhängig vom Kontext. |
{: caption="Tabelle 1. CF-App-Protokolleintragsfelder" caption-side="top"}


## Protokollformat für Containerprotokolle
{: #log_format_containers}

Die Protokolle für Container werden in einem festen Format angezeigt, ähnlich dem folgenden Muster:

<code><var class="keyword varname">Zeitmarke</var>/<var class="keyword varname">Maschine</var>/<var class="keyword varname">Nachricht</var>  </code>

Jeder Protokolleintrag enthält die folgenden Felder:

| Feld | Beschreibung |
|-------|-------------|
| Datum/Zeit | Die Zeit der Protokollanweisung. Die Zeitmarke wird millisekundengenau definiert. |
| Maschine | Der Name des Hosts, auf dem der Container aktiv ist. |
| Nachricht | Die Nachricht, die ausgegeben wird. Die Nachricht variiert abhängig vom Kontext. |
{: caption="Tabelle 2. Docker-Container-Protokolleintragsfelder" caption-side="top"}

