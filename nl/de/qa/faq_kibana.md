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


# Kibana - Häufig gestellte Fragen
{: #faq_kibana}

Im Folgenden finden Sie Antworten auf häufig gestellte Fragen zur Verwendung der {{site.data.keyword.Bluemix}}-Protokollfunktionen. {:shortdesc}

* [Was kann ich tun, wenn auf der Seite 'Discover' in Kibana keine Daten angezeigt werden?](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_no_data_discover_kibana)
* [Was kann ich tun, wenn ich eine Ausnahmebedingung bei der Authentifizierung erhalte?](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_no_data_dashboard_kibana)
* [Wie kann ich Kibana 3 starten?](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_kibana3)
* [Warum werden Fragezeichensymbole (?) für Felder auf der Kibana-Seite 'Discover' angezeigt?](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_kibana_question)
* [Wenn ich versuche, das Standardindexmuster zu ändern, wird Fehler 403 angezeigt.](/docs/services/CloudLogAnalysis/qa/faq_kibana.html#error_403)

## Was kann ich tun, wenn auf der Seite 'Discover' in Kibana keine Daten angezeigt werden?
{: #logging_qa_no_data_discover_kibana}

Es können folgende Situationen entstehen, in denen keine Daten in Kibana angezeigt werden:

1. Beim Starten von Kibana werden keine Daten auf der Seite 'Discover' angezeigt. Sie erhalten die folgende Nachricht: **No results found.**. 
2. Sie arbeiten mit der Seite 'Discover' in Kibana. Nach kurzer Zeit erhalten Sie die Nachricht **No results found**, wenn Sie versuchen, eine Task in Kibana auszuführen. 

Um das Problem zu beheben, führen Sie die folgenden Schritte aus:

1. Überprüfen Sie den *Time Picker* (Zeitauswahlfeld), der auf der Seite 'Discover' festgelegt ist, und geben Sie einen höheren Wert für den Zeitraum an. 

    **Hinweis**: Standardmäßig ist der *Time Picker* in {{site.data.keyword.Bluemix_notm}} so eingestellt, dass Daten für die letzten 15 Minuten angezeigt werden.

    Weitere Informationen zum Einstellen des *Time Picker* finden Sie unter [Zeitfilter festlegen](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
       
2. Klicken Sie auf die Lupe, die sich in der Suchleiste der Seite *Discover* befindet. Die Seitendaten werden auf der Basis der Standardsuchabfrage aktualisiert.

    Alternativ können Sie für den Zeitraum auch *Auto refresh* einstellen.

    **Hinweis:** In {{site.data.keyword.Bluemix_notm}} ist das Zeitintervall für automatisches Aktualisieren (*Auto-refresh*) standardmäßig inaktiviert (**OFF**).
    
    Informationen zum Aktivieren des Zeitintervalls finden Sie unter [Daten automatisch aktualisieren](/docs/services/CloudLogAnalysis/kibana/analize_logs_interactively.html#discover_view_refresh_interval).



## Was kann ich tun, wenn ich eine Ausnahmebedingung bei der Authentifizierung erhalte?
{: #logging_qa_no_data_dashboard_kibana}

Wenn keine Daten in Ihren Visualisierungen auf einer Dashboard-Seite angezeigt werden und Sie die Fehlernachricht **Error: Exception Authorization** erhalten, überprüfen Sie Ihre Berechtigungen zur Anzeige von Daten in den einzelnen Visualisierungen.

Beachten Sie Folgendes:
Sie können eine oder mehrere Visualisierungen in einer Dashboard-Seite konfigurieren. Wenn die Dashboard-Seite die Erfassung der angezeigten Daten über Visualisierungen anfordert, wird nur eine solche Anforderung für alle Visualisierungen ausgegeben. Wenn Ihnen die Berechtigung zur Anzeige der Daten einer der Visualisierungen fehlt, schlägt die Anforderung insgesamt fehl.

Um das Problem zu beheben, führen Sie die folgenden Schritte aus:

1. Ermitteln Sie die Visualisierungen, für die Sie nicht berechtigt sind.

    1. Klicken Sie auf das *Stiftsymbol* einer Visualisierung auf der Seite *Dashboard*. Die Visualisierung wird auf der Seite *Visualize* geöffnet. Alternativ können Sie eine Visualisierung auf der Seite *Visualize* laden. 
    2. Überprüfen Sie, ob Sie Daten anzeigen können.
    
    Wiederholen Sie diese Schritte für jede Visualisierung.

2. Fordern Sie bei Ihrem Cloudadministrator den gewünschten Zugriff auf Daten in Visualisierungen an.

3. Erstellen Sie eine neue Seite 'Dashboard', die die Visualisierungen ausschließt, für die Sie nicht berechtigt sind, während Sie Zugriff auf die Daten in den Visualisierungen erhalten, die das Problem verursachen. 

    Wenn Sie das Dashboard gemeinsam nutzen, löschen Sie die Visualisierungen nicht, da sich dies auf andere Teammitglieder auswirkt, die dasselbe Dashboard verwenden.

## Wie kann ich Kibana 3 starten?
{: #logging_qa_kibana3}

**Hinweis:** Kibana 3 ist veraltet.

Sie können Kibana 3 über einen Browser starten.

Führen Sie den folgenden Schritt aus, um Kibana 3 über einen Browser zu starten:

1. Öffnen Sie die Seite [https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net), um sich an der Kibana-Benutzerschnittstelle anzumelden. 
    
2. Wählen Sie die Version von Kibana aus, die Sie verwenden möchten, um Ihre Protokolle zu analysieren.
    * Wählen Sie die Registerkarte **Kibana 4** aus, um mit Kibana 4 zu arbeiten. Die Seite 'Discover' wird geöffnet. Weitere Informationen finden Sie unter [Protokolle in Kibana interaktiv analysieren](/docs/services/CloudLogAnalysis/qa/faq_kibana.html#logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Wählen Sie die Registerkarte **Kibana 3** aus, um mit Kibana 3 zu arbeiten. Das Standard-Kibana-Dashboard wird geöffnet. Weitere Informationen zur Verwendung von Kibana 3 für die Analyse Ihrer Protokolle finden Sie unter [Protokolle in Kibana 3 analysieren (Veraltet)](docs/monitor_log/kibana3/logging_view_kibana3.html#analyzing_logs_Kibana3). Weitere Informationen zum Anpassen eines Kibana 3-Dashboards finden Sie in [diesem Blogbeitrag ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/ "Symbol für externen Link"){: new_window}.
     

## Warum werden Fragezeichensymbole (?) für Felder auf der Kibana-Seite 'Discover' angezeigt?
{: #logging_qa_kibana_question}

Wenn Sie die Seite 'Discover' in Kibana öffnen, werden möglicherweise Fragezeichen (`?`) für Felder im Abschnitt für verfügbare Felder anstelle des Zeichens `t` angezeigt. Wenn Sie die Feldliste erneut laden, wird der Typ der Felder analysiert und die Zeichen `?` werden durch das Zeichen `t` ersetzt. Weitere Informationen finden Sie unter [Feldliste neu laden](/docs/services/CloudLogAnalysis/kibana/analize_logs_interactively.html#discover_view_reload_fields). 


## Wenn ich versuche, das Standardindexmuster zu ändern, wird Fehler 403 angezeigt. 
{: #error_403}

Das Standardindexmuster kann nicht geändert werden.  

Wenn Sie versuchen ein neues Indexmuster als neuen Standard festzulegen, wird der folgende Fehler angezeigt: `Config: Error 403 Forbidden`


