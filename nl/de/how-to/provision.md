---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---



{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Log Analysis-Service bereitstellen
{: #provision}

Sie können den {{site.data.keyword.loganalysisshort}}-Service über die {{site.data.keyword.Bluemix}}-Benutzerschnittstelle oder die Befehlszeile bereitstellen.
{:shortdesc}


## Bereitstellung über die Benutzerschnittstelle
{: #ui}

Führen Sie die folgenden Schritte aus, um eine Instanz des {{site.data.keyword.loganalysisshort}}-Service in {{site.data.keyword.Bluemix_notm}} bereitzustellen:

1. Melden Sie sich an Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.

    Das {{site.data.keyword.Bluemix_notm}}-Dashboard finden Sie unter [http://bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}.
    
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie auf **Katalog**. Die Liste der Services, die unter {{site.data.keyword.Bluemix_notm}} verfügbar sind, wird geöffnet.

3. Wählen Sie die Kategorie **DevOps** aus, um die angezeigte Serviceliste zu filtern.

4. Klicken Sie auf die Kachel **Log Analysis**.

5. Wählen Sie einen Serviceplan aus. Standardmäßig ist der Plan **Lite** festgelegt.

    Weitere Informationen zu Serviceplänen finden Sie unter [Servicepläne](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
6. Klicken Sie auf **Erstellen**, um den {{site.data.keyword.loganalysisshort}}-Service in dem {{site.data.keyword.Bluemix_notm}}-Bereich bereitzustellen, an dem Sie angemeldet sind.
  
 

## Bereitstellung über die Befehlszeilenschnittstelle
{: #cli}

Führen Sie die folgenden Schritte aus, um eine Instanz des {{site.data.keyword.loganalysisshort}}-Service in {{site.data.keyword.Bluemix_notm}} über die Befehlszeile bereitzustellen:

1. [Voraussetzung] Installieren Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle.

   Weitere Informationen finden Sie unter [{{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle installieren](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Fahren Sie mit dem nächsten Schritt fort, wenn die Befehlszeilenschnittstelle bereits installiert ist.
    
2. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an der Region, der Organisation und dem Bereich an, in der/dem Sie den Service bereitstellen möchten. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Führen Sie den Befehl `bx cf create-service` aus, um eine Instanz bereitzustellen.

    ```
	bx cf create-service service_name service_plan service_instance_name
	```
	{: codeblock}
	
	Hierbei gilt Folgendes:
	
	* service_name ist der Name des Service, also **ibmLogAnalysis**.
	* service_plan ist der Name des Serviceplans. Eine Liste der Pläne finden Sie unter [Servicepläne] (/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	* service_instance_name ist der Name, den Sie für die neue von Ihnen erstellte Serviceinstanz verwenden möchten.
	
	Weitere Informationen zum Befehl cf finden Sie unter [cf create-service] (/docs/cli/reference/cfcommands/index.html#cf_create-service).

	Beispiel: Führen Sie zum Erstellen einer Instanz des Service {{site.data.keyword.loganalysisshort}} mit einem Lite-Plan den folgenden Befehl aus:
	
	```
	bx cf create-service ibmLogAnalysis standard my_logging_svc
	```
	{: codeblock}
	
4. Stellen Sie sicher, dass der Service ordnungsgemäß erstellt wurde. Führen Sie den folgenden Befehl aus:

    ```	
	bx cf services
	```
	{: codeblock}
	
	Die Ausgabe sieht nach Ausführung des Befehls wie folgt aus:
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_logging_svc                ibmLogAnalysis           standard                                        create succeeded
	```
	{: screen}

	



