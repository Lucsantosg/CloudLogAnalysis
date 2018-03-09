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

# Consideraciones sobre la migración después de la actualización de Elastic Stack a la versión 5.1 
{: #es17_to_es51}

En {{site.data.keyword.Bluemix}}, la pila ElasticSearch (ELK) se actualiza de la versión 1.7 a la versión 5.1. Dispone de nuevas características, nuevos URL para ingerir registros y nuevos URL para analizar registros en Kibana. Para obtener más información, consulte [ElasticSearch 5.1 ![icono de enlace externo](../../../icons/launch-glyph.svg "icono de enlace externo")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html).
{:shortdesc}

Esta característica no se aplica a los usuarios que utilizan el servicio de registro con contenedores Docker desplegados en un clúster Kubernetes. 

## Regiones
{: #regions}

Elastic versión 5.1 está disponible en la siguiente región:

* Reino Unido
* EE.UU. sur
* Alemania
* Sídney


## Novedades
{: #features}

1. Distintos URL para trabajar con registros y métricas.

    En Elastic 1.7, se compartía el mismo URL para mostrar y supervisar registros y métricas. Con la actualización a Elastic 5.1, tiene distintos URLS a ver registros y métricas. Para obtener más información, consulte [URL de registro](#logging).
    
2. Soporte para Kibana 5.1.

    Puede iniciar Kibana desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} o directamente desde el nuevo URL de registro. Para obtener más información, consulte [Navegación al panel de control de Kibana](/docs/services/CloudLogAnalysis/kibana/launch.html#launch).
    
    Kibana 3 y Kibana 4 están en desuso.
	
	**Nota:** Hay distintos URL por región. El acceso a los paneles de control de Kibana 4 está disponible actualmente en el Reino Unido para que compare y migre los paneles de control a los de Kibana 5.1. 
    
    Debe migrar sus paneles de control al entorno de Elastic 5.1.
    
    Para obtener más información sobre Kibana 5.1, consulte la [Guía del usuario de Kibana ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}.
    
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


## URL de registro
{: #logging}

Se utilizan distintos URL para enviar registros a {{site.data.keyword.Bluemix_notm}} y para analizar datos en Kibana.

En la tabla siguiente se muestran los URL correspondientes a la región EE.UU. Sur:

<table>
  <caption>Tabla 1. URL correspondientes a la región EE.UU. Sur</caption>
    <tr>
      <th>Tipo</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
    </tr>
  <tr>
    <td>URL de ingestión para registros</td>
    <td>logs.opvis.bluemix.net:9091</td>
  	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>URL de Kibana para analizar registros</td>
    <td>[https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net)</td>
	  <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
  </tr>
</table>

En la tabla siguiente se muestran los URL correspondientes a la región Reino Unido: 

<table>
  <caption>Tabla 2. URL correspondientes a la región Reino Unido</caption>
  <tr>
     <th>Tipo</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>URL de ingestión para registros</td>
	   <td>logs.eu-gb.opvis.bluemix.net:9091</td>
	   <td>ingest.logging.eu-gb.bluemix.net:9091</td>
  </tr>
  <tr>
     <td>URL de Kibana para analizar registros</td>
	 <td>[https://logmet.eu-gb.bluemix.net](https://logmet.eu-gb.bluemix.net)</td>
	 <td>[https://logging.eu-gb.bluemix.net](https://logging.eu-gb.bluemix.net)</td>
  </tr>
</table>

En la tabla siguiente se muestran los URL correspondientes a la región Frankfurt: 

<table>
  <caption>Tabla 3. URL correspondientes a la región Frankfurt</caption>
  <tr>
     <th>Tipo</th>
      <th>Elastic 2.3 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>URL de ingestión para registros</td>
	 <td>ingest.logging.eu-de.bluemix.net</td>
	 <td>ingest-eu-fra.logging.bluemix.net</td>
  </tr>
  <tr>
     <td>URL de Kibana para analizar registros</td>
	 <td>[https://logging.eu-de.bluemix.net](https://logging.eu-de.bluemix.net)</td>
	 <td>[https://logging.eu-fra.bluemix.net](https://logging.eu-fra.bluemix.net)</td>
  </tr>
</table>



