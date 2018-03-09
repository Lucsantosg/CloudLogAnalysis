---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Lernprogramm 'Einführung'
{: #getting-started-with-cla}

In diesem Lernprogramm werden Ihnen die ersten Schritte für die Arbeit mit dem {{site.data.keyword.loganalysislong}}-Service in {{site.data.keyword.Bluemix}} gezeigt.
{:shortdesc}

## Zielsetzungen
{: #objectives}

* Den {{site.data.keyword.loganalysislong}}-Service in einem Bereich bereitstellen.
* Die Befehlszeile für die Verwaltung von Protokollen einrichten.
* Berechtigungen für einen Benutzer einrichten, damit dieser Protokolle in einem Bereich anzeigen kann.
* Kibana starten, das Open-Source-Tool, das zur Anzeige von Protokollen verwendet werden kann.


## Vorbereitende Schritte
{: #prereqs}

Sie müssen über eine Benutzer-ID verfügen, die ein Mitglied oder Eigner eines {{site.data.keyword.Bluemix_notm}}-Kontos ist. Um eine {{site.data.keyword.Bluemix_notm}}-Benutzer-ID zu erhalten, wechseln Sie zu [Registrierung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/registration/){:new_window}

Dieses Lernprogramm gibt Anweisungen zur Bereitstellung und Arbeit mit dem {{site.data.keyword.loganalysisshort}}-Service in der Region "USA (Süden)".


## Schritt 1: Den {{site.data.keyword.loganalysisshort}}-Service bereitstellen
{: #step1}

**Hinweis:** Sie stellen eine Instanz des {{site.data.keyword.loganalysisshort}}-Service in einem Cloud Foundry (CF)-Bereich bereit. Pro Bereich benötigen Sie nur eine Instanz des Service. Der {{site.data.keyword.loganalysisshort}}-Service kann nicht auf Kontoebene bereitgestellt werden. 

Führen Sie die folgenden Schritte aus, um eine Instanz des {{site.data.keyword.loganalysisshort}}-Service in {{site.data.keyword.Bluemix_notm}} bereitzustellen:

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an: [http://bluemix.net ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}.  

2. Wählen Sie die Region, Organisation und den Bereich aus, in dem der {{site.data.keyword.loganalysisshort}}-Service bereitgestellt werden soll.  

3. Klicken Sie auf **Katalog**. Die Liste der Services, die unter {{site.data.keyword.Bluemix_notm}} verfügbar sind, wird geöffnet.

4. Wählen Sie die Kategorie **DevOps** aus, um die angezeigte Serviceliste zu filtern.

5. Klicken Sie auf die Kachel **Log Analysis**.

6. Wählen Sie einen Serviceplan aus. Standardmäßig ist der Plan **Lite** festgelegt.

    Weitere Informationen zu Serviceplänen finden Sie unter [Servicepläne](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
7. Klicken Sie auf **Erstellen**, um den {{site.data.keyword.loganalysisshort}}-Service in dem {{site.data.keyword.Bluemix_notm}}-Bereich bereitzustellen, an dem Sie angemeldet sind.




## Schritt 2: [Optional] Den Serviceplan für den {{site.data.keyword.loganalysisshort}}-Service ändern
{: #step2}

Wenn Sie ein größeres Suchkontingent, Langzeitspeicherung für Protokolle oder beides benötigen, können Sie den Plan für Ihre {{site.data.keyword.loganalysisshort}}-Serviceinstanz über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder durch Ausführen des Befehls `bx cf update-service` ändern, sodass diese Funktionen aktiviert werden. 

Sie können den Serviceplan jederzeit aktualisieren oder reduzieren.

Weitere Informationen finden Sie unter [{{site.data.keyword.loganalysisshort}}-Servicepläne](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

**HINWEIS:** Das Ändern des Plans in einen Zahlungsplan ist kostenpflichtig.

Um den Serviceplan über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle zu ändern, führen Sie die folgenden Schritte aus:

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an: [http://bluemix.net ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}.  

2. Wählen Sie die Region, Organisation und den Bereich aus, in dem der {{site.data.keyword.loganalysisshort}}-Service verfügbar ist.  

3. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-*Dashboard* auf die {{site.data.keyword.loganalysisshort}}-Serviceinstanz. 
    
4. Wählen Sie die Registerkarte **Plan** im {{site.data.keyword.loganalysisshort}}-Dashboard aus.

    Daraufhin werden Informationen zu Ihrem aktuellen Plan angezeigt.
	
5. Wählen Sie einen neuen Plan aus, um Ihren Plan zu aktualisieren oder zu reduzieren. 

6. Klicken Sie auf **Speichern**.



## Schritt 3: Ihre lokale Umgebung für die Arbeit mit dem {{site.data.keyword.loganalysisshort}}-Service einrichten
{: #step3}


Der {{site.data.keyword.loganalysisshort}}-Service beinhaltet eine Befehlszeilenschnittstelle (CLI), die Sie zur Verwaltung von Protokollen in 'Log Collection' (die Komponente für die Langzeitspeicherung) verwenden können. 

Sie können das {{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}}-Plug-in verwenden, um den Status des Protokolls anzuzeigen, um Protokolle herunterzuladen und um die Protokollaufbewahrungsrichtlinie zu konfigurieren. 

Die Befehlszeilenschnittstelle bietet verschiedene Arten von Hilfe: erweiterte Hilfe zu den CLI- und unterstützten Befehlen sowie Hilfe zur Verwendung von Befehlen und Unterbefehlen.

Führen Sie die folgenden Schritte aus, um die {{site.data.keyword.loganalysisshort}}-Befehlszeilenschnittstelle über das {{site.data.keyword.Bluemix_notm}}-Repository zu installieren:

1. Installieren Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle.

   Weitere Informationen finden Sie unter [{{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle installieren](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).

2. Installieren Sie das Plug-in für {{site.data.keyword.loganalysisshort}}. Führen Sie den folgenden Befehl aus:

    ```
    bx plugin install logging-cli -r Bluemix
    ```
    {: codeblock}
 
3. Überprüfen Sie, ob das {{site.data.keyword.loganalysisshort}}-Plug-in installiert wurde.
  
    Führen Sie beispielsweise den folgenden Befehl aus, um die Liste der installierten Plug-ins anzuzeigen:
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    Die Ausgabe sieht wie folgt aus:
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}




## Schritt 4: Berechtigungen für einen Benutzer einrichten, damit dieser Protokolle anzeigen kann
{: #step4}

Um die Aktionen in {{site.data.keyword.loganalysisshort}} zu steuern, die ein Benutzer ausführen darf, können Sie einem Benutzer Rollen und Richtlinien zuweisen. 

In {{site.data.keyword.Bluemix_notm}} gibt es zwei Typen von Sicherheitsberechtigungen, die die Aktionen steuern, die Benutzer bei der Arbeit mit dem {{site.data.keyword.loganalysisshort}}-Service ausführen können:

* Cloud Foundry (CF)-Rollen: Sie erteilen einem Benutzer eine CF-Rolle, um die Berechtigungen des Benutzers für die Anzeige von Protokollen in einem Bereich zu definieren.
* IAM-Rollen: Sie erteilen einem Benutzer eine IAM-Richtlinie, um die Berechtigungen des Benutzers für die Anzeige von Protokollen in der Kontodomäne sowie zur Verwaltung der in 'Log Collection' gespeicherten Protokolle zu definieren. 


Führen Sie die folgenden Schritte aus, um einem Benutzer Berechtigungen zur Anzeige von Protokollen in einem Bereich zu erteilen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://bluemix.net ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste auf **Verwalten > Konto > Benutzer**. 

    Im Fenster *Benutzer* wird eine Liste mit Benutzern und den entsprechenden E-Mail-Adressen für das aktuell ausgewählte Konto angezeigt.
	
3. Wenn der Benutzer ein Mitglied des Kontos ist, wählen Sie den Benutzernamen aus der Liste aus oder klicken Sie im Menü *Aktionen* auf **Benutzer verwalten**.

    Wenn der Benutzer kein Mitglied des Kontos ist, finden Sie unter [Benutzer einladen](/docs/iam/iamuserinv.html#iamuserinv) Informationen zum entsprechenden Vorgehen in diesem Fall.

4. Wählen Sie **Cloud Foundry-Zugriff** und anschließend die Organisation aus.

    Die in dieser Organisation verfügbaren Bereiche werden aufgelistet.

5. Wählen Sie den Bereich aus, in dem Sie den {{site.data.keyword.loganalysisshort}}-Service bereitgestellt haben. Anschließend wählen Sie aus der Menüaktion **Bereichsrolle bearbeiten** aus.

6. Wählen Sie *Prüfer* aus. 

    Sie können eine oder mehrere Bereichsrollen auswählen. Alle folgenden Rollen ermöglichen einem Benutzer die Anzeige von Protokollen: *Manager*, *Entwickler* und *Prüfer*
	
7. Klicken Sie auf **Rolle speichern**.


Weitere Informationen finden Sie unter [Berechtigungen erteilen](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account).



## Schritt 5: Kibana starten
{: #step5}

Zum Anzeigen und Analysieren von Protokolldaten müssen Sie in der öffentlichen Cloudregion, in der die Protokolldaten verfügbar sind, auf Kibana zugreifen. 


Um Kibana in der Region "USA (Süden)" zu starten, öffnen Sie einen Web-Browser und geben Sie die folgende URL ein:

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}


Weitere Informationen zum Starten von Kibana in anderen Regionen finden Sie unter [Von einem Web-Browser zu Kibana navigieren](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser).

**Hinweis:** Wenn Sie Kibana starten und die Nachricht *bearer token not valid* (Bearer-Token ungültig) erhalten, überprüfen Sie Ihre Berechtigungen für den Bereich. Diese Nachricht weist darauf hin, dass Ihre Benutzer-ID nicht über die Berechtigungen zur Anzeige von Protokollen verfügt.
    

## Nächste Schritte 
{: #next_steps}

Generieren Sie Protokolle. Benutzen Sie dazu eines der folgenden Lernprogramme:

* [Protokolle in Kibana für eine App analysieren, die in einem Kubernetes-Cluster bereitgestellt ist](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs){:new_window} 

    In diesem Lernprogramm werden die Schritte gezeigt, die erforderlich sind, um das folgende End-to-End-Szenario umzusetzen: einen Cluster bereitstellen, den Cluster für das Senden von Protokollen an den {{site.data.keyword.loganalysisshort}}-Service in {{site.data.keyword.Bluemix_notm}} konfigurieren, eine App im Cluster bereitstellen und Kibana zum Anzeigen und Filtern von Containerprotokollen für diesen Cluster verwenden.     
    
* [Protokolle in Kibana für eine Cloud Foundry-App analysieren](/docs/tutorials/application-log-analysis.html#generate-access-and-analyze-application-logs){:new_window}                                                                                                            

    In diesem Lernprogramm werden die Schritte gezeigt, die erforderlich sind, um das folgende End-to-End-Szenario umzusetzen: eine Python Cloud Foundry-Anwendung bereitstellen, unterschiedliche Protokolltypen generieren und Kibana für die Anzeige, Suche und Analyse von CF-Protokollen verwenden.
   








