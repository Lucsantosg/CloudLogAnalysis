---

copyright:
  years: 2017, 2018

lastupdated: "2018-07-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Obtención de la señal de UAA
{: #auth_uaa}

Para gestionar los registros disponible mediante la API de {{site.data.keyword.loganalysisshort}}, debe utilizar una señal de autenticación.
{:shortdesc}

		
## Obtención de la señal de UAA
{: #uaa_cli}


Para obtener la señal de autorización, siga estos pasos:

1. Instale la CLI de {{site.data.keyword.Bluemix_notm}}.

   Para obtener más información, consulte [Descargar e instalar la CLI de {{site.data.keyword.Bluemix}}](/docs/cli/index.html#overview).
   
   Si la CLI está instalada, continúe en el paso siguiente.
    
2. Inicie la sesión en una región, organización y espacio en {{site.data.keyword.Bluemix_notm}}. 

    Para obtener más información, consulte [Cómo iniciar la sesión en {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Ejecute el mandato `ibmcloud iam oauth-token` para obtener la señal de UAA de {{site.data.keyword.Bluemix_notm}}.

    ```
	ibmcloud iam oauth-token
	```
	{: codeblock}
	
	La salida devuelve la señal de UAA que debe utilizar para autenticas su ID de usuario en dicho espacio y organización.
	

**Nota:** Cuando utilice la señal, elimine *Bearer* del valor de la señal que pasa en una llamada de API.
