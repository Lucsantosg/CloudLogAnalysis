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


# Obtención de la señal de UAA
{: #auth_uaa}

Para gestionar registros mediante la API de {{site.data.keyword.loganalysisshort}}, debe utilizar una señal de autenticación. Utilice la CLI de {{site.data.keyword.loganalysisshort}} para obtener la señal de UAA. La señal tiene un tiempo de caducidad.
{:shortdesc}

		
## Obtención de la señal de UAA mediante la CLI de análisis de registros (plugin de CF)
{: #uaa_cli}


Para obtener la señal de autorización, siga estos pasos:

1. Instale la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Descargue e instale la CLI de {{site.data.keyword.Bluemix}}](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Si la CLI está instalada, continúe en el paso siguiente.
    
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Ejecute el mandato `bx cf oauth-token` para obtener la señal de UAA de {{site.data.keyword.Bluemix_notm}}. 

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	La salida devuelve la señal de UAA que debe utilizar para autenticas su ID de usuario en dicho espacio y organización.
	

**Nota:** Cuando utilice la señal, elimine *Bearer* del valor de la señal que pasa en una llamada de API.
