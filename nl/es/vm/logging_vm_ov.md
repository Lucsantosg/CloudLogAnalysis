---

copyright:
  years: 2017
lastupdated: "2017-07-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Registro para máquinas virtuales
{: #logging_vm_ov}

Las funciones de registro no se habilitan automáticamente para las máquinas virtuales (VM). Sin embargo, puede configurar la VM para que envíe registros al componente de recopilación de registros. Para recopilar y enviar datos de registro desde una VM al servicio {{site.data.keyword.loganalysisshort}}, debe configurar un reenviador de Logstash multiarrendatario. Luego podrá ver, filtrar y analizar registros en Kibana.
{:shortdesc}


## Ingestión de registros
{: #log_ingestion}

El servicio {{site.data.keyword.loganalysisshort}} ofrece diversos planes. Cada plan define si el usuario puede o no enviar registros al componente de recopilación de registros. Todos los planes, excepto el plan *Lite*, incluyen la posibilidad de enviar registros a la recopilación de registros. Para obtener más información sobre los planes, consulte [Planes de servicio](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

Puede enviar registros a {site.data.keyword.loganalysisshort}} mediante mt-logstash-forwarder. Para obtener más información, consulte el apartado sobre [Envío de datos de registro mediante el reenviador de Logstash multiarrendatario (mt-logstash-forwarder)](/docs/services/CloudLogAnalysis/how-to/send-data/send_data_mt.html#send_data_mt).


## Recopilación de registros
{: #log_collection}

De forma predeterminada, {{site.data.keyword.Bluemix_notm}} almacena los datos de registro durante un máximo de 3 días:   

* Se almacenan un máximo de 500 MB por espacio de datos al día. Cualquier registro que supere dicha capacidad de 500 MB se descartará. Las asignaciones de capacidades se restablecen todos los días a las 12:30 AM UTC.
* Se pueden buscar hasta 1,5 GB de datos para un máximo de 3 días. Los datos de registro se renuevan (Primero en entrar, primero en salir) una vez que se ha alcanzado 1,5 GB de datos o después de 3 días.

El servicio {{site.data.keyword.loganalysisshort}} proporciona planes adicionales que le permiten almacenar registros en la recopilación de registros tanto tiempo como desee. Para obtener más información sobre el precio de cada plan, consulte [Planes de servicio](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

Puede configurar una política de retención de registros que puede utilizar para definir el número de días que desea conservar los registros en la recopilación de registros. Para obtener más información, consulte [Política de retención de registros](/docs/services/CloudLogAnalysis/log_analysis_ov.html#policies).


## Búsqueda de registros
{: #log_search}

De forma predeterminada, puede utilizar Kibana para buscar un máximo de 500 MB de registros al día en {{site.data.keyword.Bluemix_notm}}. 

El servicio {{site.data.keyword.loganalysisshort}} proporciona varios planes. Cada plan tiene distintas funciones de búsqueda de registros; por ejemplo, el plan *Recopilación de registros* le permite buscar un máximo de 1 GB de datos al día. Para obtener más información sobre los planes, consulte [Planes de servicio](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).


## Análisis de registros
{: #log_analysis}

Para analizar los datos de registro, utilice Kibana para realizar tareas de análisis avanzado. Puede utilizar Kibana, una plataforma de visualización y análisis de código abierto, para supervisar, buscar, analizar y visualizar datos en diversos gráficos, como diagramas y tablas. Para obtener más información, consulte [Análisis de registros en Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana).
