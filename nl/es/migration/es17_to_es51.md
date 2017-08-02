---

copyright:
  years: 2017
lastupdated: "2017-07-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Consideraciones sobre la migración después de la actualización de la pila ELK a la versión 5.1 
{: #es17_to_es51}

En {{site.data.keyword.Bluemix}}, la pila ElasticSearch (ELK) se actualiza de la versión 1.7 a la versión 2.3. Dispone de nuevas características, URLS para ingerir registros y nuevos URL para analizar registros en Kibana. Para obtener más información, consulte [ElasticSearch 5.1 ![icono de enlace externo](../../../icons/launch-glyph.svg "icono de enlace externo")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html "icono de enlace externo").
{:shortdesc}

Esta característica no se aplica a los usuarios que utilizan el servicio de registro con contenedores Docker desplegados en un clúster Kubernetes. Estos contenedores que ya utilizan la pila ELK versión 2.3.

## Regiones
{: #regions}

La pila ELK versión 5.1 está disponible en la siguiente región:

* EE.UU. sur


## Novedades
{: #features}

1. Distintos URL para trabajar con registros y métricas.

    En ELK 1.7, se compartía el mismo URL para mostrar y supervisar registros y métricas. Con la actualización a ELK 5.1, tiene distintos URLS a ver registros y métricas. Para obtener más información, consulte [URL de registro](#logging).
    
2. Soporte de Kibana 5.1. 

    Puede iniciar Kibana desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} o directamente desde el nuevo URL de registro. Para obtener más información, consulte [Análisis de registros con Kibana](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana).
    
    Kibana 3 está en desuso. Puede iniciar Kibana 3 mediante el [URL de registro de ELK 1.7](#logging). Hay distintos URL por región. **Nota:** Dispone de acceso a los paneles de control de Kibana 3 para poder comparar y migrar sus paneles de control de Kibana 3 a los de Kibana 5.1. 
    
    Si tiene paneles de control de Kibana creados en la pila ELK 1.7, debe migrarlos al entorno ELK 5.1.
    
    Para obtener más información sobre Kibana 5.1, consulte la [Guía del usuario de Kibana ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.elastic.co/guide/en/kibana/5.1/index.html "Icono de enlace externo"){: new_window}.
    
3. Adición de sufijos basados en tipo a campos personalizados.

    Puede configurar campos personalizados como campos de búsqueda de Kibana. Cada campo disponible en un mensaje se analiza según el tipo de campo que coincide con su valor. Por ejemplo, cada campo en el siguiente mensaje JSON: 

    ```
    {"field1":"string type",
        "field2":123,
        "field3":false,
        "field4":"4567"
    }
    ```
    {: screen}
    
    está disponible como un campo que se puede utilizar para filtrar y realizar búsquedas:

    * field1 se analiza como field1_str de tipo serie.
    * field2 se analiza como field1_int de tipo entero.
    * field3 se analiza como field3_bool de tipo booleano.
    * field4 se analiza como field4_str de tipo serie.
    
    El mensaje JSON de ejemplo es un registro que se envía al servicio de registro. 

    **Nota:** esta característica solo está disponible en Elastic 5.1. Esta característica no está disponible en Elastic 1.7 para evitar la ruptura de los paneles de control de Kibana3.


## Registro 
{: #logging}

Se utilizan distintos URL para enviar registros a {{site.data.keyword.Bluemix_notm}} y para analizar datos en Kibana.

En la tabla siguiente se muestra el nuevo URL de la región EE. UU. sur:

<table>
  <caption>URL para la región EE. UU. sur</caption>
    <tr>
      <th>Tipo</th>
      <th>ELK 1.7 </th>
	  <th>ELK 5.1 </th>
    </tr>
  <tr>
    <td>URL de ingestión para registros</td>
    <td>logs.opvis.bluemix.net:9091</td>
	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>URL de Kibana para analizar registros</td>
    <td>https://logmet.ng.bluemix.net</td>
	<td>https://logging.ng.bluemix.net</td>
  </tr>
</table>

