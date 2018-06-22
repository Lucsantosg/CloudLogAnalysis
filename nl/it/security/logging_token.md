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


# Ottenimento del token di registrazione
{: #logging_token}

Ottieni un token di registrazione per inviare i log nel servizio {{site.data.keyword.loganalysisshort}}. 
{:shortdesc}


## Ottenimento del token di registrazione per inviare i log a uno spazio utilizzando la CLI {{site.data.keyword.loganalysisshort}} 
{: #logging_token_la_cloud_cli}

Per ottenere il token di registrazione che puoi usare per inviare i log al servizio {{site.data.keyword.loganalysisshort}}, completa la seguente procedura:

1. Installa la CLI {{site.data.keyword.Bluemix_notm}}.

   Per ulteriori informazioni, vedi [Scarica e installa la CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Se la CLI è installata, continua con il passo successivo.
    
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Esegui il seguente comando:

    ```
	bx logging token-get
	```
	{: codeblock}

L'output restituisce il token di registrazione.


## Ottenimento del token di registrazione per inviare i log a uno spazio utilizzando la CLI{{site.data.keyword.Bluemix_notm}}
{: #logging_token_cloud_cli}

Per ottenere il token di registrazione che puoi usare per inviare i log al servizio {{site.data.keyword.loganalysisshort}}, completa la seguente procedura:

1. Installa la CLI {{site.data.keyword.Bluemix_notm}}.

   Per ulteriori informazioni, vedi [Scarica e installa la CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Se la CLI è installata, continua con il passo successivo.
    
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Crea una chiave di servizio nello spazio in cui viene eseguito il provisioning del servizio {{site.data.keyword.loganalysisshort}}. Esegui questi comandi:

    Elenca i servizi per ottenere il nome dell'istanza {{site.data.keyword.loganalysisshort}} nello spazio:
	
    ```
	bx service list
	```
	{: codeblock}
	
	Ad esempio:
	
	```
	bx service list
    Invoking 'cf services'...

    Getting services in org lopezdsr_org / space dev as xxx@yyyy...
    OK

    name              service          plan       bound apps   last operation
    Log Analysis-vg   ibmloganalysis   standard                create succeeded
    ```
	{: screen}
	
	Crea una chiave. Usa il valore di**name** per il nome servizio e immetti il nome della tua chiave.
	
	```
	bx service key-create servicename KeyName 
	```
	{: codeblock}
	
	Ad esempio,
	
	```
	bx service key-create "Log Analysis-vg" mykey2
    Invoking 'cf create-service-key Log Analysis-vg mykey2'...

    Creating service key mykey2 for service instance Log Analysis-vg as xxx@yyyy...
    OK
    ```
	{: screen}
	
4. Ottieni il token di registrazione. Esegui il seguente comando:
	
	```
	bx service key-show name Keyname
	```
	{: codeblock}
	
	Ad esempio, 
	
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
	
	Per ottenere il token di registrazione, puoi eseguire questo comando:
	
	```
	bx service key-show "Log Analysis-vg" "mykey2" | tail -n +4 | jq -r .logging_token
    sdtghyrtfde4
	```
	{: screen}


	
## Ottenimento del token di registrazione per inviare i log a uno spazio utilizzando la API Analisi dei log
{: #logging_token_api}


Per ottenere il token di registrazione che puoi usare per inviare i log al servizio {{site.data.keyword.loganalysisshort}}, completa la seguente procedura:

1. Installa la CLI {{site.data.keyword.Bluemix_notm}}.

   Per ulteriori informazioni, vedi [Scarica e installa la CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Se la CLI è installata, continua con il passo successivo.
    
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, vedi [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Ottieni il [token UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#uaa_cli).

    Ad esempio, esegui il comando `bx cf oauth-token` per ottenere il token UAA.

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	L'output restituisce il token UAA che devi usare per autenticare il tuo ID utente in tale spazio e organizzazione.

4. Ottieni il GUID per lo spazio.

   Per ulteriori informazioni, vedi [Come ottengo il GUID di uno spazio](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).  
	
5. Esporta le seguenti variabili: TOKEN e SPACEID.

    * *TOKEN* è il token oauth che hai ottenuto nel passo precedente escludendo Bearer.
	
	* *SPACEID* è il GUID dello spazio che hai ottenuto nel passo precedente. 
		
	Ad esempio,
	
	```
	export TOKEN="eyJhbGciOiJI....cGFzc3dvcmQiLCJjZiIsInVhYSIsIm9wZW5pZCJdfQ.JaoaVudG4jqjeXz6q3JQL_SJJfoIFvY8m-rGlxryWS8"
	export SPACEID="667fb895-abcd-defg-aaaa-cf4587341095"
	```
	{: screen}
	
6. Ottieni il token di registrazione. Esegui il seguente comando:
 
    ```
	curl -k -X GET  --header "X-Auth-Token: ${TOKEN}"  --header "X-Auth-Project-Id: s-${SPACEID}"  LOGGING_ENDPOINT/token
    ```
    {: codeblock}	
	
	dove
	* SPACEID è il GUID dello spazio in cui è in esecuzione il servizio.
	* TOKEN è il token UAA che ottieni in un passo precedenza senza il prefisso bearer.
	* LOGGING_ENDPOINT è l'endpoint {{site.data.keyword.loganalysisshort}} per la regione {{site.data.keyword.Bluemix_notm}} in cui sono disponibili l'organizzazione e lo spazio. Il LOGGING_ENDPOINT è diverso per ogni regione. Per visualizzare gli URL per i diversi endpoint, vedi [Endpoint](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
    Il comando restituisce il token di registrazione che devi utilizzare per inviare i log a tale spazio.
	
