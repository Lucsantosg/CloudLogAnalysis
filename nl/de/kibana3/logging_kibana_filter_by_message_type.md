---

copyright:
  years: 2015, 2018

lastupdated: "2018-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Protokolle der Cloud Foundry-App nach Nachrichtentyp in Kibana filtern
{: #logging_kibana_message_type_filter}

Zeigen Sie {{site.data.keyword.Bluemix_notm}}-Anwendungsprotokolle im Kibana-Dashboard an und filtern Sie sie nach Nachrichtentyp. Sie können über die Registerkarte **Protokolle** für Ihre Cloud Foundry-App auf das Kibana-Dashboard zugreifen. 
{:shortdesc}

Führen Sie die folgenden Schritte aus, um die Cloud Foundry-Anwendungsprotokolle nach Nachrichtentyp im Kibana-Dashboard zu filtern:

1. Greifen Sie auf die Registerkarte **Protokolle** Ihrer Cloud Foundry-App zu. 

    1. Klicken Sie im **Apps**-Dashboard von {{site.data.keyword.Bluemix_notm}} auf den App-Namen.
    2. Klicken Sie auf die Registerkarte **Protokolle**. 
    
    Die Protokolle für Ihre App werden angezeigt.

2. Greifen Sie auf das Kibana-Dashboard für Ihre App zu. Klicken Sie auf **Erweiterte Ansicht** ![Link für erweiterte Ansicht](images/logging_advanced_view.jpg "Link für erweiterte Ansicht"). Das Kibana-Dashboard wird angezeigt.

3. Klicken Sie im Fenster **ALL EVENTS** auf den Rechtspfeil, um alle Felder anzuzeigen. 

    ![Fenster 'ALL EVENTS' mit Rechtspfeilsymbol](images/logging_all_events_no_fields.jpg "Fenster 'ALL EVENTS' mit Rechtspfeilsymbol")

4. Wählen Sie im Fenster **Fields** die Option **message_type** aus, um die Komponente anzuzeigen, mit der die einzelnen Protokolleinträge im Fenster **ALL EVENTS** generiert wurden.

    ![Fenster 'ALL EVENTS' mit ausgewählten Feld 'message_type'](images/logging_message_type.png "Fenster 'ALL EVENTS' mit ausgewählten Feld 'message_type'")

5. Klicken Sie im Fenster **ALL EVENTS** auf die Zeile mit dem Protokollereignis, um die Details zu diesem Ereignis anzuzeigen. Wählen Sie ein Ereignis aus, das den Nachrichtentyp (**message_type**) anzeigt, den Sie filtern möchten.

    ![Fenster 'ALL EVENTS' mit Details zu einem ausgewählten Protokollereignis](images/logging_message_type_add_filter.png "Fenster 'ALL EVENTS' mit Details zu einem ausgewählten Protokollereignis")

6. Fügen Sie einen Filter hinzu, um Informationen zu einem Nachrichtentyp ein- oder auszuschließen. 

    * Um einen Filter hinzuzufügen, der Informationen zu einem Nachrichtentyp einschließt, klicken Sie in der Zeile 'message_type' in der Tabelle auf das **Lupensymbol** ![Lupensymbol](images/logging_magnifying_glass.jpg "Lupensymbol"). 
    
           ![Filterbedingung für das Feld 'message_type'](images/logging_message_type_filter.png "Filterbedingung für das Feld 'message_type'")
    
    * Um einen Filter hinzuzufügen, der Informationen zu einem Nachrichtentyp einschließt, klicken Sie in der Zeile 'message_type' in der Tabelle auf da **Ausschlusssymbol** ![Ausschlusssymbol](images/logging_exclusion_icon.png "Ausschlusssymbol"). 
    
    Eine neue Filterbedingung wird zum Kibana-Dashboard hinzugefügt.

7. Wiederholen Sie optional den vorherigen Schritt, um einen Filter für andere Nachrichtentypen hinzuzufügen. Eine vollständige Liste von Nachrichtentypen finden Sie unter [Protokollformat](../logging_view_kibana3.html#kibana_log_format_cf).

9. Speichern Sie das Dashboard.    
        
    Wenn Sie mit dem Erstellen der Filter fertig sind, klicken Sie auf das **Speichersymbol** ![Speichersymbol](images/logging_save.jpg "Speichersymbol") und geben Sie einen Namen für das Dashboard ein. 
      
    **Hinweis:** Wenn Sie versuchen, das Dashboard unter einem Namen mit Leerzeichen zu speichern, kann es nicht gespeichert werden. Geben Sie einen Namen ohne Leerzeichen ein und klicken Sie auf das Symbol für **Speichern**.
    
    ![Dashboard-Namen speichern](images/logging_save_dashboard.jpg "Dashboard-Namen speichern").

Sie haben ein Dashboard erstellt, mit dem Protokolleinträge nach Nachrichtentyp gefiltert werden können. Sie können das gespeicherte Dashboard jederzeit laden, indem Sie auf das **Ordnersymbol** ![Ordnerymbol](images/logging_folder.jpg "Ordnersymbo") klicken und anhand des Namens das gewünschte Dashboard auswählen.
