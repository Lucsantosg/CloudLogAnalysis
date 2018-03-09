---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Obtención de la señal de registro
{: #logging_token}

Obtenga una señal de registro para enviar registros al servicio {{site.data.keyword.loganalysisshort}}. 
{:shortdesc}


## Obtención de la señal de registro para enviar registros a un espacio mediante la CLI de {{site.data.keyword.loganalysisshort}} 
{: #logging_token_la_cloud_cli}

Para obtener la señal de registro que puede utilizar para enviar registros al servicio {{site.data.keyword.loganalysisshort}}, siga estos pasos:

1. Instale la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Descargue e instale la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Si la CLI está instalada, continúe en el paso siguiente.
    
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Ejecute el mandato siguiente:

    ```
	bx logging token-get
	```
	{: codeblock}

La salida devuelve la señal de registro.


## Obtención de la señal de registro para enviar registros a un espacio mediante la CLI de {{site.data.keyword.Bluemix_notm}}
{: #logging_token_cloud_cli}

Para obtener la señal de registro que puede utilizar para enviar registros al servicio de {{site.data.keyword.loganalysisshort}}, siga estos pasos:

1. Instale la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Descargue e instale la CLI de {{site.data.keyword.Bluemix_notm}}] CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Si la CLI está instalada, continúe en el paso siguiente.
    
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Cree una clave de servicio en el espacio donde se suministra el servicio de {{site.data.keyword.loganalysisshort}}. Ejecute los siguientes mandatos:

    Cree una lista de los servicios para obtener el nombre de la instancia de {{site.data.keyword.loganalysisshort}} en el espacio:
	
    ```
	bx service list
	```
	{: codeblock}
	
	Por ejemplo:
	
	```
	bx service list
    Invoking 'cf services'...

    Getting services in org lopezdsr_org / space dev as xxx@yyyy...
    OK

    name              service          plan       bound apps   last operation
    Log Analysis-vg   ibmLogAnalysis   standard                create succeeded
    ```
	{: screen}
	
	Cree una clave. Utilice el valor de **name** para el nombre de servicio y especifique el nombre de la clave.
	
	```
	bx service key-create servicename KeyName 
	```
	{: codeblock}
	
	Por ejemplo,
	
	```
	bx service key-create "Log Analysis-vg" mykey2
    Invoking 'cf create-service-key Log Analysis-vg mykey2'...

    Creating service key mykey2 for service instance Log Analysis-vg as xxx@yyyy...
    OK
    ```
	{: screen}
	
4. Obtenga la señal de registro. Ejecute el mandato siguiente:
	
	```
	bx service key-show name Keyname
	```
	{: codeblock}
	
	Por ejemplo, 
	
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
	
	Para obtener la señal de registro, puede ejecutar el mandato siguiente:
	
	```
	bx service key-show "Log Analysis-vg" "mykey2" | tail -n +4 | jq -r .logging_token
    sdtghyrtfde4
	```
	{: screen}

## Obtención de la señal de registro para enviar registros a un espacio mediante la CLI de análisis de registros (plugin de CF)
{: #logging_token_cf_plugin}

Para obtener la señal de registro que puede utilizar para enviar registros al servicio {{site.data.keyword.loganalysisshort}}, siga estos pasos:

1. Instale la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Descargue e instale la CLI de {{site.data.keyword.Bluemix}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Si la CLI está instalada, continúe en el paso siguiente.
    
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Obtenga el GUID correspondiente al espacio para el que ha obtenido una señal de autenticación.

   Para obtener más información, consulte [Cómo se obtiene el GUID de un espacio](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid)  
   
4. Obtenga la señal de registro. Ejecute el mandato siguiente:

    ```
    bx cf logging auth
    ```
    {: codeblock}

El mandato devuelve ka *señal de registro* y el *ID de espacio* que necesita enviar registros al espacio con dicho ID.	
	
## Obtención de la señal de registro para enviar registros a un espacio mediante la API de análisis de registro
{: #logging_token_api}


Para obtener la señal de registro que puede utilizar para enviar registros al servicio {{site.data.keyword.loganalysisshort}}, siga estos pasos:

1. Instale la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Descargue e instale la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Si la CLI está instalada, continúe en el paso siguiente.
    
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Obtenga la [señal de UAA](/docs/services/CloudLogAnalysis/security/auth_uaa.html#uaa_cli).

    Por ejemplo, ejecute el mandato `bx cf oauth-token` para obtener la señal de UAA.

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	La salida devuelve la señal de UAA que debe utilizar para autenticas su ID de usuario en dicho espacio y organización.

4. Obtenga el GUID del espacio.

   Para obtener más información, consulte [Cómo se obtiene el GUID de un espacio](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).  
	
5. Exporte las siguientes variables: TOKEN y SPACEID.

    * *TOKEN* es la señal de oauth que ha obtenido en el paso anterior, sin incluir 'Bearer'.
	
	* *SPACEID* es el GUID del espacio que ha obtenido en el paso anterior. 
		
	Por ejemplo,
	
	```
	export TOKEN="eyJhbGciOiJI....cGFzc3dvcmQiLCJjZiIsInVhYSIsIm9wZW5pZCJdfQ.JaoaVudG4jqjeXz6q3JQL_SJJfoIFvY8m-rGlxryWS8"
	export SPACEID="667fb895-abcd-defg-aaaa-cf4587341095"
	```
	{: screen}
	
6. Obtenga la señal de registro. Ejecute el mandato siguiente:
 
    ```
	curl -k -X GET  --header "X-Auth-Token: ${TOKEN}"  --header "X-Auth-Project-Id: s-${SPACEID}"  LOGGING_ENDPOINT/token
    ```
    {: codeblock}	
	
	donde
	* SPACEID es el GUID del espacio en el que se está ejecutando el servicio.
	* TOKEN es la señal de UAA que ha obtenido en el paso anterior sin el prefijo bearer.
	* LOGGING_ENDPOINT es el punto final de {{site.data.keyword.loganalysisshort}} correspondiente a la región de {{site.data.keyword.Bluemix_notm}} en la que están disponibles la organización y el espacio. El valor LOGGING_ENDPOINT varía según la región. Para ver los URL correspondientes a los distintos puntos finales, consulte [Puntos finales](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
    El mandato devuelve la señal de registro que debe utilizar para enviar registros a ese espacio.
	
## Obtención de la señal de registro para enviar registros al dominio de la cuenta mediante la API de análisis de registro
{: #logging_acc_token_api}


Para obtener la señal de registro que puede utilizar para enviar registros al servicio {{site.data.keyword.loganalysisshort}}, siga estos pasos:

1. Instale la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Descargue e instale la CLI de {{site.data.keyword.Bluemix_notm}}] CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Si la CLI está instalada, continúe en el paso siguiente.
    
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Obtenga la [señal de IAM](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).

    La salida devuelve la señal de IAM.

4. Obtenga el GUID de la cuenta.

   Para obtener más información, consulte [Cómo se obtiene el GUID de una cuenta](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).  
	
5. Exporte las siguientes variables: TOKEN y AccountID.

    * *TOKEN* es la señal de oauth que ha obtenido en el paso anterior, sin incluir 'Bearer'.
	
	* *AccountID* es el GUID de la cuenta que ha obtenido en el paso anterior. 
		
	Por ejemplo,
	
	```
	export TOKEN="eyJhbGciOiJI....cGFzc3dvcmQiLCJjZiIsInVhYSIsIm9wZW5pZCJdfQ.JaoaVudG4jqjeXz6q3JQL_SJJfoIFvY8m-rGlxryWS8"
	export AccountID="667fb8953456fg41095"
	```
	{: screen}
	
6. Obtenga la señal de registro. Ejecute el mandato siguiente:
 
    ```
	curl -k -X GET  --header "X-Auth-User-Token:iam ${TOKEN}"  --header "X-Auth-Project-Id: a-${AccountID}" -k  LOGGING_ENDPOINT/token
    ```
    {: codeblock}	
	
	donde
	* AccountID es el GUID del espacio en el que se está ejecutando el servicio.
	* TOKEN es la señal de IAM que ha obtenido en el paso anterior sin el prefijo bearer.
	* LOGGING_ENDPOINT es el punto final de {{site.data.keyword.loganalysisshort}} correspondiente a la región de {{site.data.keyword.Bluemix_notm}} en la que están disponibles la organización y el espacio. El valor LOGGING_ENDPOINT varía según la región. Para ver los URL correspondientes a los distintos puntos finales, consulte [Puntos finales](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
    El mandato devuelve la señal de registro que debe utilizar para enviar registros al dominio de la cuenta.
	

