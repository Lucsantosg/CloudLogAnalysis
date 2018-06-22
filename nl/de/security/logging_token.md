---

copyright:
  years: 2017, 2018

lastupdated: "2018-04-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Protokollierungstoken abrufen
{: #logging_token}

Rufen Sie ein Protokollierungstoken ab, um Protokolle an den {{site.data.keyword.loganalysisshort}}-Service zu senden. 
{:shortdesc}


## Protokollierungstoken zum Senden von Protokollen an einen Bereich über die {{site.data.keyword.loganalysisshort}}-Befehlszeilenschnittstelle abrufen 
{: #logging_token_la_cloud_cli}

Führen Sie die folgenden Schritte aus, um das Protokollierungstoken abzurufen, mit dem Sie Protokolle an den {{site.data.keyword.loganalysisshort}}-Service senden können:

1. Installieren Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle.

   Weitere Informationen finden Sie unter [{{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle herunterladen und installieren](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Fahren Sie mit dem nächsten Schritt fort, wenn die Befehlszeilenschnittstelle bereits installiert ist.
    
2. Melden Sie sich bei einer Region, Organisation und bei einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Führen Sie den folgenden Befehl aus:

    ```
	bx logging token-get
	```
	{: codeblock}

Die Ausgabe gibt das Protokollierungstoken zurück.


## Protokollierungstoken zum Senden von Protokollen an einen Bereich mithilfe der {{site.data.keyword.Bluemix_notm}}-CLI abrufen
{: #logging_token_cloud_cli}

Führen Sie die folgenden Schritte aus, um das Protokollierungstoken abzurufen, mit dem Sie Protokolle an den {{site.data.keyword.loganalysisshort}}-Service senden können:

1. Installieren Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle.

   Weitere Informationen finden Sie unter [{{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstellen herunterladen und installieren](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Fahren Sie mit dem nächsten Schritt fort, wenn die Befehlszeilenschnittstelle bereits installiert ist.
    
2. Melden Sie sich an einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Erstellen Sie einen Serviceschlüssel in dem Bereich, in dem der {{site.data.keyword.loganalysisshort}}-Service bereitgestellt ist. Führen Sie die folgenden Befehle aus:

    Listen Sie die Services auf, um den Namen der {{site.data.keyword.loganalysisshort}}-Instanz im Bereich abzurufen:
	
    ```
	bx service list
	```
	{: codeblock}
	
	Beispiel:
	
	```
	bx service list
    Invoking 'cf services'...

    Getting services in org lopezdsr_org / space dev as xxx@yyyy...
    OK

    name              service          plan       bound apps   last operation
    Log Analysis-vg   ibmloganalysis   standard                create succeeded
    ```
	{: screen}
	
	Erstellen Sie einen Schlüssel. Verwenden Sie den Wert **name** als Servicenamen und geben Sie den Namen Ihres Schlüssels ein.
	
	```
	bx service key-create Servicename Schlüsselname 
	```
	{: codeblock}
	
	Beispiel:
	
	```
	bx service key-create "Log Analysis-vg" mykey2
    Invoking 'cf create-service-key Log Analysis-vg mykey2'...

    Creating service key mykey2 for service instance Log Analysis-vg as xxx@yyyy...
    OK
    ```
	{: screen}
	
4. Rufen Sie das Protokollierungstoken ab. Führen Sie den folgenden Befehl aus:
	
	```
	bx service key-show Name Schlüsselname
	```
	{: codeblock}
	
	Beispiel: 
	
	```
	bx service key-show "Log Analysis-vg" "mykey2" 
    Invoking 'cf service-key Log Analysis-vg mykey2'...

    Getting key mykey2 for service instance Log Analysis-vg as xxx@yyyy...

    {
     "LOG_INGESTION_MTLJ_URL": "https://ingest-eu-fra.logging.bluemix.net:9091",
     "logging_token": "sdtghyrtfde4",
     "space_id": "12345678-avfg-erft-b1f2-2efrtgcb1744"
    }
    ```
	{: screen}
	
	Führen Sie zum Abrufen des Protokollierungstokens den folgenden Befehl aus:
	
	```
	bx service key-show "Log Analysis-vg" "mykey2" | tail -n +4 | jq -r .logging_token
    sdtghyrtfde4
	```
	{: screen}


	
## Protokollierungstoken zum Senden von Protokollen an einen Bereich über die Log Analysis-API abrufen
{: #logging_token_api}


Führen Sie die folgenden Schritte aus, um das Protokollierungstoken abzurufen, mit dem Sie Protokolle an den {{site.data.keyword.loganalysisshort}}-Service senden können:

1. Installieren Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle.

   Weitere Informationen finden Sie unter [{{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle herunterladen und installieren](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Fahren Sie mit dem nächsten Schritt fort, wenn die Befehlszeilenschnittstelle bereits installiert ist.
    
2. Melden Sie sich bei einer Region, Organisation und bei einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Rufen Sie das [UAA-Token](/docs/services/CloudLogAnalysis/security/auth_uaa.html#uaa_cli) ab.

    Führen Sie zum Abrufen des UAA-Tokens beispielsweise den Befehl `bx cf oauth-token` aus.

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	Die Ausgabe enthält das UAA-Token, das Sie für die Authentifizierung Ihrer Benutzer-ID in diesem Bereich und dieser Organisation benötigen.

4. Rufen Sie die GUID für den Bereich ab.

   Weitere Informationen finden Sie unter [Wie rufe ich die GUID von einem Bereich ab?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).  
	
5. Exportieren Sie die folgenden Variablen: TOKEN und SPACEID.

    * *TOKEN* ist das OAuth-Token aus dem vorherigen Schritt mit Ausschluss von 'Bearer'.
	
	* *SPACEID* ist die GUID des Bereichs aus dem vorherigen Schritt. 
		
	Beispiel:
	
	```
	export TOKEN="eyJhbGciOiJI....cGFzc3dvcmQiLCJjZiIsInVhYSIsIm9wZW5pZCJdfQ.JaoaVudG4jqjeXz6q3JQL_SJJfoIFvY8m-rGlxryWS8"
	export SPACEID="667fb895-abcd-defg-aaaa-cf4587341095"
	```
	{: screen}
	
6. Rufen Sie das Protokollierungstoken ab. Führen Sie den folgenden Befehl aus:
 
    ```
	curl -k -X GET  --header "X-Auth-Token: ${TOKEN}"  --header "X-Auth-Project-Id: s-${BEREICHS-ID}"  PROTOKOLLIERUNGSENDPUNKT/token
    ```
    {: codeblock}	
	
	Dabei gilt:
	* BEREICHS-ID ist die GUID des Bereichs, in dem der Service ausgeführt wird.
	* TOKEN ist das UAA-Token aus dem vorherigen Schritt ohne das Präfix 'bearer'.
	* PROTOKOLLIERUNGSENDPUNKT ist der {{site.data.keyword.loganalysisshort}}-Endpunkt für die {{site.data.keyword.Bluemix_notm}}-Region, in der sich die Organisation und der Bereich befinden. Der PROTOKOLLIERUNGSENDPUNKT ist für jede Region anders. Informationen zum Anzeigen von URLs für die verschiedenen Endpunkte finden Sie unter [Endpunkte](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
    Der Befehl gibt das Protokollierungstoken zurück, das Sie verwenden müssen, um Protokolle an diesen Bereich senden zu können.
	
