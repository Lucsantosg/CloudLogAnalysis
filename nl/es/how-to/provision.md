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


# Suministro del servicio de análisis de registros
{: #provision}

Puede suministrar el servicio {{site.data.keyword.loganalysisshort}} desde la interfaz de usuario de {{site.data.keyword.Bluemix}} o desde la línea de mandatos.
{:shortdesc}


## Suministro desde la interfaz de usuario
{: #ui}

Siga estos pasos para suministrar una instancia del servicio {{site.data.keyword.loganalysisshort}} en {{site.data.keyword.Bluemix_notm}}:

1. Inicie una sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}.

    El panel de control de {{site.data.keyword.Bluemix_notm}} se puede encontrar en: [http://bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net "Icono de enlace externo"){:new_window}.
    
	Cuando inicia sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. Pulse **Catálogo**. Se abrirá la lista de servicios disponibles en {{site.data.keyword.Bluemix_notm}}.

3. Seleccione la categoría **DevOps** para filtrar la lista de servicios mostrados.

4. Pulse el mosaico **Análisis de registros**.

5. Seleccione un plan de servicio. De forma predeterminada, se establece el plan **Lite**. 

    Para obtener más información sobre los planes de servicio, consulte [Planes de servicio](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
6. Pulse **Crear** para suministrar el servicio {{site.data.keyword.loganalysisshort}} en el espacio de {{site.data.keyword.Bluemix_notm}} en el que ha iniciado sesión.
  
 

## Suministro desde la CLI
{: #cli}

Siga estos pasos para suministrar una instancia del servicio {{site.data.keyword.loganalysisshort}} en {{site.data.keyword.Bluemix_notm}} mediante la línea de mandatos:

1. Instale la CLI de Cloud Foundry (CF). Si la CLI de CF está instalada, continúe con el paso siguiente.

   Para obtener más información, consulte [Instalación de la CLI de cf ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "Icono de enlace externo"){: new_window}. 
    
2. Inicie la sesión en una región, organización y espacio de {{site.data.keyword.Bluemix_notm}}. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:

    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Siga las instrucciones. Indique sus credenciales de {{site.data.keyword.Bluemix_notm}}, seleccione una organización y un espacio.
	
3. Ejecute el mandato `cf create-service` para suministrar una instancia.

    ```
	cf create-service service_name service_plan service_instance_name
	```
	{: codeblock}
	
	Donde
	
	* service_name es el nombre del servicio, que es **ibmLogAnalysis**.
	* service_plan es el nombre del plan de servicio. Para ver una lista de planes, consulte [Planes de servicio](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	* service_instance_name es el nombre que desea utilizar para la nueva instancia de servicio que cree. 	
	Para obtener más información sobre el mandato cf, consulte [cf create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service).

	Por ejemplo, para crear una instancia del servicio {{site.data.keyword.loganalysisshort}} con un plan gratuito, ejecute el siguiente mandato:
	
	```
	cf create-service ibmLogAnalysis lite my_logging_svc
	```
	{: codeblock}
	
4. Verifique que el servicio se ha creado correctamente. Ejecute el mandato siguiente:

    ```	
	cf services
	```
	{: codeblock}
	
	El resultado de la ejecución del mandato tiene este aspecto:
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_logging_svc                ibmLogAnalysis               lite                                        create succeeded
	```
	{: screen}

	



